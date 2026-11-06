
The point is that the computer can’t make this decision; you need to choose how you want the data to appear. After you decide how you want them sorted, you’d create a function that determines when one record is less than, equal to, or greater than the other. If you want the list to sort by name, you would make your function look strictly at the names. But if you want your list to sort by Social Security number, you would write your function to compare the Social Security numbers.

The Maps3 example, shown in Listing 6-7, contains a map class with a comparison function that determines whether two keys are equal.

### LISTING 6-7: Containing Instances and Needing Functions That Compare Them

```cpp
#include <iostream>
#include <map>

using namespace std;

class Emp {
public:
    string Nickname;
    string SSN;

    Emp(string anickname, string asocial) :
        Nickname(anickname),
        SSN(asocial) {}

    Emp() : Nickname(""), SSN("") {}
};

class Salary {
public:
    int YearlyInc;
    int Taxes;

    Salary(int annual, int adeductions) :
        YearlyInc(annual),
        Taxes(adeductions) {}

    Salary() : YearlyInc(0), Taxes(0) {}
};

bool operator < (const Emp& first, const Emp& second) {
    return first.Nickname < second.Nickname;
}

int main() {
    map<Emp, Salary> employees;

    Emp emp1("sparky", "123-22-8572");
    Salary sal1(135000, 18);
    employees[emp1] = sal1;

    Emp emp2("buzz", "234-33-5784");
    Salary sal2(150000, 23);
    employees[emp2] = sal2;

    // Now test it out!
    Emp emptest("sparky", "");
    cout << employees[emptest].YearlyInc << endl;
    return 0;
}
```

When you run this application, you see the YearlyInc member of the Salary value, where the key is an Employee with the name sparky:

```text
135000
```

Now notice a couple things about this code. First, to locate the salary for Sparky, you don't need the Employee instance for Sparky. Instead, you create an instance of Employee and set up the Nickname member without worrying about the SSN member. Then you retrieve the value by using the bracket notation for map:

```cpp
cout << employees[emptest].YearlyInc << endl;
```

The map code uses the less-than function to perform this task. The < function compares only the Nickname members, not the SSN member. Notice that this function must return a bool value and that you precede the < with the operator keyword, defining this as an operator function — one that defines an operation between operands. You could change things around a bit by comparing the SSN members like so:

```cpp
bool operator < (const Emp& first, const Emp& second) {
    return first.SSN < second.SSN;
}
```

Then you can locate Sparky's salary based on the SSN:

```cpp
Emp emptest("", "123-22-8572");
cout << employees[emptest].YearlyInc << endl;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_673_0.png)

A single `<` function may not seem like enough to perform all the required comparisons, such as equality. However, the code calls the less-than function twice, the second time flip-flopping the order of the parameters; and if the function returns false both times, the computer determines that they are equal. Using this approach makes life easier because you need to provide only a single comparison function.

### UNDERSTANDING THE DEFAULT `<` FUNCTION

Containers in the Standard Library have a default `<` function. If you don’t supply a `<` function of your own, the container supplies this default `<` function for you. This default function relies on a template class called less. This template is simple: It includes a single method that returns the Boolean value:

```text
x < y
```

For most basic types, the default works fine. For example, the compiler can easily use the default when you’re working with integers. However, the compiler doesn’t understand the `<` operator when working with custom classes unless you provide your own `<` operator function, as you see everywhere else in this chapter. However, because the container takes a class in its parameter that defaults to the class less, you can put together your own class and use that instead of writing your own `<` operator function. Here’s a sample:

```cpp
class MyLess {
public:
  bool operator()(const MyClass &x, const MyClass &y) const {
    return x.Name < y.Name;
  }
};
```

Then when you create, for example, a map, you pass this class as a third parameter, rather than relying on the default:

`map<MyClass, MyClass, MyLess> mymap;`

Then you don’t need your own less-than function. The advantage of this approach is that you now have a standardized `<` function implementation to use everywhere, and it’s especially helpful when working within a team environment.

## Iterating through a container

Containers in the Standard Library provide an overview of the container’s content. If you have a container filled with objects, you normally get an overview of what’s there, but being able to drill down into the details would be nice. You use an *iterator* to drill down into the container. An iterator works with a container to let you step object by object through the container. The following sections tell you about iterators and how to work with them.

### Working with iterators

Each container class contains an embedded type called `iterator`. You use the fully qualified name to create an iterator instance. For example, if you have a map that holds integers and strings, as in `map<int, string>`, you create an iterator instance like this:

```cpp
map<string, int>::iterator loopy
```

Although `loopy` is an instance of `iterator`, some serious type defining is going on, and, in fact, `loopy` is a pointer to an item stored inside the container. To initialize `loopy` to point to the first item in the container, you call the container’s `begin()` method, storing the results in `loopy`. Then `loopy` will point to the first item in the container. You can access the item by dereferencing `loopy`; then, when you’re finished, you can move to the next item by incrementing `loopy` like this:

```cpp
loopy++;
```

You can use this technique in various ways, such as by using the call to `reverse_copy()` shown previously in Listing 6-3. You can tell whether you’re finished by checking to see whether `loopy` points to the last item in the container. To do this, you call the container’s `end()` method and compare `loopy` to the `end()` value. If it’s equal, you’re done. The following few lines of code perform these steps:

```cpp
vector<string>::iterator vectorloop = Words.begin();
while (vectorloop != Words.end())
{
    cout << *vectorloop << endl;
    vectorloop++;
}
```

You can see the type used for the iterator, in this case called `vectorloop`, which is initialized by calling `begin()`. `vectorloop` is dereferenced to access the data, and is then incremented to get to the next item. The while loop tests `vectorloop` against the results of `end()` to determine when the processing is complete. The Iterators example code, shown in Listing 6-8, shows a more complete example of how to use an iterator.

### LISTING 6-8: Iterating

```cpp
#include <iostream>
#include <map>
#include <vector>

using namespace std;

int main() {
    // Iterating through a map
    map<string, int> NumberWords;
    NumberWords["ten"] = 10;
    NumberWords["twenty"] = 20;
    NumberWords["thirty"] = 30;

    map<string, int>::iterator loopy = NumberWords.begin();
    while (loopy != NumberWords.end()) {
        cout << loopy->first << " ";
        cout << loopy->second << endl;
        loopy++;
    }

    // Iterating through a vector
    vector<string> Words;
    Words.push_back("hello");
    Words.push_back("there");
    Words.push_back("ladies");
    Words.push_back("and");
    Words.push_back("aliens");

    vector<string>::iterator vectorloop = Words.begin();
    while (vectorloop != Words.end()) {
        cout << *vectorloop << endl;
        vectorloop++;
    }
    return 0;
}
```

When you compile and run this application, you see the following output:
