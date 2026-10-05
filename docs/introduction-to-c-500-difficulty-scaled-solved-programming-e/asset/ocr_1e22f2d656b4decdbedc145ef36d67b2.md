braces even if you don't have to, the program becomes easier to read. For example, see how much easier is to read and control the code when aligning each if with the matching else:

```
#include <iostream> // Example 5.4
int main() 
{
    int a = 10;

    if(a != 10) {
        if(a < 30) 
            std::cout << "1\n";
        else 
            std::cout << "2\n";
    }
    else 
        std::cout << "3\n";
    return 0;
}
}```
```

Although the braces of the first if are not necessary, their use makes the code much clearer. To test a series of conditions, the typical choice is to use the following syntax:

```
if(condition_A)
{
    ... block of statements A
}
else if(condition_B)
{
    ... block of statements B
}
elelse
{
    ... block of statements N
}
... next program statements.```
```

There can be any number of else clauses between the first if and the last else. The conditions are evaluated in order starting from the top. Once a true condition is found, the corresponding block of statements is executed and the remaining else statements are ignored. The program continues with the execution of the next statement after the last else. For example, if condition_A is true, the first block of statements is executed. If it is false, condition_B is checked and so on. Note that the else is optional. If it and all are false, for example, the following program reads two integers and displays the result of their comparison:

```
#include <iostream> // Example 5.5
using std::cout;
using std::cin;
int main() 
{
    int i, j;

    cout << "Enter numbers: ";
    cin >> i >> j;
}```
```