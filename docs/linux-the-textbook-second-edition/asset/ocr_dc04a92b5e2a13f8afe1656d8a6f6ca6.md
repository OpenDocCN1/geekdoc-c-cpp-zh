For example, the command cat < tempfile reads input from tempfile (as opposed to the keyboard, because the standard input for cat has been attached to tempfile) and sends its output to the display screen. So, effectively, the contents of tempfile are displayed on the monitor screen. This command is different from cat tempfile, in which tempfile is passed as a command line argument to the cat command; the standard input of cat does not change and is still the keyboard attached to the terminal on which the command is run.

Similarly, in the command grep "John" < Phones, the grep command reads its input from the Phones file in the current directory, not from the keyboard. The output and error messages of the command go to the display screen. Again, this command is different from grep "John" Phones, in which the Phones file is passed as an argument to grep; the standard input of grep does not change and is still the keyboard attached to the terminal on which the command executes. However, the net effect of the grep command is the same in both cases from a user’s perspective. Similarly, the use of < is not needed in most cases because the command reads from a file in any case.

The cat and grep commands take input from standard input if they are not passed file arguments from the command line. The tr command takes input from standard input only and sends its output to standard output. The command does not work with a file as a command line argument. Thus, input redirection is often used with the tr command, as in tr -s ' ' < Bigfile. When this command is executed, it substitutes multiple spaces in Bigfile with single spaces.

# 9.4 Output Redirection

Output redirection is accomplished by using the greater than symbol (>). The following syntax is used to detach the display screen from the standard output of command and attach output-file to it. Thus, if command writes/sends its output to standard output, the output goes to output-file, not the monitor screen attached to the terminal on which the command runs. The error messages still go to the display screen, as before. The semantics of the command syntax are shown in Figure 9.3.

```
Syntax:
command > output-file
Purpose: Send output of command to the file output-file instead of to the monitor screen
```

Consider the cat > newfile command. Recall that the cat command sends its output to standard output, which is the display screen by default. This command syntax detaches the display screen from standard output of the cat command and attaches newfile to it. The standard input of cat remains attached

![](bbox=[0.12, 0.79, 0.88, 0.92])

FIGURE 9.3 Output redirection: (a) file descriptors and standard files for command; (b) semantics of input redirection.