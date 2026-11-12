
## Two-Way Selection

- Logical expressions evaluate to either a true or false value.
- If the resulting logical value is true we have one path to travel, but if the result is false we will execute alternative (and unique) statements found down a second path.
- Two selection constructs are available for two-way selection in C programming: if/else and the conditional expression.

### if / else

- The if/else construct, or a very similar variation, exists in about every programming language. The idea is that a logical expression is evaluated with one set of statements to be executed when the logical expression is true and an alternative set of statements to be executed when it is false.

```
if(logical expression)
{
//TRUE ACTIONS TO EXECUTE
}
else
{
//FALSE ACTIONS TO EXECUTE
}
```

- If the first condition (logical expression) listed is evaluated to be true the statements found in the body of the if will be executed, otherwise execute the statements found in the body of the else.

### Diagram of Two-way Logic:

### Example: A function receives a non-negative integer, add one and return it when even or subtract one and return it when odd.

```
int changeNumber(int n)
{
    if(n % 2 == 0)
    {
        n++;
    }
    else
    {
        n--;
    }
    return(n);
}
```

### Example #2: Revise the previous function to only change the value (subtract one) if odd.

| int changeNumber(int n) | int changeNumber(int n) |
|---|---|
| { | { |
| if (n % 2 == 1) | if (n % 2 == 0) |
| { | { |
| n--; | //NEVER LEAVE A BODY EMPTY |
| } | } |
| else | else |
| { | { |
| ////NEVER LEAVE A BODY EMPTY | n--; |
| } | } |
| return(n); | return(n); |
| } | } |

### Best solution option for revised problem (else is optional):

```
int changeNumber(int n)
{
if (n % 2 == 1)
{
n--;
}
return(n);
}
```

## Nested Selection

The if/else can contain any executable statement, including another if/else construct. When this occurs we call it nested selection. Often, nested selection involves the comparison of two or more different variables.

### Logical Flow of Nested Selection:

![](img/50641bd70680c74d7c49fe705f0d8389_86_0.png)

### Code example of nested selection:

```
int calcStatus(float gpa, int credit_hrs)
{
 int status;
 if(credit_hrs > 120)
 {
 if(gpa >= 3.50)
 {
 status = HONORS;
 }
 else
 {
 status = CANDIDATE;
 }
 }
 else
 {
 status = NONCANDIDATE;
 }
 return(status);
}
```

### Dangling Else Logical Error and Nested if/else

- Debugging Concern: Please note that the text and many other sources will not always use { } with if/else statements that contain only a single statement in their body. However, this can lead to a difficult logical problem known as the "dangling else".
- Because this problem can be so difficult to debug, we will require ALL if/else statements to use { } even if the body contains only a single executable statement.

| Example of dangling else logical error: | Output Generated: |
|---|---|
| `int x = 3;`<br>`int y = 2;`<br>`int z = 0;`<br>`if(x == 3)`<br>`    if(y != 2)`<br>`        z++;`<br>`else`<br>`    z--;`<br>`printf("z = %d\n", z);` | warning: suggest explicit braces to avoid ambiguous 'else' |

Logic interpretation of code above:

## Conditional Expressions

The conditional expression has three operands and two operators. Each operand is itself an expression.

- The first operator is a question mark that separates the first two expressions.
- The second operator is a colon and separates the last two expressions.

To evaluate a conditional expression, we first must evaluate the leftmost expression. When this expression is true, then the value of the second expression (the first expression after the ?) is evaluated. However, if the logical expression (before the ?) is false, then the third expression is evaluated.

Below, when the sum of the two variables is greater than zero the variable a is incremented. When the sum is less than or equal to zero then the variable b is incremented.

```
a + b > 0 ? a++ : b++;
```

### More Conditional Expression Examples:

| Code | Output Generated: |
|---|---|
| int a = 1;<br>int b = -1;<br>int c;<br><br>a + b > 0 ? a++ : b++;<br><br>c = a > b ? 5 : 3;<br><br>printf("c = %d\n", c);<br><br>a == b ? printf("a == b\n") : printf("a != b\n"); | |

Must there be an expression for both the second and third expressions?

- Yes.
- error: expected expression before ';' token

Is it possible for each option, true and false to have more than one expression?

- No.

## Multi-way Selection

It is a common problem to require selection from more than two alternative sections of unique code. This is the idea of multi-way selection.

- In C, there are two different constructs available to implement multi-way selection. The first is by using if/else if/else, the second is a switch construct. The switch construct has a few more restrictions than the if/else if/else construct but the switch does have circumstances in which its use might be favored over the alternative option.

### Multi-way Selection if/else if/else

- Example: Write a program that will accept a score as input and reply to the user based on the score what letter grade they can expect to receive.

```
#define MINA 90
#define MINB 80
#define MINC 70
#define MIND 60

int getScore(void);
char determineGrade(int);
void displayResults(char, int);

int main(void)
{
    int score; //SCORE OF STUDENT
    char grade; //CALCULATED GRADE BASED ON SCORE

    score = getScore();
    grade = determineGrade(score);

    displayResults(grade, score);

    return(0);
}

void displayResults(char grade, int score)
{
    printf("Based on your score of %d, you will receive the grade of %c in this course.\n", score, grade);
}

int getScore(void)
{
    int score; //SCORE TO BE ENTERED BY THE USER

    printf("Enter the score for the course: ");
    scanf("%d", &score);

    return(score);
}

char determineGrade(int score)
{
   char grade;

   if(score >= MINA)
   {
      grade = 'A';
   }
   else if(score >= MINB)
   {
      grade = 'B';
   }
   else if(score >= MINC)
   {
      grade = 'C';
   }
   else if(score >= MIND)
   {
      grade = 'D';
   }
   else
   {
      grade = 'F';
   }

   return(grade);
}
```

Figure 5-24 on page 261 is a good flowchart illustration of this selection construct.

> Note: In this example as soon as one of the conditions is true the statements in the body for the particular condition are executed and then the if/else if/else structure is exited.

### Are either of the constructs below logically equivalent to the one on the previous page?

```
if(score >= MINA)
{
    grade = 'A';
}
else if(score >= MINB && score < MINA)
{
    grade = 'B';
}
else if(score >= MINC && score < MINB)
{
    grade = 'C';
}
else if(score >= MIND && score < MINC)
{
    grade = 'D';
}
else
{
    grade = 'F';
}

if(score >= MINA)
{
    grade = 'A';
}
if(score >= MINB && score < MINA)
{
    grade = 'B';
}
if(score >= MINC && score < MINB)
{
    grade = 'C';
}
if(score >= MIND && score < MINC)
{
    grade = 'D';
}
else
{
    grade = 'F';
}
```

### Multi-way Selection switch

A switch construct is used to make a selection among possible integer value alternatives. The switch may be favored when the possible integer values are well known and few in number.

The control expression that follows the keyword switch is evaluated and then compared with a series of cases for equality. Each case represents an expected value of the control expression.

- Associated with each case is one or more executable statements.
- There should exist one or more possible cases. You should consider an if/else if when the number of cases is large or represent a range of values.
- A default case is an option to cover all values not represented by the other individual cases.

> Note: Each case is compared with the value of the control expression for equality.

```
void displayResults(char grade, int score)
{
    printf("Given score of %d, you will earn a grade of %c in this course.\n", score, grade);
    switch(grade)
    {
        case 'A': printf("Great job!\n");
            break;
        case 'B': printf("Well done!\n");
            break;
        case 'C': printf("Mission Accomplished.\n");
            break;
        case 'D': printf("Perhaps you need to consider repeating?\n");
            break;
        default: printf("See you next semester?\n");
    }
}
