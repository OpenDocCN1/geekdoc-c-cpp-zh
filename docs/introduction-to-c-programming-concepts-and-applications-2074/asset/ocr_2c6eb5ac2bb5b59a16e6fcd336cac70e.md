So, in Program 23_2, you could create a new type, that is just a pair of integer and a string by writing typedef pair<int, string> person This lets you declare variables of type person, they'll be integer-string pairs (7).

```
// Program 23_2
// Using typedefed to create a new name for a type
#include<iostream>
#include<string>
using namespace std;

defef pair<int, string> person;
int main() {
    pair p = make_pair("John");
    cout << p.second << " years old." << endl;
}
```

You could also make your own class by combining specific types, and one advantage of doing that over pair is that the class would give you an indication of the intention of the class. You can get around this by using a typedef, which is giving a new name for a type. The syntax is to use typedef, the actual type, and then the name you want to use refer to that type.

While this lets you a more descriptive name overall, accessing the member variables is still going to be done with first and second (12), and there's not an easy way to extend this if you ever wanted something.

Another command available for a pair is make_pair, which takes in 2 arguments and returns a pair of those two arguments. It can be a useful way of using elements in one statement rather than with 2 separate assignments (11).

For example, if you didn't like using int and second to call integers numbers, you could write typedef int number and then could declare things of type number–they'd still be integers.

```
// Program 23_3
// Tuple example
#include<iostream>
#include<string>
#include<tuple>
using namespace std;

int main() {
    // Tuple will hold name, team, age, weight
    tuple<string, int, double, double> c = make_tuple("James Smith", "Cubs", 22, 182.1);
    cout << c.get<0>(c) << " is " old." << endl;
    cout << c.get<3>(c) << " pounds." << endl;
}
```

# / TUPLES /

If you want to group more than 2 items together, you can use a tuple, which lets you group any number of different objects together. You just list those in the angle brackets. You also have a make_tuple command, which is similar to make_pair.

The downside of a tuple is that you have a simple first and second to access individual elements. There, there's a function named get that has a real form: You have to put the element of the tuple in angle brackets after. In the parentheses, afterward you put the tuple name. That will give you to that element of the tuple.