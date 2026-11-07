Look closely at the output of the statements in Lines 7 and 9 (the last two lines of output). In Line 9, because the formal parameter `p` is a value parameter, the member variables of `dog` are copied into the corresponding member variables of `p`. However, because `p` is an object of type `petType`, it has only one member variable. Consequently, only the member variable name of `dog` is copied into the member variable name of `p`. Moreover, the statement `p.print();` in the function `callPrint` executes the function `print` of the `class petType`, not of the `class dogType`. Therefore, the last line of the output shows only the value of `name` (the member variable of `dog`).

> > **NOTE**
> >
> > An object of the base class type cannot be passed to a formal parameter of the derived class type.

Before closing this section, we discuss another issue related to virtual functions.

Suppose that the definition of the `class petType` is as before, and the definition of the `class dogType` is modified slightly as follows:

```
```cpp
class dogType: public petType
{
public:
    void print();
    void setBreed(string b = "");
    dogType(string n = "", string b = "");

private:
    string breed;
};
```
```

Consider the following statements:

```
```cpp
petType pet("Lucky");
dogType dog("Tommy", "German Shepherd");
```
```

```
```cpp
pet = dog;
```
```

C++ allows this type of assignment, that is, the values of a derived class object can be copied into a base class object. (Note that the reverse statement, that is, `dog = pet;` is not allowed.) Now, because the object `pet` has only one data member (`name`) and the object `dog` has two data members (`name` and `breed`), only the value of the data member `name` of `dog` is copied into the data member `name` of `pet`. This is called the **slicing problem**. The following statement will result in a compile-time error.

```
```cpp
pet.setBreed("Siberian Husky");
```
```

C++ offers a way to treat a `dogType` object as a `petType` object without losing the additional properties of the `class dogType` by using pointers.