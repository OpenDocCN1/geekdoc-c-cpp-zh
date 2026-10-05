# Strings 241

```
int main() {
  char str1[] = "Old text", str2[] = "New", str3[] = "Get";

  strncpy(str1, str2, 3);
  std::cout << str1 << '\\n';

  strncpy(str1, str3, 5);
  std::cout << str1 << '\\n';
  return 0;
}
```

Since the number 3 is less than the length of the string stored in str2, the first strncpy copies the first three characters into str1 and does not append a null character. Therefore, the program displays New. Since the number 5 is greater than the length of the string stored in str3, the second strncpy copies three characters from str3 into str1 and appends two null characters to reach the value 5. Therefore, the program displays Get.

# The strcpy() Function

The strcpy() function is declared in cstring:

```
char *strcpy(char *dest, const char *src);
```

strcpy() appends the string pointed to by src to the end of the string pointed to by dest. strcpy() appends the null character and returns dest, which points to the resulting string. For example, the following program reads two strings of less than 100 characters and uses strcpy() to merge them and store the result into an array.

```
#include <iostream> // Example 10.8
#include <cstring>
using std::cout;
using std::cin;

int main() {
  char str1[100], str2[100], str3[200] = {0}; /* Store the null character in str3 for the first strcpy(). */

  cout << "Enter first text: ";
  cin.getline(str1, sizeof(str1));

  cout << "Enter second text: ";
  cin.getline(str2, sizeof(str2));

  strcpy(str3, str1); // The string contained in str1 is added to str3.
  strcpy(str3, str2);
  cout << "The merged text is: " << str3 << '\\n';
  return 0;
}
```

> It is the programmer's responsibility to ensure that there is enough room in the memory to append the string pointed to by src. Otherwise, it is a potential cause of memory overrun with unpredictable results.

![](bbox=[0.108, 0.882, 0.158, 0.918])