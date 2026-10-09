• No arguments. If you send no arguments, the length of the params list is zero.

# Private Access Modifier (private)

The private keyword is a member access modifier.

Private access is the least permissive access level. Private members are accessible only within the body of the class or the struct in which they are declared, as in this example:

```
```c++
class Employee
{
    private int i;
    double d;   // private access by default
}
```
```

Nested types in the same body can also access those private members.

It is a compile-time error to reference a private member outside the class or the struct in which it is declared.

# Protected Access Modifier (protected)

The protected keyword is a member access modifier.

A protected member is accessible within its class and by derived class instances.

# Public Access Modifier (public)

The public keyword is an access modifier for types and type members. Public access is the most permissive access level. There are no restrictions on accessing public members, as in this example: