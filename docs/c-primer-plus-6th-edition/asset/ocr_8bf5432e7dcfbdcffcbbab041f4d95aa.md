# Pointers, Arrays, and Pointer Arithmetic 179

```
struct things {
  int good;
  int bad;
}
```

![](bbox=[0.226, 0.198, 0.68, 0.233])

grubose is a structure.

pt points to the grubnose structure.

```
Use .operator with {
  structure name;
}
```

grubnose.good grubnose.bad

```
grubnose structure
Use ->operator with
pointer-to-structure.
```

![](bbox=[0.486, 0.359, 0.663, 0.417])

Figure 4.11 Identifying structure members.

> Tip
Sometimes new C++ users become confused about when to use the dot operator and when to use the arrow operator to specify a structure member. The rule is simple: If the structure identifier is the name of the structure, use the dot operator. If the identifier is a pointer to the structure, use the arrow operator.

A second, uglier approach to accessing structure members is to realize that if ps is a pointer to a structure, (*ps) represents the pointed-to-the structure itself. Then, because ps is a structure, (*ps).price is the price member of the structure. C++ operator precedence rules require that you use parentheses in this construction.

Listing 4.21 uses new to create an unnamed structure and demonstrates both pointer notations for accessing structure members.

# Listing 4.21 newstruct.cpp

```
// newstruct.cpp -- using new with a structure
#include <iostream>
struct inflatable {
  char name[20];
  float volume;
  double price;
}
int main() {
  using namespace std;
}
```