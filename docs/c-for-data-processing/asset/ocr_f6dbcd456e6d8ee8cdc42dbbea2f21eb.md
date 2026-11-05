```
```csharp
heightString = Console.ReadLine();
height = double.Parse(heightString);
```
```

These two statements simply repeat the process of reading in the text of the height value and then converting it into a double precision value holding the height of the window.

```
```csharp
woodLength = 2*(width + height)*3.25 ;
```
```

When I write programs I use brackets even when the compiler does not need them. This makes the program clearer.

This is the actual nub of the program itself. This is the bit that does the work. It takes the height and width values and uses them to calculate the length of wood required.

The calculation is an expression much like above, this time it is important that you notice the use of parenthesis to modify the order in which values are calculated in the expression. Normally C# will work out expressions in the way you would expect, i.e. all multiplication and division will be done first, followed by addition and subtraction. In the above expression I wanted to do some parts first, so I did what you would do in mathematics, I put brackets around the parts to be done first.

Note that I use a factor of 3.25 to allow for the fact that the customer wants the length of wood in feet. There are around 3.25 feet in a meter, so I multiply the result in meters by this factor.

The + and * characters in the expression are called *operators* in that they cause an operation to take place. The other items in the expression are called *operands*. These are what the operators work on.

```
```csharp
glassArea = 2 * ( width * height ) ;
```
```

This line repeats the calculation for the area of the glass. Note that the area is given in square meters, so no conversion is required. I've put one multiplication in brackets to allow me to indicate that I am working out two times the area (i.e. for two panes of glass). There is no need to do this particularly, but I think it makes it slightly clearer.

```
```csharp
Console.WriteLine
```
```

This is a call of a method, just like the ReadLine method, except that this one takes what it is given and then prints it out on the console.

```
```csharp
(
```
```

This is the start of the *parameters* for this method call. We have seen these used in the calls of Parse and also ReadLine

```
```csharp
"The length of the wood is "
```
```

This is a *string literal*. It is a string of text which is literally just in the program. The string of text is enclosed in double quote characters to tell the compiler that this is part of a value in the program, not instructions to the compiler itself.

```
```csharp
+
```
```

Plus is an addition operator. We have seen it applied to add two integers together. However, the plus here means something completely different. In this case it means "add two strings together".