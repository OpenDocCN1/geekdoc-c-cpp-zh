function terminates. Most probably, the program won't display example. But, even if it is displayed, the code is not correct.

Always remember, don't return the address of a local variable unless it is declared as static. If you want to change the contents of an array, the simplest way is to pass the array as an argument. For example, test(i) is modified like this:

```
void test(char str[]) {
    strcpy(str, "example");
}
```

# C.11.11 Write a function that takes two strings, uses them as pointers, and returns 0 if they are identical or the difference of the two non-matching characters. Write a program that reads two strings of less than 100 characters and uses the function to display the result of the comparison.

```
#include <iostream>
using std::cout;
using std::cin;
```

```
int str_cmp(const char *str1, const char *str2)
int main() {
    char str1[100], str2[100];
    cout << "Enter first text: ";
    cin.getline(str1, sizeof(str1));
    cout << "Enter second text: ";
    cin.getline(str2, sizeof(str2));
    int i = str_cmp(str1, str2);
    if(i == 0)
        cout << str1 << " = " << str2 << '\\n';
    else if (i < 0)
        cout << str1 << " < " << str2 << '\\n';
    else
        cout << str1 << " > " << str2 << '\\n';
    return 0;
}
```

```
int str_cmp(const char *s1, const char *s2) {
    while (*s1) {
        if (*s1 == '\0')
            return 0;
        s1++;
        s2++;
    }
    return *s1-*s2;
}
```

Comments: If two different characters are found, the loop terminates and the function returns their difference. The str_cmp() function is an implementation example of the strcmp() library function.