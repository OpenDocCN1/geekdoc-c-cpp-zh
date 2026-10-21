

## 1. 內建類型
- (a) 整數類型
    - (i) int
    - (ii) char
- (b) 浮點類型
    - (i) float
    - (ii) double
- (c) void
- (d) bool
- (e) wchar_t

## 2. 使用者自訂資料型別
- (a) class
- (b) struct
- (c) union
- (d) enumeration

## 3. 衍生資料型別
- (a) array
- (b) function
- (c) pointer
- (d) reference

wchar_t 是一種支援長字元的新資料型別。wchar_t 關鍵字指定一種寬字元型別。wchar_t 型別定義為 unsigned short（16 位元）資料物件。wchar_t 常數可以透過在前面加上 L 來宣告，例如 L"abc"、L'a'。要使用此資料型別，你必須包含標頭檔 wchar.h。

## 2.7 限定符

限定符修飾資料型別的含義。Unsigned、signed、short 和 long 是 C++ 中可用的 4 個限定符。它們的使用方式如下：

```
signed int x, y, b;
unsigned int p,q;
long int num;
short int n;
```

long int 是前面提到的資料型別，而 short int 在大多數 C++ 編譯器上與 signed int 或簡單的 int 相同。當我們需要處理正負值時，使用 signed 限定符。當我們只需要正值時，可以使用 unsigned 限定符。它們只能與 char 和整數資料型別一起使用。使用 unsigned 時，可用範圍會向正方向增加，例如，signed char 或簡稱 char 的範圍是 −128 到 127，而 unsigned char 的範圍是 0 到 255。對於 int 或 long int 也是如此。除了這兩個重要關鍵字外，const 和 volatile 也用作限定符。const 限定符用於將變數宣告為常數，例如 const int x=10; 宣告一個型別為 int、常數值為 10 的常數 x。關於常數的更多內容請參閱下一章。

## 2.8 資料型別的範圍

表 2.5：資料型別及其範圍

| 序號 | 資料型別 | 大小（位元組） | 範圍 |
|---|---|---|---|
| 1 | int or short | 2 | −32768 到 32767 |
| 2 | Unsigned int | 2 | 0 到 65535 |
| 3 | Long int | 4 | −2147483648 到 2147483647 |
| 4 | Float | 4 | 3.4e-38 到 3.4e+38 |
| 5 | Char | 1 | −128 到 127 |
| 6 | Unsigned char | 1 | 0 到 255 |
| 7 | Unsigned long | 4 | 0 到 4294967295 |
| 8 | Double | 8 | 1.7e-308 到 1.7e+308 |
| 9 | Long double | 10 | 3.4e-4932 到 3.4e+4932 |

對於資料型別範圍的計算，我們有一個固定公式：

- 1. 對於有符號資料型別，如果它在記憶體中佔用 n 位元，則此資料型別的特定變數可以取的值的範圍是
    - −2^(n-1) 到 2^(n-1) − 1
    - 例如：對於 n=16（int），範圍是
    - −2^15 到 2^15 −1
    - 對於 char 資料型別，n=8，範圍是
    - −2^7 到 2^7−1

- 2. 對於無符號資料型別，如果它在記憶體中佔用 n 位元，則此資料型別的特定變數可以取的值的範圍是
    - 0 到 2^n−1
    - 例如，對於 n=16（unsigned short int），範圍是 0 到 2^16−1；對於 unsigned char 資料型別，n=8，範圍是 0 到 2^8−1。

## 2.9 你的第一個 C++ 程式

```
/*PROG 2.1 PRINTS HELLO C++ ON THE SCREEN */

#include <iostream.h>
int main()
{
    cout << " Hello C++";
    return 0;
}

OUTPUT :
Hello C++
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_48_0.png)

圖 2.3. 程式 2.1 的輸出畫面。

說明：在第一行，#include 是預處理指令，iostream.h 是標頭檔，寫在 < 和 > 或 "" 中。"io" 在 iostream 中代表輸入輸出，.h 代表標頭檔。每個 C++ 程式都必須包含 iostream.h 檔案。#include 和 <iostream.h> 之間可以有空格。下一行是 main() 函數，其中 () 被稱為函數符號。每個 C++ 檔案都必須有這個函數，因為 C++ 程式的執行是從 main() 開始的。{ 是 main 函數的起始大括號，} 是結束大括號。所有語句和指令都寫在 main 函數內部。main 之前的 int 被視為其返回型別。cout 是定義在 iostream.h 中的類別 iostream_withassign 的預定義物件。符號 << 是一個運算子，稱為輸出運算子或插入運算子。cout << 的組合效果是將其後雙引號中的內容列印到螢幕上，這就是輸出。C++ 程式中的每個語句都必須以 ;（分號）結束。C++ 是區分大小寫的程式語言，因此你使用的所有 C++ 內建功能都必須使用小寫。return 0; 這一行只是為了避免警告。如果你不寫 return 0;，不會得到錯誤，但會得到警告。上述程式可以修改為（對 main 函數的返回型別稍作更改）：

```
void main()
{
    cout << "Hello C++";
}
```

### 2.9.1 編譯和執行過程

要在 Windows 環境下執行你的第一個程式，請遵循以下步驟。

- 1. 在 Visual Studio 6.0 中開啟 Microsoft Visual C++ 6.0。
- 2. 在 IDE 中，從 file 選單中選擇 new。
- 3. 在 Project 標籤下，選擇 win 32 Console Application 選項，並給專案命名，例如 "CPP"。選擇你想要放置專案的位置，例如 D:\。你的所有檔案都將保存在該專案中。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_49_0.png)

圖 2.4

4. 按一下 Finish。會出現一個新的對話方塊，直接按 OK。此時你已成功在 D:\ 下建立了一個名為 CPP 的新專案。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_49_1.png)

圖 2.5

5. 現在從 file 選單中選擇 new。選擇 Files 標籤和 C++ source file 選項。給一個合適的檔案名稱，例如 first。按 OK。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_50_0.png)

圖 2.6

6. 會出現一個新視窗。在視窗中輸入上述程式，保持原樣。

7. 從 build 選單中選擇 build CPP.exe 選項。假設程式沒有錯誤，會在底部出現一個新視窗，顯示 0 error 0 warnings。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_50_1.png)

圖 2.7

一天工作後，當你想開啟同一個專案時，只需尋找副檔名為 .dsp 的檔案，它代表 **資料來源專案**。之後你可以繼續製作 C++ 程式。

## 2.10 C++ 程式的結構

任何 C++ 程式的一般結構如下。它簡單地說明一個標準 C++ 程式可能根據結構中各個部分呈現的樣子。

|  |
|---|---|
| 文件註解 |
| 標頭檔 |
| 符號常數 |
| 全域變數、函數 |
| 類別宣告 |
| 成員函數定義 |
| main()
{
  ....................;
  ....................;
} |
| 全域函數定義 |

圖 2.10. C++ 程式的一般結構。

- - 第一部分「文件註解」是可選的，用於為程式加入註解，通常如我們所給的程式標題。
- - 在第二部分中，我們包含 C++ 程式所需的各種標頭檔。
- - 符號常數和全域變數、函數在需要時定義於其後。
- - 類別是 C++ 程式設計的主要建構區塊，其宣告包含資料成員和函數的宣告。成員函數可以在類別中宣告並定義，或者它們在類別中宣告但在類別外部定義，即在類別宣告之外完成。
- - **main()** 函數必須存在於每個 C++ 程式中。它包含所有要執行的語句。在這個 main 函數內部，我們建立先前建立的類別的物件。所有語句都放在大括號內，並以分號結束。

下面給出一個完整的 C++ 程式。如果你此時不理解額外的內容，不要擔心。這只是為了讓你了解 C++ 程式的結構。

```
/*Documentation*/
/* DEMO PROGRAM FOR C++ STRUCTURE, DOES NOT SERVE ANY PURPOSE EXCEPT DEMONSTRATION */

#include <iostream.h> /*header file inclusion */
#include <iomanip.h>
```

```
int x;float y; char z; /* global variables */
void disp(); /* global function */
/*class declaration starts here */
class demo
{
private :
    int x, y;
public :
    void input(int a, int b);
    void show();
};
/*class declaration ends here */
/*class function definition */
void demo ::input(int a, int b)
{
    x = a;
    y = b;
}
/*class function definition */
void demo ::show()
{
    cout << "x=" << x << endl;
    cout << "y=" << y << endl;
}
void main() /*main function definiton */
{
    demo d1,d2; //creating objects
    d1.input(10,20);
    ..............;
    ..............;
    d1.show();
    int num;
    show(); //local function call
}
/*global function definitions */
void show()
{
    cout << "in show" << endl;
}
```

