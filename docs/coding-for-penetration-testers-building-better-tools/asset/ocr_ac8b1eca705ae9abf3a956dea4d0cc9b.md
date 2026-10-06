Each argument is numbered sequentially as it comes in, with $0 being reserved. So, in essence, by placing $1 on our echo line, we told the shell to put the contents of the first argument, along with the text we provided.

# Note

The use of arguments prompts the question, how many arguments can we have? Quite a lot, but it depends on the system and amount of memory available. On most UNIX-like systems, we can get an answer to this by issuing the command `getconf ARG_MAX`. On the Kali 2.0 system used to develop this chapter, there is 2,097,152 KB of storage open for arguments.

# Control statements

Control statements allow us to control the flow of our script as it executes. There are a number of control statements we can use. Many of these are common among the more frequently used programming languages, even though the syntax may differ slightly. Here we will look at conditional and looping statements.

# Conditionals

Conditional statements allow us to change the way our program behaves based on the input it receives, the contents of variables, or any of a number of other factors. The most common and useful conditional for us to use in bash is the `if` statement. We can use an if like so:

```
#!/bin/bash
if [ "$1" = "Neo" ]; then
  MESSAGE=Wake up, "$1"
else
  MESSAGE=Hey, you're not Neo"
fi
echo $MESSAGE
```

We will need to run the script twice to see both branches. We should end up with something along the lines of the results shown in