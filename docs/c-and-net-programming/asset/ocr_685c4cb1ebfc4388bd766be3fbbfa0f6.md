```
}
}
```

# Generics in inheritance

# Generic Class as Base Class

In C# the generic class can used as a base class, but there is need to provide a type instead of type parameter for the base class because there is no way to send a required type argument to instantiate a base class at run time. Hence, while deriving from a generic base class, one must provide a type argument instead of the base-class's generic type parameter as shown below.

```
// Below code do not have any Error
class DerivedClass1 : GenericClass<string> {
// implementation
}
// Where as in below code there is Compile Time Error
//class DerivedClass2 : GenericClass<T> {
// // implementation
//}
```

```
Example: Generic base class
class DerivedClass1 : GenericClass1<string>
{
    //implementation
}
```

If the derived class is required to be generic then no need to specify type for the generic base class.

Example : Generic derived class

```
class DerivedClass1<U> : GenericClass1<U>
{
    //implementation
}
```

**If the generic base class has constraints, the derived class must use the same constraints.**

Example : Constraints

```
class GenericClass1<T> where T: class
{
    // Implementation
}
class DerivedClass1<U> : GenericClass1<U> where U: class
{
    //implementation
}
```