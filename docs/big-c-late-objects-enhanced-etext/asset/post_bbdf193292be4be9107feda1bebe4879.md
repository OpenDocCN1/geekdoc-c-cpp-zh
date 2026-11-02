
## Step 7 Implement the loop in C++.

Here's the loop for our example. Exercise E4.4 asks you to complete the program.

```cpp
double highest_value;
cin >> highest_value;
int highest_month = 1;
for (int current_month = 2; current_month <= 12; current_month++)
{
    double next_value;
    cin >> next_value;
    if (next_value > highest_value)
    {
        highest_value = next_value;
        highest_month = current_month;
    }
}
cout << highest_month << endl;
```

## WORKED EXAMPLE 4.1

### Credit Card Processing

Learn how to use a loop to remove spaces from a credit card number. See your E-Text or visit wiley.com/go/bc103.

![](img/d61019b035dd82beb581604273c0ee6b_199_0.png)

![](img/d61019b035dd82beb581604273c0ee6b_199_1.png)

## 4.8 Nested Loops

When the body of a loop contains another loop, the loops are nested. A typical use of nested loops is printing a table with rows and columns.

In Section 3.4, you saw how to nest two if statements. Similarly, complex iterations sometimes require a nested loop: a loop inside another loop statement. When processing tables, nested loops occur naturally. An outer loop iterates over all rows of the table. An inner loop deals with the columns in the current row.

In this section you will see how to print a table. For simplicity, we will simply print powers x^n, as in the table below.

Here is the pseudocode for printing the table:

- Print table header.
- For x from 1 to 10
  - Print table row.
- Print endl.

| x^1 | x^2 | x^3 | x^4 |
|---|---|---|---|
| 1 | 1 | 1 | 1 |
| 2 | 4 | 8 | 16 |
| 3 | 9 | 27 | 81 |
| ... | ... | ... | ... |
| 10 | 100 | 1000 | 10000 |

The hour and minute displays in a digital clock are an example of nested loops. The hours loop 12 times, and for each hour, the minutes loop 60 times.

![](img/d61019b035dd82beb581604273c0ee6b_200_0.png)

We say that the inner loop is *nested* inside the outer loop (see Figure 7).

![](img/d61019b035dd82beb581604273c0ee6b_200_1.png)

**Figure 7** Flowchart of a Nested Loop

There are 10 rows in the outer loop. For each x, the program prints four columns in the inner loop. Thus, a total of 10 × 4 = 40 values are printed. Following is the complete program. Note that we also use loops to print the table header. However, those loops are not nested.

## 4.9 Problem Solving: Solve a Simpler Problem First

When developing a solution to a complex problem, first solve a simpler task.

As you learn more about programming, the complexity of the tasks that you are asked to solve will increase. When you face a complex task, you should apply an important skill: simplifying the problem, and solving the simpler problem first.

This is a good strategy for several reasons. Usually, you learn something useful from solving the simpler task. Moreover, the complex problem can seem unsurmountable, and you may find it difficult to know where to get started. When you are successful with a simpler problem first, you will be much more motivated to try the harder one.

It takes practice and a certain amount of courage to break down a problem into a sequence of simpler ones. The best way to learn this strategy is to practice it. When you work on your next assignment, ask yourself what is the absolutely simplest part of the task that is helpful for the end result, and start from there. With some experience, you will be able to design a plan that builds up a complete solution as a manageable sequence of intermediate steps.

Let us look at an example. You are asked to arrange pictures, lining them up along the top edges, separating them with small gaps, and starting a new row whenever you run out of room in the current row.

![](img/d61019b035dd82beb581604273c0ee6b_203_0.png)

National Gallery of Art (see Credits page for details.)

We use the Picture type of Worked Example 4.2. The add member function can be used to add one picture to another:

```cpp
pic.add(pic2, x, y);
```

The second picture is added so that its top-left corner is at the given x and y position. The original picture grows to hold all pixels of the added picture. We will use this member function repeatedly in order to build up the result.

Instead of tackling the entire assignment at once, here is a plan that solves a series of simpler problems.

- 1. Draw one picture.

![](img/d61019b035dd82beb581604273c0ee6b_203_1.png)

Make a plan consisting of a series of tasks, each a simple extension of the previous one, and ending with the original problem.

- 2. Draw two pictures next to each other.

![](img/d61019b035dd82beb581604273c0ee6b_204_0.png)

- 3. Draw two pictures with a gap between them.

![](img/d61019b035dd82beb581604273c0ee6b_204_1.png)

- 4. Draw all pictures in a long row.

![](img/d61019b035dd82beb581604273c0ee6b_204_2.png)

- 5. Draw a row of pictures until you run out of room, then put one more picture in the next row.

![](img/d61019b035dd82beb581604273c0ee6b_204_3.png)

Let's get started with this plan.

- 1. The purpose of the first step is to become familiar with the Picture type. As it turns out, the pictures are in files a.png ... t.png. Let's load the first one:

```cpp
Picture pic("a.png");
pic.save("gallery.png");
```

That's enough to produce the picture.

![](img/d61019b035dd82beb581604273c0ee6b_204_4.png)

- 2. Now let's put the next picture after the first. We need to position it at the rightmost x-coordinate of the preceding picture.

![](img/d61019b035dd82beb581604273c0ee6b_204_5.png)

```cpp
Picture pic("a.png");
Picture pic2("b.png");
pic.add(pic2, pic.width(), 0);
```

- 3. The next step is to separate the two by a small gap when the second is added:

![](img/d61019b035dd82beb581604273c0ee6b_205_0.png)

```cpp
const int GAP = 10;

Picture pic("a.png");
Picture pic2("b.png");
pic.add(pic2, pic.width() + GAP, 0);
```

- 4. Now let's put all pictures in a row. Read the pictures in a loop, and then put each picture to the right of the one that preceded it. In the loop, you need to track the x-coordinate at which the next image should be inserted.

![](img/d61019b035dd82beb581604273c0ee6b_205_1.png)

```cpp
const int GAP = 10;
const string names = "abcdefghijklmnopqrst";
const int PICTURES = names.length();

Picture pic("a.png");
int x = pic.width() + GAP;
for (int i = 1; i < PICTURES; i++)
{
    Picture pic2(names.substr(i, 1) + ".png");
    pic.add(pic2, x, 0);
    x = x + pic2.width() + GAP;
}
```

- 5. Of course, we don't want to have all pictures in a row. The right margin of a picture should not extend past MAX_WIDTH.

```cpp
if (x + pic.width() < MAX_WIDTH)
{
    Place pic on current row.
}
else
{
    Place pic on next row.
}
```

If the image doesn't fit any more, then we need to put it on the next row, below all the pictures in the current row. We'll set a variable max_y to the maximum y-coordinate of all placed pictures, updating it whenever a new picture is placed:

```cpp
if (pic2.height() >= max_y)
{
    max_y = pic2.height();
}
```

![](img/d61019b035dd82beb581604273c0ee6b_206_0.png)

The following statement places a picture on the next row:

```cpp
pic.add(pic2, 0, max_y + GAP);
```

Now we have written complete programs for all preliminary stages. We know how to line up the pictures, how to separate them with gaps, how to find out when to start a new row, and where to start it.

### EXAMPLE CODE

See sec09 of your companion code for the preliminary stages of the gallery program.

### sec09/gallery6.cpp

```cpp
1 #include "picture.h"
2 #include <string>
3
4 using namespace std;
5
6 int main()
7 {
8     const int MAX_WIDTH = 720;
9     const int GAP = 10;
10    const string names = "abcdefghijklmnopqrst";
11    const int PICTURES = names.length();
12
13    // Read the first picture
14    Picture pic("a.png");
15
16    // x and y are the top-left corner of the next picture
17    int x = pic.width() + GAP;
18    int y = 0;
19
20    // max_y is the largest y encountered so far
21    int max_y = pic.height();
22    for (int i = 1; i < PICTURES; i++)
23    {
24        // Read the next picture
25        Picture pic2(names.substr(i, 1) + ".png");
26        if (x + pic2.width() >= MAX_WIDTH) // The picture doesn't fit on the row
27        {
28            // Place the picture on the next row
29            x = 0;
30            y = max_y + GAP;
31        }
```
