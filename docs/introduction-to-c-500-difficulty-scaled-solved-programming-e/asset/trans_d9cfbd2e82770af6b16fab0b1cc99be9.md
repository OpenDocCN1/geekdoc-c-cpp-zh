

以不同的顺序。这第二行构成了加密密钥。注意，所有密钥字符必须互不相同。参见此图。

| a b c d e f g h i j k l m n o p q r s t u v w x y z |
| d y p r i a j u h t q w e s f o v c n b l x m k z g |

原文中的单词被相应的密钥所替换。例如，单词 word 被加密为 binb。

编写一个程序，读取一个长度小于 100 个字符的字符串、一个 26 个字符的密钥字符串，并对输入字符串的小写字母进行加密。然后，程序应该解密加密字符串并显示（应与原始字符串相同）。程序应该检查密钥字符是否只出现一次。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;
int main()
{
    const int LETTERS = 26;
    bool error;
    char str[100], key[LETTERS+1];
    int i, j, len;

    cout << "Enter text: ";
    cin.getline(str, sizeof(str));
    len = strlen(str);
    do {
        error = 0;
        cout << "Enter key (" << LETTERS << " different characters): ";
        cin.getline(key, sizeof(key));
        if (strlen(key) != LETTERS)
        {
            cout << "Error: Key must be of " << LETTERS << " characters\n";
            error = 1;
        } else {
            for (i = 0; i < LETTERS; i++) {
                for (j=i+1; j < LETTERS; j++) {
                    if (key[i] == key[j]) {
                        error = 1;
                        cout << "Key characters must be different\n";
                        break;
                    }
                }
            }
            if (error == 1)
                break;
        }
    } while (error != 0);
```

# 258 C++ 绪

```cpp
for(i = 0; i < len; i++)
{
    if(str[i] >= 'a' && str[i] <= 'z')
        str[i] = key[str[i]]-'a';
}
cout << "Encrypted text: " << str << '\n';
for(i = 0; i < len; i++)
{
    for(j = 0; j < LETTERS; j++)
    {
        if(str[i] == key[j])
        {
            str[i] = 'a'+j;
            break;
        }
    }
    cout << "Original text: " << str << '\n';
}
return 0;
```

# 二维数组与 C 风格字符串

二维数组通常用于存储多个 C 风格的字符串。例如，语句：

```cpp
char str[10] [40];
```

声明了具有十行的 str[10]。每行行可以存储一个多达 40 个字符的字符串。如果字符串较短，则会浪费内存。

我们可以在声明二维数组时存储字符串字面量。例如：

```cpp
char str[3] [40] = "One", "Two", "Three";
```

"One" 的字符存储在 str 的第一行，“Two" 存储在第二行，而 "Three" 的字符在第三行中不足以填满空字符，会进行填充，如图：

| str[0][0]str[0][2] | str[0][3] | ... | str[0][39] |
|---|---|---|---|
| O n | e | \0 | ... | \0 |
| str[1][0]str[1][1] | str[1][3] | ... | str[1][39] |
| T w | o | \0 | ... | \0 |
| str[2][0]str[2][2] | str[2][3]str[2][5] | ... | str[2][39] |
| T h | r | e | \0 | ... | \0 |

回想第 8 章和“指针与二维数组”部分，我们可以将二维数组 str[N][M] 的每个元素 str[0], str[1], ..., str[N-1] 视为指向 M 个元素的指针。

# 10 字符串 259

例如，str[0] 可以用作指向 40 个字符数组的指针，持有字符串 "One"。

回想“指针数组”部分，为了节省内存，可以使用指针数组代替二维数组。例如：

```cpp
const char *str[] = {"One", "Two", "Three"};
```

虽然为 str 分配了某些内存，但字符串所需的内存恰好如此。受益于指针和数组之间的关系，我们可以像下标访问二维数组一样访问字符。例如：

```cpp
for(i = 0; i < 3; i++)
  if(str[i][0] == 'T')
    cout << str[i] << '\n';
```

循环显示字符串。C10.27 是另一个示例，证明了使用指针数组更高效。此外，为了更灵活和安全的字符串管理，可以使用 vector 类。C10.28 是这样的示例。正如我提到的，我的意图是向你们展示这些方法，因为它们是流行的。

# 练习题

**C10.26** 下列程序的输出是什么？

```cpp
#include <iostream>
#include <string>
int main()
{ char arr[7][10] = {"Monday", "Tuesday", "Wednesday", "Thursday", "Saturday", "Sunday"};
  int i;
  for(i = 0; i < 7; i++)
    if(arr[i][2] == 'n' && *(arr[i]+3) == 'd' && *(arr[i]+4) == 'a')
      cout << arr[i] << " is No." << i << " week day";
  return 0;
}
```

**答案：** "Monday" 的字符存储在 arr 的第一行，“Tuesday" 的字符在第二行，以此此类推。记住 *(arr[i]+3) 等于 arr[i][3]*(arr[i]+4) 等于 arr[i][4]，即 arr[i]。因此，循环检查 arr 的每一行并显示第三、第四和第五字符分别为 'n'、'd' 和 'a'。因此，程序显示：

Monday is No.1 week day
Sunday is No.7 week day

# 260 C++ 绪

C10.27 编写一个程序，读取 20 个名字（每个小于 100 个字符），将它们存储在数组中，并使用指针数组按字母顺序显示它们。

```cpp
#include <iostream>
#include <string>
#include <cstring>
using std::cout;
using std::cin;

int main() {
    const int SIZE = 20;
    char *temp, *ptr[SIZE], str[100];
    int i, j;

    for(i = 0; i < SIZE; i++) {
        cout << "Name: ";
        cin.getline(str[i], sizeof(str[i]));
        ptr[i] = str[i]; /* 数组元素指向输入字符串。 */
    }
    for(i = 0; i < SIZE-1; i++) {
        for(j = i+1; j < SIZE; j++) {
            /* 如果 ptr[j] 指向的字符串小于 ptr[i] 指向的字符串，则交换指针。 */
            if(strcmp(ptr[j], ptr[i]) < 0) {
                temp = ptr[j];
                ptr[j] = ptr[i];
                ptr[i] = temp;
            }
        }
        cout << ptr[i] << '\n';
    }
    return 0;
}
```

注释：我添加这个练习题的主要目的是向你们展示指针数组有多用。当交换两个字符串时，交换的是指针而不是字符串。因此，我们获得了性能提升。我们使用的排序算法称为选择排序，将在第 12 章中讨论。该解决方案的“负面”点是空间浪费。str 的每行都分配了 100 个字符，即使字符串包含较少。对于更高效的内存管理，请参见下一个练习。我们将在第 14 章的 C.14.6 练习中使用替代方案。

C.10.28 编写一个程序，连续读取并将以 'a' 开头并's' 结尾的字符串存储在 vector 中。如果用户输入 end，停止插入字符串。程序应该读取并显示它在 vector 中出现了多少次。

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main()
{
    int i, cnt, size;
    string s;
    vector<string> v_str;

    while (1)
    {
        cout << "Enter text: ";
        getline(cin, s);
        if(s == "end")
            break;
        v_str.push_back(s);
    }
    size = v_str.size();
    if(size == 0)
    {
        cout << "None string is stored\n";
        return 0;
    }

    cout << "Enter text: ";
    getline(cin, s);
    cnt = 0;
    for(i = 0; i < size; i++)
    {
        if(v_str[i] == s)
            cnt++;
    }
    cout << s << " is stored " << cnt << " times\n";
    return 0;
}
```

# # 未完成练习

**U.10.1** 编写一个程序，读取三个小于 100 个字符的字符串并将它们存储在两个数组中（例如 str1, str2, str3）。然后，程序应该将它们的内容向右移动一位，即将 str3 的内容复制到 str1，将 str2 的内容复制到 str3。

**U.10.2** 编写一个程序读取一个字符串并存储在字符串对象中，如果以 aa 结尾，程序应该反向显示它。

**U.10.3** 下列程序的输出是什么？

```cpp
#include <iostream>
#include <string>
int main()
```

