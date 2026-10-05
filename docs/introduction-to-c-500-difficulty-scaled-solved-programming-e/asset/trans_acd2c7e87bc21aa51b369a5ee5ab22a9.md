

# 252 C++ 简介

程序应该显示相关信息。如果玩家找到了该单词或猜错了了 7 次，游戏将结束。假设第二个玩家不允许重复输入同一个字母。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

int main()
{
    const int ERROR_TRIES = 7;
    char ch, secret[30], hide[30] = {};
    int i, found, len, error, correct;

    cout << "Enter secret word: ";
    cin.getline(secret, sizeof(secret));
    len = strlen(secret);

    for(i = 0; i < len; i++)
        hide[i] = '_';

    error = 0;
    while(error < ERROR_TRIES)
    {
        cout << "Enter character: ";
        ch = cin.get();
        found = 0;
        for(i = 0; i < len; i++)
        {
            if(secret[i] == ch)
            {
                hide[i] = ch;
                found = 1;
                correct++;
                if(correct == len)
                {
                    cout << "Secret word is found !!!\n";
                    return 0;
                }
            }
        }
        if(found == 0)
        {
            error++;
            cout << "Error, " << ch << " does not exist. You've got " << ERROR_TRIES - error << " more attempts\n";
        }
        else
        {
            cout << hide << "\n";
            cin.get(); // 丢弃上一次 get() 中的换行符
        }
    }
    cout << "Sorry, the secret word was " << secret << "\n";
    return 0;
}
```

# C10.20 这里有一个奇怪的程序，用于向你展示在一个表达式中混合指针、函数调用和指针算术的语法示例。输出是什么？

```cpp
#include <iostream>
#include <cstring>
int main()
{
    char str[] = "notesasy";
    std::cout << str*(str+3)-1-strlen(str+3) << '\n';
    return 0;
}
```

答案：由于表达式 *(str+3) 等于 str[3]，即 'e'，*(str+3)-1 等于 str[3]-1，而 'e'-1 = 'd'。strlen() 返回第三个字符之后字符串的长度，即 4。因此，该表达式等于 str+'d'-'a' = str+3，程序输出 easy。

# C10.21 通用产品代码 (UPC) 条形码由 12 位数字组成。最后一位是用于错误检测的校验位。要计算其值，我们使用前 11 位数字，方法如下：

- 将奇数位置上的数字相加并将结果乘以 3。
- 将偶数位置上的数字加到上一个结果中。
- 将结果除以 12。用 10 减去余数，即为校验位。如果减法结果为 10（意味着余数为 0），则使用 0 作为校验位。

例如，假设条形码为 123456789015。校验位的计算如下：

- a. 1+3+5+7+9+1 = 26。乘以 3 26*3 = 78。
- b. 2+4+6+8+0 = 20。加到上一个结果 78+20 = 98。
- c. 校验的值为 10-(98%10) = 10-8 = 2。

由于最后一位是 5 而计算出的校验位是 2，因此该条形码是不正确的。
编写一个程序读取 UPC 条形码并检查它是否正确。程序应强制用户输入有效的条形码，这意味着字符串长度必须为 12 且必须包含数字。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;
int main()
{
    char upc[13];
    int i, len, flag, chk_dig, sum;
    while (1)
    {
        cout << "Enter UPC (12 digits): ";
        cin.getline(upc, sizeof(upc));
        len = strlen(upc);
        if(len != 12)
        {
            cout << "Error: wrong length\n";
            continue;
        }
```

# 254 C++ 简介

```cpp
flag = 1;
for(i = 0; i < 12; i++)
{
    if(upc[i] < '0' || upc[i] > '9')
    {
        cout << "Error: only digits allowed\n";
        flag = 0;
        break;
    }
    if (flag == 1)
        break;
}
sum = 0;
for(i = 0; i < 11; i+=2)
    sum += upc[i]-'0'; /* 减去 '0' 以获得数字的数值。 */
sum *= 3;
for(i = 1; i < 11; i+=2)
    sum += upc[i]-'0';

chk_dig = 10 - (sum%10);
if(chk_dig == 10) chk_dig = 0;

if(flag == 1 && chk_dig == upc[11])
    cout << "Valid UPC\n";
else
    cout << "Invalid UPC\n";

return 0;
}
```

# C10.22 运行长度编码 (RLE) 是基于数据流中的字符可能多次重复的，通过显示字符及其出现的次数来压缩字符串。如果字符连续出现，则显示计数。编写一个程序读取字符串并压缩它。

```cpp
#include <iostream>
#include <cstring>
#include <string>
using std::string;

int main()
{
    char str[100];
    int i, len, cnt;
    string compressed;

    cout << "Enter string: ";
    getline(cin, str);
    len = strlen(str);

    for (i = 0; i < len; i++)
    {
        cnt = 1;
        while (i + 1 < len && str[i] == str[i+1])
        {
            cnt++;
            i++;
        }
        compressed += str[i];
        compressed += to_string(cnt);
    }

    cout << "Compressed string: " << compressed << endl;

    return 0;
}
```

# 255 字符串

# C10.23 编写一个程序读取字符串并将其存储在字符串对象中。然后，使用指针显示字符串的每一个字符。注意指针是如何移动的。

```cpp
#include <iostream>
#include <string>
using std::string;
using std::cout;

int main()
{
    string s;
    const char *ptr;

    cout << "Enter string: ";
    std::cin >> s;
    ptr = &s[0];

    cout << "String characters: ";
    while (*ptr != '\0')
    {
        cout << *ptr << " ";
        ptr++;
    }
    cout << endl;

    return 0;
}
```

# 256 C++ 简介

# C10.24 下列程序的输出是什么？

```cpp
#include <iostream>
int main()
{
    const char *arr[] = {"TEXT", "SHOW", "OPTIM", "DAY"};
    const char **ptr1;

    ptr1 = arr;
    std::cout << ***ptr1 << ' ';
    std::cout << **ptr1+2;
    std::cout << (char)(**ptr1+1) << '\n';
    return 0;
}
```

答案：由于表达式 ***ptr1 等于 arr[0][0]，即 'T'，**ptr1+2 等于 arr[0]+2，即 'X'，而 (char)(**ptr1+1) 等于 (char)(arr[0]+1)，即 'E'+1 = 'F'。因此，该程序输出 TX U。

