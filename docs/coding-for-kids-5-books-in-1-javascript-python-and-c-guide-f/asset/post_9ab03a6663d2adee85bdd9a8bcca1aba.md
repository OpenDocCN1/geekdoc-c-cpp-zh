
```
Execute()
```

Finally, if we want to keep running execute() till 6 PM, we use a WHILE loop.

```
while (checktime != 18:00):
    Execute();
```

These are simple examples of the loops to explain the concepts of loops. This concept is very important in coding.

Now, let’s do some examples in Python.

## FOR LOOP Example 1

A simple example of a For Loop is a program that counts to 10.

```
for i in range(11):
    print(i)
```

The above code is probably the simplest example of a for loop. The loop runs from 0 to 10, so it runs 11 times, each time printing i, which is the loop iteration number.

**Note:** range(n) function makes the loop runs from 0 to n-1.

```
for i in range(11)
```

The line above means that the loop starts from 0 (i=0). It is increasing by 1 each time. The loop ends when i reaches 10.

### Output:

```text
0
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
```

You can see the numbers 0 to 10 printed on the screen.

## FOR LOOP Example 2

Now, let’s do a slightly different version of this. In this example, we’re going to use an input that takes in a number for the loop. That means we can make the loop as long as we want.

```python
loop_length = int(input("How long? "))
for i in range(loop_length):
    print(i)
```

The input takes in a number input and stores in a variable called “loop_length”.

```
Please enter the loop length: 15
0
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
11
12
13
14
```

The loop prints all the numbers between 0 and “loop_length” variable. In the example below, we put 15 in input; and as we can see, it prints out numbers between 0 and 14. Note that loop stops right before n because Python starts indexing at 0 and up to but not including “loop_length”.

## FOR LOOP Example 3 – Nested Loops

In this final example, we use FOR loops to create a half pyramid pattern. The program asks for a pyramid length and stores it in a variable called `pyramid_height`.

Then it runs 2 nested loops where the outer loop iterates for the pyramid ‘levels’ and the inner loop prints the stars at each level starting from zero. Each level contains j stars where j is the current level number.

So, for example, if you’re going through the first loop for the 5th time, i=5. The second loop prints * from 0 to 4 (i.e. 5 times).

In the example below, we print a half pyramid for a pyramid_height of 8.

```python
pyramid_height = int(input("Please enter the pyramid height: "))

for i in range(pyramid_height):
    for j in range(i):
        print("*", end="")
    print()
```

```text
Please enter the pyramid height: 8

*
**
***
****
*****
******
*******
```

## WHILE LOOP EXAMPLE 1

A while loop runs while a certain condition is met. If the condition is no longer met, it breaks out of the loop. In the example below, the program executes a while loop that takes in a user input via the input function. The while loop keeps running and printing the user text. The loop stops when the user inputs the word ‘STOP’. Once the word is input, that’s the end of the while loops and the program stops.

```python
text = ''

while(text != 'stop'):
    text = input("What do you want to do now ? ")
    print("Activity is : ", text)
```

### Output:

```
What do you want to do now ? Read
Activity is : Read
What do you want to do now ? play
Activity is : play
What do you want to do now ? study
Activity is : study
What do you want to do now ? stop
Activity is : stop
```

We can see while loop kept asking the user for an input until the user entered “stop”, the while loop condition was met and it ceased execution.

## Practice Problems

- 1. Write a program that takes 2 inputs numbers a and b and return the remainder of a divided by b.

- 2. Write a program that outputs a number multiplication table up to 10. For example, if 3 is entered it outputs: 3, 6, 9, 12, 15, 18, 21, 24, 27, 30

- 3. Write a program that find the length of given word using a for loop. Note: Python already have len() function that return the length of a string, try to use both a loop and len().

- 4. Write a program that counts the total number of digits in number. For example, “345abcd32” has 5 digits.

- 5. Write a program that keeps taking user input number until an even number is entered where it stops.

- 6. Write a program that takes two numbers a and b then it outputs all odd numbers between a and b inclusive.

- 7. Write a program that takes a user input pyramid height and outputs the following symmetrical pyramid pattern. For example, if the user inputs the number ‘5’ then the pattern is:

    ```
    *
    **
    ****
    ******
    ********
    ```

- 8. Write a program that sums all numbers from 1 up to n where n is a number that the user input. Note: First approach this problem using for loop then use the formula 1 + 2 + ... + n = n(n+1) / 2 .

## Gaming Time - Loops

Now, it’s time to design a few games based on what we’ve learned so far. There’s no better way of learning concepts than applying them; and even better to apply them to something fun.

### Game 1 – Guess Random Numbers

In this game, we’re going to create a program that takes in a number via Input function. The number is between 0 and 10. Then we compare that number to a random number generated via random module (using random.randint). If it is the same, then the guessed number is correct. If not, then we give them the right number. See the code and output below.

```python
import random

print("You have only three tries to guess number correctly")

# generate random integer between 0 and 10
random_number = random.randint(0, 10)


won = False
for try_num in range(3):
    print()
    print(f"Try number {try_num+1}")
    guessed_number = int(input("Guess a number between 0 and 10 inclusive: "))

    if(guessed_number == random_number):
        won = True
        print("Good job ! You won")
        break

    else:
        print("Incorrect, try again !")

if(won == False):
    print()
    print("You ran out of tries, Good luck next time")
    print("The right number is ", random_number)
```

random.randint(n, m) generates a random number between n and m inclusive. This is different from random.random(), which generates a random real number anywhere in the range 0 and 1.

This is basically built around a for loop which runs 3 times giving the user 3 tries to guess the random number correctly. If the user guesses the random number correctly, then the if block at line 15 will set the **won** variable to **True** and break out of the loop. In Python, to break out of the loop, we use “break”. The **if** block at line number 22 is used when the user has run out of his tries.

### Output:

```text
You have only three tries to guess number correctly

Try number 1
Guess a number between 0 and 10 inclusive: 4
Incorrect, try again !

Try number 2
Guess a number between 0 and 10 inclusive: 4
Incorrect, try again !

Try number 3
Guess a number between 0 and 10 inclusive: 5
Incorrect, try again !

You ran out of tries, Good luck next time
The right number is 9
```

If the user wins here is a sample output:

```text
You have only three tries to guess number correctly

Try number 1
Guess a number between 0 and 10 inclusive: 5
Good job ! You won
```

This program is a good way to practice conditional loops and random number generators.

### Game 2 – Math Quiz Game

This program prints out 5 simple math problems and takes in answers to these problems via input they are (user_ans1, user_ans2, user_ans3, user_ans4, user_ans5). The answers are stored in variables as (ans1, ans2, ans3, ans4, ans5). These answers are compared to the real answers using if conditional. A counter score is incremented by 1 each time the user gets a correct answer and finally the counter is printed to see how many correct answers the user gets.

```python
# Game 2 - Math Quiz Game

print("This is a game where you find basic mathematical operations for 2 integer numbers n1 and n2 \n")
n1 = 8
n2 = 2

ans1 = n1 + n2
ans2 = n1 - n2
ans3 = n1 * n2
ans4 = n1 % n2

user_ans1 = int(input(f"{n1} + {n2} = "))
user_ans2 = int(input(f"{n1} - {n2} = "))
user_ans3 = int(input(f"{n1} * {n2} = "))
user_ans4 = int(input(f"{n1} % {n2} = "))
print()

score = 0

if ans1 == user_ans1:
    score += 1
if ans2 == user_ans2:
    score += 1
if ans3 == user_ans3:
    score += 1
if ans4 == user_ans4:
    score += 1

print(f"You have got {score} answers correct")
```
