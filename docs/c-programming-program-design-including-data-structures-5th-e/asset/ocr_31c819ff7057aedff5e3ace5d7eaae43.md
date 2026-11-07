```
b. `class cClass: public aClass`
{
public:
    void print();
    int sum();
    cClass();
    cClass(int)
};
```

8. Consider the following statements:

```
class yClass
{
public:
    void one();
    void two(int, int);
    yClass();

private:
    int a;
    int b;
};

class xClass: public yClass
{
public:
    void one();
    xClass();

private:
    int z;

};
```

Suppose the following statements are in a user program (client code):

`yClass y;`
`xClass x;`

+   a. The **private** members of `yClass` are **public** members of `xClass`.
+      True or False?

+   b. Mark the following statements as valid or invalid. If a statement is invalid, explain why.

```
i. void yClass::one()
   {
       cout << a + b << endl;
   }
```

```
ii. y.a = 15;
    x.b = 30;
```

```
iii. void xClass::one()
     {
         a = 10;
         b = 15;
         z = 30;
         cout << a + b + z << endl;
     }
```

```
iv. cout << y.a << " " << y.b << " " << x.z << endl;
```

9. Assume the declaration of Exercise 8.

+   a. Write the definition of the default constructor of `yClass` so that the **private** member variables of `yClass` are initialized to 0.