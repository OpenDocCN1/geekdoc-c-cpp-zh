Friend functions are not scoped within the class but have the same scope as any normal function declared in C++. However, these functions have access into all access regions of the class just like member functions.

A big difference between member functions and friend functions is how the function gets the address of the object it will read from or write to. In friend functions, we must explicitly pass the object of interest or a reference to the object. We'll see this later with operator overloading.

Note the keyword friend is with the function declaration within the class but not with the function definition. Only a class can say who its friends are. If any function could declare itself a friend of a particular class, that function could access the private data without going through the class interface.

# Friend Member Functions

A member function of one class can be a friend of another class. For example, a class can declare a member function of another class as a friend. The friend member function can access the declaring class's private members.

```
#include <iostream>

using namespace std;

class Alpha;

class Beta {
private:
char* s2;
public:
Beta() {
s2 = new char(strlen("one, two, three")+1);
strcpy(s2, "one, two, three");
}
void show(Alpha a);
};

class Alpha {
private:
char *s1;
public:
Alpha() {
s1 = new char(strlen("Testing")+1);
strcpy(s1, "Testing");
}
friend void Beta::show(Alpha a);
};
```