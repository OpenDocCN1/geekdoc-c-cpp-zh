
The primary module interface file for boxes is trivial as always:

```cpp
export module boxes;
export import :box;
export import :tough_pack;
```

And in this case the main program is trivial as well. All it does is create an instance of the derived class ToughPack and then show its volume:

```cpp
// Ex15_08.cpp
// Calling virtual functions from constructors and destructors
import boxes;

int main()
{
    ToughPack toughPack{1.0, 2.0, 3.0};
    toughPack.showVolume();     // Should show a volume equal to 85% of 1x2x3, or 5.1
}
```

This is the resulting output:

```text
Box constructor called for a Box of volume 6
ToughPack constructor called for a Box of volume 5.1
The volume from inside Box::showVolume() is 5.1
ToughPack destructor called for a Box of volume 5.1
Box destructor called for a Box of volume 6
```

Let’s first focus our attention on the middle line of this output, which is the product of the ToughPack::showVolume() function call. ToughPack overrides volume(), so if you call volume() on a ToughPack object, you expect the version of ToughPack to be used, even if this call originates from inside a base class function such as Box::showVolume(). The output clearly shows that this is also what happens. Box::showVolume() prints out a volume of 0.85 * 1 * 2 * 3, or 5.1, as expected.

Now let’s see what happens if you call volume() not from a regular base class member function such as showVolume() but from a base class constructor. The first line in the output shows you that volume() then returns 6. So, it’s clearly the original function of Box that gets called, not the overridden version of ToughPack! Why is that? You’ll recall from the previous chapter that when an object is constructed, all its subobjects are constructed first, including the subobjects of all its base classes. While initializing such a subobject—for instance, the Box subobject of our ToughPack—the object of the derived class will therefore at most be partially initialized. It would in general be extremely dangerous to call member functions on an object whose subobjects have not yet been fully initialized. This is why all function calls from inside a constructor, including those of virtual members, are always resolved statically.

Conversely, when destroying an object, all its subobjects are destructed in the reverse order in which they were constructed. So, by the time the destructor of the base class subobject is called, the derived class is already partially destructed. It would thus again be a bad idea to call members of this derived object. So, all function calls in destructors are thus resolved statically as well.

> **Caution** Virtual function calls made from inside a constructor or a destructor are always resolved statically.
> If you, in rare cases, do need polymorphic calls during initialization, you should do so from within an `init()` member function—often virtual itself—that you then call after the construction of the object has completed.
> This is called the dynamic binding during initialization idiom.

### The Cost of Polymorphism

As you know, there's no such thing as a free lunch, and this also applies to polymorphism. You pay for polymorphism in two ways: it requires more memory, and virtual function calls result in additional runtime overhead. These consequences arise because of the way that virtual function calls are typically implemented in practice. Luckily, both costs are mostly marginal at best and can mostly be ignored.

For instance, suppose two classes, A and B, contain identical member variables, but A contains virtual functions, whereas B's functions are all nonvirtual. In this case, an object of type A requires more memory than an object of type B.

> **Note** You can create a simple program with two such class objects and use the `sizeof` operator to see the difference in memory occupied by objects with and without virtual functions.

The reason for the increase in memory is that when you create an object of a polymorphic class type, a special pointer is created in the object. This pointer is used to call any of the virtual functions in the object. The special pointer points to a table of function pointers that gets created for the class. This table, usually called a *vtable*, has one entry for each virtual function in the class. Figure 15-7 illustrates this.

```cpp
object->doMore();
```

![](img/020c376b6cc4874983a4344f51a256de_570_0.png)

*Figure 15-7. How polymorphic function calls work*

When a function is called through a pointer to a base class object, the following sequence of events occurs:

- 1. The pointer to the vtable in the object pointed to is used to find the beginning of the vtable for the class.
- 2. The entry for the function to be called is found in the vtable, usually by using an offset.
- 3. The function is called indirectly through the function pointer in the vtable. This indirect call is a little slower than a direct call of a nonvirtual function, so each virtual function call carries some overhead.

However, the overhead in calling a virtual function is small and shouldn't give you cause for concern. A few extra bytes per object and slightly slower function calls are small prices to pay for the power and flexibility that polymorphism offers. This explanation is just so you’ll know why the size of an object that has virtual functions is larger than that of an equivalent object that doesn’t.

> **Note** The only time you should even debate whether the overhead of a virtual function table pointer is worth it is when you have many objects of the corresponding type at once. Suppose you have a `Point3D` class that represents a point in 3D space. If your program manipulates millions and millions of such points—a Microsoft Kinect, for instance, produces up to 9 million points per second—then avoiding virtual functions in `Point3D` can save you a significant amount of memory. For most objects, the cost of a virtual function table pointer is only marginal, though, and well worth the benefits.

### Determining the Dynamic Type

Suppose you have a reference to an object of a polymorphic class—which as you recall is a class with at least one virtual function. Then you can determine the dynamic type of this object using the `typeid()` operator. This standard operator returns a reference to a `std::type_info` object that encapsulates the actual type of its operand. Similar in use to the `sizeof` operator, the operand to the `typeid()` operator can be either an expression or a type. Concretely, the semantics of the `typeid()` operator are more or less as follows:

- If its operand is a type, `typeid()` evaluates to a reference to a `type_info` object representing this type.
- If its operand is any expression that evaluates to a reference to a polymorphic type, this expression is evaluated, and the operand returns the dynamic type of the value referred to by the outcome of this evaluation.
- If its operand is any other expression, the expression is **not evaluated**, and the result is the static type of the expression.

The reason we introduce this already more advanced operator to you is because `typeid()` can be a useful learning or debugging aid. It enables you to easily inspect the type of various expressions or to observe the difference between an object’s static and dynamic type.

Let’s create a program to see this operator in action. We’ll again use the Box and Carton classes of Ex15_06. Of course, by now you know that any base class should have a virtual destructor, so naturally we have given the Box class a defaulted virtual destructor this time. But this small change is not that relevant in this example. Here, we’ll use the Box classes to illustrate `typeid()`’s behavior with polymorphic classes.

**Note** To use the `typeid()` operator, you always first have to import the `<typeinfo>` module from the Standard Library. This makes the `std::type_info` class available, which is the type of the object returned by the operator. Note that there is an underscore in the name of the type but not in that of the module. Go figure!

```cpp
// EX15_09.cpp
// Using the typeid() operator
import <iostream>;
import <typeinfo>;    // For the std::type_info class
import boxes;

// Define polymorphic and non-polymorphic base and derived classes:
class NonPolyBase {};
class NonPolyDerived : public NonPolyBase {};

Box& getSomeBox();                 // Function returning a reference to a polymorphic type
NonPolyBase& getSomeNonPoly();     // Function returning a reference to a non-polymorphic type

int main()
{
  // Part 1: typeid() on types and == operator
  std::cout << "Type double has name " << typeid(double).name() << std::endl;
  std::cout << "1 is " << (typeid(1) == typeid(int) ? "an int" : "no int") << std::endl;

  // Part 2: typeid() on polymorphic references
  Carton carton{ 1, 2, 3, "paperboard" };
  Box& boxReference = carton;

  std::cout << "Type of carton is " << typeid(carton).name() << std::endl;
  std::cout << "Type of boxReference is " << typeid(boxReference).name() << std::endl;
  std::cout << "These are " << (typeid(carton) == typeid(boxReference) ? "" : "not ")
            << "equal" << std::endl;

  // Part 3: typeid() on polymorphic pointers
  Box* boxPointer = &carton;
  std::cout << "Type of &carton is " << typeid(carton).name() << std::endl;
  std::cout << "Type of boxPointer is " << typeid(*boxPointer).name() << std::endl;

  // Part 4: typeid() with non-polymorphic classes
  NonPolyDerived derived;
  NonPolyBase& baseRef = derived;

  std::cout << "Type of baseRef is " << typeid(baseRef).name() << std::endl;

  // Part 5: typeid() on expressions
  const auto& type_info1 = typeid(getSomeBox());       // function call evaluated
  const auto& type_info2 = typeid(getSomeNonPoly());   // function call not evaluated
```
