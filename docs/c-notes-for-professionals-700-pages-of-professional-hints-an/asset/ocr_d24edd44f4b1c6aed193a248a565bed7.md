# ## Section 3.15: Class Member Operators: Null Conditional Member Access

```
```csharp
var zipcode = myEmployee?.Address?.ZipCode;
//returns null if the left operand is null.
//the above is the equivalent of:
var zipcode = (string)null;
if (myEmployee != null && myEmployee.Address != null)
    zipcode = myEmployee.Address.ZipCode;
```
```

# ## Section 3.16: Class Member Operators: Null Conditional Indexing

```
```csharp
var letters = null;
char? letter = letters?[1];
Console.WriteLine("Second Letter is {0}",letter);
//in the above example  rather than throwing an error because letters is null
//letter is assigned the value null
```
```

# ## Section 3.17: Postfix and Prefix increment and decrement

Postfix increment X++ will add 1 to x

```
```csharp
var x = 42;
x++;
Console.WriteLine(x); // 43
```
```

Postfix decrement

X--

will subtract one

```
```csharp
var x = 42
x--;
Console.WriteLine(x); // 41
```
```

++x is called prefix increment it increments the value of x and then returns x while x++ returns the value of x and then increments

```
```csharp
var x = 42;
Console.WriteLine(++x); // 43
System.out.println(x); // 43
```
```

while

```
```csharp
var x = 42;
Console.WriteLine(x++); // 42
System.out.println(x); // 43
```
```

both are commonly used in for loop

```
```csharp
for(int i = 0; i < 10; i++)
{
}
```
```