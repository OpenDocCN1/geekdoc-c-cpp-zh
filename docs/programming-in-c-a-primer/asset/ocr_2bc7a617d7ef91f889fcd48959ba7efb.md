The process of assigning a smaller type to a larger one is known as widening or promotion and that of assigning a larger type to a smaller one is known as narrowing. Note that narrowing may result in loss of information.

For numeric types, widening implicit conversions exist for all the signed and unsigned types. Figure 5.2 shows the conversion hierarchy chart.

![](bbox=[0.22, 0.25, 0.78, 0.78])

# Fig. 5.2 C# conversion hierarchy chart

In Fig. 5.2, arrows indicate the direction of implicit conversion from source to destination. If a path of arrows can be followed from a source type to a destination type, then an implicit conversion is possible between them. For example, implicit conversions are possible in the following cases:

+   - From byte to decimal
+   - From uint to double
+   - From ushort to long

Note that the conversions in these cases take place in a single operation, not by converting them in stages. Some examples of implicit conversion are:

```
byte x1 = 75;
short x2 = x1;
int x3 = x2;
long x4 = x3;
float x5 = x4;
decimal x6 = x4;
```