This is the reason why a function prototype must precede calls to that function. Because a prototype is a declaration of the function, it begins the scope of the function. Calls to that function later in the program thus lie within its scope.

Identifiers that are declared in a library's header file, such as cin, cout, cerr, and clog in iostream and the class string in the string library, are also governed by Scope Rule S4. When the compiler processes a #include directive outside all blocks as in

```
#include <iostream>
using namespace std;

int main()
{
...
}
```

all objects in that file are inserted outside all blocks and thus fall under Scope Rule S4. The scope of such declarations thus extends from their declarations (i.e., from the #include directive) to the end of the file.

# 10.4.1.3 Scopes of for-Loop Control Variables

Scope Rule S3 governs the scope of an identifier declared in the initialization expression of a for loop. To illustrate it, suppose that a program contains the statements

```
for (int i = 1; i <= someLimit; i++)
{
...
}

cout << "i = " << i << endl;        // ERROR
```

When the program is compiled, an error message like

```
Identifier 'i' is undeclared
```

results because Scope Rule S3 asserts that the scope of i ends at the bottom of the loop, so the output statement lies outside the scope of i. But this also means that i could be redeclared and used after the loop has ended. For example, it could be used in a later for loop,

```
for (int i = 1; i <= 100; i++)
{
...
}
...

for (int i = 50; i > 0; i--)
{
...
}
```