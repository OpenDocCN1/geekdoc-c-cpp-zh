```
{
  const char *ptr = "This is text";
  int i;

  for(i = 0; ptr[i] != '\0'; i++)
    std::cout << *(ptr+i) << ' ' << ptr[i] << '\\n';
  return 0;
}
```

The statement ptr = "This is text", the compiler allocates memory to store the string literal and the null character. Then, ptr points to the first character of the string, as depicted here.

| ptr | T | h | i | s | i | s | t | e | x | t | |

To access the characters of the string, we use either pointer arithmetic or the pointer as an array subscript. The program uses both ways to display one by one characters of the string. The loop is executed until the null character is met.

Because a string literal is constant, C++11 it require the pointer type to be const char so that literal cannot be modified. For example

```
const char *ptr = "This is text";
ptr = 'a'; // Illegal.
```

Regarding the declarations:

```
char ptr[] = "This is text"; and const char *ptr = "This is text";
```

although may look similar they have different properties you already know from the section Pointers and Arrays in Chapter 8. In particular, the first declaration declares ptr as an array of 13 characters (the last is the null character). We can safely store another string into ptr, as long as its length is no more than 13 characters, otherwise the program may behave unpredictably. The second declaration declares ptr as a pointer and makes it point to the memory that holds the string literal. As discussed, in the first case we can write ptr[0] = 'a'; without any concern, while in the second case this statement causes a compilation error. The ptr can point to any string during program execution, no matter what its length is. For example:

```
const char *ptr = "First";
ptr = "Second";
std::cout << *ptr << '\\n';
```

At first, ptr points to the first character of the string literal "First". Then, the statement ptr = "Second", makes ptr point to the new memory allocated to store that string. Since ptr points to its first character, ptr is equal to 'S' and the code displays S.
As've outlined in Chapter 8, a pointer should have been initialized before being used. Consider the following program:

```
#include <iostream> // Example 10.3
int main() {
  char *ptr;

  ptr[0] = 'a';
  ptr[1] = 'b';
}
```