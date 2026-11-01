![](bbox=[0.13, 0.18, 0.67, 0.6])

FIGURE 14.2 Products page displaying inaccessible suppliers.

To prevent inaccessible entity information from appearing in pages of related entities completely, the dynamic page templates must somehow hide it. Implementing this functionality, sometimes also referred to as security trimming, by reading complex authorization rules from the Web configuration is challenging. Instead, it is often more practical to simply create a custom page or page template for the entity, such as Product in this example, that requires trimming.

# Metadata Security API

The metadata API provides a good foundation for implementing entity-level security with both access control and trimming. As discussed in Chapter 7, “Metadata API,” the MetaTable class defines the following methods that encapsulate action-level authorization rules for individual entities based on the identity and roles of a given user:

```
public virtual bool CanDelete(IPrincipal principal);
public virtual bool CanInsert(IPrincipal principal);
public virtual bool CanRead(IPrincipal principal);
public virtual bool CanUpdate(IPrincipal principal);
```

As implemented in the built-in MetaTable class, the permission methods always return true, allowing any user to access any entity by default. However, because these methods are virtual, you can override them and implement your own authorization rules.

In simplest form, you could hard-code the authorization rules. The example that follows demonstrates implementation of the CanRead method, which allows all users to access the Product and Category entities and only users in role Employee to access the Suppliers and other tables: