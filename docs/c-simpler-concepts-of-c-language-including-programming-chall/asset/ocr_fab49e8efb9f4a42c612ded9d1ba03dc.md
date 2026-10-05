# # 12
Command Line Arguments

# ## 12.1. INTRODUCTION

As previously mentioned, main() is the first function in any program to get executed. So far, main() was executed without any argument. This statement is quite arguable. The statement poses a question that, main() take arguments? The answer is yes. The main() function can take arguments which cannot be passed from any other user defined function, when the program gets executed, main() will be the entry point in any program. So, from where to pass the arguments to main? The answer is Command Line Arguments. In this chapter, let's explore more about them.

# ## 12.2. THE ARGUMENTS

+   - main() takes two arguments generally.
- 1. argc - integer argument that indicates the argument count.
- 2. argv - character pointer array.

For example, refer to the following code snippet.

```
void main(int argc, char *argv[])
{
    
}
```

Syntax - How to pass the values to argc, argv?
From the command prompt, the programmer needs to pass the values.
Assume the following call from the command prompt,

```
C:\turbo\prog cmdline_prog one two three
```

As it be observed from the previous line, C:\turbo\prog> is the path from where the C programs are executed. The following steps are followed to pass arguments to main().

+   - 1. go to Start->Run->cmd
- 2. in the command prompt, type the path from where the programs are executed using 'cd'. cd C:\turbo\prog.\n- 3. From the prompt, first the name of the program is mentioned. In our case, cmdline_prog is the name of the program.
- 4. Followed by the program name, the parameters are passed to the main(). In our case, one two three are the parameters being passed.

Now, it's the time for us to explore more on argc, argv things.