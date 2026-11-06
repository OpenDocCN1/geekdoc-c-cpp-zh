anything but numbers because it called our EnterOnlyNumbers() routine. And finally, we entered a password, and you can see that the computer displayed asterisks when we pressed each key. Then the application kept the secret password and wrote it on the screen anyway.

# ## Understanding Preprocessor Directives

When you compile an application, the first thing the compiler does is run your code through something called a preprocessor. The preprocessor simply looks for certain statements in your code that start with the # symbol. You have already seen one such statement in every one of your applications: #include. These preprocessor statements are known as directives because they tell the preprocessor to do something; they direct it.

Think of the preprocessor as just a machine that transforms your code into a temporary, fixed-up version that's all ready to be compiled. For example, take a look at this preprocessor directive:

```
    #include <iostream>
```

If the preprocessor sees this line, it inserts the entire text from the file called iostream (yes, that's a filename; it has no extension) into the fixed-up version of the source code.

Suppose that the file called iostream looks like this:

```
    int hello = 10;
    int goodbye = 20;
```

Just two lines are all that's in it. (Of course, the real iostream file is much more sophisticated.) And suppose that your own source file, MyProgram.cpp, has this in it (as found in the Preprocessor example):

```
    #include <iostream>
    int main()
    {
        cout << "Hello" << endl;
    }
```

Then, after the preprocessor finishes its preprocessing, it creates a temporary fixed-up file (which has the lines from the iostream file inserted into the MyProgram.cpp file where the #include line had been) to look like this:

```
    int hello = 10;
    int goodbye = 20;
    int main()
    {
        cout << "Hello" << endl;
    }
```