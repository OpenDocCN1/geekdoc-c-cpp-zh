All these statements can be rewritten as follows using self-assignment operators:

```
```csharp
salary += 1000;    //---same as salary = salary + 1000---
salary -= 1000;    //---same as salary = salary - 1000---
salary /= 2;       //---same as salary = salary / 2---
salary *= 2;       //---same as salary = salary * 2---
```
```

A self-assignment operator alters its own value before assigning the altered value back to itself. In this example, +=, -=, /=, and *= are all self-assignment operators.

You can also use the modulus self-assignment operator like this:

```
```csharp
int num = 5;
num %= 2; //---num is now 1---
```
```

# Prefix and Postfix Operators

The previous section described the use of the self-assignment operators. For example, to increase the value of a variable by 1, you would write the statement as follows:

```
```csharp
int num = 5;
num += 1; //---num is now 6---
```
```

In C#, you can use the prefix or postfix operator to increment/decrement the value of a variable by 1. The preceding statement could be rewritten using the prefix operator like this:

```
```csharp
++num;
```
```

Alternatively, it could also be rewritten using the postfix operator like this:

```
```csharp
num++;
```
```

To decrement a variable, you can use either the prefix or postfix operator, like this:

```
```csharp
--num;
//---or---
num--;
```
```

So what is the difference between the prefix and postfix operators? The following example makes it clear:

```
```csharp
int num1 = 5;
int num2 = 5;
int result;

result = num1++;
Console.WriteLine(num1); //---6---
Console.WriteLine(result); //---5---

result = ++num2;
Console.WriteLine(num2); //---6---
Console.WriteLine(result); //---6---
```
```