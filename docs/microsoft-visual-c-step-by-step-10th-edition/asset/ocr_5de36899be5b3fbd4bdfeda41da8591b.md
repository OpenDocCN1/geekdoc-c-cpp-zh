9. Add the overloaded + operator to the Complex struct as shown in bold in the code that follows:

Click here to view code image

```
struct Complex
{
  ..
  public static Complex operator +(Complex lhs, Complex rhs)
  => new Complex(lhs.Real + rhs.Real, lhs.Imaginary + rhs.Imaginary);
}
```

This is the binary addition operator. It adds two Complex objects together by performing the calculation shown in the table preceding the exercise. The operator returns a new Complex object containing the results of this calculation.

10. Add the overloaded - operator to the Complex struct.

Click here to view code image

```
struct Complex
{
  ..
  public static Complex operator -(Complex lhs, Complex rhs)
  => new Complex(lhs.Real - rhs.Real, lhs.Imaginary - rhs.Imaginary);
}
```

This operator follows the same form as the overloaded + operator.

11. Implement the * operator and / operators by adding the code shown in bold to the Complex struct.

Click here to view code image

```
struct Complex
{
  ..
  public static Complex operator *(Complex lhs, Complex rhs)
  =>
```