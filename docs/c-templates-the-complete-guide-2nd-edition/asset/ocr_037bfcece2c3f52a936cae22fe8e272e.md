```
template<typename T>
class Trap {
public:
enum { x }; // #1 x is not a type here
};

template<typename T>
class Victim {
public:
int y;
void poof() {
Trap<T>::x * y; // #2 declaration or multiplication?
}
};

template<>
class Trap<void> { //evil specialization!
public:
using x = int; // #3 x is a type here
};

void boom(Victim<void>& bomb)
{
bomb.poof();
}
```

As the compiler is parsing line #2 , it must decide whether it is seeing a declaration or a multiplication. This decision in turn depends on whether the dependent qualified name Trap<T>::x is a type name. It may be tempting to look in the template Trap at this point and find that, according to line #1 , Trap<T>::x is not a type, which would leave us to believe that line #2 is a multiplication. However, a little later the source corrupts this idea by overriding the generic Trap<T>::x for the case where T is void. In this case, Trap<T>::x is in fact type int.

In this example, the type Trap<T> is a dependent type because the type depends on the template parameter T. Moreover, Trap<T> refers to an unknown specialization (described in Section 13.2.4 on page 223), which means that the compiler cannot safely look inside the template to determine whether the name Trap<T>::x is a type or not. Had the type preceding the :: referred to a current instantiation—for example, with Victim<T>::y—the compiler could have looked into the template definition because it is certain that no other specialization could intervene. Thus, when the type preceding :: refers to the current instantiation, qualified name lookup in a template behaves very similarly to qualified name lookup for nondependent types.

However, as illustrated by the example, name lookup into an unknown