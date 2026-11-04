**TABLE 26-1**

| TYPE | OPERATORS |
|------|-----------|
| Unary | +, -, !, ~, ++, -- |
| Binary | +, -, *, /, %, &, \|, ^, <<, >> |
| Comparison | ==, !=, <, >, <=, >= |

The comparison operators come in pairs. For example, if you overload the < operator, you must also overload the > operator.

The compound assignment operators (+=, -=, *=, /=, %=, &=, |=, ^=, <<=, and >>=) are automatically overloaded when you overload the corresponding binary operator. For example, if you overload *, C# automatically overloads *= for you.

The syntax for overloading operators is easiest to understand by looking at examples. The following sections explain how to overload the different types of operators.

# ## UNARY OPERATORS

The following code shows how you can overload the unary - operator for the ComplexNumber class:

```
```csharp
public static ComplexNumber operator -(ComplexNumber me)
{
    return new ComplexNumber(-me.Real, -me.Imaginary);
}
```
```

The method begins with public static followed by the operator's return type. In this case the operator returns a ComplexNumber because the negation of a complex number is another complex number.

Next comes the keyword operator and the operator's symbol, in this case -.

The parameter list tells on which class the operator should be defined. Because this code is defining an operator for the ComplexNumber class, that's the parameter's data type. I often name this parameter me to help me remember that this is the object to which the operator is being applied.

Note that the overload must be declared inside the class used by the parameter. In this case, the parameter is a ComplexNumber so this code must be in the ComplexNumber class.

The code inside this method simply negates the ComplexNumber's real and imaginary parts and returns a new ComplexNumber.

The following code shows how a program might use this operator:

```
```csharp
ComplexNumber a = new ComplexNumber(1, 2);    //  1 + 2i
ComplexNumber minusA = -a;                    // -1 - 2i
```
```