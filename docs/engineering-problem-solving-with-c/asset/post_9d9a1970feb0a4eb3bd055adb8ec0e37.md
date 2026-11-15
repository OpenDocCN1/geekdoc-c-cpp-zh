
{
   // Declare and initialize objects.
   int degrees;
   double radians;

   // Set formats.
   cout.setf(ios::fixed);
   cout.precision(6);

   // Print radians and degrees in a loop.
   cout << "Degrees to Radians \n";
   while(degrees <= 360)
   {
      radians = degrees*PI/180;
      cout << setw(6) << degrees << setw(10) << radians << endl;
      degrees += 10;
   }

   // Exit program.
   return 0;
}
/**********************************************************************/

The first few lines of output from the program follow:

```
Degrees to Radians
0   0.000000
10  0.174533
20  0.349066
.   ...
```

To further illustrate the while loop, we provide a program trace and memory snapshot for the first three iterations of the loop. Notice that the value of degrees is printed inside the while loop before the value is incremented by 10.

## Program Trace

```
main()
Step 1: int degrees(0);
Step 2: double radians;
Step 3: while(degrees <= 360)
{
   radians = degrees*PI/180;
   cout << setw(6) << degrees << setw(10)
   << radians << endl;
   degrees += 10;
}
```

## Memory Snapshot

### main()

| Step | Variable | Value |
| :--- | :--- | :--- |
| Step 1: | integer degrees | 0 |
| Step 2: | double radians | ? |
| Step 3: | End first iteration | |
| | integer degrees | 10 |
| | double radians | 0.0 |
| End second iteration | integer degrees | 20 |
| | double radians | 0.174533 |
| End third iteration | integer degrees | 30 |
| | double radians | 0.349066 |
| ... | ... | ... |

We see that degrees is initialized to zero in the type declaration statement, thus the condition degrees <= 360 is true the first time it is tested and the statement block that defines the while loop is executed. Inside the statement block the first line of the conversion table is printed, and degrees is incremented by 10. When the end of the statement block is encountered, control branches back to the condition and it is tested a second time. Again the condition is true and the statement block is executed, this time with a value of 10 for degrees. This repetition continues until the value of degrees reaches 370. Since 370 is greater than 360, the condition is false and the while loop terminates. Termination of the while loop results in control branching down to the first statement following the statement block, the return 0; statement in this case. Note that the directed arrows in the flowchart in Figure 4.2. illustrate the branching associated with the while loop.

## do/while Loop

The do/while loop is similar to the while loop, except that the condition is tested at the end of the loop instead of at the beginning of the loop, as illustrated in Figure 4.3. Testing the condition at the end of the loop ensures that the do/while loop is always executed at least once; a while loop will not be executed at all if the condition is initially false. The general form of the do/while loop is as follows:

```
do
{
 statements;
} while(condition);
```

![](img/0235a4ea835dc4575bd036e024a533b3_182_0.png)

Figure 4.3 Flowchart for do/while.

## Statement Box 4.2

do/while Statement: The do/while statement allows a program to execute a block of statements repeatedly while the specified condition is true. The statement or statement block in a do/while statement will always be executed at least once.

```
do
  statement;
while(condition);

do
{
  statement block
} while(condition);
```

```
do
  cin.get(ch);
while(ch != '\n');

do
{
  v = a*t + v0;
  cout << t << " " << v << endl;
  t += 0.5;
} while(t<10);
```

The following pseudocode and program print the degree-to-radian conversion table using a do/while loop instead of a while loop:

## Refinement in Pseudocode

```
main: set degrees to zero
  do
    convert degrees to radians
    print degrees, radians
    add 10 to degrees
  while degrees < 360
```

/*--------------------------------------------------------------*/
/* Program chapter4_3                                           */
/*                                                              */
/* This program prints a degree-to-radian table                 */
/* using a do-while loop structure.                             */
/*                                                              */
/*--------------------------------------------------------------*/
#include<iostream>   //Required for cout
#include<iomanip>    //Required for setw()

const double PI(3.141593);

int main()
{
   // Declare and initialize objects.
   int degrees(0);
   double radians;

   // Set formats.
   cout.setf(ios::fixed);
   cout.precision(6);

   // Print degrees and radians in a loop.
   cout << "Degrees to Radians \n";
   do
   {
      radians = degrees*PI/180;
      cout << setw(6) << degrees << setw(10) << radians << endl;
      degrees += 10;
   } while (degrees <= 360);

   // Exit program.
   return 0;
}
/*--------------------------------------------------------------*/

## Practice 4.1

For Problems 1 through 6, show what is printed to standard output. If the cout statement is not executed, please explain why.

- 1. int count(1);
     while (count < 5)
     {
     ++count;
     }
     cout << count << endl;
   
- 2. int count(1);
     while (count < 5)
     {
     --count;
     }
     cout << count << endl;

## Practice 4.1 continued

- 3. int count(10);
   while(count > 0)
   {
    count -= 2;
   }
   cout << count << endl;
   
- 4. int count(0);
   do
   {
    count = count+3;
   } while(count > 10);
   cout << count << endl;
   
- 5. const int MAX(2);
   int count(0);
   bool flag(true);
   while(flag)
   {
    ++count;
    cout << count << endl;
    if(count > MAX) flag = false;
   }
   
- 6. int count(0);
   do
   {
    cout << count << endl;
    ++count;
   } while(count <= 0);

## Modify 4.1

- 1. Modify program chapter4_1 by replacing the while loop with a do/while loop. Verify that the output is the same.
   
- 2. Modify program chapter4_1 by adding the necessary C++ statements to prompt the user to enter the values for initial velocity and constant acceleration. Use these values to compute and print velocity.
   
- 3. Modify program chapter4_1 by adding the necessary C++ statements to prompt the user to enter the initial and final values for time. Use these values to compute and print velocity.

## for Loop

Many programs require loops that are based on the value of a counter that increments (or decrements) by the same amount each time through the loop. When the counter reaches a specified value, we then want to exit the loop. This type of loop can be implemented as a while loop, but it can also be easily implemented with the for loop. The general form of the for loop is as follows:

```
for(expression_1; expression_2; expression_3)
{
 statements;
}
```

The first expression is used to initialize the loop-control variable, expression_2 specifies the condition that must be true to continue the loop repetition, and expression_3 specifies the modification to the loop-control object that follows the execution of the statement block.

Note that expression_1 is executed one time only. The condition, expression_2 is tested 1 to (n + 1) times and expression_3 is executed 0 to n times, where n is the number of times the statement block is executed. The syntax box is provided below, and a flowchart is provided in Figure 4.4.

![](img/0235a4ea835dc4575bd036e024a533b3_185_0.png)

## Statement Box 4.3

for Statement: The for statement allows a program to execute a block of statements repeatedly based on the value of a counter that is modified by the same amount each time through the loop.

```
Syntax:
for(initialization; condition; modification)
    statement;

for(initialization; condition; modification)
{
    statement block
}
```

```
Example:
for(int count(1); count<=10; ++count)
    sum = sum + count;

for(int i(counter); i>0; --i)
{
    cin >> degrees;
    radians = degrees * PI/180;
    cout << degrees << " "
         << radians << endl;
}
```
