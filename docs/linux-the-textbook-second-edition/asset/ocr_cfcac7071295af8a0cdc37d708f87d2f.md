```
$ declare -r
declare -r BASHOPTS="checkwinsize:cmdhist:complete_fullquote:expand_aliases:extglob:extquote:force_fignore:histappend:interactive_comments:login_shell:progcomp:promptvars:sourcepath"
declare -ir BASHPID
declare -r BASH_COMPLETION_COMPAT_DIR="/etc/bash_completion.d"
declare -ar BASH_VERSION=( [0]="4" [1]="3" [2]="42" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")
declare -ir EUID="1004"
declare -ir PPID="3347"
declare -r
SHELLOPTS="braceexpand:emacs:hashall:histexpand:history:interactive-comments:monitor"
declare -ir UID="1004"
declare -r name="Jim"
declare -r place="Ames"
$
```

On some Linux systems, the output of the readonly command shows the list of read-only variables along with the values of these variables. You cannot reset the value of a read-only variable. The following session shows an example:

```
$ unset name
-bash: unset: name: cannot unset: readonly variable
$
```

# 12.3.8 Reading from Standard Input

So far, we have shown how you can assign values to shell variables statically at the command line level or by using the assignment statement in your programs. If you want to write an interactive shell script that prompts the user for keyboard input, you need to use the read command to store the user input in a shell variable. This command allows you to read one line of standard input. The following is a brief description of the command:

```
Syntax:
    read [options] [variable-list]
Purpose: Read one line from standard input and assign words in the line to variables in variable-list
Commonly used options/features:
    -a name    Read words into the "name" array
    -e         Read the whole line into the first variable; the rest of the variables are null
    -p prompt  Display "prompt" if reading from a terminal
```

A line is read in the form of words separated by white spaces (<Space> or <Tab> characters, depending on the value of the shell environment variable IFS). The words are assigned to the variables in the order of their occurrence, from left to right. If the number of words in the line is greater than the number of variables in variable-list, the last variable is assigned the extra words. If the number of words in a line is less than the number of variables, the remaining variables are reset to null.

We illustrate the semantics of the read command by way of the following script in the read_demo file.

```
$ cat read_demo
#!/bin/bash
echo -n "Enter input: "
read line
echo "You entered: $line"
echo -n "Enter another line: "
read word1 word2 word3
```