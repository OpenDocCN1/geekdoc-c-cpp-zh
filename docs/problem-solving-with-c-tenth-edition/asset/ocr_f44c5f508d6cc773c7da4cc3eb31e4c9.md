# DISPLAY 2.15 A do-while Loop

```
#include <iostream>
using namespace std;
int main()
{
    char ans;
    do
    {
        cout << "Hello\n";
        cout << "Do you want another greeting?\n" << "Press y for yes, n for no,\n" << "and then press return: ";
        cin >> ans;
    } while (ans == 'y' || ans == 'Y');
    cout << "Good-Bye\n";
    return 0;
}
```

# Sample Dialogue

```
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: y
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: Y
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: n
Good-Bye
```

unary operators, ++ and --. The ++ operator is called the increment operator and the -- operator is called the decrement operator. They are usually used with variables of type int. If n is a variable of type int, then n++ increases the value of n by one and n-- decreases the value of n by one. So n++ and n-- (when followed by a semicolon) are executable statements. For example, the statements

```
int n = 1, m = 7;
n++;
cout << "The value of n is changed to " << n << endl;
m--;
cout << "The value of m is changed to " << m << endl;
```