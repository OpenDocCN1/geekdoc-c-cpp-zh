Table 6.4 **The cctype Character Functions**

| Function Name | Return Value |
| --- | --- |
| `isxdigit()` | This function returns `true` if the argument is a hexadecimal digit character (that is, 0–9, a–f, or A–F). |
| `tolower()` | If the argument is an uppercase character, `tolower()` returns the lowercase version of that character; otherwise, it returns the argument unaltered. |
| `toupper()` | If the argument is a lowercase character, `toupper()` returns the uppercase version of that character; otherwise, it returns the argument unaltered. |

# The ?: Operator

C++ has an operator that can often be used instead of the `if else` statement. This operator is called the *conditional operator*, written `?:`, and, for you trivia buffs, it is the only C++ operator that requires three operands. The general form looks like this:

`expression1 ? expression2 : expression3`

If `expression1` is true, then the value of the whole conditional expression is the value of `expression2`. Otherwise, the value of the whole expression is the value of `expression3`. Here are two examples that show how the operator works:

`5 > 3 ? 10 : 12  // 5 > 3 is true, so expression value is 10`
`3 == 9? 25 : 18  // 3 == 9 is false, so expression value is 18`

We can paraphrase the first example this way: If 5 is greater than 3, the expression evaluates to 10; otherwise, it evaluates to 12. In real programming situations, of course, the expressions would involve variables.

Listing 6.9 uses the conditional operator to determine the larger of two values.

Listing 6.9 `condit.cpp`

```
```cpp
// condit.cpp -- using the conditional operator
#include <iostream>
int main()
{
    using namespace std;
    int a, b;
    cout << "Enter two integers: ";
    cin >> a >> b;
    cout << "The larger of " << a << " and " << b;
    int c = a > b ? a : b;  // c = a if a > b, else c = b
    cout << " is " << c << endl;
    return 0;
}
```
```