

```
//Get the next line of data
strcpy(bData, "");
bIndex = 0;
fin.getline(bData, MAXLEN);
}
else
{
    //This is not a comment
    //parse bData for image information
    charCount = 0;
    //look past whitespace
    while( bIndex < MAXLEN && isspace(bData[bIndex]) )
    {
        ++bIndex;
    }
    //may be the beginning of a decimal value..
    while( bIndex < MAXLEN && isdigit(bData[bIndex]) )
    {
        aNumber[charCount] = bData[bIndex];
        ++bIndex;
        ++charCount;
        if(charCount == MAXWIDTH)
        {
            cerr << "Maximum width of " << MAXWIDTH
                 << " digits was exceeded.." << endl;
            exit(1);
        }
    }
    //end while
    //look at size of aNumber...
    if(charCount > 0)
    {
        //we have image information, terminate string
        aNumber[charCount] = nullChar;
        //convert from ascii to integer
        imageInfo[infoCount] = atoi(aNumber);
        ++infoCount;
        //verify input
        switch(infoCount)
        {
            case 1:
                cout<<"a width of "<<imageInfo[infoCount-1]
                    <<" has been read." << endl;
                break;
            case 2:
                cout<<"a height of "<<imageInfo[infoCount-1]
                    <<" has been read." << endl;
                break;
            case 3:
                cout<<"a maximum color of "<< imageInfo[infoCount-1]
                    <<" has been read."<<endl;
                break;
        }
    }
else if(infoCount < 3)
{
    //aNumber has 0 digits and infoCount is < 3
    //We need more image information
    //Get next line of data and parse for image information
    strcpy(bData," ");
    bIndex = 0;
    fin.getline(bData,MAXLEN);
    //end else if
}//end else parse
while(infoCount<3 && !fin.eof());
if(infoCount < 3)
{
    cerr <<"Image information could not found"<< endl;
    exit(1);
}
//We have all of the information
//Write header to ascii file
strcpy(magicNumber,"P3");
strcat(comment," Converted from P6 to P3 by ConvertP6ToP3");
writeHeader(fout, magicNumber, comment, imageInfo[0],
            imageInfo[1], imageInfo[2]);
}
void writeHeader(ofstream& fout, char magicNumber[],
                 char comment[], int w, int h,
                 int maxPixelVal)
{
    //Write image information to output file
    fout << magicNumber << endl;
    fout << comment << newline;
    fout << w << ' ' << h << ' ' << maxPixelVal << newline;
}//end file imageFunctions.cpp
```

## 5. 测试

以下是我们解决方案的测试。我们程序的输出，以及平滑前后的冥王星图像，如下所示：

```
INGBER-MLT-1$ g++ main.cpp Pixel.cpp imageFunctions.cpp
INGBER-MLT-1$ ./a.out
enter file name Pluto.ppm
a width of 1024 has been read.
a height of 1042 has been read.
a maximum color of 255 has been read.
P3 Image written to PlutoP3Smoothed.ppm
Goodbye.
```

![](img/0235a4ea835dc4575bd036e024a533b3_602_0.png)

## 修改 10.4

- 1. 编写一个函数 `brightenImage()` 来如第 10.1 节所述亮化图像。提示用户输入一个用于亮化的小正整数值。
- 2. 编写一个函数，通过将每个像素的红色值设置为最大像素值来修改图像。
- 3. 从网络下载一张新图像。转换、亮化和平滑该图像。

## 10.5 递归

递归是解决某些类问题的强大工具，这类问题的解可以定义为一个类似但更小的问题，然后该更小的问题又可以定义为一个类似但更小的问题。将问题重新定义为更小的问题的过程持续进行，直到更小的问题具有一个唯一解，然后用该唯一解来确定整体解。

支持递归的编程语言允许函数引用或调用自身。引用自身的函数称为**递归函数**。要递归地解决问题，函数的编写方式是：每次递归函数调用自身时，都将问题减少为一个类似但更小的问题。函数继续调用自身，直到最终将小问题的一部分的唯一解返回给自身。这个唯一解沿调用链向上传递，从而确定整体解。

每次递归函数调用自身时，关于该函数实例的信息都存储在称为**堆栈**的内存部分中。回顾第 9 章，堆栈是一种先进后出（FILO）数据结构。对递归函数的每次连续调用都将信息压入堆栈。每次连续返回都会从堆栈中弹出信息。

由于堆栈大小有限，递归函数调用自身的次数存在系统相关的限制，但如果递归函数编写正确，这些限制通常不会造成困难。

递归函数需要两个代码块：

- 1. 定义终止条件或返回点的代码块，在该点返回问题较小版本的唯一解，
- 2. 将问题减少为类似但更小版本的递归代码块。

为了说明递归，我们将首先开发一个计算阶乘函数的递归算法。

### 阶乘函数

回顾一下，n!（读作 n 阶乘）定义如下：n! = n(n-1)(n-2)...(1)

其中 n 是非负整数，且按定义 0! = 1。该问题的递归定义如下：

```
f(n) = n! = \begin{cases} 1 & : n = 0 \\ n * f(n - 1) & : n > 1 \end{cases}
```

该递归定义提供了终止条件（本例中为 f(0) = 1）和递归代码块的归约语句（f(n) = n * f(n - 1)）。归约语句将求解 f(n) 的问题归约为求解 f(n - 1) 的问题，并将结果乘以 n。

为了说明，我们将使用以下步骤手动计算 5!：

```
5! = 5 * 4!
4! = 4 * 3!
3! = 3 * 2!
2! = 2 * 1!
1! = 1 * 0!
0! = 1
```

因此，我们用涉及更小阶乘的乘积定义了阶乘。更小的阶乘不断被重新定义，直到我们达到 0!。我们在最后一个方程中代入 0! 的唯一解，然后开始沿方程列表向上回溯，代入阶乘的值：

```
1! = 1 * 1
2! = 2 * 1! = 2
3! = 3 * 2! = 6
4! = 4 * 3! = 24
5! = 5 * 4! = 120
```

我们现在已经开发出计算阶乘的递归算法。

我们提供一个带有递归函数的程序来计算阶乘。阶乘值会迅速变得很大，因此我们对阶乘值使用长整型。请注意，main() 中的函数调用看起来与非递归函数的调用相同。

```
/*-----------------------------------------------------------*/
/* Program chapter10_5                                       */
/*                                                           */
/* This program calls a recursive function to                */
/* compute a factorial.                                      */
/*-----------------------------------------------------------*/
#include <iostream> //Required for cout
using namespace std;

// Function prototypes.
long factorialR(int n);

int main()
{
   // Declare objects
   int n;

   // Get user input.
   cout << "Enter positive integer: \\n";
   cin >> n;

   // Compute and print factorials.
   cout << "Recursive: " << n << "! = " << factorialR(n) << endl;

   // Exit program.
   return 0;
}
/*-----------------------------------------------------------*/
/* This function computes a factorial recursively.           */
/*-----------------------------------------------------------*/
long factorialR(int n)
{
   /* Recursive reference until n is equal to 0.              */
   if (n == 0) //Solution is known
   {
      return 1; //Return unique solution.
   }
   return n*factorialR(n - 1); //Reduce the problem
}
/*-----------------------------------------------------------*/
```

终止条件 n == 0 防止递归例程变成无限循环。递归代码块以一个不断减 1 的参数调用自身，直到参数达到零。

