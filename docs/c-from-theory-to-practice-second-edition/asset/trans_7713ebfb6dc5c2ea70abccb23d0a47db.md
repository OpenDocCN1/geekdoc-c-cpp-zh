

## C.10.18 以下程序的输出是什么？

```
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[] = "csfbl", *p = str;
    while(*p)
    {
        --*p; /* To make it harder, we could merge the two statements into --*p++; */
        p++;
    }
    printf("%s\n", p-strlen(str));
    return 0;
}
```

答案：语句 `--*p;` 会减少 `p` 所指向地址中的内容。例如，在第一次迭代中，`p` 指向字符串的第一个字符，即 `'c'`。因此，`*p` 等于 `'c'`，语句 `--*p;` 改变 `str[0]` 的值，使其等于 ASCII 字符集中的前一个字符。因此，`str[0]` 变为 `'b'`。接着，`p` 递增并指向 `str` 的下一个元素。以同样的方式，后续迭代使 `str[1]`、`str[2]`、`str[3]` 和 `str[4]` 分别等于 `'r'`、`'e'`、`'a'` 和 `'k'`。

一旦 `p` 等于 `str+5`，即遇到空字符时，循环终止。由于 `strlen()` 返回字符串的长度，表达式 `p-strlen(str)` 等价于 `str+5-5 = str`。因此，程序显示存入 `str` 的新字符串，即 `break`。确实，在继续下一个练习之前休息一下。

## C.10.19 以下程序的输出是什么？

```
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[] = "Text", *p = str;
    int i;
    for(i = 0; i < strlen(str)-1; i++, p++)
        printf("%c", p[i]);
    return 0;
}
```

答案：由于 `strlen()` 返回 4，循环执行三次。让我们跟踪迭代过程：

第一次迭代（`i = 0`）：显示 `p[0]` 的值，即 `T`。
第二次迭代（`i++ = 1`）：由于 `p` 递增一，`p` 指向字符串的第二个字符，即 `'e'`。由于我们将 `p` 作为数组处理，`p[0]` 是 `'e'`，`p[1]` 是 `'x'`。因此，程序输出 `x`。

第三次迭代（`i++ = 2`）：现在，`p` 指向第三个字符，即 `'x'`。因此，`p[0]` 是 `'x'`，`p[1]` 是 `'t'`，而 `p[2]` 等于 `'\0'`。因此，程序不显示任何内容。

总之，程序显示：`Tx`

## C.10.20 编写一个程序，读取一个少于 100 个字符的字符串，并显示其小写字母和数字出现的次数。此外，程序应显示出现次数最多的小写字母及其出现次数。如果有多个字母出现相同的最多次数，程序应显示最先找到的那个。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    char ch, max_ch, str[100];
    int i, len, max_times, low_let[26] = {0}; /* The size of the array
    is equal to the number of the lowercase letters. This array holds the
    number of the appearances of each letter. For example, low_let[0] holds
    the appearances of 'a', and low_let[25] the appearances of 'z'. */
    int dig[10] = {0}; /* Similarly, dig[0] holds the appearances of
    digit 0, and dig[9] the appearances of digit 9. */

    printf("Enter text: ");
    len = read_text(str, sizeof(str), 1);
    max_ch = max_times = 0;
    for(i = 0; i < len; i++)
    {
        if((str[i] >= 'a') && (str[i] <= 'z'))
        {
            ch = str[i]-'a';
            low_let[ch]++; /* For example, if the character is
            'a', the value of low_let['a'-'a'] = low_let[0], which holds the
            appearances of 'a', will be incremented by one. */
            if(low_let[ch] > max_times)
            {
                max_times = low_let[ch];
                max_ch = str[i];
            }
        }
        else if((str[i] >= '0') && (str[i] <= '9'))
            dig[str[i]-'0']++;
    }
    printf("****** Lowercase letters appearances\n");
    for(i = 0; i < 26; i++)
        if(low_let[i] != 0) /* Check if the letter appears once at
        least. */
            printf("Letter %c appeared %d times\n", 'a'+i,
            low_let[i]);
printf("***** Digits appearances\n");
for(i = 0; i < 10; i++)
    if(dig[i] != 0)
        printf("Digit %d appeared %d times\n", i, dig[i]);
if(max_times != 0)
    printf("'%c' appears %d times\n", max_ch, max_times);
return 0;
}
```

注释：如果字符串包含多个出现相同最多次数的字符，程序会显示最先找到的那个。例如，如果用户输入 `exit1`，输出将是：`'e'` 出现 1 次，因为所有字符都出现一次，而字符 `'e'` 是第一个。

## C.10.21

编写一个程序，模拟流行的猜词游戏“hangman”。程序读取一个少于 30 个字符的秘密单词，即要猜的单词。该单词由第一个玩家输入。然后，第二个玩家逐个输入字母。程序应检查每个字母并通知玩家。如果该字母出现在单词中，程序应在相应位置显示正确猜测的字母，并在未知字母的位置设置下划线字符。如果该字母没有出现，程序应显示相关消息。如果玩家找到单词或出现 7 次错误猜测，游戏结束。假设第二个玩家不允许多次输入同一个字母。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define ERROR_TRIES 7

int read_text(char str[], int size, int flag);

int main(void)
{
    char ch, secret[30], hide[30] = {0};
    int i, found, len, error, correct;

    printf("Enter secret word: ");
    len = read_text(secret, sizeof(secret), 1);

    for(i = 0; i < len; i++)
        hide[i] = '_';

    error = correct = 0;
    while(error < ERROR_TRIES)
    {
        printf("Enter character: ");
        ch = getchar();
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
                    printf("Secret word is found !!!\n");
                    return 0;
                }
            }
        }
        if(found == 0)
        {
            error++;
            printf("Error, %c does not exist. You've got %d more attempts\n", ch, ERROR_TRIES - error);
        }
        else    printf("%s\n", hide);
        getchar(); /* Get '\n' from the previous getchar(). */
    }
    printf("Sorry, the secret word was %s\n", secret);
    return 0;
}
```

## C.10.22 以下程序的输出是什么？

```c
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[] = "noteasy";

    printf("%s\n", str + *(str+3) -1 - str[strlen(str+3)]);
    return 0;
}
```

答案：由于表达式 `*(str+3)` 等价于 `str[3]`，即 `'e'`，所以 `*(str+3)-1` 的值等于 `str[3]-1`，即 `'e'-1 = 'd'`。`strlen()` 返回第三个字符之后的字符串长度，即 4。因此，该表达式等价于 `str+'d'-'a' = str+3`，程序输出 `easy`。

## C.10.23

通用产品代码（UPC）条形码由 12 位数字组成。最后一位是用于错误检测的校验位。为了计算其值，我们使用前 11 位数字，如下所示：

- a. 将奇数位置上的数字相加，并将结果乘以 3。
- b. 将偶数位置上的数字加到前一个结果中。
- c. 将结果除以 10。用 10 减去余数，所得即为校验位。如果相减结果为 10（意味着余数为 0），则使用 0 作为校验位。

例如，让我们看看条形码 `123456789015` 是否正确。校验位计算如下：

- a. 1+3+5+7+9+1 = 26。乘以 3 得到 26*3 = 78。
- b. 2+4+6+8+0 = 20。加到前一个结果得到 78+20 = 98。
- c. 校验位的值为 10-(98%10) = 10-8 = 2。

由于最后一位是 5，而计算出的校验位是 2，因此该条形码不正确。

编写一个程序，读取一个 UPC 条形码并检查它是否正确。程序应强制用户输入有效的条形码，即字符串长度应为 12，且只能包含数字。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    char upc[13];
    int i, len, flag, chk_dig, sum;

    while(1)
    {
        printf("Enter UPC (12 digits): ");
        len = read_text(upc, sizeof(upc), 1);
        if(len != 12)
        {
            printf("Error: wrong length\n");
            continue;
        }
        flag = 1;
        for(i = 0; i < 12; i++)
        {
            if(upc[i] < '0' || upc[i] > '9')
            {
                printf("Error: only digits allowed\n");
                flag = 0;
                break;
            }
        }
        if(flag == 1)
            break;
    }
    sum = 0;
    for(i = 0; i < 11; i+=2)
        sum += upc[i]-'0'; /* Subtract '0' to get the numeric value
    of the digit character. */
    sum *= 3;
```

