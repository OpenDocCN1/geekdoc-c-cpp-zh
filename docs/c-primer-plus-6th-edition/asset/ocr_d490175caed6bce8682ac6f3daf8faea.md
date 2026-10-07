# Chapter 15 Friends, Exceptions, and More

```
Grand * GetOne() // generate one of three kinds of objects randomly
{
    Grand * p;
    switch (std::rand() % 3) {
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

> Note
Even if your compiler supports RTTI, it might have that feature turned off by default. If the feature is inactive, the program may still compile but produce runtime errors. If you find this to be the case, you should check your documentation or explore the menu options.

The program in Listing 15.17 illustrates an important point. You should use virtual functions when possible and RTTI only when necessary. Here is some sample output:

```
I am a superb class!!
I hold the superb value of 68!
I am a magnificent class!!
I hold the character R and the integer 68!
I am a magnificent class!!
I hold the character D and the integer 12!
I am a magnificent class!!
I hold the character V and the integer 59!
I am a grand class!
```

As you can see, the Say() methods were invoked for the Superb and Magnificent classes (The output will vary from run to run because the program uses rand() to select the object type).
You can use dynamic_cast with references, too. The usage is slightly different; there is no reference value corresponding to the null-pointer type, so there's no special reference value that can be used to indicate failure. Instead, when goaded by an improper request, dynamic_cast throws a bad_cast exception, which is derived from the exception class and defined in the typeinfo header file. Thus, the operator can be used as follows, where rg is a reference to a Grand:

```
#include <typeinfo> // for bad_cast
try {
```