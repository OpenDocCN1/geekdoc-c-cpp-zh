
- 1. 使用预处理器指令开始一个新程序，以包含标准输入/输出库函数和日期时间函数
```c
#include <stdio.h>
#include <time.h>
```
- 2. 添加一个 main 函数，声明一个字符数组变量、一个 time_t 变量和一个 tm 结构体
```c
int main()
{
  char buffer[100];
  time_t elapsed;
  struct tm *now;
}
```
- 3. 接下来，在 main 函数块中，获取自 Epoch 以来经过的当前秒数
```c
elapsed = time(NULL);
```
- 4. 现在，将计数转换为本地时间组件
```c
now = localtime(&elapsed);
```
- 5. 以标准格式输出日期和时间
```c
printf("%s\n", asctime(now));
```
- 6. 然后，输出单独的日期和时间组件
```c
strftime(buffer, 100, "Today is %A, %B %d.\n", now);
printf("%s", buffer);
strftime(buffer, 100, "The time is %I:%M %p.\n", now);
printf("%s", buffer);
```
- 7. 最后，返回所需的零整数，然后保存程序文件；编译并执行程序以查看当前日期和时间信息
```c
return 0;
```

注意，在转换为本地时间时使用了 `&` 取地址运算符，以便从 time_t 数据类型获取日历时间。

![](img/d1dfb0563339ba187decb78799155b7f_154_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_154_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_154_2.png)

## 运行计时器

在事件发生前后获取当前时间意味着可以通过它们的差值计算事件的持续时间。time.h 头文件包含一个用于此目的的 difftime() 函数。该函数需要两个参数，两者均为 time_t 数据类型。它用第一个参数减去第二个参数，并返回以秒为单位的差值，但作为 double 数据类型。

time.h 头文件中的 clock() 函数提供了另一种处理时间的方法。它返回自程序开始以来使用的处理器时间，以 clock “ticks” 表示。该函数可通过运行空循环直到达到未来的时间点来“暂停”程序的执行。

![](img/d1dfb0563339ba187decb78799155b7f_155_0.png)

- 1. 使用预处理器指令开始一个新程序，以包含标准输入/输出库函数和日期时间函数
```c
#include <stdio.h>
#include <time.h>
```
- 2. 接下来，声明一个用于暂停程序的函数原型
```c
void wait( int seconds );
```
- 3. 添加一个 main 函数，声明两个 time_t 变量和一个整数变量
```c
int main()
{
    time_t go , stop ;
    int i ;
}
```
- 4. 接下来，在 main 函数块中，获取当前时间并输出一条消息
```c
go = time( NULL );
printf ( "\nStarting countdown...\n\n" );
```
- 5. 添加一个循环，在每次迭代中输出倒计时值并调用另一个函数
```c
for( i = 10 ; i > -1 ; i-- )
{
    printf ( "  %d", i );
    wait(1);
}
```
- 6. 接下来，在 main 函数块中再次获取当前时间，然后输出运行循环所花费的时间
```
stop = time( NULL );
printf("\nRuntime: %.0f seconds\n" , difftime( stop, go ) );
```
- 7. 最后，在 main 函数块中，返回零整数值，如函数声明所要求
```
return 0 ;
```
- 8. 在 main 函数块之后，开始函数定义，通过在当前经过的运行时间之外的未来点初始化一个 clock_t 变量
```
void wait( int seconds )
{
    clock_t end_wait =
        ( clock() ) + ( seconds * CLOCKS_PER_SEC );
}
```
- 9. 最后，在 wait 函数块中，添加一个空循环，当当前时间达到未来点时终止，将控制权返回到 main 函数中的循环
```
while ( clock() < end_wait ) { }
```
- 10. 保存程序文件，然后编译并执行程序以查看倒计时器和运行时间

![](img/d1dfb0563339ba187decb78799155b7f_156_0.png)

每秒的时钟滴答数取决于实现，但在 time.h 中由 CLOCKS_PER_SEC 常量定义。

![](img/d1dfb0563339ba187decb78799155b7f_156_1.png)

你可以通过将 clock() 函数返回的值除以 CLOCKS_PER_SEC 值来得到以秒表示的经过运行时间。

![](img/d1dfb0563339ba187decb78799155b7f_156_2.png)

![](img/d1dfb0563339ba187decb78799155b7f_156_3.png)

- 3. 在 main 函数块中，首先使用当前经过的秒数值对随机数生成器进行种子设置
```c
srand( time(NULL) );
```
- 4. 接下来，按顺序用数字 0-59 填充一个数组
```c
for( i = 0 ; i < 60 ; i++ ) { nums[i] = i ; }
```
- 5. 现在，将序列洗牌为随机顺序
```c
for( i = 1 ; i < 60 ; i++ )
{
 r = ( rand() % 59 ) + 1 ;
 temp = nums[i] ; nums[i]=nums[r] ; nums[r] = temp ;
}
```
- 6. 将六个数组元素中的数字添加到一个字符串中
```c
for( i = 1 ; i < 7 ; i++ )
{
 sprintf( buf , "%d " , nums[i] ) ;
 strcat( buf , " " ) ; strcat( str , buf ) ;
}
```
- 7. 然后，输出该字符串
```c
printf( "\n%6s\n\n" , str ) ;
```
- 8. 在 main 函数块结束时，返回零整数值，如函数声明所要求
```c
return 0 ;
```
- 9. 保存程序文件，然后反复编译并执行程序，以在每次执行时看到 1-59 范围内的六个不同随机数的选择

**不要忘记**
数组元素 nums[0] 被赋值为零，但这不包含在洗牌中，因为只有元素 1-59 才有资格被选择。

**热提示**
注意这里是如何使用 sprintf() 函数将 int 值转换为 char 值，然后再将其连接到更大的文本字符串。

![](img/d1dfb0563339ba187decb78799155b7f_158_0.png)

## 显示对话框

![](img/d1dfb0563339ba187decb78799155b7f_159_0.png)

请注意，WinMain() 函数在完成时需要返回一个整数，就像通常的 main() 函数一样。

在 Windows 操作系统中，C 程序可以通过 Windows 应用程序编程接口（WINAPI）提供的特殊函数轻松生成图形组件。这是通过添加编译器指令来包含 Windows 特定的 windows.h 头文件而使程序可用的。

在 Windows 的 C 程序中，通常的 main() 函数程序入口点被这个特殊的 WinMain() 函数取代：

```
int WINAPI WinMain( HINSTANCE hInstance,
    HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow )
```

这些参数始终是必需的，以便程序与操作系统通信。hInstance 参数是对程序的“句柄”引用；并且 hPrevInstance 参数在早期的 Windows 编程中使用，如今可以安全地忽略。lpCmdLine 参数是一个字符串，表示用于编译应用程序的命令行上使用的所有项，而 nCmdShow 参数控制窗口的显示方式。

在 Windows 中创建的最简单的图形组件是仅带一个“OK”按钮的基本对话框。这是通过调用此 MessageBox() 函数创建的：

```
int MessageBox( HWND hWnd, LPCTSTR lpText,
    LPCTSTR lpCaption, UINT uType );
```

![](img/d1dfb0563339ba187decb78799155b7f_159_1.png)

其他 MessageBox 图标常量包括 MB_ICONERROR、MB_ICONQUESTION 和 MB_ICONINFORMATION。

hWnd 参数是对父窗口（如果有）的“句柄”引用——如果没有父窗口，则此值指定为 NULL。lpText 参数是要显示的消息字符串，而 lpCaption 参数是要在对话框上显示的标题。最后，uType 参数可以使用管道分隔列表中的特殊常量值指定图标和按钮。例如，常量 MB_OK 添加一个 OK 按钮，并且可以使用常量 MB_ICONEXCLAMATION 添加一个感叹号图标。

编译后，创建对话框的 C 程序可以像往常一样从命令行运行。此外，它可以通过在其可执行文件图标上双击来运行——但这将同时打开命令提示符窗口和对话框。但是 GNU C 编译器有一个特殊的 -mwindows 选项，可以在编译命令的最后添加，以在通过双击运行程序时抑制命令提示符窗口。
