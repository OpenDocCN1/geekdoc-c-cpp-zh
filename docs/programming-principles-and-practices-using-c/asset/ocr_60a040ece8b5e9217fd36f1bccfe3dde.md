# 8.7.1 **using** declarations and **using** directives

Writing fully qualified names can be tedious. For example, the facilities of the C++ standard library are defined in namespace **std** and can be used like this:

```
#include<string>        // get the string library
#include<iostream>      // get the iostream library

int main()
{

    std::string name;
    std::cout << "Please enter your first name\n";
    std::cin >> name;
    std::cout << "Hello, " << name << "\n";
}
```

Having seen the standard library **string** and **cout** thousands of times, we don't really want to have to refer to them by their "proper" fully qualified names **std::string** and **std::cout** all the time. A solution is to say that "by **string**, I mean **std::string**," "by **cout**, I mean **std::cout**," etc.:

```
using std::string;    // string_means std::string
using std::cout;      // cout_means std::cout
// . . .
```

That construct is called a **using** declaration; it is the programming equivalent to using plain "Greg" to refer to Greg Hansen, when there are no other Gregs in the room.

Sometimes, we prefer an even stronger "shorthand" for the use of names from a namespace: "If you don't find a declaration for a name in this scope, look in **std.**" The way to say that is to use a **using** directive:

```
using namespace std;  // make names from std directly accessible
```

So we get this common style:

```
#include<string>        // get the string library
#include<iostream>      // get the iostream library
using namespace std;    // make names from std directly accessible

int main()
{
    string name;
    cout<< "Please enter your first name\n";
```