```
[ for (substring:string) in subList do
  for i = 0 to substring.Length do
    let resultString = substring.Insert(i, string ch)
  yield resultString]
```

permute "abcd"

Execution result from FSI
val it : string list =
["abcd"; "bad"; "bcad"; "bcda"; "acbd"; "cad"; "cbad"; "cbda"; "acbd";
"cdb"; "cdab"; "abcd"; "badc"; "bdac"; "bdca"; "adbc"; "dabc";
"dbac"; "dbca"; "acdb"; "dcab"; "dcba"]

**String interleaving** String interleaving is a restricted permutation. An interleaved string of two strings keeps the order of the characters in the strings. If two given strings are "a" and "bc", "abc", and "bac" are valid interleaving results, but "cba" is not because the "cb" is in the wrong order. The code to implement string interleaving is shown in Listing 7-37.

# LISTING 7-37 String interleaving

```
open System
let ( AllEmpty | StrNotEmpty | StrNotEmpty | Both | ) (str0, str1) =
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
  let rec = interleaving str0 str1 current =
    match str0, str1 with
    | AllEmpty _ -> ()
    | StrNotEmpty _ -> add (current+str1)
    | StrNotEmpty -> add (current+str0)
    | Both ->
      interleavingStrs (str0.Substring(1)) str1 (current + string str0.[0])
      interleavingStrs str0 (str1.Substring(1)) (current + string str1.[0])

  interleavingStrs str0 str1 ""

interleaving "ab" "cd"
```