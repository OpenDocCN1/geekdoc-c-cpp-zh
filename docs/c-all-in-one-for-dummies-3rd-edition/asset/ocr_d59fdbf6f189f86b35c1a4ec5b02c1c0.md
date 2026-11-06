The second parameter in the `main()` function is the cryptic-looking `char *argv[]`. The name of the variable is `argv`, and it is pronounced "arg-VEE." Book I, Chapter 9 deals with the topic arrays. An *array* is a sequence of variables stored under one name. The `argv` variable is one such animal. To access the individual variables stored under the single umbrella known as `argv`, you do something like this:

```
cout << argv[0] << endl;
cout << argv[1] << endl;
```

(In the preceding example, you're using brackets as you did similarly with accessing the individual characters in a string.)

In the case of the two command-line parameters `myfile` and `yourfile`, these two lines of code would print the lines

```
myfile
yourfile
```

You can access the command-line parameters using a `for` loop. The `CommandLineParameters` example, shown in Listing 5-12, demonstrates this technique.

# Listing 5-12: Accessing the Command-Line Parameters

```
#include <iostream>
#include <stdlib.h>
int main(int argc, char *argv[])
{
    for (int index=0; index < argc; index++)
    {
        cout << argv[index] << endl;
    }
    return 0;
}
```

**Setting the command-line parameters in Code::Blocks**

| | |
|---|---|
| If you attempt to run the example in Code::Blocks by choosing Build→Run with the default settings, the example doesn't output anything other than the execution path and application name. To add command-line arguments, choose Project→Set Program's Arguments. You see the | Select Target dialog box, where you can type the command-line arguments in the Program Arguments field. Type CommandLineParameters in this field and click OK. You're ready to run the example. |