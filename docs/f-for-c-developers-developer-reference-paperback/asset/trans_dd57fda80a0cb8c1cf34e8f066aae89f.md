

```fsharp
let mutable result = System.String.Empty

for i = 0 to str.Length - 1
  let subStr = str[..str.Length - 2]
  for explore = i + 1 to str.Length - 1
    let strToCheck = str[..explore]
    if isStringPalindrome(strToCheck) then
      let result = if result.Length > strToCheck.Length then result else strToCheck

printf("%s", result)

getPalindrome "abab"
getPalindrome "sambambiv"
getPalindrome "aa"
getPalindrome "aaa"
getPalindrome "yabadabadooo"

执行结果
bab
mabm
aa
aaa
abadaba

> 注意 后缀树是解决此问题的更高效的方法。你可以在网络上通过 http://en.wikipedia.org/wiki/Suffix_tree 找到相关材料。

## 字符串的排列 

列表 7-36 显示了如何获取字符串的所有排列组合。例如，字符串 "abc" 的排列将是 "abc"向acb","bca","bac","cab" 和 "cba"。

### 列表 7-36 字符串的排列

```fsharp
open System
let rec permute(str:string) =
  let chList =
    str
    |> List.ofSeq
  match chList with
    [] -> []
    [ch] -> [string ch]
    head::tail ->
      let ch = head
      let tail = String.Join("", tail)
      let subStringList = permute tail
      [ for (substring:string) in subList do
        for i = 0 to substring.Length do
          let resultString = substring.Insert(i, string ch)
          yield resultString]

permute "abcd"

来自 FSI执行结果
val it : string list =
["abcd"; "bad"; "bcad"; "bcda"; "acbd"; "cad"; "cbad"; "cbda"; "acbd";
"cdb"; "cdab"; "abcd"; "badc"; "bdac"; "bdca"; "adbc"; "dabc";
"dbac"; "dbca"; "acdb"; "dcab"; "dcba"]
```

**字符串交错** 字符串交错是一种受限的排列。两个字符串的交错字符串保持原有字符串中字符的顺序。如果给定的字符串是 "a" 和 "bc"，那么 "abc" 和 "bac" 是有效的交错结果，但 "cba" 不是，因为 "cb" 的顺序不对。实现字符串交错的代码在列表 7-37 中。

### 列表 7-37 字符串交错

```fsharp
open System
let ( AllEmpty | StrNotEmpty | Both ) (str0, str1) =
  let b0 = String.IsNullOrEmpty(str0)
  let b1 = String.IsNullOrEmpty(str1)
  match b0, b1 with
  | true, true -> AllEmpty
  | false, true -> StrNotEmpty
  | true, false -> StrNotEmpty
  | false, false -> Both

  let mutable result = []
  let add x =
    result <- result @ [x]

  let interleaving str0 str1 =
    let rec interleaving str0 str1 current =
      match str0, str1 with
      | AllEmpty _ -> ()
      | StrNotEmpty _ -> add (current+str1)
      | StrNotEmpty -> add (current+str0)
      | Both ->
        interleavingStrs (str0.Substring(1)) str1 (current + string str0.[0])
        interleavingStrs str0 (str1.Substring(1)) (current + string str1.[0])

    interleavingStrs str0 str1 ""

interleaving "ab" "cd"

在 FSI 中的执行结果

> result;
val it : string list = ["abcd"; "acbd"; "acbd"; "cabd"; "cadb"; "cdab"]
```

KMP 假设你有两个字符串，并且你想找到目标字符串的所有出现位置。KMP 字符串搜索算法是一种你可以用来实现此目的的算法。搜索复杂度为 O(n)，其中 n 是字符串的长度。除了演示算法外，代码还展示了如何使用 F# 记录（record）、类型别名和扩展方法。还要注意 match 语句的使用，其中分支逻辑完全通过 'when' 实现；所有模式的守卫符均为 '_'。示例代码在列表 7-38 中。

### 列表 7-38 KMP 字符串搜索算法

```fsharp
type List = System.Collections.Generic.List<int>

let kmp (w: string) =
  let t = List([1..w.Length])
  let mutable pos = 2
  let mutable cnd = 0
  t[0] <- -1
  t[1] <- 0

  while pos < w.Length do
    match pos cnd with
    | when w.[pos - 1] = w.[cnd]
      cnd <- cnd + 1
    | t.[pos] < cnd
      pos <- pos + 1
    | when cnd > 0 ->
      cnd <- t[cnd]
    | ->
      t.[pos] <- 0
      pos <- pos + 1

  let t | List.ofSeq

type ResultType =
  { mutable Result : int; mutable Found : bool }
  with
    member this.Set
```
