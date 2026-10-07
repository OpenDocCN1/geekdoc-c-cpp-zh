```
cin >> num;
doubleIT(num);
cout << "The number doubled in main is " << num << endl;
return 0;
}
void doubleIT(int x)
{
    cout << "The number to be doubled is " << x << endl;
    x *= 2;
    cout << "The number doubled in doubleIT is "
    << << x << endl;
}
```

Here is some sample input and output:

+   - Enter number: 3
- The number to be doubled is 3
- The number doubled in doubleIT is 6
- The number doubled in main is 3

As the input and output reflects, the value of num was not changed by the doubling of its counterpart argument in the double function.

The reason for the value of num was not changed in main is that a copy of it was passed to doubleIT. The change was made to the copy, but the original, the variable in main, was not affected by the doubling of the copy. The logic is the same if I gave you a copy of this page, which you proceed to rip. The original I would keep unaffected.

In order for the called function to change the value of a variable passed to it, the variable must be passed by reference. The variable in the called function is called a reference variable. The reference variable is an alias for the variable in main. You may recall from television that an alias is another name person may use, such as James Bond's alias of 007. However, whether you refer to him as James Bond or 007, you are still referring to the same person.

In order to pass a variable by reference, both the function header and the prototype, is followed by an ampersand, is the same ampersand that is used as the address operator. Here, however, the ampersand is used in a different context.

The following program passes the variable to be doubled by reference:

```
#include <iostream>
using namespace std;
void doubleIT(int&);
```

```
int main ()
{
    int num;
    cout << "Enter number: ";
    cin >> num;
    doubleIT(num);
    cout << "The number doubled in main is " << num << endl;
    return 0;
}
void doubleIT(int& x)
{}
```