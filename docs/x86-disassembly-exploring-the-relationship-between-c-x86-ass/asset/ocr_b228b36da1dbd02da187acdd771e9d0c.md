# Objects and Classes

```
push 1
push [ebp4]
call 0x00498372
; int a
; the address of the object
; call to function
```

Figure 5: A function call.
Figure 5.A: A function call in the C++ syntax. foo() is taking four arguments, one pointer and three integers.
Figure 5.B: The same call in x86 assembly. It takes four arguments, the address of the object and three integers. The pointer to the object is ebp-4 and the method is at address 0x00498372.

# 20.2.3 Inheritance & Polymorphism

Inheritance and polymorphism completely changes the structure of a class, the object no longer contains just variables, they also pointers to the inherited methods. This is due to the fact that polymorphism requires the address of main or inner object to be figured out at runtime.

Take Figure 6 into consideration. How does the application know to call D::one or C::one? The answer is that the compiler uses a convention in which to order variables and method pointers inside the object that when they're referenced, the offsets are the same for any object that has inherited its methods and variables.

```
* obj[2];
obj[0] = new C();
[1] = new D();

for(int i=0; i<2; i++)
obj[i]->one();
```

Figure 6: A small C++ polymorphic loop that calls a function, one. The classes C and D both inherit an abstract class, A. The class A, for this code to work, must have a virtual method with the name, "one."*

The abstract class A acts as a blueprint for the compiler, defining an expected structure for any class in A and every virtual method defined in A will have the exact same offset for any of its children. Figure 7 details a possible inheritance scheme as well as its storage in memory. Notice how the offset to C::one is the same as D::one, and the offset to C's copy of A::a is the same as D's copy. In this, our polymorphic loop can just iterate through the array of pointers and know exactly where to find each method.

A:

```
class A{
public:
	intint a;
	virtual void one() = 0;
```