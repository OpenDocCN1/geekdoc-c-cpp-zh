# TABLE 25-3: String and Character Literals

| EXAMPLE | F# TYPE | DESCRIPTION |
| --- | --- | --- |
| "Hello World!" | string | Ordinary string |
| "This is a line\nAnd another\n" | string | String with escape characters |
| @"c:\Program Files\" | string | Verbatim string |
| "This is a multi-line \ comment." | string | Multi-line string |
| "1234567890ABC" | byte array | Literal byte array |
| '0' | char | Character |
| '\n' | char | Escape character |

In addition to the static System.String members, the F# standard library provides the Microsoft .FSharp.Core.String module contains a number of additional convenient operations on strings. These are summarized in Table 25-4.

# TABLE 25-4: Static Members in the F# String Module

| MEMBER | TYPE | DESCRIPTION |
| --- | --- | --- |
| collect | (char -> string) -> string | Maps each character of a string to build another by concatenating the resulting strings |
| concat | string -> seq<string> -> string | Concatenates the given strings using the separator string in elements |
| exists | (char -> bool) -> string | Checks whether any character of the string satisfies the given predicate |
| forall | (char -> bool) -> string ->bool | Tests all characters of the string satisfy the given predicate |
| init | int -> (int -> string) -> string | Builds a new string by concatenating the results of the function applied to values from 0 to the number |
| iter | (char -> unit) -> string | Applies the function to each character of the string |
| iteri | (int -> char -> unit) -> string -> unit | Applies the function to each character and their position indexes in the string.