

| | 0 | 1 | 2 |
|---|---|---|---|
| 0 | 6 | 7 | 8 |
| 1 | 1 | 2 | 17 |
| 2 | 2 | 4 | 12 |
| 3 | 3 | 6 | 50 |
| 4 | 5 | 0 | 49 |
| 5 | 5 | 3 | 92 |
| 6 | 6 | 0 | 38 |
| 7 | 6 | 1 | 11 |
| 8 | 6 | 3 | 15 |

| | |
|---|---|
| 0 | 2 |
| 1 | 1 |
| 2 | 1 |
| 3 | 2 |
| 4 | 1 |
| 5 | 0 |
| 6 | 1 |

| | |
|---|---|
| 0 | 3 |
| 1 | 4 |
| 2 | 5 |
| 3 | 7 |
| 4 | 8 |
| 5 | 8 |
| 6 | 8 |

| | 0 | 1 | 2 |
|---|---|---|---|
| 0 | 7 | 6 | 8 |
| 1 | 0 | 5 | 49 |
| 2 | 0 | 6 | 38 |
| 3 | 1 | 6 | 11 |
| 4 | 2 | 1 | 17 |
| 5 | 3 | 5 | 92 |
| 6 | 3 | 6 | 15 |
| 7 | 4 | 2 | 12 |
| 8 | 6 | 3 | 50 |

Fig. 2.35 快速转置中按行存储列 (a) 输入矩阵 B (b) Freq[] (c) RowStartPos[] (d) B^T

### 快速转置的时间和空间复杂度分析

算法 2.4 中有三个循环，分别执行 n（行数）、τ（非零元素个数）、n - 1 和 τ 次，总体时间复杂度为 O(n + τ)。

在最坏情况下，即当 τ = m × n（非零元素）时，量级变为 O(n + mn) = O(mn)，这与常规二维转置相同。然而，快速转置相关的常数因子相当高。当 τ 相对于其最大值 m × n 足够小时，快速转置运行速度更快。

与简单转置相比，快速转置节省了时间，但需要为两个一维数组 Freq 和 RowStartPos 额外分配空间。程序代码 2.11 实现了稀疏矩阵快速转置。

### 程序代码 2.11

```
Sparse_Matrix Sparse_Matrix::Fast_Transpose()
{
    Sparse_Matrix B;
    int m, n, t, i, j, Freq[], RowStartPos[];
    Row = S_Mat[0][0];
    Col = S_Mat[0][1];
    M = S_Mat[0][2];
    B.S.Mat[0][0] = Col;
    B.S.Mat[0][1] = Row;
    B.S.Mat[0][2] = M;
    if(M == 0) return B;
    else
    {
        for(i = 0; i < Col; i++)
        {
            Freq[i] = 0;
        }
        for(i = 1; i <= t; i++)
        {
            T = A[i][1];
            Freq[T]++;
        }
        RowStartPos[0] = 1;
        for(i = 1; i < n; i++)
        {
            RowStartPos[i] = RowStartPos[i - 1] + Freq[i - 1];
        }
        for(i = 1; i <= M; i++)
        {
            j = A[i][1];
            B[RowStartPos[j]][0] = S_Mat[i][1];
            B[RowStartPos[j]][1] = S_Mat[i][0];
            B[RowStartPos[j]][2] = S_Mat[i][2];
            RowStartPos[j] = RowStartPos[j] + 1;
        }
    }
    return B;
}
```

在此程序中，最初确定每个列中的元素数量。这些实际上将是转置矩阵中的列数。这些信息帮助我们更新数组 RowStartPos，它告诉我们应该从转置数组中的哪个位置开始存储元素，以便它们按行排序。

## 2.12 使用数组进行字符串操作

字符串是最常用的数据对象。它通常由编程语言的字符集构成。假设 S = a1, a2, ..., an。

值 n 是字符串 S 的长度，其中 n >= 0。如果 n = 0，则 S 称为空字符串或空串。可以对字符串执行各种操作：

- 1. 查找字符串长度
- 2. 连接两个字符串
- 3. 复制字符串
- 4. 反转字符串
- 5. 执行字符串比较
- 6. 回文检查
- 7. 识别子字符串。

这些使用数组的操作将在后续章节中详细讨论。

基本上，字符串作为字符序列存储在一维字符数组中，例如 A（图 2.36）。

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| A = | S | T | R | I | N | G | \0 | - | - | - |

Fig. 2.36 数组中存储的字符串

将 'String' 存储在大小为 10 的数组中的简单 C++ 语句如下：

```
char A[10] = "STRING";
```

每个字符串由一个特殊字符终止，即空字符 '\0'。这个空字符指示每个字符串的结束或终止。程序代码 2.12 中的 compare() 函数比较两个字符串以判断它们是否相等。

要比较两个字符串，我们首先检查它们的长度是否相同。如果长度相同，那么字符串相同的可能性就更大。如果长度已预先计算或已知，则需要比较长度，否则这会增加复杂度。然后，我们将字符串 A 的每个字符与字符串 B 进行比较。如果匹配，则字符串相同；否则不同。

### 程序代码 2.12

```
class String
{
  private:
    char Str[];
  public:
    String() {}
    int Length();
    void Concat(String B);
    int Substring(String S);
};

int String::Length()
{
  int length = 0, i;
  for(i = 0; Str[i] != '\0'; i++)
    length++;
  return length;
}

void String::Concat(String B)
{
  int len_A, i, j;
  // To concatenate B to A we need to traverse
  // string A till the end
  for(i = 0; Str[i] != '\0'; i++);
  len_A = i;
  // Let us concatenate B to A now
  for(i = len_A, j = 0; B.Str[j] != '\0'; j++,i++)
  {
    Str[i] = B.Str[j];
  }
  Str[i] = '\0';
}

String String::Copy()
{
  String B;
  int i;
  for(i = 0; Str[i] != '\0'; i++)
  B.Str[i] = Str[i];
  B.Str[i] = '\0'; // Append the termination character
  return B;
}

String String::Copy_Reverse()
{
  int i, l, Len_A, j;
  for(i = 0; Str[i] != '\0'; i++);
  // loop terminates after reaching end of A
  Len_A = l--;
  for(i = l, j = 0; i >= 0; i--, j++)
  B.Str[j] = Str[i];
  B.Str[j] = '\0'; //Append termination character
  return B;
}

void String::Rev_String()
{
  int i, len = 0;
  //exchange i^th and j^th characters till middle position
  char t;
  for(len = 0; Str[len] != '\0'; len++);
  for(i = 0, j = len - 1; i != j; i++, j--)
  {
    t = Str[i]; Str[i] = Str[j]; Str[j] = t;
  }
}

int String::Str_cmp(String A, String B)
{
  int i = 0;
  if (A.Length() != B.Length())
    return 0;
  while (A.Str[i] == B.Str[i] && A.Str[i] != '\0' && B.Str[i] != '\0')
    ++i;
  if(A.Str[i] == '\0' && B.Str[i] == '\0')
    return 1;
  else
    return 0;
}
```

### 回文检查

回文是正向和反向读取都相同的字符串。例如，_madam_ 和 _malayalam_ 是回文（图 2.37）。

![](img/a99ec79093c067f0bed8f1086197950e_99_0.png)

Fig. 2.37 回文检查

要检查字符串是否为回文，有两种方法：

- 1. 我们先求出字符串的逆序，然后将其与原字符串进行比较。如果匹配，则该字符串是回文；否则不是。如果字符串长度为 _n_，此方法需要 _n_ 次比较，并需要一个额外数组来存储逆序字符串。
- 2. 另一种方法不需要 _n_ 次比较，只需 _n_/2 次比较。我们可以将第一个字符与最后一个字符比较。如果匹配，则再将第二个字符与倒数第二个字符比较。继续此过程直到字符串中间。我们可以从两端设置两个索引，并比较直到索引不重叠。字符不匹配表明该字符串不是回文。此方法不需要额外的数据结构。

检查回文的程序在程序代码 2.13 中给出。

### 程序代码 2.13

```
int String::Palindrome_Check()
{
    int i, j, l, flag = 0, k;
    for(l = 0; Str[l] != '\0'; l++); //loop terminates
    l--; k = l/2; //to avoid null char
    for(i = 0; j = l; i < k; i++, j--)
    {
        if(Str[i] == Str[j])
        {
            flag = 1;
            continue;
        }
        else
        {
            flag = 0;
            break;
        }
    }
    if(flag == 1)
        return 0;
    else
        return 1;
}
```

### 子字符串检查

对于子字符串识别，我们将查找字符串 B 在字符串 A 中的出现情况。

例如，

```
A = 'A B C D'
B = 'BC' or 'BCD' and so on
```

有两种可能性：

- 1. 要么 B 是 A 的子字符串，或
- 2. B 不是 A 的子字符串。

程序代码 2.14 检查给定字符串是否为子字符串。

### 程序代码 2.14

```
int String::substring(String B)
{
    int i, j = 0, flag = 0;
    for(i = 0; A.Str[i] != '\0' || B.Str[j] != '\0'; i++)
    {
        if(A.Str[i] == B.Str[j])
        {
            j++;
            flag = 1;
        }
        else
        {
            j = 0;
            flag = 0;
        }
    }
}
```

