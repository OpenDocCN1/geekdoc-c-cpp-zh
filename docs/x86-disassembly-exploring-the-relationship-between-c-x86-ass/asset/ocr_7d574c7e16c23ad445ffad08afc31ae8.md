```
};
class B {
public:
  int b;
  int c;
  virtual void two() = 0;
};
class C : public A {
public:
  int d;
  void one();
};
class D : public A, public B {
public:
  int e;
  void one();
  void two();
};
```

Object C
0x00200000 dd 0x00423848 ; address of C::; offset =
*word_size 0x00200004 dd 1 ; C,s copy of A::; offset =
*word_size 0x00200008 dd 4 ; C::d ; offset = 4*word_size
Object D
0x00200100 dd 0x00412348 ; address of D::one; offset =
*word_size 0x00200104 dd 1 ; D,s copy of A::; offset =
*word_size 0x00200108 dd 0x00431255 ; address of D::two ; offset =
*4*word_size 0x002001BC dd 2 ; D,s copy of B::b; offset =
*6*word_size 0x00200110 dd 3 ; D,s copy of B::c; offset =
*8*word_size 0x00200114 dd 5 ; D::e; ; offset = 10*word_size

Figure 7. A polymorphism scheme.

Figure 7.A defines the inheritance scheme. It shows that class C inherits class A, and class D inherits class A and class B.
Figure 7.B shows how the inheritance scheme might be structured in memory. Class C's object has everything that was declared in class A in the first two double words. The remainder of the object was defined by class C. Class D's object also has everything that was declared in class A in the first two double words. Then the next three double words are everything declared in class B. And the last double word is the variable defined by class D.

# 20.3 Classes Vs. Structs