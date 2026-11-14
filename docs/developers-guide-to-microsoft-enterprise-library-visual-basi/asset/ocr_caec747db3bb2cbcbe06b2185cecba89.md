+   • **Creating and Using Individual Validators.** This section shows how you can create and use the validators provided with the block to validate individual values and members of objects.

+   • **WCF Service Validation Integration.** This section describes how you can use the block to validate parameters within a WCF service.

Finally, we'll round off the chapter by looking briefly at how you can integrate the Validation block with user interface technologies such as Windows Forms, WPF, and ASP.NET.

# VALIDATING OBJECTS AND COLLECTIONS OF OBJECTS

The most common scenario when using the Validation block is to validate an instance of a class in your application. The Validation block uses the combination of rules defined in a rule set and validators added as attributes to test the values of members of the class, and the result of executing any self-validation methods within the class.

The Validation block makes it easy to validate entire objects (all or a subset of its members) using a specific type validator or by using the Object validator. You can also validate all of the objects in a collection using the Object Collection validator. We will look at the Object validator and the Object Collection validator later. For the moment, we'll concentrate on creating and using a specific type validator.

# Creating a Type Validator using the ValidatorFactory

You can resolve a ValidatorFactory instance through the Enterprise Library container and use it to create a validator for a specific target type. This validator will validate objects using a rule set, and/or any attributes and self-validation methods the target object contains. To obtain an instance of the ValidatorFactory class, you can use the following code.

```
Dim valFactory As ValidatorFactory _
= EnterpriseLibraryContainer.Current.GetInstance(Of ValidatorFactory)()
```

You can then create a validator for any type you want to validate. For example, this code creates a validator for the Product class and then validates an instance of that class named myProduct.

```
Dim pValidator As Validator(Of Product) _
= valFactory.CreateValidator(Of Product)()
Dim valResults As ValidationResults = pValidator.Validate(myProduct)
```

By default, the validator will use the default rule set defined for the target type (you can define multiple rule sets for a type, and specify one of these as the default for this type). If you want the validator to use a specific rule set, you specify this as the single parameter to the CreateValidator method, as shown here.

```
Dim productValidator As Validator(Of Product) _
= valFactory.CreateValidator(Of Product)("RuleSetName")
Dim valResults As ValidationResults = productValidator.Validate(myProduct)
```