# 4.4 Combination of Classes — 139

```
class A          //definition of class A
{
  public:
    //external interface
    void f(B b); //member function with object b of class B
                //as parameter, which cause compile error,
                //because 'B' is an unknown symbol.

};
class B          //definition of class B
{
  public:
    //external interface
    void g(A a); //function member with object a of class A
                //as parameter
};
```

Here the parameter of the public member function f of class A is an object of class B, while the parameter of the public member function g of class B is an object of class A. Because a class must be defined before it is used, no matter the definition of which class is put at the front, it will cause a compiling error. One way to solve this problem is to use forward declaration. Forward declaration means telling the name of an undefined class to the compiler so the compiler knows it. When this name is used in the program, the compiler won't consider it an error, and the complete definition of the class can be put elsewhere in the program. By adding forward declaration to the program we talked above, the problem will be solved:

```
class B; //Forward declaration
class A          //definition of class A
{
  public:
    //external interface
    void f(B b); //member function with object b of class B
                //as parameter
};
class B          //definition of class B
{
  public:
    //external interface
    void g(A a); //function member with object a of class A
                //as parameter
};
```

Forward declaration can help in some situations, but it is not omnipotent. It is important to know that even if forward declaration is used, we can't define an object of this class or use an object of this class in an inline function before we provide a complete definition of the class. Let's see the code below: