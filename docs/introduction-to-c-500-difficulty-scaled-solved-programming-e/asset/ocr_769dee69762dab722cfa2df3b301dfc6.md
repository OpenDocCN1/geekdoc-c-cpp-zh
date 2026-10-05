presence of set_IP(). So, we need to include Net_Mgt before System. But if we do, the compiler
won't have met the declaration of System and won't be able to process the Net_Mgt functions that take
a System object as argument. Fine, and how do we overcome this circular dependency? As did in
example C13.6, by adding a forward declaration of System. The code is restructured as follows:

```
class System; // Forward declaration (incomplete declaration)
class Net_Mgt { ... };
class System { ... };
```

There is one problem: When the compiler encounters the inline definition of set_IP() in
Net_Mgt it will display an error message because it does not know anything about the System class\and the members it contains, it cannot compile. This is why I chose to make set_IP() inline.
So, if something happens to you, to show how to solve this problem. The solution is to
place the declarations in the Net_Mgt class and their definitions after the declaration of System.
And if you want to make inline just add the word inline in their definition. Thus, the code is
restructured as follows:

```
class System; // Forward declaration
class Net_Mgt { ... }; // Function declarations.
class System { ... };
// Definitions of Net_Mgt functions.
```

Now, when the compiler encounters the function declarations in Net_Mgt it won't complain, because
it is informed from the forward declaration that the System type is a class. Then, when it encounters their
definitions it can compile them, because the System has already been declared. Note that even after these
changes the program won't compile, because set_type() is no longer friend. Therefore, because the
type is a private member, the statement s.type = type; is not acceptable.

# NESTED CLASSES

A class can be declared within another class. Such a class is called nested. The typical reason to use nested
classes is to group together classes that are only used in one place and describe the entity in a more com-
pact form. For example, in an application that manages a company we could declare the Company class
and within nested classes for each department of the company. Consider the following program, where the
Mgt_Dpt class is declared inside the Company class:

```
#include <iostream> // Example 19.10
class Company {
public:
    class Mgt_Dpt {
        private:
            int code;
        public:
            Mgt_Dpt(int c, int e) : code(c), empl(e) {}
            int empl;
            void show() const;
    };
}
```