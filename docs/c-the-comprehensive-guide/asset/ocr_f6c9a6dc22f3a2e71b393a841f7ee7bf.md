```
```cpp
{
        // block that is repeatedly executed
        sum += number;          // for the result
        number += 1;            // next number
}                              // end of the repeated block
std::cout << sum << std::endl;
}
```
```

**Listing 8.12** The loop runs 100 times.

Before the loop block is executed, the condition is checked first. Therefore, this loop will run for every number between 1 and 100 inclusive—exactly 100 times. And each individual number will be added to sum. At the end, sum contains the result of adding all numbers from 1 to 100—the task that the mathematician Gauss is said to have solved in his head within seconds in elementary school because he supposedly realized he only needed to calculate (100 · 101) / 2. Well, with the help of the computer, you are even faster than Gauss.

![](bbox=[0.143, 0.398, 0.434, 0.639])

**Figure 8.3** Flowchart of the “while” loop.

When you come up with such loops, it is very important to ensure that the condition eventually no longer holds true and the loop terminates. Here, number is a simple counting variable and is incremented within the block. Common mistakes include forgetting to increment or setting the condition incorrectly. Can you see what happens if you forget `number = number + 1`?

```
```cpp
while(number <= 100) {      // number is checked but never incremented
    sum += number;
};
```
```

This loop will run forever because number is never incremented, so the condition number <= 100 will always be true. The program will never reach the line for the output, and you