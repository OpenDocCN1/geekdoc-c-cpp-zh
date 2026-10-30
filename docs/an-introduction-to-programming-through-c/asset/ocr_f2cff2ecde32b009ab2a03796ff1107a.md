# 12.3 Input/output redirection

When you write programs professionally, you are required to keep a record of the testing you have done. This can be done nicely by using a feature called input redirection. Most operating systems support input redirection.

In Chapter 1 we told you that cin represents the keyboard and whenever your program executes a statement of the form cin >> ... you are expected to type in an appropriate value. This is an oversimplification. If fact, cin represents an abstract, standard input device, which is the keyboard by default, but this default can be changed. If you wish, you can make the standard input device be a file, say named file1. Thus, instead of waiting for you to type in input, the program would take input from file file1 whenever it executes a cin >> ... statement. This is called input redirection. To redirect input, you specify the name of the file on the command line, preceded by the character <, after the name of the executable. Thus to redirect input to come from file1, you will type the following on the command line.

```
% a.out <file1
```

As you can see, input redirection is very convenient. Even before you write the program, each test instances you create as discussed above can be placed in a file. When the program is ready, you run it, merely redirecting input so that the data comes from the file of your choosing.

Thus we can suggest the following process for creating and using test cases. Even before you write the program create test cases, placing the input in files, one file per instance. Thus you will create several files, say input1.txt, input2.txt, ... . Also create files output1.txt, output2.txt, ... which contain the outputs as you expect for the corresponding input instances. After the program is ready, simply redirect input, say from input3.txt in order to test it on the third instance you created. Check that the output you get is indeed what you had written down in output3.txt.

Note by the way that input redirection is also useful if your program does not run correctly on the very first run. If you have placed the data in a file then you can redirect input from it, and thus do not have to type the data again and again. This saves typing effort, and is especially useful for programs for which the input is large.

Note finally that the standard output stream, cout can also be redirected. For this you can execute your program by typing

```
% a.out >file2
```

If you do this, whatever you print by executing cout << ... in your program will be placed in the file file2, rather than being shown on the screen.

This is useful for programs which the output is large. If the output is put into a file, you can examine it at leisure. Also, the file thus created can serve as a record of your testing activities.

# 12.4 Algorithm design

The next step after the development of the specifications and test cases is algorithm design. By algorithm we mean the abstract ideas we need to solve a problem. For example, how do