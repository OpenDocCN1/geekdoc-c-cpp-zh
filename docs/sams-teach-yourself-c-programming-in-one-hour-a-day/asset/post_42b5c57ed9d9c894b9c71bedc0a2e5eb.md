
4. The first line of a function definition must be the function header. It contains the function’s name, its return type, and its parameter list.

5. A function can return one value or no values. The value can be of any of the C variable types. In Lesson 19, “Getting More from Functions,” you can see how to get more values back from a function.

6. A function that returns nothing should be type void.

7. A function definition is the complete function, including the header and all the function’s statements. The definition determines what actions take place when the function executes. The prototype is a single line, identical to the function header, but it ends with a semicolon. The prototype informs the compiler of the function’s name, return type, and parameter list.

8. A local variable is declared within a function.

9. Local variables are independent from other variables in the program.

10. main() should be the first function in your listing.

# Exercises

- 1. float do_it(char a, char b, char c) Add a semicolon to the end, and you have the function prototype.
- 2. void print_number(int a) In an actual program, the header is followed by the function’s statements.
- 3. a. int b. long. The first print_msg() function is declared as void; however, it returns a value. The second problem is on the fifth line. The call to print_msg() passes a string (a). The prototype states this function has a void parameter list and, therefore, shouldn't passed anything. The following is corrected listing:
```c
#include <stdio.h>
void print_msg(void);
int main(void) {
    print_msg();
    return 0;
}

void print_msg(void) {
    puts("This is a message to print ");
}
```
- 4. There should not be a semicolon at the end of the function header.
- 5. Only the larger_of() function needs to change:
```c
int larger_of(int a, int b) {
    int save;
    if (a > b)
        save = a;
    else
        save = b;
    return save;
}
```
- 6. The following assumes two values are integers and an integer is returned:
```c
int product(int x, int y) {
    return (x * y);
}
```
- 7. The following listing checks the second value passed to verify it is not 0. Division by zero causes an error. You should never assume that the values passed are correct. However, this only prevents a division-zero error at the function level. It will return 0 to the calling program because the program needs to always return an integer type. To avoid division error, your program should check the value of b before you call the divide() function:
```c
int divide(int a, int b) {
    int answer = 0;
    if (b == 0)
        answer = 0;
    else
        answer = a / b;
    return answer;
}
```
- 8. Although the following code uses main(), it could use any function. Lines 9, 10, and 11 show the calls to the two functions. Lines 13 through 16 print the values. To run this listing, you need to include the code from exercises 7 and 8 after line 19.

# Answers for Lesson 5

```c
#include <stdio.h>
int main(void) {
    int number1 = 10, number2 = 5;
    int x, y, z;
    x = product(number1, number2);
    y = divide(number1, number2);
    z = divide(number1, 0);
    printf("number1 is %d and number2 is %d\n", x, x);
    printf("number1 / number2 is %d\n", y);
    printf("number1 / 0 is %d\n", z);
    return 0;
}
```

- 10. The code is as follows:
```c
/* Averages float values entered by the user. */
#include <stdio.h>

float v, w, x, y, z, answer;

float average(float a, float b, float c, float d, float e);

int main(void) {
    puts("Enter five numbers:");
    scanf("%f%f%f%f%f", &v, &w, &x, &y, &z);
    answer = average(v, w, x, y, z);
    printf("The average is %f.\n", answer);
    return 0;
}

float average(float a, float b, float c, float d, float e) {
    return ((a+b+c+d+e)/5);
}
```

- 11. The following is the answer using int variables. It can run only with values less or equal to 9. To use values larger than 9, you need to change the values to type long.
```c
/* this is a program with a recursive function */
#include <stdio.h>

int three_powered(int power);

int main(void) {
    int a = 4;
    int b = 9;

    printf("\n3 to the power of %d is %d\n", a, three_powered(a));
    printf("\n3 to the power of %d is %d\n", b, three_powered(b));

    return 0;
}

int three_powered(int power) {
    if (power < 1)
        return (1);
    else
        return (3 * three_powered(power - 1));
}
```

# Answers for Lesson 6

# Quiz

1. The first index value of an array in C is 0.
2. A for statement contains initializing and increment expressions as parts of the command.
3. A do...while contains the while statement at the end and always executes the loop at least once.
4. Yes, a while statement can accomplish the same task as a for statement, but you need to do two additional things. You must initialize any variables before starting the while command, and you need to increment any variables as a part of the while loop.
5. There is no limit to the number of statements you nest.
6. Yes, while a statement can be nested in a do...while loop. You can nest any command within any other command.
7. The four parts of a for statement are the initializer, the condition, the increment, and the statement(s).
8. The two parts of a while statement are the condition and the statement(s).
9. The two parts of a do...while statement are the condition and the statement(s).

# Exercises

- 1. long array[50];
- 2. Notice that in the following, array[49] = 123;
- 3. When the statement is complete, x equals 100.
- 4. The inner loop prints five times. The outer loop prints 10 times.
- 5. This totals 50.
- 6. The code is as follows:
```c
int x;
for(x = 1; x <= 50; x += 3);
```
- 7. The code is as follows:
```c
int ctr = 1;
{
  ctr += 3;
} while(ctr < 100);
```
- 9. This program never ends. record is initialized to 0. The while loop then checks to see record is less than 100. 0 to the calling program because the program needs to always return an integer type. To avoid division error, your program should check the value of b before you call the divide() function:
record++;
- 10. Using a defined constant is common in looping; you can see examples similar to this fragment throughout the book. The problem with this fragment is simple. The semicolon doesn't belong at the end of the for statement. This is a common bug.

# Answers for Lesson 7

# Quiz

1. There are two differences between puts() and printf():
   printf() can print variable parameters.
   puts() automatically adds a newline character to the end of the string it prints.
2. You should include the stdio.h header file using printf().
3. a. \ prints a backslash.
   b. \b prints a backspace.
   c. \n prints a newline.
   d. \t prints a tab.
   e. \a for "alert" sounds the beep.
4. a. %s for a character string
   b. %d for a signed decimal integer
   c. %f for a decimal floating-point number
5. a. b prints the literal character b.
   b. \ prints a backspace character.
   c. \ looks at the next character to determine an escape character (see Table 7.1).
   d. \ prints a single backslash.

# Exercises

- 1. puts() automatically adds the newline; printf() does not. The code is as follows:
```c
printf("\n");
puts(" ");
```
- 2. The code is as follows:
```c
char c1, c2;
int d1;
scanf("%c %u %c", &c1, &d1, &c2);
```
