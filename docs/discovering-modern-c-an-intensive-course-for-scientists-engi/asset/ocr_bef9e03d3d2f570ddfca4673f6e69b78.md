For instance, if we declare a member of the before-defined `move_only` class in `tray`:

```
class tray
{
    public:
    tray(unsigned s = 0) : v(s) {}
    std::vector<float> v;
    std::set<int> s;
    move_only mo;
};
```

its objects can no longer be copied and copy-assigned. Of course, we are not obliged to rely on the generated copy constructor and assignment; we can write our own.

The rule applies recursively: a method deleted in some type implicitly deletes this method in all classes where it is contained and everywhere those classes are contained and so on.

For instance, in the absence of user-defined copy operations, a class `bucket` containing `tray` cannot be copied; neither can a class `barrel` containing `bucket`, or a class `truck` containing `barrel`, and so on.

# A.5.2.2 Difficult Member Types

Types not providing all six generatable methods can create problems when they are used as member types. The most prominent examples are:

+   • References are not default-constructible. Thus, every class with a reference has no default constructor unless the user implements one. This in turn is difficult too because the referenced address cannot be set later. The easiest work-around is using a pointer internally and providing a reference externally. Unfortunately, the default constructor is needed quite often, e.g., for creating containers of the type.

+   • `unique_ptr` is neither copy-constructible nor copy-assignable. If the class needs one of the copy operations, we have to use another pointer type, e.g., a raw pointer, and live with all its risks, or a `shared_pointer` and accept the performance overhead.

# A.5.2.3 Rule 2: Destructors Are Generated Unless the User Does

This is certainly the simplest rule: either the programmer writes a destructor or the compiler does. Since all types must provide a destructor, Rule 1 is irrelevant here.

# A.5.2.4 Rule 3: Default Constructors Are Generated Alone

The default constructor is the shyest operation when it comes to implicit generation. As soon as `any` other constructor is defined, the default constructor is not generated any longer, e.g.:

```
struct no_default1
{
    no_default1(int) {}
};
```

```
struct no_default2
```