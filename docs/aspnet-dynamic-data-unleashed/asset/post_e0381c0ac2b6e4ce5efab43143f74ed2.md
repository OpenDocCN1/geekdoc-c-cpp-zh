
```csharp
public override int SaveChanges(SaveOptions options)
{
    IEnumerable<ObjectStateEntry> stateEntries = this.ObjectStateManager
        .GetObjectStateEntries(ChangedEntityStates)
        .Where(stateEntry => !stateEntry.IsRelationship);

    foreach (ObjectStateEntry stateEntry in stateEntries)
        this.BeforeSaveChanges(stateEntry);

    return base.SaveChanges(options);
}
```

When the SaveChanges method is called, you could have multiple entities that were added, modified, and deleted. The modifications are stored in the ObjectContext but not saved in the database yet. The BeforeSaveChanges method ensures that each of these changes is valid according to the business rules defined by the entity type. Authorization, being a specialized form of business rules, fits this pattern as well and you can extend the code to perform it. Here is a new version of this method with the changes highlighted in bold font:

```csharp
private void BeforeSaveChanges(ObjectStateEntry stateEntry)
{
    Authorize(stateEntry.Entity.GetType(),
        EntityStateToAction(stateEntry.State));

    var savable = stateEntry.Entity as ISavableObject;
    if (savable != null)
        savable.BeforeSave(stateEntry);

    if (stateEntry.State != EntityState.Deleted)
        this.Validate(stateEntry);
}
```

For each added, modified, or deleted entity, the BeforeSaveChanges method now calls the Authorize method, passing it the type of the entity and the action performed. Notice that the State property of the ObjectStateEntry defines the action performed on an entity as a value of the built-in enum type EntityState; however, the AuthorizationAttribute relies on the custom Actions enum type instead. To translate between the two types, you need a simple function, EntityStateToAction, shown here:

```csharp
private static Actions EntityStateToAction(EntityState state)
{
    switch(state)
    {
        case EntityState.Added:      return Actions.Insert;
        case EntityState.Modified:   return Actions.Update;
        case EntityState.Deleted:    return Actions.Delete;
        default: throw new ArgumentException("state");
    }
}
```

The Authorize method is responsible for throwing SecurityException (a built-in exception class defined in the System.Security namespace) if the current user is not authorized to perform a given set of actions for the specified entity type. Here is how this method is implemented in the UnleashedObjectContext class:

```csharp
private static void Authorize(Type entityType, Actions action)
{
    IPrincipal user = Thread.CurrentPrincipal;
    if (!IsAuthorized(user, entityType, action))
    {
        throw new SecurityException(string.Format(
            "User '{0}' is not authorized to {1} entities of type '{2}'.",
            user.Identity.Name, action, entityType.Name));
    }
}
```

To obtain the IPrincipal object representing the current user of the application, the Authorize method relies on the static property of the Thread class called CurrentPrincipal. This is different from how you implemented the authorization logic in the dynamic page templates earlier. There, you used the User property of the Page class, and although the static User property of the HttpContext class would be a closer alternative, using the Thread.CurrentPrincipal in the UnleashedObjectContext avoids adding dependency on the ASP.NET to the business layer.

The Authorize method delegates the task of evaluating the authorization rules to the IsAuthorized method, which takes a user, an entity type, and a set of actions as parameters and returns a boolean value, which indicates whether the user is permitted to perform them. This method tries to find the AuthorizationAttribute that might be applied to the entity class and, if found, calls its IsAuthorized method to evaluate the authorization rules. If the AuthorizationAttribute cannot be found, the IsAuthorized method returns true, following the ASP.NET convention of allowing access unless it is explicitly denied.

```csharp
private static readonly ConcurrentDictionary<Type, AuthorizationAttribute>
    authorizationAttributes = new ConcurrentDictionary<Type,
        AuthorizationAttribute>();

private static bool IsAuthorized(IPrincipal user, Type entityType,
    Actions action)
{
    var authorizationAttribute = authorizationAttributes.GetOrAdd(
        entityType,
        type => TypeDescriptor.GetAttributes(type)
            .OfType<AuthorizationAttribute>().FirstOrDefault());

    return authorizationAttribute == null
        || authorizationAttribute.IsAuthorized(user, action);
}
```

In any performance-critical method, such as IsAuthorized, it is important to minimize the amount of reflection-based code executed repeatedly. This code relies on the TypeDescriptor API to locate the AuthorizationAttribute and, to minimize the performance impact, caches the search results in the static authorizationAttributes dictionary. When the AuthorizationAttribute for a given entity type has been located, the next time it is retrieved from the dictionary, resulting in a much faster execution.

The IsAuthorized method can be executed by several different threads simultaneously, especially in a web application, and has to be thread-safe. To implement thread-safe caching, this code uses the ConcurrentDictionary type from the System.Collections.Concurrent namespace, which offers a specialized method GetOrAdd for safely retrieving an existing value from the dictionary or adding it if it does not exist. As its second parameter, this method takes a function that is executed if the dictionary does not contain a value for the given key; the value it returns is stored in the dictionary and returned to the caller of the GetOrAdd method. It is this anonymous function (this example uses the shorter lambda syntax to define it) where the code calls the TypeDescriptor.GetAttributes method to find the AuthorizationAttribute.

## Extending ObjectContext to Enforce Read Permission

The SaveChanges method of the ObjectContext allows you to enforce only the Insert, Update, and Delete permissions. Because this method does not have to be called by code retrieving entities from the database, you cannot enforce the Read permission here. It is actually quite challenging to authorize the Read actions properly because there are so many different ways of reading the entity information. First, there is the straightforward access through the ObjectSet properties, which can be illustrated with code like this:

```csharp
using (var context = new NorthwindEntities())
{
    var supplierInformation = context.Suppliers;
}
```

You can implement Read authorization for the Suppliers object set by changing implementation of its property. Here is the default implementation of the Suppliers property in the NorthwindEntities class generated by the built-in Entity Framework code generator, which was modified to call the Authorize method of the UnleashedObjectContext base class:

```csharp
public ObjectSet<Supplier> Suppliers
{
    get
    {
        Authorize(typeof(Supplier), Actions.Read);
        if (_Suppliers == null)
        {
            _Suppliers = base.CreateObjectSet<Supplier>("Suppliers");
        }
        return _Suppliers;
    }
}
private ObjectSet<Supplier> _Suppliers;
```

Now the code in the first snippet performs an authorization check and throws a SecurityException when the application tries to access the Suppliers property and the current user does not have the permission to read it.

> **NOTE**
>
> You cannot change implementation of the entity set properties directly in the code generated by the Entity Designer without losing the changes the next time the code is regenerated. As discussed in Chapter 8, you need to replace the built-in generator with a T4-based template provided by the ADO.NET team and modify the template logic responsible for generating these properties.

Unfortunately (from the perspective of implementing security), you could also retrieve suppliers through the Products object set, with the help of the Supplier navigation property:

```csharp
using (var context = new NorthwindEntities())
{
    var supplierInformation = context.Products.Select(p => p.Supplier);
}
```

And if that weren't enough, you could also use projection and return supplier information in objects of an anonymous type:

```csharp
using (var context = new NorthwindEntities())
{
    var supplierInformation = context.Products
        .Select(p => new { p.Supplier.CompanyName, p.Supplier.Address });
}
```

Code in the last two examples is compiled into LINQ expressions. You cannot inject the authorization logic by simply changing implementation of the Supplier navigation property of the Product entity because the property getter will not be called during query execution. At this time, you have to leave this problem unsolved because in the current version, the Entity Framework does not provide extensibility mechanisms that would allow implementing Read authorization in all possible scenarios.
