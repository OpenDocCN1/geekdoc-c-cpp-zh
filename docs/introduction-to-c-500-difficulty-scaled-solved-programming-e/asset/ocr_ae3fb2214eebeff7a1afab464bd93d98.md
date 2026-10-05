# 120 Introduction to C++

Caught you sleeping? Is your answer?
Who told you that the += is a compound operator? You were warned at Chapter 4 that the =+ in a compound operator comes, weren't you? Therefore, the statement sum += 20; is equivalent to sum +=20, which merely assigns 20 to sum, and that is the output value. Had I written sum += 20, the program would display 80 indeed.

Basically, the main purpose of this example is to show you when reading code, even if it is a few lines, minutes of thousands, it is very easy to skip a simple bug. Sometimes, the easier you insert a bug, the harder it is to fix. Remember, when writing code you should be particularly concentrated, cautious, and in a good mood. Continue with the exercises; watch out for the next traps.

# EXERCISES

C.6.14 What is the output of the following program?

```
#include <iostream>
int main()
{
    int i = 4, j = 3;
    while (i >> 1)
    {
        i--;
        while (!j)
        {
            std::cout << "One ";
            j--;
            if (i == 1)
                break;
        }
        j += 2;
    }
    std::cout << j << '\n';
}
```

Answer: As the nested for loops, each iteration of the outer while loop triggers the execution of the nested loop. Note that while(i >> 1) is equivalent to while(i != 0), that is, it is checked whether the value of one bit shifted to the right is Not 0. Also, while(!j) is equivalent to while(j%i == 0). Let's trace the first iteration of the outer loop:

First iteration of the outer loop: Since i is 4, the condition is true, so the inner loop is executed.
First iteration of the inner loop: Since i and j are both 3 the condition (!j) is true, so the program displays One and j becomes 2. As we've, the break statement terminates the loop in which it is contained.

Second iteration of the inner loop: Since the condition is false, the loop terminates. Then, j becomes 4.

Eventually, the program outputs: One One One 6