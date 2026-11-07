
That is safe. Yet Cast #3, however, is safe because it assigns the address of a derived-class object to a base-class pointer. That is, public derivation promises that a `Magnificent` object also is a `Superb` object (direct base) and a `Grand` object (indirect base). Thus, it’s safe to assign its address to pointers of all three types. Virtual functions ensure that using pointers of any of the three types to a `Magnificent` object will invoke `Magnificent` methods.

Note that the question of whether a type conversion is safe is both more general and more useful than the question of what kind of object is pointed to. The usual reason for wanting to know the type is so that you can know if it’s safe to invoke a particular method. You don’t necessarily need an exact type match to invoke a method. The type can be a base type for which a virtual version of the method is defined. The next example illustrates this point.

First, however, let’s look at the `dynamic_cast` syntax. The operator is used like this, where `pg` points to an object:

```cpp
Superb * pm = dynamic_cast<Superb *>(pg);
```

This code asks whether the pointer `pg` can be type cast safely (as described previously) to the type `Superb *`. If it can, the operator returns the address of the object. Otherwise it returns 0, the null pointer.

> **Note**
>
> In general, the following expression converts the pointer `pt` to a pointer of type `Type *` if the pointed-to object `(*pt)` is of type `Type` or else derived directly or indirectly from type `Type`:
>
> `dynamic_cast<Type *>(pt)`
>
> Otherwise, the expression evaluates to 0, the null pointer.

Listing 15.17 illustrates the process. First it defines three classes, coincidentally named `Grand`, `Superb`, and `Magnificent`. The `Grand` class defines a virtual `Speak()` function, which each of the other classes redefines. The `Superb` class defines a virtual `Say()` function, which `Magnificent` redefines (see Figure 15.4). The program defines a `GetOne()` function that randomly creates and initializes an object of one of these three types and then returns the address as a type `Grand *` pointer. (The `GetOne()` function simulates an interactive user making decisions.) A loop assigns this pointer to a type `Grand *` variable called `pg` and then uses `pg` to invoke the `Speak()` function. Because this function is virtual, the code correctly invokes the `Speak()` version that is appropriate to the pointed-to object:

```cpp
for (int i = 0; i < 5; i++)
{
    pg = GetOne();
    pg->Speak();
    ...
}
```

![](img/9afc44517b591d64e2e19f623c9308ef_950_0.png)

Figure 15.4   The Grand family of classes.

You can’t use this exact approach (using a pointer-to-Grand) to invoke the Say() function; it’s not defined for the Grand class. However, you can use the dynamic_cast operator to see if pg can be type cast to a pointer to Superb. This will be true if the object is either type Superb or Magnificent. In either case, you can invoke the Say() function safely:

```cpp
if (ps = dynamic_cast<Superb *>(pg))
    ps->Say();
```

Recall that the value of an assignment expression is the value of its left-hand side. Thus, the value of the if condition is ps. If the type cast succeeds, ps is nonzero, or true. If the type cast fails, which it will if pg points to a Grand object, ps is zero, or false. Listing 15.17 shows the full code. (By the way, some compilers, noting that programmers usually use the == operator in an if statement condition, may issue a warning about unintended assignment.)

**Listing 15.17   rtti1.cpp**

```cpp
// rtti1.cpp -- using the RTTI dynamic_cast operator
#include <iostream>
#include <cstdlib>
#include <ctime>

using std::cout;

class Grand
{
private:
    int hold;
public:
    Grand(int h = 0) : hold(h) {}
    virtual void Speak() const { cout << "I am a grand class!\n"; }
    virtual int Value() const { return hold; }
};

class Superb : public Grand
{
public:
    Superb(int h = 0) : Grand(h) {}
    void Speak() const { cout << "I am a superb class!!\n"; }
    virtual void Say() const
        { cout << "I hold the superb value of " << Value() << "!\n"; }
};

class Magnificent : public Superb
{
private:
    char ch;
public:
    Magnificent(int h = 0, char c = 'A') : Superb(h), ch(c) {}
    void Speak() const { cout << "I am a magnificent class!!!\n"; }
    void Say() const { cout << "I hold the character " << ch <<
        " and the integer " << Value() << "!\n"; }
};

Grand * GetOne();

int main()
{
    std::srand(std::time(0));
    Grand * pg;
    Superb * ps;
    for (int i = 0; i < 5; i++)
    {
        pg = GetOne();
        pg->Speak();
        if( ps = dynamic_cast<Superb *>(pg) )
            ps->Say();
    }
    return 0;
}

Grand * GetOne()    // generate one of three kinds of objects randomly
{
    Grand * p;
    switch ( std::rand() % 3)
    {
        case 0: p = new Grand(std::rand() % 100);
                break;
        case 1: p = new Superb(std::rand() % 100);
                break;
        case 2: p = new Magnificent(std::rand() % 100,
                                    'A' + std::rand() % 26);
                break;
    }
    return p;
}
```

> **Note**
>
> Even if your compiler supports RTTI, it might have that feature turned off by default. If the feature is inactive, the program may still compile but produce runtime errors. If you find this to be the case, you should check your documentation or explore the menu options.

The program in Listing 15.17 illustrates an important point. You should use virtual functions when possible and RTTI only when necessary. Here is some sample output:

```text
I am a superb class!!
I hold the superb value of 68!
I am a magnificent class!!!
I hold the character R and the integer 68!
I am a magnificent class!!!
I hold the character D and the integer 12!
I am a magnificent class!!!
I hold the character V and the integer 59!
I am a grand class!
```

As you can see, the Say() methods were invoked just for the Superb and Magnificent classes. (The output will vary from run to run because the program uses rand() to select the object type.)

You can use dynamic_cast with references, too. The usage is slightly different: there is no reference value corresponding to the null-pointer type, so there’s no special reference value that can be used to indicate failure. Instead, when goaded by an improper request, dynamic_cast throws a `bad_cast` exception, which is derived from the exception class and defined in the typeinfo header file. Thus, the operator can be used as follows, where rg is a reference to a Grand object:

```cpp
#include <typeinfo> // for bad_cast
...
try {
    Superb & rs = dynamic_cast<Superb &>(rg);
    ...
}
catch(bad_cast &) {
    ...
};
```

## The `typeid` Operator and `type_info` Class

The `typeid` operator lets you determine whether two objects are the same type. Somewhat like `sizeof`, it accepts two kinds of arguments:

- The name of a class
- An expression that evaluates to an object

The `typeid` operator returns a reference to a `type_info` object, where `type_info` is a class defined in the `typeinfo` header file (formerly `typeinfo.h`). The `type_info` class overloads the `==` and `!=` operators so that you can use these operators to compare types. For example, the following expression evaluates to the bool value true if `pg` points to a Magnificent object and to false otherwise:

```cpp
typeid(Magnificent) == typeid(*pg)
```

If `pg` happens to be a null pointer, the program throws a `bad_typeid` exception. This exception type is derived from the `exception` class and is declared in the `typeinfo` header file.

The implementation of the `type_info` class varies among vendors, but it includes a `name()` member that returns an implementation-dependent string that is typically (but not necessarily) the name of the class. For example, the following statement displays the string defined for the class of the object to which the pointer `pg` points:

```cpp
cout << "Now processing type " << typeid(*pg).name() << ".\n";
```

Listing 15.18 modifies Listing 15.17 so that it uses the `typeid` operator and the `name()` member function. Note that they are used for situations that `dynamic_cast` and virtual functions don’t handle. The `typeid` test is used to select an action that isn’t even a class method, so it can’t be invoked by a class pointer. The `name()` method statement shows how the method can be used in debugging. Note that the program includes the `typeinfo` header file.

**Listing 15.18   rtti2.cpp**

```cpp
// rtti2.cpp -- using dynamic_cast, typeid, and type_info
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <typeinfo>
using namespace std;
```
