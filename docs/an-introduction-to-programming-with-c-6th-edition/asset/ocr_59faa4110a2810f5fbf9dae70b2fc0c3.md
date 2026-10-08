# Answers to Chapter 12 Mini-Quizzes

# Mini-Quiz 12-1

+   1. b. int quantities[4][2] = {0};

+   2. 20

+   3. quantities[0][0]

+   4. quantities[3][1]

+   5. quantities[0][1] = 5;

# Mini-Quiz 12-2

+   1. d. total += purchases[1][0];

+   2. c. if (scores[2][3] > 25)

+   3. bonus = sales[0][1] * .15;

+   4. a. if (row >= 0 && row < 10)

# Answers to Chapter 12 Labs

# LAB 12-1 Stop and Analyze

+   1. 34000

+   2. The total sales made in February can be calculated by adding the contents of the company[0][1] element to the contents of the company[1][1] element.

3. The highest row subscript in the company array is 1. The highest column subscript is 5.

4. The January international stores are stored in the company[1][0] element.

```
int location = 0;
while (location < 2)
  for (int month = 0; month < 6; month += 1)
    companySales += company[location[month];
  //end for
  location += 1;
//end while
```