
The conditional statement is very useful for shortening programs. We can rewrite the following if-else statement:

```
if (x > y) {
    printf("%d\n", x);
} else {
    printf("%d\n", y);
}
```

as

```
printf("%d\n", x > y ? x : y);
```

In the following statement:

```
num = value > 0 ? ++x : ++y;
```

only one of the expressions, either `++x` or `++y` gets evaluated, but never both!

Two functions are shown below using the conditional operator. Note that they also use functions from the ctype.h library:

```
// convert lower case to upper case
char toUpper(char c) {
    return islower(c) ? c - 32 : c;
}

// convert upper case to lower case
char toLower(char c) {
    return isupper(c) ? c + 32 : c;
}
```

Here's an example that prints n elements of an array, 10 per line, with each column separated by one blank, and with each line (including the last) terminated by exactly one new line:

```
// Long Form
for (i = 0; i < n; ++i) {
    printf("%6d", a[i]);
    if (i % 10 == 9 || i == n - 1) {
        printf("%s", "\n");
    } else {
        printf("%s", " ");
    }
}
```

A newline is printed after every 10th element, and after the nth all other elements are followed by one blank.

```
// Short Form
for (i = 0; i < n; ++i) {
    printf("%6d%c", a[i], (i % 10 == 9 || i == n - 1) ? '\n' : ' ');
}
```

### 1. Write a single statement to accomplish each of the following:

- a) If value is not equal to 15, print "The variable value is not equal to 15."
- b) Test if the value of the variable num is less than 5. If it is, print "Num is less than 5."

### 2. What are the values of the following expressions? Remember that C does not use Boolean logic (true or false), but rather uses semi-boolean logic (zero or non-zero). You may assume all variables are declared to be of type int.

- a) i = 2; j = 3; i + j == 6
- b) i = 3; j = 2; k = 1; i < j < k
- c) i = 3; j = 4; k = 5; i % j + i < k
- d) i = 10; j = 5; i < j
- e) i = 2; j = 1; i + j
- f) i = 5; j = 0; k = -5; i && j || k

```
i = 1;
j = 2;
k = 3;
i < j || k
/ 2 or 3 True
```

### 3. What are the values of the following expressions. You may assume all variables are declared to be of type int.

```
c = 2;
d = 3;
a = 0;
e = -1;
```

- a) (c < d) || a
- b) 2 < (c + d)
     z < 3
- c) !(!((c > d)) || ...

### 4. The following if statement is unnecessarily complicated. Simplify it as much as possible. (Hint: The entire statement can be replaced by a single assignment.)

```
if (age >= 13)
if (age <= 19)
teenager = true;
else
teenager = false;
else if (age < 13)
teenager = false;
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_166_0.png)

### 5. The mathematical operation:

```
min(x, y)
```

can be represented by the conditional expression:

```
(x < y) ? x : y
```

In a similar fashion, using only conditional expressions, describe the mathematical operation:

```
min(x, y, z)
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_166_1.png)

## Body Mass Index Lab

The BMI, or Body Mass Index, is a measure of one's body fat based upon the individual's height and weight. It can determine whether or not an individual is overweight or obese.

The formula for calculating BMI is as follows:

```
BMI = weightInPounds x 703
heightInInches x heightInInches
```

The following table can be used to evaluate a BMI score:

| BMI VALUES | |
| :--- | :--- |
| Less than 18.5 | Underweight |
| Between 18.5 and less than 25.0 | Normal |
| Between 25.0 and less than 30.0 | Overweight |
| 30.0 or greater | Obese |

For this lab you are to construct a C program, bmi.c, which includes a function, calculateBMI(), that prompts the user to input a weight, in pounds, and height, in inches, and then calculates and displays the body mass index. The function should also display whether a person is underweight, normal, overweight, or obese.

Be sure that the user prompts as well as the height and weight values input into the program are displayed in the output file. Note that the resultant BMI values should be displayed to one decimal place. The variables in your function that receive the height and weight values should be declared as double.

Provided below is the main() function that I would like you to use for the program.

```
int main (void) {
    int i;

    csis = fopen("csis.txt", "w");
    for (i = 1; i <= 4; ++i) {
        calculateBMI();
    }
    fclose(csis);
    return 0;
}
```

Note that the for loop invokes the calculateBMI() function four times. Each time the calculateBMI() function is invoked, a different weight and height will be entered. Please be sure to use the data shown below:

| First: | 175 | 70 | 25.1 | Overweight | |
| Second: | 120 | 68 | 18.2 | Underweight | (z<x 28 x<5) |
| Third: | 225 | 65 | 37.4 | Obese | (2x<5) |
| Fourth: | 140 | 67 | 21.9 | Normal | |

Output from your program should be sent to the terminal window (your screen) as well as the requested csis.txt output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains main(). Be sure to include the csis.txt output file in your zip archive. Please do not modify the main() function that I provide above.

## Large-Small Lab

Write a C program, largeSmall.c, which includes a function, compare(), that prompts the user to input four integers and calculates and displays the largest and smallest of the integers. Be sure that the user prompts as well as the four integers input into the program are displayed in the output file.

Provided below is the main() function that I would like you to use for the program.

```
int main (void) {
    int i;
    csis = fopen("csis.txt", "w");
    for (i = 1; i <= 4; ++i) {
        compare();
    }
    fclose(csis);
    return 0;
}
```

Note that the for loop invokes the compare() function four times. Each time the compare() function is invoked, a different set of four integers will be entered. Please be sure to use the data shown below:

| | a | b | c | d | Biggest | Small |
|---|---|---|---|---|---|---|
| First: | 28 | 44 | 66 | 82 | 82 | 28 |
| Second: | 8 | 14 | 22 | 6 | 22 | 6 |
| Third: | 21 | 38 | 12 | 16 | 38 | 12 |
| Fourth: | 98 | 22 | 45 | 63 | 98 | 22 |

Output from your program should be sent to the terminal window (your screen) as well as the requested csis.txt output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains main(). Be sure to include the csis.txt output file in your zip archive. Please do not modify the main() function that I provide above.

## Chapter 8. Repetition Statements

- While Statement
- For Statement
- Comma Operator
- Do-While Loop
- Break Statement
- Continue Statement
- Repetition Homework
- Grade Lab
- Penny Lab
- Fibonacci Lab

## While Loop

A repetition statement allows you to specify that an action is to be repeated while some condition remains true. For example, the statement:

```
while there are more items on my shopping list
purchase next item and cross it off my list
```

describes the repetition that occurs during a shopping trip. The condition:

```
there are more items on my shopping list
```

may be true or false. If it's true, then the action:

```
purchase next item and cross it off my list
```

is performed. This action will be performed repeatedly while the condition remains true. Eventually, the condition will become false (when the last item on the shopping list has been purchased and crossed off the list). At this point, the repetition terminates, and the first statement after the repetition structure is executed.

So loops provide a means of repeating a series of executable statements (the loop body) as long as the condition controlling the loop (usually found in the loop header) evaluates to true. The loop control condition is a logical expression that evaluates to either true or false. Often, this expression involves a single variable, called a loop control variable.

The loop body is the block of code that contains the series of executable statements associated with the loop condition. Note that the loop body may be a single statement or a compound statement. The loop body will be repeated as long as the loop condition evaluates to true. When the loop condition evaluates to false, the loop will terminate. Each time the loop body is repeated, the loop is said to have gone through an iteration.
