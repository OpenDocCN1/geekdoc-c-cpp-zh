
强制转换运算符是通过将任何类型的名称放在括号中形成的。该运算符是一种一元运算符（即，只接受一个操作数的运算符）。Java 还支持加号（+）和减号（–）的一元版本，因此你可以写出像 -7 或 +5 这样的表达式。强制转换运算符从右向左结合，并且与其他一元运算符（如一元 + 和一元 -）具有相同的优先级。这个优先级比乘法运算符 *、/ 和 % 高一级。（参见附录 A 中的运算符优先级表。）在我们的优先级表中，我们用 (type) 表示强制转换运算符，以表明任何类型名称都可以用来构成强制转换运算符。

第 77 行显示班级平均分。在此示例中，我们显示四舍五入到百分位的班级平均分。printf 格式控制字符串中的格式说明符 %.2f 表示变量 average 的值应显示到小数点后两位精度——由格式说明符中的 .2 表示。在类 GradeBookTest（图 4.10）的示例执行期间输入的三个成绩总计为 257，这得出平均值 85.666666....。printf 方法使用格式说明符中的精度将数值舍入到指定的位数。在此程序中，平均值被舍入到百分位，并显示为 85.67。

``` 
1 // Fig. 4.10: GradeBookTest.java
2 // Create GradeBook object and invoke its determineClassAverage method.
3
4 public class GradeBookTest
5 {
6     public static void main( String[] args )
7     {
8         // create GradeBook object myGradeBook and
9         // pass course name to constructor
10        GradeBook myGradeBook = new GradeBook(
11            "CS101 Introduction to Java Programming" );
12
13        myGradeBook.displayMessage(); // display welcome message
14        myGradeBook.determineClassAverage(); // find average of grades
15    } // end main
16 } // end class GradeBookTest
```

Welcome to the grade book for
CS101 Introduction to Java Programming!

Enter grade or -1 to quit: 97
Enter grade or -1 to quit: 88
Enter grade or -1 to quit: 72
Enter grade or -1 to quit: -1

Total of the 3 grades entered is 257
Class average is 85.67

图 4.10 | GradeBookTest 类创建了类 GradeBook（图 4.9）的一个对象，并调用其 determineClassAverage 方法。

## 4.10 算法制定：嵌套控制语句

对于下一个示例，我们再次使用伪代码和自顶向下、逐步细化来制定一个算法，并编写相应的 Java 程序。我们已经看到控制语句可以一个接一个地堆叠（顺序执行）。在本案例研究中，我们考察控制语句可以连接的另一种也是唯一的结构化方式——即，将一个控制语句嵌套在另一个控制语句内。

考虑以下问题描述：

一所大学开设了一门课程，帮助学生备考房地产经纪人的州执业资格考试。去年，完成这门课程的学生中有十人参加了考试。该大学想知道其学生在考试中的表现如何。要求你编写一个程序来汇总结果。你得到了一份包含这 10 名学生的名单。每名学生名字旁边写着 1（如果该学生通过了考试）或 2（如果该学生未通过）。

你的程序应按如下方式分析考试结果：

- 1. 输入每个测试结果（即 1 或 2）。每次程序请求另一个测试结果时，在屏幕上显示消息“Enter result”。
- 2. 统计每种类型的测试结果数量。
- 3. 显示测试结果的摘要，指出通过的学生人数和未通过的学生人数。
- 4. 如果超过八名学生通过考试，则打印消息“Bonus to instructor!”。

仔细阅读问题描述后，我们得出以下观察结果：

- 1. 程序必须处理 10 名学生的测试结果。可以使用计数器控制循环，因为测试结果的数量是事先已知的。
- 2. 每个测试结果都有一个数值——要么是 1，要么是 2。每次读取测试结果时，程序必须确定它是 1 还是 2。我们在算法中测试是否为 1。如果数字不是 1，我们假定它是 2。（练习 4.24 考虑了这种假设的后果。）
- 3. 使用两个计数器来跟踪考试结果——一个用于统计通过考试的学生人数，一个用于统计未通过的人数。
- 4. 程序处理完所有结果后，必须判断是否超过八名学生通过了考试。

让我们继续使用自顶向下、逐步细化。首先用伪代码表示顶层：

分析考试结果并决定是否应支付奖金

同样，顶层是整个程序的完整表示，但在伪代码自然演变为 Java 程序之前，可能还需要进行几次细化。

我们的第一次细化是

初始化变量
输入 10 个考试结果，并统计通过和未通过的人数
打印考试结果摘要，并决定是否应支付奖金

这里，尽管我们已经有了整个程序的完整表示，但仍需要进一步细化。我们现在确定具体的变量。需要计数器来记录通过和未通过的人数，一个计数器将用于控制循环过程，一个变量用于存储用户输入。存储用户输入的变量将通过声明来体现，这些声明使用 Java 将变量初始化合并到声明中的能力（passes 被赋为 0，failures 为 0，studentCounter 为 1）。循环程序可能需要在每次重复开始时进行初始化——通常通过赋值语句而不是声明来执行。

错误预防提示 4.3
在声明局部变量时对其进行初始化，有助于避免由于尝试使用未初始化变量而可能产生的编译错误。虽然 Java 不要求将局部变量初始化合并到声明中，但确实要求局部变量在表达式中使用其值之前进行初始化。

while 语句（第 19–33 行）循环 10 次。在每次迭代中，循环输入并处理一个考试结果。注意，用于处理每个结果的 if…else 语句（第 26–29 行）嵌套在 while 语句中。如果结果是 1，if…else 语句递增 passes；否则，它假定结果是 2 并递增 failures。第 32 行在循环条件于第 19 行再次测试之前递增 studentCounter。在输入 10 个值后，循环终止，第 36 行显示通过和未通过的人数。第 39–40 行的 if 语句确定是否有超过八名学生通过了考试，如果是，则输出消息“Bonus to instructor!”。

``` 
1 // Fig. 4.12: Analysis.java
2 // Analysis of examination results using nested control statements.
3 import java.util.Scanner; // class uses class Scanner
4
5 public class Analysis
6 {
7     public static void main( String[] args )
8     {
9         // create Scanner to obtain input from command window
10        Scanner input = new Scanner( System.in );
11
12        // initializing variables in declarations
13        int passes = 0; // number of passes
14        int failures = 0; // number of failures
15        int studentCounter = 1; // student counter
16        int result; // one exam result (obtains value from user)
17
18        // process 10 students using counter-controlled loop
19        while ( studentCounter <= 10 )
20        {
21            // prompt user for input and obtain value from user
22            System.out.print( "Enter result (1 = pass, 2 = fail): " );
23            result = input.nextInt();
24
25            // if...else is nested in the while statement
26            if ( result == 1 )            // if result 1,
27                passes = passes + 1;      // increment passes;
28            else                        // else result is not 1, so
29                failures = failures + 1; // increment failures
30
31            // increment studentCounter so loop eventually terminates
32            studentCounter = studentCounter + 1;
33        } // end while
34
35        // termination phase; prepare and display results
36        System.out.printf( "Passed: %d\nFailed: %d\n", passes, failures );
37
38        // determine whether more than 8 students passed
39        if ( passes > 8 )
40            System.out.println( "Bonus to instructor!" );
41    } // end main
42 } // end class Analysis
```

``` 
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 9
Failed: 1
Bonus to instructor!
```

图 4.12 | 使用嵌套控制语句分析考试结果。（第 2 部分，共 3 部分。）

- 1 将 passes 初始化为零
- 2 将 failures 初始化为零
- 3 将学生计数器初始化为 1
- 4
- 5 当学生计数器小于或等于 10 时
- 6 提示用户输入下一个考试结果
- 7 输入下一个考试结果
- 8
- 9 如果学生通过
- 10 将 passes 加 1
- 11 否则
- 12 将 failures 加 1
- 13
- 14 将学生计数器加 1
- 15
- 16 打印 passes 的数量
- 17 打印 failures 的数量
- 18
- 19 如果超过八名学生通过
- 20 打印“Bonus to instructor!”

图 4.11 | 考试结果问题的伪代码。

