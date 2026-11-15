

```
{
    max_height = height;
    max_time = time;
    }
}
// Print maximum height and corresponding time.
cout << "\nMaximum balloon height was " << setw(8)
     << max_height << " meters \n";
cout << "and it occurred at " << setw(6) << max_time
     << " hours \n";
/* Exit program. */
return 0;
}
/*---------------------------------------------*/
```

## 5. 测试

如果我们使用手动示例中的数据，则与程序有以下交互：

```
Enter initial value for table (in hours)
0
Enter increment between lines (in hours)
1
Enter final value for table (in hours)
5
```

### 气象气球信息

| 时间 (小时) | 高度 (米) | 速度 (米/秒) |
|---|---|---|
| 0 | 220.00 | 1.14 |
| 1 | 3951.88 | 0.94 |
| 2 | 6994.08 | 0.76 |
| 3 | 9414.28 | 0.59 |
| 4 | 11277.28 | 0.45 |
| 5 | 12645.00 | 0.32 |

气球最大高度为 12645.00 米，出现在 5.00 小时。

图 4.9 包含气球在 48 小时期间的高度和速度图。从图中，我们可以看到气球上升或下降的时期。

![](img/0235a4ea835dc4575bd036e024a533b3_205_0.png)

## 修改 4.3

这些问题与本节开发的打印气象气球信息表的程序有关。

- 1. 使用此程序生成一个表格，显示气象气球在发射后 4 小时开始，每 10 分钟持续 2 小时的信息。
- 2. 修改程序以包含检查，确保最终时间大于初始时间。如果不是，要求用户重新输入完整的报告信息。
- 3. 本节给出的方程仅针对 0 到 48 小时的时间开发以确保准确，因此请修改程序以向用户打印一条消息，指定 48 小时的上限。还要检查用户输入，确保其保持在适当范围内。如果有任何错误，要求用户重新输入完整的报告信息。
- 4. 如果有两个时间具有相同的最大高度，此程序将打印最大高度首次出现的时间。修改程序，使其打印最大高度最后出现的时间。

## 4.7 使用 IDE 构建 C++ 解决方案：Microsoft Visual C++

在本节中，我们使用 Microsoft Visual C++ 开发一个 C++ 解决方案，以说明嵌套控制结构的使用。我们的程序实现了分治算法来猜测 1 到 20 之间的数字。分治算法在每次迭代时通过调整定义范围的高值或低值，将可能猜测的范围分为两半。猜测始终是范围的中点。

当数字被猜中或范围中的高值小于低值时，我们的程序终止。如果用户没有正确回答每个问题，将发生第二种情况。我们的猜数字算法的伪代码如下：

```
Pseudocode
main: print greeting to user
while ((!done && high > low)
   guess = (high + low)/2
   print guess
   if guess equals number
      print number of trys required to guess number
      done = true
   else if guess is larger than number
      increment number of tries
      high = guess - 1
   else if guess is smaller than number
      increment number of tries
      low = guess + 1
end while
```

伪代码中的步骤足够详细，可以转换为 C++。我们使用 ceil() 函数和自然对数函数 log() 来预测使用分治算法猜测数字应该需要多少次尝试。

```
/***********************************************************/
/* Program chapter4_9                                      */
/* This program guesses a number between 1 and 20 inclusive. */
/***********************************************************/
#include<iostream>    //Required for cout, cin
#include<cmath>       //Required for ceil, log
using namespace std;
int main()
{
```

```
// Declare and initialize objects
int high(20), low(1), guess, count(1), ceiling;
bool done(false);
char answer;
const char YES('Y'), NO('N');

// Print greeting to user
ceiling = ( ceil(log( (double)high ) ) + 1 );
cout << "Think of a number between " << low << " and " << high
     << " and I will guess it in\n" << ceiling << " or fewer tries.  Just answer y(es) or n(o) to my questions.\n"
     << "Are you thinking of a number? " << endl;
cin >> answer;
switch(toupper(answer))
{
   case YES:
   // While number has not been guessed
   while(!done && high >= low)
   {
      guess = ( high + low)/2;
      cout << "Are you thinking of " << guess << '?' << endl;
      cin >> answer;
      switch(toupper(answer))
      {
         case YES:
            cout << "I guessed it in " << count << " tries." << endl;
            if(count > ceiling) cout << " Good pick." << endl;
            done = true;
            break;
         case NO:
            //Must guess again.
            ++count;
            cout << "Is " << guess << " larger?" << endl;
            cin >> answer;
            if(toupper(answer) == YES) high = guess - 1;
            else low = guess + 1;
            break; //case NO
         default:
            cout << "Don't support " << answer << endl;
            done = true;
         } //end switch
   } //end while
   break;
   case NO:
      cout << " OK. Goodbye. " << endl;
      break;
   default:
      cout << "Don't support " << answer << endl;
   }
   return 0;
}//end main
```

## Microsoft Visual C++

Visual C++ 是微软开发的用于设计和开发 C 和 C++ 程序解决方案的 IDE。启动 Visual C++ 应用程序时，将出现一个开始页，类似于下图所示：

![](img/0235a4ea835dc4575bd036e024a533b3_208_0.png)

来源：Microsoft® Visual Studio ®。

要创建新项目，请从窗口顶部的“文件”菜单中选择“新建项目 ...”，或从“最近的项目”窗口中选择“创建: 项目 ...”。将出现一个新项目屏幕，类似于下图所示。

![](img/0235a4ea835dc4575bd036e024a533b3_208_1.png)

对于本示例，我们将选择 Win32 控制台应用程序。我们将文件命名为 chapter4_8，并单击窗口底部的“确定 ...”按钮。将出现一个新的 Win32 应用程序向导窗口，如下图所示。

![](img/0235a4ea835dc4575bd036e024a533b3_209_0.png)

如果此时选择“完成”按钮，将创建带有预编译头的新项目。为简单起见，在本示例中，我们想要创建一个没有添加头文件的空项目，因此单击窗口底部的“下一步 >”按钮。将出现以下“完成”屏幕。

![](img/0235a4ea835dc4575bd036e024a533b3_209_1.png)

从此屏幕中，我们选择“控制台应用程序”和“空项目”，然后单击“完成”按钮。将创建一个名为 chapter4_8 的新空项目，如下图所示，在 chapter4_8 Visual C++ 项目屏幕的左窗口中。

![](img/0235a4ea835dc4575bd036e024a533b3_210_0.png)

要向项目添加新文件，请从窗口顶部的“项目”菜单中选择“添加新项”。将出现以下“添加新项”窗口：

![](img/0235a4ea835dc4575bd036e024a533b3_210_1.png)

从左窗口选择“代码”，从右窗口选择“C++ 文件 (.cpp)”。将文件命名为 main，然后单击“添加”按钮。编辑器窗口将打开。输入程序 chapter4_9 的代码，如下图所示。

![](img/0235a4ea835dc4575bd036e024a533b3_211_0.png)

从“生成”菜单中选择“生成解决方案”。如果生成成功，请从“调试”菜单中选择“启动但不调试”以执行程序。将出现一个控制台窗口，所有标准输入/输出都可以从此窗口查看。下面的屏幕图像中提供了我们程序运行的结果。数字 7 仅用了三次尝试就被猜中。是否有任何数字需要超过三次尝试才能猜中？

![](img/0235a4ea835dc4575bd036e024a533b3_211_1.png)

