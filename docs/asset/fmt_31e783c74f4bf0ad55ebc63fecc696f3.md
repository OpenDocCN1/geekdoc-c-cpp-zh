
```cpp
    cout << "Enter a failure time (eof char to quit): ";

    cin >> failureTime;

    if (cin.eof()) break;

    failureTimeSum += failureTime;

    numComponents++;

}

if (numComponents != 0)

    cout << "\nThe mean failure time of the "

         << numComponents << " components is "

         << failureTimeSum / numComponents << endl;

else

    cerr << "\nNo failure times to process!\n";

}
```

## 示例运行：

```text
Computing Component Mean Time to Failure

Enter a failure time (eof char to quit): 2.3
Enter a failure time (eof char to quit): 2.4
Enter a failure time (eof char to quit): 2.5
Enter a failure time (eof char to quit): 2.6
Enter a failure time (eof char to quit): 2.1
Enter a failure time (eof char to quit): ^d
The mean failure time of the 5 components is 2.38
```

使用`eof`标记作为哨兵有两个缺点。第一个是它依赖于平台，即取决于所使用的特定操作系统。第二个是，如第 7.3 节所述，如果我们希望在读取`eof`标记后读取任何值，则必须调用`istream`函数成员`clear()`来重置状态标志。

## 9.5.4 输入循环：查询方法

前面每种输入循环都有其缺点。计数循环方法要求事先知道要输入值的数量。哨兵方法只能用于存在合适哨兵值的问题中。`eof`标记依赖于平台。我们考虑的最后一种方法是，在每次重复结束时查询用户以确定是否还有更多数据需要处理。虽然并非没有缺点，但这种方法是最广泛适用的。

示例 9.10 中的程序是使用这种查询方法的前述平均失效时间程序的修改。在用户输入数据值后，程序会询问

```text
Do you have more data to enter (y or n)?
```

然后从键盘读取用户的响应。如果是`y`或`Y`，则读取另一个数据值。这会一直继续，直到用户回答的不是`y`或`Y`为止，并且循环条件

```cpp
response == 'y' || response == 'Y'
```

然后终止重复。

## 示例 9.10 查询方法

```cpp
/* This program uses a query-controlled loop to process a collection of failure times and find the mean time to failure.

    Input:  a collection of component failure times and user's

            response to "more data?" query

    Output: prompts and the average of the failure times

--------------------------------------------------------------------------*/

#include <iostream>          // <<, >>, cout, cin

using namespace std;

int main()

{

    cout << "Computing Component Mean Time to Failure\n\n";

    int numComponents;

    double failureTime,

           failureTimeSum = 0.0;

    char response;

    do

    {

        cout << "\nEnter a failure time: ";

        cin >> failureTime;

        failureTimeSum += failureTime;

        numComponents++;

        cout << "Do you have more data to enter (y or n)? ";

        cin >> response;

    }

    while (response == 'y' || response == 'Y');

    cout << "\nThe mean failure time of the "

         << numComponents << " components is "

         << failureTimeSum / numComponents << endl;

}
```

### SAMPLE RUN:

```text
Computing Component Mean Time to Failure

Enter a failure time: 2.3
Do you have more data to enter (y or n)? y

Enter a failure time: 2.4
Do you have more data to enter (y or n)? y

Enter a failure time: 2.5
Do you have more data to enter (y or n)? y

Enter a failure time: 2.6
Do you have more data to enter (y or n)? y

Enter a failure time: 2.1
Do you have more data to enter (y or n)? n

The mean failure time of the 5 components is 2.38
```

在合理假设至少有一个数据值需要输入和处理的问题中，查询和相应的循环条件放在循环底部，使其成为后测循环。⁵ 这提示了查询控制输入循环的以下模式：

### 查询控制输入循环模式

```cpp
char response;

do
{
    Display a prompt for a data value.
    Read the Value to be processed.
    Process the Value.
    Display a query that asks if there is more data.
    Input the user's response (y or n)
}
while ((response != 'n' && (response != 'N')));
```

⁵ 若要允许不输入和处理任何值，可使用无限循环：

```cpp
for (;;)
{
    cout << "\nDo you wish to continue (y or n)? ";
    char response;
    cin >> response;
    if (response == 'n' || response == 'N') break;
    cout << "\nEnter a value: ";
    double value;
    cin >> value;
    // process value
}
```

### 9.5.4.1 查询函数

执行查询的代码往往会使循环变得杂乱，从而可能掩盖程序的结构，特别是当查询较长时，也许是由于向用户提供了特殊说明。避免这种情况的一种方法是使用如下的查询函数来执行查询、读取用户的响应，并根据响应返回 true 或 false，从而隐藏实际执行查询的代码：

```cpp
bool moreData()
{
    char answer;
    cout << "Do you have more values to enter (y or n)? ";
    cin >> answer;
    return (answer == 'y') || (answer == 'Y');
}
```

由于它返回布尔值，因此对该查询函数的调用可作为循环条件使用。例如，我们可以修改示例 9.10 的平均失效时间程序，使用查询函数`moreData()`来控制输入循环：

```cpp
int main()
{
    .
    .
    .
    do
    {
        cout << "\nEnter a failure time: ";
        cin >> failureTime;
        failureTimeSum += failureTime;
        numComponents++;
    }
    while ( moreData() );
    .
    .
    .
}
```

每次执行到达循环条件时，都会调用函数`moreData()`。它查询用户，读取响应，如果响应为`y`或`Y`则返回 true，否则返回 false。如果`moreData()`返回 true，则`do`循环的主体会被重复，但如果返回 false，则终止重复。

```text
initialization statements

Loop
    statement₁
    .
    .
    .
    statementₙ
End loop
```

最后，制定适当的终止条件。然后，确定它在循环中的放置位置将决定使用哪种循环：

- 循环开头，则为预测循环；选择 while 循环；
- 循环底部，则为后测循环；选择 do 循环；
- 语句列表内部，则为中途测试循环；选择带有 if-break（或 if-return）组合的无限循环。

为了演示此过程，让我们再次回顾第 9.3 节中的弹跳球问题。使用通用循环，我们可能会使用以下作为算法的第一个版本：

- 1. 将 `bounce` 初始化为 0。
- 2. 输入 `height` 的值并显示它。
- 3. 循环
  - a. 用 `height` 除以 2 的结果替换 `height`。
  - b. 将 `bounce` 增加 1。
  - c. 显示 `bounce` 和 `height`。
  - 结束循环

作为循环的终止条件，我们可以使用

```cpp
height < SMALL_NUMBER
```

因为当 `height` 小于某个 `SMALL_NUMBER` 时应停止重复。然而，用户可能为 `height` 输入零或负值，在这种情况下不应执行循环体。因此，我们应在进入循环时立即评估此条件：

- 1. 将 `bounce` 初始化为 0。
- 2. 输入 `height` 的值。

# 章节总结

# 关键术语

- analysis of algorithms
- break statement
- continue statement
- counting (or counter-controlled) loops
- do loop
- do statement
- end-of-data flag
- end-of-file mark
- for loop
- forever loop
- grows linearly
- if-break combination
- indefinite loop
- initialization list
- nested loops
- one-trip behavior
- posttest loop
- pretest loop
- query-controlled loop
- query function
- sentinel
- test-at-the-bottom loop
- termination condition
- trace table
- while loop
- zero-trip behavior

# 注释

- 追踪表是追踪循环行为的有用工具（尤其在调试时）。
- for 语句可通过使用适当的增量表达式以任意增量遍历值范围。
- 不定循环可在 C++ 中使用没有循环条件的 for 语句实现——`for(;;){ ... }`——或可使用形式为 `while(true){ ... }` 的 while 语句。
- 无限循环在终止条件为假时继续重复，在该条件为真时终止重复。
- break 语句可用于终止封闭循环的执行。它终止最内层的封闭循环。
- 在某些情况下，return 语句是用于终止函数执行并返回到调用函数的 break 的有用替代方案。
- continue 语句可用于跳过当前迭代的其余部分并开始新的迭代。

- *while* 循环是预测（或测试在顶部）循环。它只要条件为真就继续重复，在条件为假时终止重复。while 循环具有 *零次遍历* 行为。

- *do* 循环是后测（或测试在底部）循环。由于其循环体在测试循环条件之前总是至少执行一次，因此说它具有 *一次遍历* 行为。

- 三种常见的输入循环是：

  - *计数* 循环，其中输入项的数量事先已知；
  - *哨兵控制* 循环，其中结束数据标志（或哨兵）表示数据的结束；
  - *查询控制* 循环，其中询问用户是否还有更多数据。

- 以下准则可能有助于决定使用哪种循环：

  1. 如果算法需要遍历某个固定值范围，请使用计数循环。
  2. 如果需要通用循环，请使用通用不定循环来制定算法。然后确定终止条件应放在何处。如果在开头，使用 while 循环；如果在结尾，使用 do 循环；如果在其他位置，使用带有 if-break 或 if-return 的无限循环。

# 风格和设计提示

在本教材中，我们对本章讨论的重复语句采用以下格式约定。

- for、while、do 和 forever 循环中的语句会被缩进。如果语句是复合语句，花括号与 for、while 或 do 对齐，块内的语句会被缩进。在 do 循环中，do 与其对应的 while 对齐。

```cpp
for (...)

    statement

while(loop_condition)

    statement
```

```cpp
for (...)

{

    statement₁

    ...

    statementₙ

}

while(loop_condition)

{

    statement₁

    ...

    statementₙ

}
```

and thus will display only a single value,

```cpp
100
```

Likewise, the statement that increments count in the following is outside the body of the loop:

```cpp
int count = 1;

while (count <= 10)

    cout << count << " " << count*count << endl;

    count++;
```

and an infinite loop results:

```cpp
1 1

1 1

1 1

.

.
.
```

4. 在 do 循环中，结束的 `while (loop_condition)` 必须后跟一个分号。

5. 在 for 循环中，控制变量以及循环条件中的变量通常不应在循环体内部被修改，因为其目的是遍历指定范围的连续值。否则可能会产生奇怪且不期望的结果。

6. 循环条件中每次使用等号运算符都应仔细检查，以确保没有使用赋值运算符。使用 `=` 而不是 `==` 是最容易犯的错误之一。以下示例说明了此错误：

```cpp
do
{

    // ... do some processing ...

    cout << "Do you wish to continue (y or n)? ";

    cin >> answer;

}

while (answer = 'y');
```

- a. 循环条件是一个赋值，将 `answer` 设置为 `y`（它不是比较）；
- b. 赋值运算符（`=`）会产生其结果所赋的值；
- c. 此赋值因此产生值 121（字符 `y` 的 ASCII 值）；并且
- d. C++ 将任何非零值视为 `true`。

## Programming in C++ for Engineering and Science

同样，永远循环

```cpp
for
{

cout << "\nPlease enter an integer value (0 to quit): ";

cin >> value;

if (value = 0) break;

// ... do something with value ...

}
```

