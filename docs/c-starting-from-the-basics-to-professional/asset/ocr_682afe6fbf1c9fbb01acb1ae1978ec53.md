You can consult your compiler’s documentation on how to interpret these names or possibly even on how to convert them to a human-readable format. Normally, the mangled names themselves should already carry sufficient information for you to follow this discussion.

The Ex15_09 test program consists of five parts, each illustrating a particular aspect of using the `typeid()` operator. We’ll discuss each of them in turn.

In the first part, we apply `typeid()` on a hard-coded type name. In itself, this is not that interesting, at least not until you compare the resulting type_info to the result of applying `typeid()` to an actual value or expression, as shown in the second statement of `main()`. Note that the compiler does not perform any implicit conversions with type names. That is, `typeid(1) == int` is not legal C++; you have to explicitly apply the `typeid()` operator, as in `typeid(1) == typeid(int)`.

The second part of the program demonstrates that `typeid()` can indeed be used to determine the dynamic type of an object of a polymorphic type—the main topic of this section. Even though the static type of the `boxReference` variable is `Box&`, the program’s output should reflect that `typeid()` correctly determines the object’s dynamic type: `Carton`.

The third part of the program shows you that `typeid()` does not work with pointers in quite the same way as it does with references. Even though `boxPointer` points to a Carton object, the result of `typeid(boxPointer)` does not represent `Carton*`; instead, it simply reflects the static type of `boxPointer`: `Box*`. To determine the dynamic type of the object pointed to by a pointer, you therefore have to dereference the pointer first. The outcome of `typeid(*boxPointer)` shows that this indeed works.

The program’s fourth part illustrates that there is no way to determine the dynamic type of objects of nonpolymorphic types. To test this, we quickly define two simple classes, `NonPolyBase` and `NonPolyDerived`, both trivially nonpolymorphic. Even though `baseRef` is a reference to an object of dynamic type `NonPolyDerived`, `typeid(baseRef)` evaluates to the static type of the expression instead, which is `NonPolyBase`. You can see the difference if you turn `NonPolyBase` into a polymorphic class, such as by adding a defaulted virtual destructor like this:

```
class NonPolyBase { public: virtual ~NonPolyBase() = default; };
```

If you then run the program again, the output should show that `typeid(baseRef)` now resolves to the `type_info` value for the `NonPolyDerived` type.

> **Note** To determine the dynamic type of an object, the `typeid()` operator needs so-called runtime type information (RTTI for short), which is normally accessed through the object’s vtable.¹ Because only objects of polymorphic types contain a vtable reference, `typeid()` can determine the dynamic type only for objects of polymorphic types. (This, by the way, is also why `dynamic_cast<>` works only for polymorphic types.)

In the fifth and final part, you learn that the expression passed as an operand to `typeid()` is evaluated if and only if it has a polymorphic type; from the program’s output, you should be able to read that the `getSomeBox()` got called, but `getSomeNonPoly()` did not. In a way, this is logical. In the former case, `typeid()` needs to determine the dynamic type because `getSomeBox()` evaluates to a reference to a polymorphic type. Without executing the function, the compiler has no way of determining the dynamic type of its result. The `getSomeNonPoly()` function, on the other hand, evaluates to a reference to a nonpolymorphic type. In this case, all the `typeid()` operator needs is the static type, which is something the compiler already knows at compile time simply by looking at the function’s return type.

¹ Some compilers don’t enable runtime type identification by default, so if this doesn’t work, look for a compiler option to switch it on.