
```csharp
if (!Validator.TryValidateObject(entity, context, results, true))
    ThrowValidationException(entity, results);
}
```

The new version calls the TryValidateObject method of the static Validator class. Unlike the ValidateObject method used previously, which throws a single ValidationException for the first error it detects, the TryValidateObject method invokes all validation attributes and implementations of the IValidatableObject interface. The TryValidateObject method collects the errors in the list of ValidationResult objects it receives as the third parameter and returns false if any errors were detected.

The ThrowValidationException method (shown next) uses the validation results to create a list of ValidationException objects. If multiple validation results were reported, it throws the AggregateException. Otherwise, it throws the ValidationException to mimic the simple behavior implemented earlier:

```csharp
protected static void ThrowValidationException(
    object entity, IEnumerable<ValidationResult> results)
{
    var exceptions = new List<ValidationException>();
    foreach (ValidationResult result in results)
        exceptions.Add(new ValidationException(result, null, entity));

    if (exceptions.Count == 1)
        throw exceptions[0];

    throw new AggregateException(exceptions);
}
```

> **NOTE**
> The AggregateException does not inherit from the ValidationException class. Now that the SaveChanges method can throw two different exception types, many of the automated tests written so far will fail because they only expect the ValidationException. To make them pass, change the ExpectedValidationExceptionAttribute to support both types of validation exceptions. You can find the updated implementation of this attribute in the source code accompanying this book.

## Extending DynamicValidator to Support AggregateException

As discussed in Chapter 3 and Chapter 6, Dynamic Data relies on the DynamicValidator control for exception handling. When used in a field template, this control is responsible for evaluating the validation attributes applied to the entity property the template instance represents. In field and page templates, this control also handles any exceptions Entity Framework may throw. Here is the part of this class that implements exception handling:

```csharp
public class DynamicValidator : BaseValidator
{
    protected virtual Exception ValidationException { get; set; }
    protected virtual void ValidateException(Exception exception) { }
}
```

The control calls the ValidateException method whenever the EntityDataSource fires its Exception event. The method receives an Exception object and determines whether it represents an error condition expected by the DynamicValidator control. If it does, the ValidateException method assigns the exception object to the ValidationException property. If this property is not null during page validation, the DynamicValidator uses it to display the exception's error message.

Out of the box, DynamicValidator supports only ValidationException and exception types, like EntityDataSourceValidationException, that implement the IDynamicValidatorException interface. Because AggregateException used in this example does not implement this interface, the DynamicValidator controls simply ignore it and let the ASP.NET runtime to generate a yellow page of death. To handle AggregateException and other types of expected exceptions your business layer may throw, you need to subclass the DynamicValidator control and override its ValidateException method.

When overriding the ValidateException method, remember that a single web page can contain a number of dynamic validators. The validators created by field templates are associated with specific entity properties (for these controls, the Column property defined in the DynamicValidator base class returns a MetaColumn object describing their entity property). These validators should report only the exceptions related to their respective entity properties. However, the validator at the top of the page is not associated with any particular entity property (its Column property is null) and should report only the exceptions related to the entire entity.

The ValidationException class used in this example allows you to determine if an error is related to a particular entity property by examining its ValidationResult. The MemberNames property of the ValidationResult can be empty if the error is not related to any particular entity property or contain multiple property names depending on how the validation logic was implemented by the entity class.

For complete details on how to extend the DynamicValidator control and implement support for AggregateException that contains multiple ValidationException instances, please refer to the UnleashedValidator control in the sample solution accompanying this book. Figure 8.10 shows how multiple validation errors are reported in the sample web application where all field and page templates have been modified to use the UnleashedValidator control instead of the built-in DynamicValidator.

![](img/11b373b78859e17d318fd76939a0df9d_274_0.png)

FIGURE 8.10 Multiple errors correctly reported on a Dynamic Data web page.

## Validating Entity State Changes

Sometimes validating current state of an entity is insufficient. Consider the Order entity and its OrderStatus property, which indicates whether an order has been submitted, paid, or fulfilled. It would be bad if someone could change the status of a fulfilled order back to paid and receive a second product free. Here is a code example that illustrates the problem:

```csharp
using (var context = new NorthwindEntities())
{
    var order = CreateOrder();
    order.OrderStatus = (byte)OrderStatus.Fulfilled;
    context.Orders.AddObject(order);
    context.SaveChanges();
    order.OrderStatus = (byte)OrderStatus.Paid;
    context.SaveChanges();
}
```

The current implementation of the validation logic in the Order class has no knowledge of the previous state of the entity and cannot distinguish a valid order, for which a payment had just been processed, from a rogue order that was tampered with.

## Accessing Original Property Values with ObjectStateManager

As discussed in Chapter 2, the Entity Framework keeps track of all changes made to entities in order to support optimistic concurrency. Each ObjectContext, such as the NorthwindEntities in these examples, has an ObjectStateManager, which uses ObjectStateEntry objects to keep track of both current and original property values for each entity. Here is how you can take advantage of this capability and compare the current value of the OrderStatus property with the original:

```csharp
using (var context = new NorthwindEntities())
{
    var order = CreateOrder();
    order.OrderStatus = (byte)OrderStatus.Fulfilled;
    context.Orders.AddObject(order);
    context.SaveChanges();
    order.OrderStatus = (byte)OrderStatus.Paid;
    var stateEntry = context.ObjectStateManager.GetObjectStateEntry(order);
    byte originalStatus = (byte)stateEntry.OriginalValues["OrderStatus"];
    if (originalStatus == (byte)OrderStatus.Fulfilled &&
        order.OrderStatus == (byte)OrderStatus.Fulfilled)
    {
        // We have a problem
    }
    context.SaveChanges();
}
```

In this new version, the code first calls the GetObjectStateEntry method of the ObjectStateManager to retrieve an ObjectStateEntry, which allows accessing original property values of the entity via its OriginalValues property. This property returns an object of type DbDataRecord defined in the System.Data namespace by the ADO.NET framework. You can use its indexer to access the original property values by name. Having retrieved the original value of the OrderStatus property, you can compare it against the current value in the entity object itself.

## Accessing Original Property Values in Validation Methods

Out of the box, validation methods, whether they are defined by applying the CustomValidationAttribute or implementing the IValidatableObject interface, do not have access to the ObjectStateEntry, the ObjectStateManager, or even the ObjectContext for that matter. To access the original property values inside the validation methods, this information needs to be supplied to them by the Validate method of the UnleashedObjectContext class. Luckily, ValidationContext (which all validation methods can receive as a parameter) defines the Items property of type Dictionary<object, object> specifically for that purpose.

Here is how the Validate method in the UnleashedObjectContext was modified to create the Items dictionary and place an ObjectStateEntry instance in it for the validation methods to find:

```csharp
private void Validate(ObjectStateEntry stateEntry)
{
    object entity = stateEntry.Entity;

    var items = new Dictionary<object, object>();
    items[typeof(ObjectStateEntry)] = stateEntry;
}
```
