Note: The process of boxing may be imagined in terms of the existence of a boxing class for every value type. For example, consider a struct S implementing an interface I, with a boxing class called S_Boxing.

```
interface I
{
    void M();
}
```

```
struct S : I
{
    public void M() { ... }
}
```

```
sealed class S_Boxing : I
{
    S value;

    public S_Boxing(S value)
    {
        this.value = value;
    }

    public void M()
    {
        value.M();
    }
}
```

Boxing a value v of type S now consists of executing the expression new S_Boxing(v) and returning the resulting instance as a value of the target type of the conversion. Thus, the statements

```
S s = new S();
object box = s;
```

can be thought of as similar to:

```
S s = new S();
object box = new S_Boxing(s);
```

The imagined boxing type described above does not actually exist. Instead, a boxed value of type S has the runtime type S, and a runtime type check using the is operator with a value type as the right operand tests whether the left operand is a boxed version of the right operand. For example,

```
int i = 123;
object box = i;
if (box is int) {
    Console.Write("Box contains an int");
}
```

will output the string "Box contains an int" on the console.

A boxing conversion implies making a copy of the value being boxed. This is different from a conversion of a reference_type to type object, in which the value continues to reference the same instance and simply is regarded as the less derived type object. For example, given the declaration

```
struct Point
{
```