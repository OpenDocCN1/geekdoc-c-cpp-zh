The syntax to use the function `putback` is:

```
istreamVar.putback(ch);
```

Here, `istreamVar` is an input stream variable, such as `cin`, and `ch` is a `char` variable.

The `peek` function returns the next character from the input stream but does not remove the character from that stream. In other words, the function peek looks into the input stream and checks the identity of the next input character. Moreover, after checking the next input character in the input stream, it can store this character in a designated memory location without removing it from the input stream. That is, when you use the peek function, the next character stays the same, even though you now know what it is.

The syntax to use the function `peek` is:

```
ch = istreamVar.peek();
```

Here, `istreamVar` is an input stream variable, such as `cin`, and `ch` is a `char` variable.

Notice how the function `peek` is used. First, the function `peek` is used in an assignment statement. It is not a stand-alone statement like `get`, `ignore`, and `putback`. Second, the function `peek` has empty parentheses. Until you become comfortable with using a function and learn how to write one, pay close attention to how to use a predefined function.

The following example illustrates how to use the `peek` and `putback` functions.

# EXAMPLE 3-7

```
```cpp
//Functions peek and putback

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{
        char ch;                                         //Line 5

        cout << "Line 6: Enter a string: ";             //Line 6
        cin.get(ch);                                     //Line 7
        cout << endl;                                    //Line 8
        cout << "Line 9: After first cin.get(ch): "    //Line 9
             << "ch = " << ch << endl;

        cin.get(ch);                                     //Line 10
        cout << "Line 11: After second cin.get(ch): "  //Line 11
             << "ch = " << ch << endl;

        cin.putback(ch);                                 //Line 12
        cin.get(ch);                                     //Line 13
        cout << "Line 14: After putback and then "     
```
```