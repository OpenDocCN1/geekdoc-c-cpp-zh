# Returning Pointers from Functions

In Chapter 10, you learned several ways to initialize a character array. The following program shows you an additional way:

```
#include <iostream>
using namespace std;
char * setName();

int main (void)
{
    char* str = "Jeff Kent"
    cout << str;
    return 0;
}
```

With some sample input and output:

Enter your name: Jeff Kent
Your name is Jeff Kent

The key statement is

```
char* str = "Jeff Kent"
```

This statement is almost the same as:

```
char str[] = "Jeff Kent"
```

In both statements, str is a character pointer, and implicit sizing is used. The difference is that str in the first statement (char* str) is a variable pointer whereas str in the second statement (char str[]) is a constant pointer.

# Returning a Pointer to a Local Variable (Not a Good Idea)

Now, following the advice in Chapter 9 to make your program more modular, try to write a separate function, setName, to obtain your input. The setName function creates a character array, assigns user input to that array using the getline function of the cin object, and returns a pointer to that character array. The address which is returned by the setName function is then assigned to the character pointer str in main. The following program implements this concept:

```
#include <iostream>
using namespace std;
char * setName();
```

```
int main (void)
{
    char* str = setName();
    cout << str;
    return 0;
}
```

```
char* setName (void)
{
    char name[80];
```