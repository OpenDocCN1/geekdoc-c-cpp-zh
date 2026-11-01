# NOTE

You could also have placed the CustomValidationAttribute on the Order class itself to achieve the same effect. It is largely a matter of personal preference. Placing data annotation attributes on the private Metadata class helps keep the entity class clean and prevents unnecessary details from leaking into help files you might be generating from the documentation comments using tools like Sandcastle.

Here is the updated version of the validation method itself:

```
public static ValidationResult ValidateOrderDate(
    Order order, ValidationContext context)
{
    if (order.OrderStatus == null)
    {
        if (order.OrderDate != null &&
            order.OrderDate.Value < DateTime.Today)
        {
            return new ValidationResult(
                "Order Date cannot be in the past",
                new string[] { "OrderDate" });
        }
    }

    return ValidationResult.Success;
}
```

The new version of the validation method takes an Order as its first parameter and uses this instance to access values of the OrderStatus and OrderDate properties. Unfortunately, now that the method is validating the Order entity, you can no longer use DisplayName and MemberName properties of the ValidationContext object to generate the ValidationResult. For simplicity, they are hard-coded in this example, although it would have been better to either use string constants or resources.

# NOTE

The ValidationContext object the custom validation methods receive as a second parameter has a property called ObjectInstance, which allows you to access the entity instance even in property validation methods. Although this works fine in the programmatic tests, when a property validation method is invoked during a web page post-back by DynamicValidator controls, the original entity instance does not exist, and all you have is a property value. In other words, if you need to access multiple entity properties to perform validation, you have to use class-level validation methods.