
```
```bash
$ cat fs
#!/bin/bash
# File Name:    ~/linux2e/chapter13/bash/fs
# Author:       Syed Mansoor Sarwar
# Written:      August 18, 2004
# Modified:     August 20, 2004; Jul 28, 2014; July 9, 2017
# Purpose:      To add the sizes of all the files in a directory passed as
#              command line argument
# Brief Description:
#        Maintain running sum of file sizes in a numeric variable
#        called sum, starting with 0. Read all the file names
#        by using the pipeline of the ls, more, and while commands.
#        Get the size of the next file and add it to the running
#        sum. Stop when all file names have been processed and
#        display the answer.
if [ $# = 0 ]              # If no command line argument, the
                           # set directory to current directory
then
        directory="."
elif [ $# != 1 ]             # If more then one command line argument
                            # then display command syntax
then
        echo "Usage: $0 [directory name]"
        exit 1
elif [ ! -e "$1" ]         # If one command line argument, but file
                            # does not exist, display error message
then
        echo "$1: File does not exist"
        exit 1
elif [ ! -d "$1" ]         # If one command line argument, but is
                            # not a directory, show command syntax
then
        echo "Usage: $0 [directory name]"
        exit 1
else
        directory="$1"    # If one command line argument and it is a
                           # directory, prepare to perform the task
fi

# Get file count in the given directory; for empty directory, display a
# message and quit.
file_count=`ls $directory | wc -w`  # Get count of files in the directory
if [ $file_count -eq 0 ]             # If no files, display error message
then
        echo "$directory: Empty directory."
        exit 0
fi
# For each file in the directory specified, add the file size to the running
# total. The more command is used to output file names one per line so can
# read command can be used to read file names.
sum=0   # Running sum initialized to 0.
ls "$directory" | more |
while read file
do
        file="$directory"/"$file"  # Store the relative path name for each file
        if [ -f "$file" ]             # If it is an ordinary file
        then                           # then
                set -- `ls -l "$file"` # set command line arguments
                sum=`expr $sum + $5`   # Add file size to the running total.
        fi
        # Code to decrement the file_count variable and display the final sum
        # if the last file has been processed.
done
```
```

```
if [ "$file_count" -gt 1 ] # Are more files left? If so, continue.
    then
        file_count=`expr $file_count - 1`
    else
        # Spell out the current directory
        if [ "$directory" = "." ]
        then
            directory="your current directory"
        fi
        echo "The size of all ordinary files in $directory is $sum bytes."
    fi
done
exit 0
$ 
$ pwd
/home/sarwar/linux2e/ch13
$ ./fs / /bin
Usage: ./fs [directory name]
$ ./fs linux2e
linux2e: File does not exist
$ ./fs ~/linux2e
The size of all ordinary files in /home/sarwar/linux2e is 0 bytes.
$ ./fs ..
The size of all ordinary files in .. is 0 bytes.
$ ./fs .
The size of all ordinary files in your current directory is 4060 bytes.
$ ./fs /
The size of all ordinary files in / is 16 bytes.
$ ./fs /bin
The size of all ordinary files in /bin is 16428442 bytes.
$ ./fs dir1
dir1: Empty directory.
$
```

Note that in the previous sample run of the fs script, the ./fs / command displays the total size of the two symbolic link files in the root directory.

In the following in-chapter exercise, you will create a Bash script that processes numeric data by using the expr command.

## Exercise 13.1

Create the addall script in your directory and run it with the first ten numbers in the Fibonacci series. What is the result? Does the program produce the correct result? If you are not familiar with the Fibonacci series, browse through the following website: http://en.wikipedia.org/wiki/Fibonacci_number.

## Exercise 13.2

Create the fs script in your directory and try it with sample runs given in the previous session.

## Exercise 13.3

Try all of the shell sessions in the previous session related to the let command, expansion syntax, and the expr command.

## 13.2.2 Arithmetic with bc

bc is a language that supports arithmetic operations on arbitrary-precision numbers. It can be used as an interactive mathematical calculator or as a mathematical scripting language with C language like syntax. It supports the usual constructs and features of a scripting language to support arithmetic, assignment, comparison, increment/decrement, and logical/Boolean operations. It also supports conditional and iterative statements, and mathematical functions available in the Linux mathematics library.

mathlib. You can also convert numbers from any number base to another, such as decimal to binary, binary to octal, octal to hexadecimal, and a number in base four to a number in base 21. Here is a brief syntax of bc:

**Syntax:**

`bc [-hilwsqv] [long-options] [file ...]`

**Purpose:** Perform arbitrary-precision arithmetic with interactive execution of statement as well as using scripts in a language with C-like syntax

**Commonly used options/features:**

`-i`  Force interactive mode

`-l`  Use functions in the Linux math library, mathlib

We show the interactive use of bc with a few examples, first by running bc as a shell and then under Bash. You can see how straightforward is expression evaluation. The second expression is evaluated without specifying precision, and thus the expression evaluates to 2. We then specify precision to three decimal digits (using `scale=3;`) and bc displays results as 2.254. In the final example, we specify precision up to six decimal digits and bc displays 27.048348 that is way different from 24, the result displayed with no precision.

```
```text
$ bc
bc 1.06.95
Copyright 1991–1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty'.

10+13.7
23.7
29.37/13.03
2
scale=3; 29.37/13.03
2.254
29.37/13.03*12
24
scale=6; 29.37/13.03*12
27.048348
quit
$
```
```

The following session shows a few Bash commands that pass some of the mathematical expressions evaluated earlier to bc through a pipe.

```
```text
$ echo '29.37/13.03' | bc
2
$ echo 'scale=4; 29.37/13.03' | bc
2.2540
$ echo '29.37/13.03*12' | bc
24
$ echo 'scale=6; 29.37/13.03*12' | bc
27.048348
$
```
```

You can also pass an expression to bc through by using the `<<<` operator, as shown in the following session:

```
```text
$ bc <<< 'scale=6; 29.37/13.03*12'
27.048348
$
```
```

Finally, you can evaluate an expression with bc, save result in a shell variable, and display the result using the echo command, as in the following session:

```
$ x=`echo 'scale=6; 29.37/13.03*12' | bc`
$ echo $x
27.048348
$
```

You can use any of the mathlib functions by running bc with -l option. The following command shows the evaluation of the sine of an angle in radians using the sine function, s().

```
$ echo "s(2)" | bc -l
.90929742682568169539
$
```

The following session shows the use of if and for statements in bc. Note the similarities between these constructs and corresponding constructs of the C language.

```
$ echo 'a=10; b=20; if(a>b) print "a is greater" else print "b is greater\n" ' | bc
b is greater
$ echo "for(i=1; i<=10; i++) {i;}" | bc
1
2
3
4
5
6
7
8
9
10
$
```

## Exercise 13.4

Repeat the commands and scripts discussed in this section on your system. Were you able to reproduce the results? Log any differences.

## 13.3 Array Processing

Bash supports one-dimensional arrays. An array is a name collection of items of the same type stored in contiguous memory locations. Array items, known as members of the array, are numbered with the first one being number 0. There is no limit on the size of an array in Bash, and array elements are not required to be assigned contiguously. This means that once you have an array, you can assign a value to any array slot (see the following example). You can use any of the following syntaxes to declare array variables.

```
Syntax:
array_name[subscript]=value
declare -a array_name
declare -a array_name[subscript]
local -a array_name
readonly array_name
```

Purpose: To declare “array_name” to be an array variable. The “subscript” is considered an arithmetic expression that must evaluate to a number greater than or equal to 0. The second and third syntaxes are equivalent as “subscript” in the third declaration is ignored. The fourth syntax can be used to declare array variables whose scope is local to a function. The fifth syntax can be used to declare read-only array variables.
