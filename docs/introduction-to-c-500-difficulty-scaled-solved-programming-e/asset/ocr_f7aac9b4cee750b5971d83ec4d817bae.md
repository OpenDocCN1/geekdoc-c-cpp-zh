Typically, a constructor is called by others when they need to perform a common set of actions.
For example, we could change the class to:

```
class T
{
private:
    int x;
public:
    T(int a, int b) {x = a+b};
    T() {x = n1+n2};
    T(int a) {x = a+n2};
}
```

Comparing the two implementations, I think that it is more readable and safer for the code to exist in a single place than to be repeated, so that if a change needs to be made, you have to edit it once. Thus, forwarding constructors can simplify the construction process and make it safer and easier to control.

Notice that this method of calling the constructor works differently from the explicit call of the constructor inside the body of the function. For example, if you write something like this:

```
T()
{
    T(n1, n2); // Creation of an unnamed object.
}
```

the constructor will not be called as you intended, but a new anonymous temporary object will be created, which will not be used. That is, if we write:

```
int main()
{
    T t;
    t.show();
    return 0;
}
```

the program will display a random value for x and not 15.

# COPY CONSTRUCTOR

The constructor is a special function that is automatically invoked whenever a new object is created and initialized with an existing object. For example:

```
#include <iostream> // Example 19.5

class T
{
private:
    int a;
public:
    int b;
    T(int i, int j) {a=i;b=j};
    void show() const {std::cout << ' ' << a << ' ' << b << '\n'};};
```