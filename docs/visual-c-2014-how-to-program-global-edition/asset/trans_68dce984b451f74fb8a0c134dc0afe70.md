

## 16.6 在字符串中定位字符和子字符串 717

```csharp
// test LastIndexOf to find a character in a string
Console.WriteLine("'c' is located at index " + \
letters.LastIndexOf('c'));
Console.WriteLine("'a' up to position 25 is located at " + \
"Index " + letters.LastIndexOf('a', 25));
Console.WriteLine("'s' in the 5 positions ending at 15 " + \
"located at index " + letters.LastIndexOf("$s", 15, 5));
```

```csharp
// test IndexOf to find a substring in a string
Console.WriteLine("'def' is located at index " + \
letters.IndexOf("def"));
Console.WriteLine("First'def' starting at 7 is located at " + \
"index " + letters.IndexOf("def", 7));
Console.WriteLine("hello' in the 15 positions " + \
"starting at 5 is located at index " + \
letters.IndexOf("hello", 5, 15));
```

```csharp
// test LastIndexOf to find a substring in a string
Console.WriteLine("'def' is located at index " + \
letters.IndexOf("def"));
Console.WriteLine("'def' up to position 25 is located at " + \
"at index " + letters.LastIndexOf("def", 25));
Console.WriteLine("hello' in the 15 positions " + \
"ending at 20 is located at index " + \
letters.LastIndexOf("hello", 20, 15));
```

```csharp
// test IndexOfAny to find first occurrence of character in array
Console.WriteLine("'c', 'a' or 's' is " + \
"located at index " + letters.IndexOfAny(searchLetters));
Console.WriteLine("'c', 'a' or 's' starting at 7 is " + \
"located at index " + letters.IndexOfAny(searchLetters, 7));
Console.WriteLine("'c', 'a' or 's' in the 5 positions " + \
"starting at 7 is located at index " + \
letters.IndexOfAny(searchLetters, 7, 5));
```

```csharp
// test IndexOfAny to find last occurrence of character
// in array
Console.WriteLine("'c', 'a' or 's' is " + \
"located at index " + letters.LastIndexOfAny(searchLetters));
Console.WriteLine("'c', 'a' or 's' up to position 1 is " + \
"located at index " + letters.LastIndexOfAny(searchLetters, 1));
Console.WriteLine("'c', 'a' or 's' in the 5 positions " + \
"ending at 25 is located at index " + \
letters.LastIndexOfAny(searchLetters, 25, 5));
```

第一个 'c' 位于索引 2
从 7 开始的第一个 'a' 位于索引 -1
从 3 开始的 5 个位置中的第一个 '$s' 位于索引 -1 

![](img/57baed2319be0bb1b5f98674846f2711_717_0.png)

# 第 16 章 字符串与字符：深入探讨

最后一个 'c' 位于索引 15
位置 25 之前的最后一个 'a' 位于索引 13
以 15结束的 5 个位置中的最后一个 '$' 位于索引 -1

第一个 'def' 位于索引 3
从 7 开始的第一个 'def' 位于索引 16
从 5 开始的 15 个位置中的第一个 'hello' 位于索引 -1

最后一个 'def' 位于索引 16
位置 25 之前的最后一个 'def' 位于索引 16
以 20结束的 15 个位置中的最后一个 'hello' 位于索引 -1

第一个 'c'、'a' 或 '$' 位于索引 0
从 7 开始的第一个 'c'、'a' 或 '$' 位于索引 13
从 7 开始的 5 个位置中的第一个 'c'、'a' 或 '$' 位于索引 -1

最后一个 'c'、'a' 或 '$' 位于索引 15
位置 1 之前的最后一个 'c'、'a' 或 '$' 位于索引 0
以 25结束的 5 个位置中的最后一个 'c'、'a' 或 '$' 位于索引 -1

**图 16.5** | 在字符串中搜索字符和子字符串。（3 部分中的第 3 部分）

第 14、16 和 18 行使用 `IndexOf` 方法来定位字符串中字符或子字符串的首次出现。如果找到了，`indexOf` 将返回该字符在字符串中的索引；否则，`indexOf` 返回 -1。第 16 行使用了带有两个参数的 `IndexOf` 方法——要搜索的字符以及起始索引。该方法不会检查起始索引之前的任何字符（在本例中为 1）。第 18 行使用了带有三个参数的 `IndexOf` 方法——要搜索的字符、开始搜索的索引以及要搜索的字符数。

第 22 和 24 行使用 `LastIndexOf` 方法来定位字符串中字符的最后出现。如果找到了，`LastIndexOf` 将返回该字符在字符串中的索引；否则，`LastIndexOf` 返回 -1。`LastIndexOf` 方法有三个版本。第 22 行使用了接受一个参数的版本——要搜索的字符。第 24 行使用了带有两个参数的版本——要搜索的字符以及起始索引。

