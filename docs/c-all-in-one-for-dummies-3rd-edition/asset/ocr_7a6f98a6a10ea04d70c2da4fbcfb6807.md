# Listing 5-6 (continued)

```
MagazineHolder dl;
dl.Add(new Magazine(
    "Dummies Life", "Vol 1 No 1", "Wile E.");
dl.Add(new Magazine(
    "Dummies Life", "Vol 1 No 2", "Wile E.");
dl.Add(new Magazine(
    "Dummies Life", "Vol 1 No 3", "Wile E.");
dl.CompleteSet = false;
cout << dl.Count << endl;

BookHolder bh;
bh.Add(new Book(
    "CEOing for Dummies", "Gookie Dan", "Wile E.");
bh.Add(new Book(
    "Crashmaking for Dummies", "Woodie and Buzz",
    "Wile E.");
bh.Add(new Book(
    "Turning off the Computer for Dummies",
    "Wrath of Andy",
    "Wile E.");
bh.GenreofAllBooks = BookHolder::shownotto;
cout << bh.Count << endl;

return 0;
}
```

# Deriving a class template from a class

A template doesn’t have to be at the absolute top of your hierarchy, the total king of the hill. No, a template can be derived from another class that’s not a template. The brain acrobatics work like this: When you have a template and the compiler creates a class based on this template, the resulting class will be derived from another class.

For example, suppose you have a class called SuperMath that is not a template. You could derive a class template from SuperMath. The TemplateFromClass example shown in Listing 5-7 demonstrates how you can do this.

# Listing 5-7: Deriving a Class Template from a Class

```
#include <iostream>

using namespace std;

class SuperMath
{
public:
    int IQ;
};

template <typename T>
```