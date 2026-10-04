# 174 Assignment, Formatting, Interactive Input

11. (Acoustics) The loudness of a sound is measured in units of decibels and is calculated
as as shown:

```
10 LOG (SL/RL)
```

SL is the intensity of the sound being measured.
RL is the reference sound-intensity level.

Using this formula, write a C++ program that calculates and displays the decibel loudness
of a busy street having sound intensity of 10,000,000 RL. Verify your program's result
by using a hand calculation. After verifying that your program is working correctly, use
it to determine the sound level in decibels of the following sounds:

+   a. A whisper at sound intensity 200 RL.
b. A rock band playing at sound intensity 1,000,000,000,000 RL.
c. An airplane taking off at sound intensity 100,000,000,000 RL.

12. (General Math) a. A balance has the following size weights: 100 lb, 50 lb, 10 lb, 5 lb,
an 1 lb. The number of 100 lb and 50 lb weights required to weigh an object weighing
WEIGHT pounds can be calculated by using the following C++ statements:

```
// Determine the number of 100 lb weights
w100 = int (WEIGHT/100);
// Determine the number of 50 lb weights
w50 = int (WEIGHT - w100 * 100) / 50
```

Using these statements as a starting point, write a C++ program that calculates the
number of each type of weight needed to weigh a 789 lb object.

+   b. Without compiling or executing your program, manually check the effect of each
statement in the program and determine what's stored in each variable as each
statement is encountered.

+   c. After verifying that your algorithm works correctly, compile and execute your program.
Verify that the results your program produces are correct. After verifying that your
program is working correctly, use it to determine the weights required to weigh a 626 lb
object.