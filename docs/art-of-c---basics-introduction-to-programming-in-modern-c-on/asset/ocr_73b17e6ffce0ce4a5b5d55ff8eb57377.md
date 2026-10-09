When used in a method's parameter list, the ref keyword indicates that an argument is passed by reference, not by value. The ref keyword makes the formal parameter an alias for the argument, which must be a variable. In other words, any operation on the parameter is made on the argument. For example, if the caller passes a local variable expression or an array element access expression, and the called method replaces the object to which the ref parameter refers, then the caller's local variable or the array element now refers to the new object when the method returns.

> Do not confuse the concept of passing by reference with the concept of reference types. The two concepts are not the same. A method parameter can be modified by ref regardless of whether it is a value type or a reference type. There is no boxing of a value type when it is passed by reference.

To use a ref parameter, both the method definition and the calling method must explicitly use the ref keyword.

An argument that is passed to a ref or in parameter must be initialized before it is passed. This differs from out parameters, whose arguments do not have to be explicitly initialized before they are passed.

Members of a class can't have signatures that differ only by ref, in, or out. A compiler error occurs if the only difference between two members of a type is that one of them has a ref parameter and the other has an out, or in parameter. The following code, for example, doesn't compile.

```
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```