![](bbox=[0.133, 0.136, 0.208, 0.208])

Always pass objects as pointers. Don’t pass objects directly into functions. Yes, it risks bad code changing the object, but careful C++ programmers want the actual object, not a copy. That outweighs the risk of an accidental change. This chapter explains how to prevent accidental changes by using the const parameters.

So just do this:

```
```cpp
void FixFlatTire(Car *mycar);
```
```

If you like references, you are welcome to do this:

```
```cpp
void FixFlatTire(Car &mycar);
```
```

But don’t just pass the object. It’s messy and not nice.

Because your function receives its objects as pointers, you continue accessing them by using the -> notation. For example, the function FixFlatTire may do this:

```
```cpp
void FixFlatTire(Car *mycar)
{
    mycar->RemoveTire();
    mycar->AddNewTire();
}
```
```

Or, if you prefer references, you would do this:

```
```cpp
void FixFlatTire2(Car &mycar)
{
    mycar.RemoveTire();
    mycar.AddNewTire();
}
```
```

In this code, because you’re dealing with a reference, you access the object’s members using the dot rather than the -> notation.

![](bbox=[0.133, 0.702, 0.208, 0.775])

Another reason to use only pointers and references as parameters for objects is that a function that takes an object as a parameter usually wants to change the function. Such changes require pointers or references. When you don’t want the function to modify the object, use const, which is covered in the following section.

# Using const parameters in functions

The “Passing By const Reference” section of Book I Chapter 7 explains how to use constant parameters with standard variable types. The const keyword is useful when working with objects because you generally don’t want to pass an object directly. That involves copying the object, which is messy. Instead, you normally pass by using a pointer or reference, which would allow you to change the object. If you put the word const before the

![](bbox=[0.882, 0.136, 1.0, 0.304])