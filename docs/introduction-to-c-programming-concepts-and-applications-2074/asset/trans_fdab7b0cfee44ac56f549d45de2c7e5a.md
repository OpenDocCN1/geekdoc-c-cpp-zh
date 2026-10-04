

一旦你使用自顶向下设计将程序分解后，就可以开始编码了。开始时，这是一个很好的时机，将你一直在生成的伪代码转换为注释，为每个部分生成注释。注释将有助于指导你的代码，并为代码的每个部分提供解释，无论是在编写代码期间还是之后。

考虑到树状层次结构，根节点成为程序的整体注释（2）。下一层级，根的子节点，每个都有自己的注释。因为这些处于层次结构的较高层级并且将是主要部分，所以以某种方式将其标记出来是有意义的——例如，使用星号（a）。

然后，你可以将其细分为下一层级。同样，你将每个节点转换为新的注释。在这种情况下，你可以使用几个星号来表明这些不是层次结构的最基本层级（b）。

然后，你可以从那里继续到甚至下一层级，将节点转换为注释（c）。

每一个仍然相当自解释。一旦你为整个程序完成了这一步，就该开始编写代码了。

```
1 // Program Fragment 11_1c
2 // Program to Predict Electricity Usage
3 #include <iostream>
4 #include <vector>
5 #include <fstream>
6 #include <string>
7 using namespace std;
8
9 int main() {
10 /** Read Past Data *****/
11 /** Read Electricity Data ***/
12 /* Open File */
13 /* Loop Through All Lines /
14 /* Store Data and Metering in Parallel Vectors */
15
16 /** Read Past Weather Data ***/
17
18 /** Read Past Individual Schedule ***/
19
20 ***** Get Detail To Predict *****/
22
23
24 ***** Calculate Predicted Usage *****/
25
26
27 ***** Present Prediction *****/
28
29 }
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_126_0.png)

## INCREMENTAL DEVELOPMENT

当你开发软件时，你希望逐块构建软件，并且每放好一块时，你都希望确保有一个稳定的结构——虽然不完整但能正常运行。你将能够看到每块是否工作并且在进行中得到测试。如果发现一切都不工作，你可以退一步并返回到稳定的软件。

这就是为什么你应该使用增量开发方法，在这种方法中，你编写一点代码，直到你确信到目前为止的一切都在工作，再编写更多代码，依此类推。这样你对已有内容就会有信心。

不幸的是，当程序员——即使是有经验的——构建更大的软件时，他们会编写大量代码，只在最后才认为所有部分都已到位，然后尝试测试它。如果一切真的有效，极其罕见地才能一次做对。相反，在某个阶段，他们犯了错误，整个程序就崩溃了。尝试找到那个错误很困难，有时即使修复了那个错误，还有其他错误，你无法确定是否真的解决了问题。

在这种情况下，提前为每个部分设计整个程序并写出注释是可以的。但在编码时，你希望编写想要实现的小块并测试已验证的内容。一般来说，这意味着你必须按顺序编写代码，一旦开始编写函数，就必须完全按此顺序进行。

在此示例中，你遇到的第一个部分是读取过去数据的一部分，在那里你将读取过去的用电数据并前往打开文件（d）。这意味着你声明一个 ifstream（13），然后为输入打开它（14）。请注意，你还写了一行代码来关闭它（17）。

| 1 // Program Fragment 11_1_d |
| 2 // Program to Predict Electricity Usage |
| 3 #include <iostream> |
| 4 #include <vector> |
| 5 #include <fstream> |
| 6 #include <string> |
| 7 using namespace std; |
| 8 |
| 9 int main() { |
| 10 /** Read Past Data *** |
| 11 /** Read Electricity Data ***/ |
| 12 /* Open File */ |
| 13 ifstream electricfile; |
| 14 electricfile.open("MeterReadings.dat", |
| 15 fstream::in); |
| 16 /* Loop Through All Lines */ |
| 17 /* Store Date and Meter Reading in Parallel |
| 18 Vectors */ |
| 19 electricfile.close(); |
| 20 /** Read Weather Data *** |
| 21 /** Read Past Individual Schedule *** |
| 22 |
| 23 |
| 24 ***** Get Detail To Predict *****/ |
| 25 |
| 26 |
| 27 |
| 28 |
| 29 |
| 30 ***** Calculate Predicted Usage *****/ |
| 31 |
| 32 ***** Present Prediction *****/ |
| 33 }

增量开发是开发大型软件的关键部分。几乎不可能在没有它的情况下开发大型程序。

在编写完此内容后，在继续下一个部分之前，你希望停下来测试你所拥有的内容，确保没有拼写错误或某些语句格式不正确。

一旦完成，就该编写并检查你的下一个部分了——遍历程序的所有行（e）。

在这种情况下，你假设文件由多行组成，每行包含一个由字符串给出的日期和一个由整数给出的电表读数。因此，要遍历文件中的所有行，你需要有两个变量，分别标记为 date（16）和 meter（17）。你将尝试从文件中读取它们（18）并循环直到到达文件末尾（19）。在循环内部，你将读取下一行（22）。

循环内部，你还希望每次都发生的事情，即将日期和读数添加到向量中（20）。但你暂时不会编写它；你将测试目前拥有的内容。

为了测试，你可以在每行读取的内容中加入一些输出语句。这总比没有好，但使用调试器还有另一种可用的选项。

```
// Program Fragment 11_1_e
// Program to Predict Electricity Usage
#include <iostream>
#include <vector>
#include <fstream>
#include <string>
using namespace std;

int main() {
    **** Read Past Data ****
    *** Read Past Electricity Data ***/
    /* Open File */
    fstream electricfile;
    electricfile.open("MeterReadings.dat", fstream::);
    /* Loop Through All Lines */
    string date;
    int meter;
    electricfile >> date >> meter;
    while (electricfile.get()) {
        /* Store Date and Meter Reading in Parallel Vectors */
        electricfile >> date >> meter;
    }
    electricfile.close();
}
*** Read Past Weather Data ***/
*** Read Past Individual Schedule ***/\n***** Get Detail To Predict *****/

***** Calculate Predicted Usage *****/

***** Present Prediction *****/
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_128_0.png)

## DEBUGGER TOOL

IDE 使访问和使用调试器工具变得容易。还有其他调试器，但最容易使用的是 IDE 内包含的那些。这里使用的是 Visual Studio 中的调试器。

随着你致力于开发更大的程序，使用 IDE 来帮助检查程序在进展过程中的状态，确保程序按预期工作，这一点至关重要。

不幸的是，调试器并不是一个消除程序中错误的东西。事实上，调试器让你一次一步地逐步执行程序的指令，并在该点检查程序中所有内容的状态。

断点是代码中你希望停止执行的位置，以便更仔细地检查代码。当你在调试器中运行程序时，它会像期望的那样，直到你遇到断点。执行将在断点所在行的正前方暂停。是一个“中断”，而不是执行的行。如果你没有设置断点，代码将一直运行到底。这就是你到目前为止所看到的。

在 Visual Studio 中，要设置断点，你点击最左侧区域的线条，在那里你想要设置。

如果你在第一个计数语句处设置断点，这会在该行放置一个红色圆圈。（在 Xcode 中，你只需点击代码行的垂直区域，一个蓝色标记就会出现以显示断点）。

调试器内部有许多工具可以帮助开发人员仔细检查代码。但只有几个简单的部分就足以使调试器非常有用，即使你需要调试器的每个功能，这些也仍占你所做工作的 90%。这些功能是断点、Step Over 和 Step Into 操作，以及变量值。

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_129_0.png)

为了使用调试器，代码必须以所谓的调试模式编译，这会自动添加一些额外的东西以使调试器工作。但这种模式也使代码的效率低于在完全调试后以更高效的发布模式编译时的效率。

由于大多数开发都在调试模式下进行，因此这是 Visual Studio 和 Xcode 中编译的默认模式。

Lecture 11 | Top-Down Design and Using a C++ Debugger

