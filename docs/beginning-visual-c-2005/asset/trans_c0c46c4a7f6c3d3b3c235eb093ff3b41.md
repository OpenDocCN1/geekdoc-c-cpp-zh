
![](img/2359b0c604600c58fba3539c738a356e_337_0.png)

图 6-5

使用这个基本逻辑定义，你现在可以编写这个函数：

```
// Function to evaluate an arithmetic expression
double expr(char* str)
{
    double value = 0.0;                // Store result here
    int index = 0;                     // Keeps track of current character position

    value = term(str, index);          // Get first term
    for(;;)                            // Indefinite loop, all exits inside
{
    switch(*(str + index++))        // Choose action based on current character
    {
        case '\0':                  // We're at the end of the string
            return value;           // so return what we have got

        case '+':                   // + found so add in the
            value += term(str, index);  // next term
            break;

        case '-':                   // - found so subtract
            value -= term(str, index);  // the next term
            break;

        default:                    // If we reach here the string
            cout << endl            // is junk
                << "Arrgh!*#!! There's an error"
                << endl;
            exit(1);
    }
}
```

## 函数如何运作

考虑到这个函数是在分析你交给它的任何算术表达式（只要它使用我们的运算符子集），代码量并不多。你定义了一个 int 类型的变量 index，它跟踪你正在处理的字符串中的当前位置，并将其初始化为 0，对应于字符串中第一个字符的索引位置。你还定义了一个 double 类型的变量 value，用来累加传入函数（通过 char 数组 str）的表达式的值。

因为表达式必须至少有一个项，所以函数中的第一个动作是通过调用你尚未编写的 term() 函数来获取第一个项的值。这实际上对 term() 函数提出了三点要求：

- 1. 它应当接受一个 char* 指针和一个 int 变量作为参数，第二个参数是所提供字符串中该项第一个字符的索引。
- 2. 它应当更新传入的索引值，使其指向所找到项最后一个字符后面的那个字符。
- 3. 它应当以 double 类型返回该项的值。

程序的其余部分是一个无限 for 循环。在循环内，动作由 switch 语句决定，它受字符串中当前字符的控制。如果是 '+'，你调用 term() 函数获取表达式中下一项的值，并将其加到变量 value 中。如果是 '-'，你从变量 value 中减去 term() 返回的值。如果是 '\0'，说明你已到达字符串末尾，所以将变量 value 的当前内容返回给调用程序。如果是任何其他字符，它不应该出现在那里，所以在向用户表示不满后，你结束程序！

只要找到 '+' 或 '-'，循环就会继续。每次调用 term() 都会将 index 变量的值移动到被求值项后面的字符处，而该字符应该是另一个 '+' 或 '-'，或者是字符串结束符 '\0'。因此，函数要么在遇到 '\0' 时正常终止，要么通过调用 exit() 异常终止。当你把整个程序放在一起时，你需要记得为 <cstdlib> 头文件添加 #include 指令，该头文件提供了 exit() 函数的定义。

你也可以使用递归函数来分析算术表达式。如果你稍微换一种方式思考表达式的定义，你可以将其指定为：要么是一个项，要么是一个项后跟一个表达式。这里的定义是递归的（即定义涉及被定义的对象），这种方法在定义编程语言结构时非常常见。这个定义与第一个定义一样灵活，但以它作为基本概念，你可以得到 expr() 的递归版本，而不是像上面实现那样使用循环。你可能想在完成第一个版本后，尝试这种替代方法作为练习。

## 获取项的值

term() 函数返回一个 double 类型的项的值，并接收两个参数：正在分析的字符串和字符串中当前位置的索引。还有其他方法可以实现这一点，但这种安排非常直接。因此，你可以写下 term() 函数的原型如下：

```
double term(char* str, int& index);      // Function analyzing a term
```

你将第二个参数指定为引用。这是因为你希望函数能够修改调用程序中变量 index 的值，使其定位于输入字符串中所找到项最后一个字符后面的那个字符。你也可以将 index 作为值返回，但那样你就需要以其他方式返回项的值，所以这种安排似乎很自然。

分析项的逻辑在结构上将与表达式的类似。一个项是一个数字，可能后跟一个或多个由乘号或除号运算符与另一个数字组成的组合。你可以编写 term() 函数的定义如下：

```
// Function to get the value of a term
double term(char* str, int& index)
{
    double value = 0.0;                  // Somewhere to accumulate
                                       // the result

    value = number(str, index);          // Get the first number in the term

    // Loop as long as we have a good operator
    while((*(str + index) == '*') || (*(str + index) == '/'))
    {
        if(*(str + index) == '*')         // If it's multiply,
            value *= number(str, ++index); // multiply by next number

        if(*(str + index) == '/')         // If it's divide,
            value /= number(str, ++index); // divide by next number
    }
    return value;                        // We've finished, so return what
                                         // we've got
}
```

## 函数如何运作

你首先声明一个局部 double 变量 value，用来累加当前项的值。因为一个项必须至少包含一个数字，所以函数中的第一个动作是通过调用 number() 函数获取第一个数字的值，并将结果存储在 value 中。你隐式地假设 number() 函数接受字符串和字符串中某个位置的索引作为参数，并返回所找到数字的值。因为 number() 函数还必须更新索引到字符串中该数字之后的位置，所以当你定义该函数时，你将再次把第二个参数指定为引用。

term() 函数的其余部分是一个 while 循环，只要下一个字符是 '*' 或 '/'，循环就会继续。在循环内，如果当前位置找到的字符是 '*'，你递增变量 index 使其定位到下一个数字的开头，调用 number() 函数获取下一个数字的值，然后将 value 的内容乘以返回的值。类似地，如果当前字符是 '/'，你递增 index 变量，并将 value 的内容除以 number() 返回的值。因为 number() 函数会自动将变量 index 的值改为所找到数字后面的那个字符，所以 index 已经设置为在下一次迭代中选择字符串中下一个可用的字符。

当遇到一个不是乘号或除号运算符的字符时，循环终止，随后将变量 value 中累计的当前项的值返回给调用程序。

你需要的最后一个分析函数是 number()，它确定字符串中出现的任何数字的数值。

## 分析数字

根据你在 term() 函数中使用 number() 函数的方式，你需要用这个原型来声明它：

```
double number(char* str, int& index);  // Function to recognize a number
```

将第二个参数指定为引用，允许该函数直接更新调用程序中的参数，这正是你所需要的。

你可以在这里使用标准 C++ 库中提供的函数。<cctype> 头文件提供了一系列用于测试单个字符的函数定义。这些函数返回 int 类型的值，其中正值对应于 true，零对应于 false。其中四个函数如下表所示：

| 用于测试单个字符的 <cctype> 头文件中的函数 |  |
|---|---|
| int isalpha(int c) | 如果参数是字母，返回 true，否则返回 false。 |
| int isupper(int c) | 如果参数是大写字母，返回 true，否则返回 false。 |
| int islower(int c) | 如果参数是小写字母，返回 true，否则返回 false。 |
| int isdigit(int c) | 如果参数是数字，返回 true，否则返回 false。 |

