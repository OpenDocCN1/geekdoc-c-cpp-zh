
# CONDITIONS AND LOOPS

To write more sophisticated programs with R, you'll need to control the flow and order of execution in your code. One fundamental way to do this is to make the execution of certain sections of code dependent on a condition. Another basic control mechanism is the loop, which repeats a block of code a certain number of times. In this chapter, we'll explore these core programming techniques using if-else statements, for and while loops, and other control structures.

## 10.1 if Statements

The if statement is the key to controlling exactly which operations are carried out in a given chunk of code. An if statement runs a block of code only if a certain condition is true. These constructs allow a program to respond differently depending on whether a condition is TRUE or FALSE.

### 10.1.1 Stand-Alone Statement

Let's start with the stand-alone if statement, which looks something like this:

```r
if(condition){
  do any code here
}
```

The condition is placed in parentheses after the keyword. This condition must be an expression that yields a single logical value (TRUE or FALSE). If it's TRUE, the code in the braces, {}, will be executed. If the condition isn't satisfied, the code in the braces is skipped, and R does nothing (or continues to execute any code after the closing brace).

Here's a simple example. In the console, store the following:

```r
R> 3
R> mynumber <- 4
```

Now, in the editor, write the following code chunk:

```r
if(a<=mynumber){
  a <- a^2
}
```

When this chunk is executed, what will the value of a be? It depends on the condition defining the if statement, as well as what's actually specified in the braced area. In this case, when the condition a<=mynumber is evaluated, the result is TRUE since 3 is indeed less than or equal to 4. This means the code inside the braces is executed, which sets a to a^2, or 9. 
Now highlight the entire chunk of code in the editor and send it to the console. Remember, you can do this in several ways:

- Copy and paste the selected text from the editor directly into the console.
- From the menu, select Edit -> Run line or selection in Windows or select Edit -> Execute in OS X.
- Use the keystroke shortcut such as CTRL-RETURN in Windows or CMD-RETURN on a Mac.

Once you execute the code in the console, you'll see something like:

```r
R> if(a<=mynumber{
+  a <- a^2
+}
```

Then, look at the object, shown here:

```r
R> a
[1] 9
```

Next, suppose you execute the same if statement giving 81? Nope! Since a is now 9 and mynumber is a squared once, still 4, the condition a<=mynumber will be FALSE, and the code in the braces will not be executed; a will remain at 9.

Note that after you send the if statement to the console, each line the first is prefaced by a +. These signs do not represent any kind of arithmetic addition; rather, that R is expecting more input before it begins. For example, when a left brace is opened, R will not begin any kind of execution until that section is closed with a right brace. To avoid redundancy, in future examples I won't show this repetition of code sent from the editor to the console.

You can change the + by assigning a different character to the component of R's options command, in the way you reset the prompt in Section 10.2.1.

The if statement offers a huge amount of flexibility—you can place any kind of code in the braced area, including more if statements (the upcoming discussion of nesting in Section 10.1.4), enabling your program to make a sequence of decisions.

To illustrate a more complicated statement, consider the following two objects:

```r
R> myvec <- c(2.73,5.40,2.15,5.29,1.36,2.16,1.41,6.97,7.99,9.52)
R> myvec
[1] 2.73 5.40 2.15 5.29 1.36 2.16 1.41 6.97 7.99 9.52
R> mymat <- matrix(c(2,0,1,2,3,0,0,1,1,5),5,2)
R> mymat
[1] 2 0
[2] 0 3
[3] 1 0
[4] 2 1
[5] 3 1
```

Use these objects in the code chunk:

```r
if(any(myvec-1)>9) || matrix(myvec,2,5)[2,1]<=6){
  cat("Condition satisfied --\n")
  myvec[seq(1,9,2)] <- NA
  mylist <- list(aa=myvec,bb=mymat)
  cat("-- list with",length(mylist),"members exists.")
}
```

Send this to the console, and it produces the following:

Condition satisfied --
-- list with 2 members exists.

Indeed, an object mylist has been created that you can examine.

```r
R> mylist
$aa
[1] NA 5.40 NA 5.29 NA 2.16 NA 6.97 NA 9.52
$bb
[,1] 2.5 0.5
[,2] 0.5 3.5
[,3] 1.5 2.5
[,4] 2.5 1.5
[,5] 3.5 1.5
```

In this example, the condition consists of two parts separated by ||, which produces a logical result. Let's walk through it.

- The first part of the condition looks at myvec-1 from myvec, and checks whether results are greater than 9. If you run this on own, it yields FALSE.

```r
R> myvec-1
[1] 1.73 4.40 1.15 4.29 0.36 1.16 0.41 5.97 6.99 8.52
R> any(myvec-1)>9
[1] FALSE
```

- The second part of the condition uses positional matching in a call to matrix to construct a two-row, five-column matrix using entries of the original myvec. Then the first column of that result is checked to see whether it is less than 6, which it is.

```r
R> matrix(myvec,2,5)
[,1] 2.73 2.15 1.36 1.41 7.99
[,2] 5.40 5.29 2.16 6.97 9.52
R> matrix(myvec,2,5)[2,1]
[1] 5.4
R> matrix(myvec,2,5)[2,1]<6
[1] TRUE
```

This means the overall condition being checked by the if statement will be FALSE || TRUE, which evaluates as TRUE.

```r
R> any(myvec-1)>9 || matrix(myvec,2,5)[2,1]<6
```

As a result, the code inside the braces is accessed and executed. First, it prints the "Condition satisfied" string and copies myvec to newmyvec. Using seq, it assigns the odd-numbered indexes of myvec and overwrites them with NA. Next, it creates list. In this list, newmyvec is stored in member name aa, and then it takes the original mymat, increases all its elements by 0.5, and stores in bb. Lastly, it prints the length of result.

Note that if statements do not match the exact style I'm using here. Some programmers, for example, prefer to open the left brace on a new line after the condition, or some may prefer a different amount of indentation.

## 10.1.2 else Statements

The if statement executes a chunk of code if and only if defined condition is TRUE. If you want something different to happen when the condition is FALSE, you can add an else declaration. Here's an example in pseudocode:

```r
if(condition)
  do any code here if condition is TRUE
} else {
  do any code here if condition is FALSE
```

You set the condition, then in the first set of braces you place the code to run if the condition is TRUE. After this, you declare else followed by a new set of braces where you can place code to run if the condition is FALSE.
Let's return to the first example in Section 10.1.1, once more storing these values at the console prompt.

```r
R a <- 3
R mynumber <- 4
```

In the editor, create a new version of the earlier if statement.

```r
if(a<mynumber){
  cat("Condition was",a=mynumber)
  a <- a^2
} else {
  cat("Condition was",a=mynumber)
  a <- a-3.5
}
a
```

Here, you square a if a condition a<=mynumber is TRUE, but FALSE, a is overwritten by the result of itself minus 3.5. You also print text to the console stating whether the condition was met. After resetting a and mynumber to their original values, the first run of the if loop computes a as 9, just as earlier, outputting the following:

Condition was TRUE

```r
R> a
[1] 9
```

Now, immediately highlight and execute the entire statement again. This time around, a<=mynumber will evaluate to FALSE and execute the code after else.

Condition was FALSE

```r
R> a
[1] 5.5
```

## 10.1.3 Using ifelse for Element-wise Checks

An if statement can check the condition of only a single logical value. If you pass in, for example, a vector of logicals for the condition, the if statement will only check (and operate based) the very first element. It will issue a warning saying as much, as the following example shows:

```r
R> if(c(FALSE,TRUE,FALSE,FALSE,TRUE,TRUE)){}
Warning message:
In (c(FALSE,TRUE,FALSE,FALSE,TRUE,TRUE)) : 
condition has length > 1 and the first element will be used
```

There is, however, a shortcut function available, ifelse, which can perform kind of vector-oriented code in relatively simple cases. To demonstrate how it works, consider the objects x and y defined as follows:

```r
R> x <- 5
R> y <- -5:5
R> y
[1] -5 -4 -3 -2 -1 0 1 2 3 4 5
```

Now, suppose you want to produce the result of x/y but with any instance of Inf (that is, any instance where y is divided by zero) replaced with NA. In other words, for each element in y, you want to whether it is zero. If so, you want the code to output NA, and if not, it should output result of x/y.
