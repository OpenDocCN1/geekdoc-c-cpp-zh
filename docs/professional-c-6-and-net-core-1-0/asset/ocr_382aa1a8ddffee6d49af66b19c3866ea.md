of type array or IEnumerable<T>.

Because metadata is applied with the export, the type of the property that matches the Add export is an array of Lazy<IBinaryOperation, SpeedMetadata> (code file UICalculator/SimpleCalculator/Calculator.cs):

```
[ImportMany("Add")]
public Lazy<IBinaryOperation, SpeedMetadata>[] AddMethods { get; set; }
```

ImportMany is explained with more detail in the next section. The Lazy type allows accessing metadata with the generic definition Lazy<T, TMetadata>. The class Lazy<T> is used to support lazy initialization of types on first use. Lazy<T, TMetadata> derives from Lazy<T> and supports, in addition to the base class, access to metadata information with the Metadata property.

The call to the Add method is now changed to iterate through the collection of Lazy<IBinaryOperation, SpeedMetadata> elements. With the Metadata property, the key for the capability is checked; if the Speed capability has the value Speed.Fast, the operation is invoked by using the Value property of Lazy<T> to invoke the operation (code file UICalculator/SimpleCalculator/Calculator.cs):

```
public double Operate(IOperation operation, double[] operands)
{
    double result = 0;
    switch (operation.Name)
    {
    case"+":
        foreach (var addMethod in AddMethods)
        {
            if (addMethod.Metadata.Speed == Speed.Fast)
            {
                result = addMethod.Value.Operation(operands[0], operands[1]);
            }
        }
        break;
        // etc.
```

# Using Metadata for Lazy Loading

Using metadata with Microsoft Composition is not only useful for selecting parts based on metadata information. Another great use is providing information to the host application about the part before the part is instantiated.

The following example is implemented to offer a title, a description, and a link to an image for the calculator extensions FuelEconomy and TemperatureConversion (code file UICalculator/CalculatorUtils/CalculatorExtensionMetadataAttribute

```
[MetadataAttribute]
[AttributeUsage(AttributeTargets.Class)]
public class CalculatorExtensionMetadataAttribute: Attribute
```