
```cpp
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
    Magnificent(int h = 0, char cv = 'A') : Superb(h), ch(cv) {}
    void Speak() const { cout << "I am a magnificent class!!!\n"; }
    void Say() const { cout << "I hold the character " << ch <<
                " and the integer " << Value() << "!\n"; }
};

Grand * GetOne();
int main()
{
    srand(time(0));
    Grand * pg;
    Superb * ps;
    for (int i = 0; i < 5; i++)
    {
        pg = GetOne();
        cout << "Now processing type " << typeid(*pg).name() << ".\n";
        pg->Speak();
        if (ps = dynamic_cast<Superb *>(pg))
            ps->Say();
        if (typeid(Magnificent) == typeid(*pg))
            cout << "Yes, you're really magnificent.\n";
    }
    return 0;
}

Grand * GetOne()
{
    Grand * p;

    switch( rand() % 3)
    {
        case 0: p = new Grand(rand() % 100);
                break;
        case 1: p = new Superb(rand() % 100);
                break;
        case 2: p = new Magnificent(rand() % 100, 'A' + rand() % 26);
                break;
    }
    return p;
}
```

Here’s a sample run of the program in Listing 15.18:

```text
Now processing type Magnificent.
I am a magnificent class!!!
I hold the character P and the integer 52!
Yes, you're really magnificent.
Now processing type Superb.
I am a superb class!!
I hold the superb value of 37!
Now processing type Grand.
I am a grand class!
Now processing type Superb.
I am a superb class!!
I hold the superb value of 18!
Now processing type Grand.
I am a grand class!
```

As with the preceding example, the exact output will vary from run to run because the program uses `rand()` to select types. Also some compilers may provide different output when `name()` is called, for example, `Grand` instead of `Grand`.

## Misusing RTTI

RTTI has many vocal critics within the C++ community. They view RTTI as unnecessary, a potential source of program inefficiency, and a possible contributor to bad programming practices. Without delving into the debate over RTTI, let’s look at the sort of programming that you should avoid.

Consider the core of Listing 15.17:

```cpp
Grand * pg;
Superb * ps;
for (int i = 0; i < 5; i++)
{
    pg = GetOne();
    pg->Speak();
    if (ps = dynamic_cast<Superb *>(pg))
        ps->Say();
}
```

By using typeid and ignoring dynamic_cast and virtual functions, you can rewrite this code as follows:

```cpp
Grand * pg;
Superb * ps;
Magnificent * pm;
for (int i = 0; i < 5; i++)
{
    pg = GetOne();
    if (typeid(Magnificent) == typeid(*pg))
    {
        pm = (Magnificent *) pg;
        pm->Speak();
        pm->Say();
    }
    else if (typeid(Superb) == typeid(*pg))
    {
        ps = (Superb *) pg;
        ps->Speak();
        ps->Say();
    }
    else
        pg->Speak();
}
```

Not only is this uglier and longer than the original, it has the serious flaw of naming each class explicitly. Suppose, for example, that you find it necessary to derive an Insufferable class from the Magnificent class. And suppose the new class redefines Speak() and Say(). With the version that uses typeid to test explicitly for each type, you would have to modify the for loop code, adding a new else if section. The original version, however, requires no changes at all. The following statement works for all classes derived from Grand:

```cpp
pg->Speak();
```

And this statement works for all classes derived from Superb:

```cpp
if (ps = dynamic_cast<Superb *>(pg))
    ps->Say();
```

**Tip**

If you find yourself using `typeid` in an extended series of `if else` statements, you should check whether you should instead use virtual functions and `dynamic_cast`.

## Type Cast Operators

The C type cast operator, in Bjarne Stroustrup’s view, is too lax. For example, consider the following:

```cpp
struct Data
{
    double data[200];
};

struct Junk
{
    int junk[100];
};
Data d = {2.5e33, 3.5e-19, 20.2e32};
char * pch = (char *) (&d);   // type cast #1 - convert to string
char ch = (char) (&d);        // type cast #2 - convert address to a char
Junk * pj = (Junk *) (&d);    // type cast #3 - convert to Junk pointer
```

First, which of these three type casts makes any sense? Unless you resort to the implausible, none of them make much sense. Second, which of these three type casts are allowed? In C, all of them are. Stroustrup’s response to this laxity was to tighten up what is allowable for a general type cast and to add four type cast operators that provide more discipline for the casting process:

```cpp
dynamic_cast
const_cast
static_cast
reinterpret_cast
```

Instead of using a general type cast, you can select an operator that is suited to a particular purpose. This documents the intended reason for the type cast and gives the compiler a chance to check that you did what you thought you did.

You’ve already seen the `dynamic_cast` operator. To summarize, suppose High and Low are two classes, that `ph` is type `High *`, and that `pl` is type `Low *`. Then the following statement assigns a `Low *` pointer to `pl` only if Low is an accessible base class (direct or indirect) to High:

```cpp
pl = dynamic_cast<Low *>(ph);
```

Otherwise, the statement assigns the null pointer to `pl`. In general, the operator has this syntax:

```cpp
dynamic_cast < type-name > (expression)
```

The purpose of this operator is to allow upcasts within a class hierarchy (such type casts being safe because of the is-a relationship) and to disallow other casts.

The const_cast operator is for making a type cast with the sole purpose of changing whether a value is const or volatile. It has the same syntax as the dynamic_cast operator:

```cpp
const_cast < type-name > (expression)
```

The result of making such a type cast is an error if any other aspect of the type is altered. That is, type_name and expression must be of the same type, except that they can differ in the presence or absence of const or volatile. Again, suppose High and Low are two classes:

```cpp
High bar;
const High * pbar = &bar;
...
High * pb = const_cast<High *> (pbar);    // valid
const Low * pl = const_cast<const Low *> (pbar);    // invalid
```

The first type cast makes *pb a pointer that can be used to alter the value of the bar object; it removes the const label. The second type cast is invalid because it attempts to change the type from const High * to const Low *.

The reason for this operator is that occasionally you may have a need for a value that is constant most of the time but that can be changed occasionally. In such a case, you can declare the value as const and use const_cast when you need to alter the value. This could be done using the general type cast, but the general type cast can also simultaneously change the type:

```cpp
High bar;
const High * pbar = &bar;
...
High * pb = (High *) (pbar);       // valid
Low * pl = (Low *) (pbar);         // also valid
```

Because the simultaneous change of type and constness may be an unintentional programming slip, using the const_cast operator is safer.

The const_cast is not all powerful. It can change the pointer access to a quantity, but the effect of attempting to change a quantity that is declared const is undefined. Let's clarify this statement with the short example shown in Listing 15.19.

### Listing 15.19  constcast.cpp

```cpp
// constcast.cpp -- using const_cast<>
#include <iostream>
using std::cout;
using std::endl;

void change(const int * pt, int n);

int main()
{
    int pop1 = 38383;
    const int pop2 = 2000;

    cout << "pop1, pop2: " << pop1 << ", " << pop2 << endl;
    change(&pop1, -103);
    change(&pop2, -103);
    cout << "pop1, pop2: " << pop1 << ", " << pop2 << endl;
    return 0;
}

void change(const int * pt, int n)
{
    int * pc;

    pc = const_cast<int *>(pt);
    *pc += n;
}
```

The `const_cast` operator can remove the const from `const int * pt`, thus allowing the compiler to accept the following statement in `change()`:

```cpp
*pc += n;
```

However, because `pop2` is declared as const, the compiler may protect it from any change, as is shown by the following sample output:

```text
pop1, pop2: 38383, 2000
pop1, pop2: 38280, 2000
```

As you can see, the calls to `change()` alter `pop1` but not `pop2`. The pointer in `change()` is declared as `const int *`, so it can’t be used to change the value of the pointed-to int. The pointer `pc` has the const cast away, so it can be used to change the pointed-to value, but only if that value wasn’t itself const. Therefore, `pc` can be used to alter `pop1` but not `pop2`.

The `static_cast` operator has the same syntax as the other operators:

```cpp
static_cast < type-name > (expression)
```

It’s valid only if `type_name` can be converted implicitly to the same type that `expression` has, or vice versa. Otherwise, the type cast is an error. Suppose that High is a base class to Low and that Pond is an unrelated class. Then conversions from High to Low and Low to High are valid, but a conversion from Low to Pond is disallowed:

```cpp
High bar;
Low blow;
...
```
