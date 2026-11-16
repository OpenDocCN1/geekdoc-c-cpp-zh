
Here, the first (initialization) expression is:

```
i = 0, j = 10
```

The comma is the comma operator, which simply evaluates the first subexpression i = 0, then the second j = 10.

The third controlling expression:

```
i++, j--
```

also contains a comma operator, and again, performs first i++ and then j--.

In this example we initialize both variable i and j to 0 in the for loop.

```
// comma4.c
for (i = 0, j = 0; i < 10; ++i)
```

Precisely stated, the meaning of the comma operator in the general expression:

```
e1 , e2
```

is “evaluate the subexpression e1, then evaluate e2; the value of the expression is the value of e2.” Therefore, e1 had better involve an assignment or an increment ++ or decrement -- or function call or some other kind of side effect, because otherwise it would calculate a value that would be discarded.

There's hardly any reason to use a comma operator anywhere other than in the first and third controlling expressions of a for loop, and in fact most of the commas you see in C programs are not comma operators. In particular, the commas between the arguments in a function call are not comma operators; they are just punctuation which separate several argument expressions.

It's pretty easy to see that they cannot be comma operators, otherwise in a call like:

```
// comma5.c

...
printf("Hello, %s!\n", "world");
```

the action would be "evaluate the string "Hello, %s!\n", discard it, and pass only the string "world" to printf(). This is of course not what we want; we expect both strings to be passed to printf() as two separate arguments (which is, of course, what happens).

## Do While Loop

The do while loop is very similar to the while loop except that the test occurs at the end of the loop body. This guarantees that the loop is executed at least once before continuing. Such a setup is frequently used where data is to be read. The test then verifies the data and loops back to read again if the data was unacceptable.

For example, suppose you want to read in a positive integer and you want to insist that the integer is positive:

```
// positive.c
do {
   printf("Enter a positive value: ");
   scanf_s("%d", &num);
} while (num <= 0);
```

## Note the following:

- The condition num <= 0 is tested after execution of the loop body.
- The loop continues as long as the evaluation expression, num <= 0, is true.
- The loop terminates when expression, num <= 0, becomes false.
- The code always executes the body of the loop at least once.
- The semicolon is required after the closing parenthesis at the end of the do-while loop construct.
- The variable(s) used in the loop condition normally should be initialized before the loop is entered, and then updated (in the loop body) before the loop condition is tested at the end of each repetition of the loop body.

Note that when a do-while loop construct has only one statement then the curly braces {} are optional. However, it's always a good idea to use the curly braces even though they're not required.

## Break Statement

The break statement is available within the while, do while, for, and switch statements. It serves in each of these constructs as a jump to the end of the statement. It causes an exit from a loop just as it does from a switch statement. After the break is executed, program control jumps to the statement following the loop. For example:

```
// break1.c

for (i = 0; i < num; ++i) {
    if (i > 100) {
        break;
    }
    sum += i;
}
```

Note that each time you code a break (with the exception of the switch statement), you should question whether there is not a straightforward way to express the same logic without the break. We can modify the code above without using a break as follows:

```
// break2.c

for (i = 0; i < num && i <= 100; ++i) {
    sum += i;
}
```

Here's another example. Suppose we want to look for the first whitespace character (blank, tab, or newline) in a string s:

```
// break3.c
// misuse of break

for (i = 0; i < max; ++i) {
    if (s[i] == ' ' ) {
        break;
    }
    else if (s[i] == '\t') {
        break;
    }
    else if (s[i] == '\n') {
        break;
    }
}
```

A more professional approach is to state the looping condition in the test of the loop:

```
// break4.c
// search for whitespace character

for (i = 0; s[i] != ' ' && s[i] != '\t' && s[i] != '\n'; ++i) {
    ;
}
```

We can also generalize the idea of whitespace:

```
// break5.c

for (i = 0; !isspace(s[i]); ++i) {
    ;
}
```

We'll soon be taking a closer look at strings.

## Continue Statement

The break statement can be used to immediately take you out of a loop.
Sometimes, however, you want to go back to the top of the loop when something
unexpected happens.

For example, we can use the continue statement to avoid a division by zero
error:

```
// reciprocals.c
// calculate reciprocals for -5 to 5
int main(void) {
    int i;
    for (i = -5; i <= 5; i += 1) {
        if (i == 0) {
            printf("Divide by zero trap.\n");
            continue;
        }
        printf("%f\n", 1.0 / i);
    }
    return 0;
}
```

Note that in the body of the for statement, the continue statement jumps to
the loopExpression, the third expression of the for statement. In the while
and do while loops, it jumps to the test.

Like a break statement, you should always question the need for a continue
statement. By simply restructuring the code you can often eliminate the need for
a continue statement. You are very unlikely to use it.

```
-0.200000
-0.250000
-0.333333
-0.500000
-1.000000
Divide by zero trap.
1.000000
0.500000
0.333333
0.250000
0.200000
```

1. What output does the following program fragment produce?

```
i = 4;
while (i <= 128) {
    printf("%d ", i);
    i *= 2;
}
```

2. What output does the following program fragment produce?

```
i = 1234;
do {
    printf("%d ", i);
    i /= 10;
} while (i > 0);
```

3. Show the output of each of the code blocks below:

```
for (i = 5; i < 32; i += 6) {
    printf("%d\n", i);
}
```

```
for (i = 25; i > 0; i -= 5) {
    printf("%d\n", i);
}
```

4. Write C statements to sum the odd integers from 1 and 100 using a for statement. Assume the integer variables sum and count have been defined, but not initialized, to be of type int.

5. Write for statements that print the following sequences of values:

- a) 10, 20, 30, 40, 50
- b) 75, 65, 55, 45, 35

## 6. Assume that we want to calculate the sum of the integers from 50 down to 1. What is wrong with the code below?

```
sum = 0;
num = 50;
while (num >= 0) {
    sum += num;
}
```

## 7. See if you can improve the following program segments through reorganization. First analyze the code to determine the function actually being performed. Then recode that function as clearly and simply as possibly (i.e. without the use of break or continue).

```
a) while(a) {
    if(b) {
        continue;
    }
    c();
}
```

```
b) do {
    if (!a) {
        continue;
    }
    else {
        b();
        c();
    }
} while (a);
```

## Grade Lab

Write a C program, grade.c, which includes a function,
calculateAverage(), that can calculate the average of an arbitrary number of
test scores. Your program will not know in advance how many test scores will be
entered into your function so you will need to use a sentinel value (-1) to
terminate the while loop used to collect the test scores. The test scores are
integers in the range 0 to 100 and the test score average should be output to two
decimal places. Be sure that the user prompts and grades input into the program
are displayed in the output file.

Provided below is the main() function that I would like you to use for your
program.

```
int main (void) {
	int i;

	fopen_s(&fp, "csis.txt", "w");

	for (i = 1; i <= 4; ++i) {
		calculateAverage();
	}

	fclose(fp);
	return 0;
}
```

Please do not modify the main() function. It should appear as the first function
in the program. Be sure to use function prototypes for each of the functions that
are used in your program.

Note that the for loop invokes the calculateAverage() function four times.
Each time the calculateAverage() function is invoked, a different set of test
grades will be entered. Please be sure to use the data shown below:

```
First: 78, 93, 45, 88, 89, -1
Second: 87, 68, 100, -1
Third: 84, 86, 90, 86, 96, 68, 82, -1
Fourth: -1
```
