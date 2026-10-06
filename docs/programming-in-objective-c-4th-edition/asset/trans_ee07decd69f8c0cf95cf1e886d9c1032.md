
对 `NSLog` 语句所做的主要更改是包含了一个字段宽度指定。字符 `%2i` 告诉 `NSLog` 例程你不仅想在该特定位置显示一个整数值，还表示要显示的整数大小在显示时至少占据两列。任何正常情况下少于两列的整数（即 0-9 之间的整数）将在显示时前带有一个空格。这被称为右对齐。

因此，通过使用 `%2i` 字段宽度指定，你可以保证至少使用两列来显示 `n` 的值；你还确保了 `triangularNumber` 的值将对齐。

## 键盘输入

程序 5.2 计算了第 200 个三角形数，不再做其他计算。但如果你想计算第 50 个或第 100 个三角形数呢？嗯，如果是那样的话，你就必须修改程序，使 `for` 循环执行正确的次数。你还需要修改 `NSLog` 语句以显示正确的消息。

更简单的解决方案可能是让程序以某种方式询问你想要计算哪个三角形数。然后，在你给出答案后，程序就可以计算所需的三角形数。你可以使用一个名为 `scanf` 的例程来实现这种解决方案。`scanf` 例程在概念上类似于 `NSLog` 例程。`NSLog` 例程用于显示值，而 `scanf` 例程的目的是允许程序员向程序中输入值。当然，如果你正在编写一个使用图形用户界面 (UI) 的 Objective-C 程序（例如 Cocoa 或 iOS 应用程序），你可能在程序中根本不会使用 `NSLog` 或 `scanf`。

程序 5.4 询问用户应该计算哪个三角形数，计算该数，然后显示结果。

## 程序 5.4

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, number, triangularNumber;

        NSLog ("@What triangular number do you want?");
        scanf("%i", &number);

        triangularNumber = 0;

        for ( n = 1; n <= number; ++n) {
            triangularNumber += n;
        }

        NSLog ("@Triangular number %i is %i\n", number, triangularNumber);
    }

    return 0;
}
```

在随后的程序输出中，用户输入的数字 **(100)** 被设为粗体，以将其与程序显示的输出区分开。

## 程序 5.4 输出

# # What triangular number do you want?
100
Triangular number 100 is 5050

根据输出，用户输入了数字 100。程序随后计算了第 100 个三角形数并在终端显示了 5050 的结果。如果用户想计算那些特定的三角形数，他们可以轻松地输入数字 10 或 30。

程序 5.4 中的第一个 `NSLog` 语句用于提示用户输入一个名称。当然，提醒用户你想要输入什么总是是好的。在打印消息后，`scanf` 例程的第一个参数是格式字符串，它不以 `@` 字符开头。与 `NSLog` 不同，后者的参数是一个 `NSString` 对象，而 `scanf` 的第一个参数是一个 C 风格字符串。正如本文前面提到的，C 风格字符字符串前面没有有 `@` 字符。

格式字符串告诉 `scanf` 从控制台（或终端窗口，如果你使用 Terminal 应用程序编译程序）读取什么类型的值。在 `NSLog` 中，使用 `%i` 字符来指定整数值。

`scanf` 例程的第二个参数指定了用户输入的值存储在何处。在这种情况下，变量前的 `&` 字符是必要的。我们并不是提供变量数字的值，而是指定我们想要将输入的值存储在哪里。现在不要担心这个，当我们在第 13 章讨论指针时，会详细地讨论这个字符（它实际上是一个运算符）。

鉴于前面的讨论，你现在可以看到程序 5.4 中的 `scanf` 调用指定要读取一个整数值并将其存储到变量 `number` 中。该值代表了用户想要计算的特定三角形数。

在用户输入此数字数字后（并按下键盘上的 Enter 键以表示数字输入完成），程序会计算所请求的三角形数。这样做的方法与程序 5.2 相同；唯一的区别是，不是使用 200 作为限制，而是使用 `number` 作为限制。

> 注意
> 在带有数字小区的键盘上按下 Enter 键可能不会导致你输入的数字发送到程序。请改用键盘上的 Return 键。

计算出所需的三角形数后，将显示结果。此时，程序的执行即告完成。

## 嵌套 for 循环

程序 5.4 为用户提供了灵活性，可以让程序计算所需的任何三角形数。但假设用户有一个需要计算五个三角形数的列表呢？在这种情况下，用户只需运行程序五次，每次输入列表中要计算的下一个三角形数。

实现相同目标的另一种方法，对于学习 Objective-C 来说也是要有趣得多的方法，是让程序来处理这种情况。这可以通过在程序中插入一个循环来重复整个系列计算五次来实现。你可以使用 `for` 语句来建立这样的循环。程序 5.5 及其输出说明了这种技术。

## 程序 5.5

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, number, triangularNumber, counter;

        for ( counter = 1; counter <= 5; ++counter ) {
            NSLog ("@What triangular number do you want?");
            scanf("%i", &number);

            triangularNumber = 0;

            for ( n = 1; n <= number; ++n ) {
                triangularNumber += n;
                NSLog ("@Triangular number %i is %i\n", number, triangularNumber);
            }
        }
    }

    return 0;
}
```

## 程序 5.5 输出

What triangular number do you want?
12
Triangular number 12 is 78

What triangular number do you want?
25
Triangular number 25 is 325

What triangular number do you want?
50
Triangular number 50 is 1275

What triangular number do you want?
75
Triangular number 75 is 2850

What triangular number do you want?
83
Triangular number 83 is 3486

该程序包含两层 `for` 语句。最外层的 `for` 语句如下：

```
for ( counter = 1; counter <= 5; ++counter )
```

这指定了程序循环将精确执行五次。`counter` 的值初始设置为 1，每次增加 1，直到它不再小于或等于 5（换句话，直到它达到 6）。

与之前的程序示例不同，变量 `counter` 在程序的其他地方都没有使用。它的功能仅仅是作为 `for` 语句中的循环计数。尽管如此，因为它是一个变量，你必须在程序中声明它。

...

在离开对 `for` 循环的讨论之前，我们应该提到在形成此循环时允许的一些语法变体。在编写 `for` 循环时，你可能会发现你想在循环开始之前初始化多个变量，或者你可能想在每次循环时评估多个表达式。你可以在 `for` 循环的任何字段中包含多个表达式，只要用逗号分隔表达式即可。例如，在 `for` 语句中：

```
for ( i = 0, j = 0; i < 10; ++i )
```
