Line 6 uses the string value (`char` array) `argv[1]` to display the first item after the program name at the command prompt.

# **Exercise 15-1:** Type the source code from Listing 15-1 into a new project. Build and run.

The program displays no output unless a command-line argument is specified. To do so at the command prompt:

```
```text
./a.out Jonah
```
```

The name of the program is `a.out`. The `./` prefix directs the command interpreter to look for the file in the current directory. This command is followed by a space and then the first command-line argument, Jonah. The program outputs this message:

```
```text
Greetings, Jonah!
```
```

If you’re using Code::Blocks, follow these steps to set a command-line argument:

+   1. **Choose Project → Set Programs’ Arguments.**

This command is available when you start a Code::Blocks project. Upon success, you see the Select Target dialog box, as shown in Figure 15-2.

![](bbox=[0.265, 0.546, 0.537, 0.827])

Type command line arguments here