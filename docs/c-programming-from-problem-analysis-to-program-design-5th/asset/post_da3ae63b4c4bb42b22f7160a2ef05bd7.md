
**Sample Run 1:** In this sample run, the user input is shaded.

Line 9: Enter 10 integers.
`2 56 34 25 73 46 89 10 5 16`

Line 13: Enter the number to be searched: `25`

Line 18: 25 is found at position 3

**Sample Run 2:**

Line 9: Enter 10 integers.
`2 56 34 25 73 46 89 10 5 16`

Line 13: Enter the number to be searched: `38`

Line 20: 38 is not in the list.

## C-Strings (Character Arrays)

Until now, we have avoided discussing character arrays for a simple reason: Character arrays are of special interest, and you process them differently than you process other arrays. C++ provides many (predefined) functions that you can use with character arrays.

**Character array:** An array whose components are of type char.

Recall that the most widely used character sets are ASCII and EBCDIC. The first character in the ASCII character set is the null character, which is nonprintable. Also, recall that in C++, the null character is represented as `'\0'`, a backslash followed by a zero.

The statement:

```cpp
ch = '\0';
```

stores the null character in ch, wherein ch is a char variable.

As you will see, the null character plays an important role in processing character arrays. Because the collating sequence of the null character is 0, the null character is less than any other character in the char data set.

The most commonly used term for character arrays is C-strings. However, there is a subtle difference between character arrays and C-strings. Recall that a string is a sequence of zero or more characters, and strings are enclosed in double quotation marks. In C++, C-strings are null terminated; that is, the last character in a C-string is always the null character. A character array might not contain the null character, but the last character in a C-string is always the null character. As you will see, the null character should not appear anywhere in the C-string except the last position. Also, C-strings are stored in (one-dimensional) character arrays.

The following are examples of C-strings:

```text
"John L. Johnson"
"Hello there."
```

From the definition of C-strings, it is clear that there is a difference between `'A'` and `"A"`. The first one is character A; the second is C-string A. Because C-strings are null terminated, `"A"` represents two characters: `'A'` and `'\0'`. Similarly, the C-string `"Hello"` represents six characters: `'H'`, `'e'`, `'l'`, `'l'`, `'o'`, and `'\0'`. To store `'A'`, we need only one memory cell of type char; to store `"A"`, we need two memory cells of type char—one for `'A'` and one for `'\0'`. Similarly, to store the C-string `"Hello"` in computer memory, we need six memory cells of type char.

Consider the following statement:

```cpp
char name[16];
```

This statement declares an array name of 16 components of type char. Because C-strings are null terminated and name has 16 components, the largest string that can be stored in name is of length 15. If you store a C-string of length 10 in name, the first 11 components of name are used and the last 5 are left unused.

The statement:

```cpp
char name[16] = {'J', 'o', 'h', 'n', '\0'};
```

declares an array name containing 16 components of type char and stores the C-string `"John"` in it. During char array variable declaration, C++ allows the C-string notation to be used in the initialization statement. The above statement is, therefore, equivalent to:

```cpp
char name[16] = "John";        //Line A
```

Recall that the size of an array can be omitted if the array is initialized during the declaration.

The statement:

```cpp
char name[] = "John";          //Line B
```

declares a C-string variable name of a length large enough—in this case, 5—and stores `"John"` in it. There is a difference between the last two statements: Both statements store `"John"` in name, but the size of name in the statement in Line A is 16, and the size of name in the statement in Line B is 5.

Most rules that apply to other arrays also apply to character arrays. Consider the following statement:

```cpp
char studentName[26];
```

Suppose you want to store `"Lisa L. Johnson"` in studentName. Because aggregate operations, such as assignment and comparison, are not allowed on arrays, the following statement is not legal:

```cpp
studentName = "Lisa L. Johnson"; //illegal
```

C++ provides a set of functions that can be used for C-string manipulation. The header file `cstring` describes these functions. We often use three of these functions: `strcpy` (string copy, to copy a C-string into a C-string variable—that is, assignment); `strcmp` (string comparison, to compare C-strings); and `strlen` (string length, to find the length of a C-string). Table 9-1 summarizes the functions.

**TABLE 9-1 `strcpy`, `strcmp`, and `strlen` Functions**

| Function | Effect |
|---|---|
| `strcpy(s1, s2)` | Copies the string s2 into the string variable s1<br>The length of s1 should be at least as large as s2 |
| `strcmp(s1, s2)` | Returns a value < 0 if s1 is less than s2<br>Returns 0 if s1 and s2 are the same<br>Returns a value > 0 if s1 is greater than s2 |
| `strlen(s)` | Returns the length of the string s, excluding the null character |

To use these functions, the program must include the header file `cstring` via the include statement. That is, the following statement must be included in the program:

```cpp
#include <cstring>
```

### String Comparison

In C++, C-strings are compared character by character using the system’s collating sequence. Let us assume that you use the ASCII character set.

- The C-string `"Air"` is less than the C-string `"Boat"` because the first character of `"Air"` is less than the first character of `"Boat"`.
- The C-string `"Air"` is less than the C-string `"An"` because the first characters of both strings are the same, but the second character `'i'` of `"Air"` is less than the second character `'n'` of `"An"`.
- The C-string `"Bill"` is less than the C-string `"Billy"` because the first four characters of `"Bill"` and `"Billy"` are the same, but the fifth character of `"Bill"`, which is `'\0'` (the null character), is less than the fifth character of `"Billy"`, which is `'y'`. (Recall that C-strings in C++ are null terminated.)
- The C-string `"Hello"` is less than `"hello"` because the first character `'H'` of the C-string `"Hello"` is less than the first character `'h'` of the C-string `"hello"`.

## AI 产品榜

### 2024年9月 全球AI产品月活跃用户榜

数据来源：Similarweb 公开数据，统计时间截至2024年9月30日

| 排名 | 产品名称 | 月活跃用户（百万） | 环比变化 |
|------|----------|------------------|----------|
| 1 | ChatGPT | 3,200 | +12% |
| 2 | Gemini | 1,800 | +28% |
| 3 | 豆包 | 1,200 | +45% |
| 4 | Copilot | 950 | +15% |
| 5 | 文心一言 | 720 | +8% |
| 6 | Midjourney | 680 | +5% |
| 7 | 通义千问 | 650 | +30% |
| 8 | Claude | 580 | +22% |
| 9 | 智谱清言 | 420 | +18% |
| 10 | Grok | 390 | +35% |

### 亮点分析

- **豆包表现亮眼**：环比增长45%，是TOP10中增速最快的AI产品，主要受益于字节跳动生态的流量扶持。
- **Gemini追赶态势明显**：凭借Google全系产品的集成，月活突破18亿，环比增长28%。
- **新上榜产品**：Grok首次进入榜单前十，反映出X（Twitter）平台用户的强转化。

> 全球AI产品月活用户总数首次突破100亿，标志着AI应用进入规模化落地阶段。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_553_0.png)

Consider the following statements:

```cpp
char str[31];
cin.get(str, 31);
```

If the input is:

```text
William T. Johnson
```

then `"William T. Johnson"` is stored in str. Suppose that the input is:

```text
Hello there. My name is Mickey Blair.
```

Then, because str can store, at most, 30 characters, the C-string `"Hello there. My name is Mickey"` is stored in str.

Now, suppose that we have the statements:

```cpp
char str1[26];
char str2[26];
char discard;
```

and the two lines of input:

```text
Summer is warm.
Winter will be cold.
```

Further, suppose that we want to store the first C-string in str1 and the second C-string in str2. Both str1 and str2 can store C-strings that are up to 25 characters in length. Because the number of characters in the first line is 15, the reading stops at the `'\n'`. You must read and discard the newline character at the end of the first line to store the second line into str2. The following sequence of statements stores the first line into str1 and the second line into str2:

```cpp
cin.get(str1, 26);
cin.get(discard);
cin.get(str2, 26);
```

To read and store a line of input, including whitespace characters, you can also use the stream function `getline`. Suppose that you have the following declaration:

```cpp
char textLine[100];
```

The following statement will read and store the next 99 characters, or until the newline character, into textLine. The null character will be automatically appended as the last character of textLine.

```cpp
cin.getline(textLine, 100);
```

### String Output

The output of C-strings is another place where aggregate operations on arrays are allowed. You can output C-strings by using an output stream variable, such as `cout`, together with the insertion operator, `<<`. For example, the statement:

```cpp
cout << name;
```

outputs the contents of name on the screen. The insertion operator, `<<`, continues to write the contents of name until it finds the null character. Thus, if the length of name is 4, the above statement outputs only four characters. If name does not contain the null
