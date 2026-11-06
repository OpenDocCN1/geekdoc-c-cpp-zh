```
#include <iostream>

using namespace std;

int main(int argc, char *argv[])
{
    int loop;
    for (loop = 0; loop < argc; loop++) {
        cout << argv[loop] << endl;
    }
    return 0;
}
```

When you compile this application, name the executable CommandLineParams, and then run it from the command prompt, using the following command:

```
CommandLineParams abc def "abc 123"
```

You see the following output. (Note that the application name comes in as the first parameter and the quoted items come in as a single parameter.)

```
CommandLineParams
abc
def
abc 123
```

![](bbox=[0.13, 0.501, 0.208, 0.576])

You can also specify command-line arguments using the IDE for debugging purposes when working with the Code::Blocks compiler. Choose Project➜Set Program’s Arguments. Code::Blocks displays the Select Target dialog box, where you choose a target in the first field and type the arguments in the Program Arguments field. Click OK and then click Run. CommandLineParams displays the command-line arguments in the command window as it did when you typed the command at the command prompt.

# Allocating an array on the heap

Arrays are useful, but it would be a bummer if the only way you could use them were as stack variables. If you could allocate an array on the heap by using the new keyword, that would be nice. (If you can’t quite remember the difference between the stack and the heap, check out the “Heap and Stacking the Variables” section in Book I, Chapter 7.) Well, good news! You can! But you need to know about a couple of little tricks to make it work.

First, you can easily declare an array on the heap by using `new int[50]`, for example. But think about what this is doing: It declares 50 integers on the heap, and the new word returns a pointer to the allocated array. But, unfortunately, the makers of C++ didn’t see it that way. For some reason, they based the array pointer type on the first element of the array (which is, of course, the same as all the elements in the array).