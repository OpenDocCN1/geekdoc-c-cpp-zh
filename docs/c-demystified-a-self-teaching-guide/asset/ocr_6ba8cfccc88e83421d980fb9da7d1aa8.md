# The cin Object’s getline Function

The program from the previous section worked fine when the input had no embedded spaces, such as "Jeff".

```
#include <iostream>
using namespace std;
int main ()
{
    char name[80] = {'J', 'e', 'f', 'f', '/0' };
    cout << "Enter your name: ";
    cin >> name;
    cout << "Your name is " << name;
    return 0;
}
```

However, examine the following sample input and output:

Enter your name: Jeff Kent
Your name is Jeff

We examined this issue in Chapter 3 with the following program, which used a string variable instead of a character array:

```
#include <iostream>
using namespace std;
#include <string>
int main (void)
{
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Your name is " << name;
    return 0;
}
```

The explanation in Chapter 3 of why the value of name is output only as "Jeff", omitting "Kent", as the cin object interprets the space between "Jeff" and "Kent" as indicating that the user has finished inputting the value of name variable. The solution is to use the getline function of the cin object.

> Note The cin object also has a function that would solve this issue. The only difference between the two is that the function reads the user's input up to, but including the newline character (the ENTER key that terminates input, whereas the getline function reads the user's input up to and including the newline character. This makes the getline function easier to use than the function when working with character arrays. The get function usually used with single characters, not character arrays.

The getline function of the cin object is overloaded. By overloaded I do not mean overworked. Rather, the term overloaded in connection with the function may mean more than one way, each varying by the number, data type, or order of arguments.

The following program uses the getline function to read the user’s input and assign that to the character array: