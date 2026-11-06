![](bbox=[0.25, 0.04, 0.8, 0.28])

FIGURE 6-3: Command-line apps often have switches and arguments.

To make these switches and their associated arguments work, the main() function must process the input. You determine how many command-line arguments the user supplied using argc, and then access them using argv. Book 2, Chapter 2 deals with the topic arrays. An array is a sequence of variables stored under one name. The argv variable is one such animal. To access the individual variables stored under the single umbrella known as argv, you do something like this:

```
```
cout << argv[0] << endl;
```
```

In this example, you use brackets as you did when accessing the individual characters in a string. When working with the /? switch, you see /? as the output. You can access the command-line parameters using a for loop. The CommandLineParameters example, shown in Listing 6-12, demonstrates this technique.

# **LISTING 6-12:** Accessing the Command-Line Parameters

```
```
#include <iostream>
#include <stdlib.h>

using namespace std;

int main(int argc, char *argv[])
{
    for (int index=1; index < argc; index++)
    {
        cout << argv[index] << endl;
    }

    return 0;
}
```
```

# Dividing Your Work with Functions