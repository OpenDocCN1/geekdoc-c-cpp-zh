
```
var context = new ValidationContext(entity, null, items);

var results = new List<ValidationResult>();
if (!Validator.TryValidateObject(entity, context, results, true))
{
    ThrowValidationException(entity, results);
}
```

Notice the ObjectStateEntry instance is stored in the dictionary using its own type as the key. This is not a strict requirement; you simply need a well-known value to serve as the key so that validation methods can find it in the dictionary. Using the type itself simply avoids having to define an extra constant just for this purpose. The dictionary is passed to the ValidationContext constructor as the third parameter.

Having changed the validation infrastructure to store the ObjectStateEntry instances in the ValidationContext, you can now implement a validation method in the Order class that takes advantage of it:

```
[MetadataType(typeof(Order.Metadata))]
partial class Order
{
    private abstract class Metadata
    {
        [CustomValidation(typeof(Order), "ValidateOrderStatus*")]
        public object OrderStatus { get; set; }
    }

    public static ValidationResult ValidateOrderStatus(
        byte? newStatus, ValidationContext context)
    {
        var stateEntry = (ObjectStateEntry)
            context.Items[typeof(ObjectStateEntry)];
        if (stateEntry.State == EntityState.Modified)
        {
            byte? oldStatus = (byte?)stateEntry.OriginalValues["OrderStatus"];
            if (oldStatus == (byte?)DataModel.OrderStatus.Fulfilled &&
                newStatus != (byte?)DataModel.OrderStatus.Fulfilled)
            {
                return new ValidationResult(
                    "Status of fulfilled orders should not be modified",
                    new string[] { "OrderStatus" });
            }
        }
        return ValidationResult.Success;
    }
}
```

```
}
```

In this example, a custom validation method called `ValidateOrderStatus` is associated with the `OrderStatus` property in the metadata class. The validation method first retrieves the `ObjectStateEntry` instance that contains the order entity being validated from the `Items` dictionary of the `ValidationContext` object. It then checks the current `State` of the entity and only performs the validation if the entity is modified. Because the entity state could also be Added, Deleted, Detached, or Unchanged, you only want to check the `OrderStatus` property when it is appropriate based on your business rules. You also want to access the `OriginalValues` property only when the original values are actually available; the property throws an `InvalidOperationException` when the entity state is Added.

## Handling DBNull Values

The `OriginalValues` property of the `ObjectStateEntry` class returns an object of type `DbDataRecord`, which is shared by the Entity Framework with classic ADO.NET. Unfortunately, this means that the original null values are returned as objects of type `DBNull` and the code has to be prepared to handle them accordingly. In particular, this means that you cannot simply cast the original `OrderStatus` value to type `Nullable<Byte>` because `DBNull` values cannot be converted to this type and throw an `InvalidCastException`.

One workaround for this problem is to store `OrderStatus` values in variables of type `Object` and to use the static `Object.Equals` method to compare them. Because it takes the object type into account, you can safely compare values of type `DBNull` and `Nullable<Byte>` for equality. Here is a new version of the `ValidateOrderStatus` method, which now correctly handles the scenario where the original value of the `OrderStatus` is `DBNull`:

```
public static ValidationResult ValidateOrderStatus(
    byte? newStatus, ValidationContext context)
{
    var stateEntry = (ObjectStateEntry)
        context.Items[typeof(ObjectStateEntry)];
    if (stateEntry.State == EntityState.Modified)
    {
        object oldStatus = stateEntry.OriginalValues["OrderStatus"];
        if (object.Equals(oldStatus, (byte)DataModel.OrderStatus.Fulfilled)
            && !object.Equals(newStatus, (byte)DataModel.OrderStatus.Fulfilled))
        {
            return new ValidationResult(
                "Status of fulfilled orders should not be modified",
                new string[] { "OrderStatus" });
        }
    }
    return ValidationResult.Success;
}
```

```
var order = (Order)stateEntry.Entity;
byte? oldStatus = stateEntry.OriginalValues
.Get(() => order.OrderStatus);
if ((oldStatus == (byte)DataModel.OrderStatus.Fulfilled)
&& newStatus != (byte)DataModel.OrderStatus.Fulfilled)
{
    return new ValidationResult(
        "Status of fulfilled orders should not be modified",
        new string[] { "OrderStatus" });
}
return ValidationResult.Success;
}
```

Here, the Get extension method uses the () => order.OrderStatus lambda expression to determine the name of the property, OrderStatus, which it passes to the indexer of the DbDataRecord object to retrieve the original property values. If the original value is DBNull, the Get method returns a default value of the property type—a value that an uninitialized variable of that type would have. In case of the OrderStatus property, whose type is Nullable<Byte>, the default value is null; for a non-nullable type, such as Byte, the default value would have been 0. If, however, the original value retrieved from the DbDataRecord object is not DBNull, the Get method returns the actual value after casting it to the type of the property itself.

The Get extension method offers several advantages. On one hand, it allows you to avoid having to write special logic to handle DBNull values. On the other hand, it allows you to specify properties as strongly-typed lambda expressions as opposed to hard-coded string literals or constants. They are not only easier to write (with the help of IntelliSense in the Visual Studio editor), but if you ever need to rename the property, the compiler ensures that all references are properly updated.

## Summary

The System.ComponentModel.DataAnnotations namespace offers a robust validation framework, which allows implementing validation rules declaratively by placing data annotation attributes, or imperatively, by writing code.

The validation framework is fully integrated in Dynamic Data web applications; a helper class, Validator, can be used to integrate validation with other frameworks as well. Version 4.0 of Entity Framework does not support the validation framework out of the box, and additional steps are necessary to extend object context classes to automatically validate entity objects before they are submitted to the database.

Automated testing allows you to improve the quality of your applications without significant additional effort. With integration tests, you begin reaping the benefits of automated testing almost immediately. However, care should be taken to isolate tests and make sure that they can run repeatedly and independently of each other. `TransactionScope` is the simplest way to isolate integration tests that access the database.

A number of built-in validation attributes is included in the framework out of the box, including attributes for performing required, string length, range, enum, and regular expression checks. Additional validation attributes can be implemented by inheriting from the `ValidationAttribute` class.

Imperative validation logic can be implemented by placing `CustomValidationAttribute` on individual properties or entire classes and implementing special validation methods that return `ValidationResult` objects. Classes can also implement the `IValidatableObject` interface to validate multiple rules and return multiple validation results.

## CHAPTER 9

### Implementing Business Logic

### IN THIS CHAPTER

- Entity Design
- Default Property Values
- Property Interaction Rules
- Entity Interaction Rules
- Validation Rules
- Saving Changes
- Invoking Business Rules in Web Applications
- Business Rules in the Database

Business logic, also known as *domain logic*, is code that implements a developer's interpretation of a business domain where the application is intended to solve one or more problems and address opportunities. Because a particular business domain can be described from different points of view, there are different definitions of what constitutes the business logic. This chapter discusses implementation of logic related to real-life *entities*, such as Customers, Products, and Orders, as well as *rules* that determine how these entities interact with each other.

The entities and rules are not directly related to any particular software application; instead, they describe the business itself. Similar to how a retailer could be selling products from a brick-and-mortar store directly to customers, accept orders by phone, allow customers to pick products up, or provide a website where customers submit orders that will be shipped to them by mail, different software applications can implement the same business logic as well. A sales clerk at a physical store could use a Windows-based point-of-sale application to sell a product, and a customer could use a Web-based application to place the order online. In both instances, the order needs to be checked to make sure that the product is in stock, order total must be calculated, product inventory needs to be updated, out-of-stock products need to be reordered, and so on.

In part due to the common need to support the same business services through different applications and in part due to their relative stability, there is a wide agreement in the software development industry that separating the business logic from its presentation is beneficial as it allows reusing
