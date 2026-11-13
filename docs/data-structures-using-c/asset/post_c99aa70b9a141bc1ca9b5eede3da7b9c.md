
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

Fig. 2.35 Storing column as row in fast Transpose (a) Input matrix B (b) Freq[] (c) RowStartPos[] (d) B^T

### Time and Space Complexity Analysis of Fast Transpose

There are three loops in Algorithm 2.4, which are executed n (no. of rows), τ (no. of non-zero members), n - 1, and τ times, respectively, resulting in overall time complexity O(n + τ).

In the worst case, that is, when τ = m × n (non-zero elements), the magnitude becomes O(n + mn) = O(mn), which is the same as the conventional 2D transpose. However, the constant factor associated with fast transpose is quite high. When τ is sufficiently small compared to its maximum of m × n, fast transpose works faster.

As compared to simple transpose, time is saved but an extra space for two one-dimensional arrays Freq and RowStartPos are required for the fast transpose. Program Code 2.11 implements the sparse matrix fast transpose.

### PROGRAM CODE 2.11

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

In this program, the number of elements in each column is determined initially. These are actually going to be the number of columns in the transposed matrix. This information helps us update the array RowStartPos, which tells us from where we should start storing elements in the transposed array so that they are row wise sorted.

## 2.12 STRING MANIPULATION USING ARRAY

String is the most commonly used data object. It is usually formed from the character set of the programming language. Suppose S = a1, a2, ..., an.

The value n is the length of the character string S, where n >= 0. If n = 0, then S is called a null string or empty string. There are various operations that can be performed on the string:

- 1. Finding the length of a string
- 2. Concatenating two strings
- 3. Copying a string
- 4. Reversing a string
- 5. Performing string compare
- 6. Palindrome check
- 7. Recognizing a sub string.

These operations using arrays are discussed in detail in the sections that follow.

Basically, a string is stored as a sequence of characters in a one-dimensional character array, say A (Fig. 2.36).

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| A = | S | T | R | I | N | G | \0 | - | - | - |

Fig. 2.36 String stored in array

The simple C++ statement for storing 'String' in an array of size 10 is as follows:

```
char A[10] = "STRING";
```

Each string is terminated by a special character, that is, null character '\0'. This null character indicates the end or termination of each string. The function compare() in Program Code 2.12 compares two strings to find whether they are equal.

To compare two strings, we first check whether their lengths are the same. If the lengths are the same, then there is a further possibility that the strings are the same. The lengths are to be compared if they have been precomputed or are known, else this adds to the complexity. Then, we compare each character of string A with string B. If they match, then the strings are the same; else they are not.

### PROGRAM CODE 2.12

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

### Palindrome check

Palindrome is a string that reads the same in forward and backward directions. For example, _madam_ and _malayalam_ are palindromes (Fig. 2.37).

![](img/a99ec79093c067f0bed8f1086197950e_99_0.png)

Fig. 2.37 Palindrome check

To check whether the string is a palindrome or not, there are two approaches:

- 1. We first find the reverse of the string and then compare it with the original string. If they match, then the string is a palindrome; otherwise, it is not. This approach needs _n_ comparisons if the string length is _n_ and an additional array to store the reversed string.
- 2. The other approach does not need _n_ comparisons but just _n_/2 comparisons. We can compare the first character with the last. If they match, then again match the second character with the second last. Continue this process till the middle of the string. We can set two indices from both the ends and compare till the indices do not overlap. The mismatch of characters indicates that the string is not a palindrome. This approach does not need an additional data structure.

The program for checking a palindrome is given in Program Code 2.13.

### PROGRAM CODE 2.13

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

### Substring check

For substring recognition, we will find the occurrence of string B in string A.

For example,

```
A = 'A B C D'
B = 'BC' or 'BCD' and so on
```

There are two possibilities:

- 1. Either B is a substring of A or
- 2. B is not a substring of A.

Program Code 2.14 checks if a given string is a substring or not.

### PROGRAM CODE 2.14

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
