a reference to the current object, the name of the enumeration, and a reference to the ValidationResults instance being use to hold all of the validation errors.

# ValidationResults

```
Dim enumConverterValidator = New EnumConversionValidator(GetType(ProductType), _ "Product type must be a value from the '(3)' enumeration.") _ enumConverterValidator.DoValidate(ProductType, Me, "ProductType"), results)
```

The code that creates the object to validate, validates it, and then displays the results is the same as you saw in the previous example, with the exception that it creates an invalid instance of the AnnotatedProduct class, rather than the AttributedProduct class. The result when you run this example is also similar to that of the previous example, but with a few exceptions. We've listed some of the output here.

```
Created and populated an invalid instance of the AnnotatedProduct class.
The following 7 validation errors were detected:
+ Target object: AnnotatedProduct, Member: ID
- Detected by: [none]
- Tag value:
- Message: 'Product ID must be 6 characters.'
...
+ Target object: AnnotatedProduct, Member: ProductSelfValidation
- Detected by: [none]
- Tag value:
- Message: 'Total inventory (in stock and on order) cannot exceed 100 items.'
+ Target object: AnnotatedProduct, Member: ID
- Detected by: ValidationAttributeValidator
- Message: 'Product ID must be 2 capital letters and 4 numbers.'
+ Target object: AnnotatedProduct, Member: InStock
- Detected by: ValidationAttributeValidator
- Message: 'Quantity in stock cannot be less than 0.'
```

You can see that validation failures detected for data annotations contain less information than those detected for the Validation block attributes, and validation errors are shown as being detected by the ValidationAttributeValidator class—the base class for data annotation validation attributes. However, where we performed additional validation using the self-validation method, there is extra information available.

# Defining Attributes in Metadata Classes

In some cases, you may want to locate your validation attributes (both Validation block attributes and .NET Data Annotation validation attributes) in a file separate from the one that defines the class that you will validate. This is a common scenario when you are using tools that generate the class files, and would therefore overwrite your validation attributes. To avoid this you can locate your validation attributes in a separate file that forms a partial class along with the main class file. This approach makes use of the Meta dataType attribute from the System.ComponentModel.DataAnnotations namespace.

You apply the MetadataType attribute to your main class file, specifying the type of the class that stores the validation attributes you want to apply to your main class