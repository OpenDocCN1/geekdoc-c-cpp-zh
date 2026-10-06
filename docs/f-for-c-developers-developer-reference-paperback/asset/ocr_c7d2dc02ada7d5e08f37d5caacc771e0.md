Note In C#, you can use the new modifier to explicitly hide a member inherited from a base class. F# does not need to use the new keyword. F# by default hides members from base class unless the override keyword is used.

Also, sprintf provides the same functionality as String.Format. sprintf requires the pattern specify the data type, as %d for integer ,and it also supports %O and %A, which accept any data type and convert values to string as String.Format. Additionally, sprintfn does not support a pass-pattern string as parameter, as sprintfn myPattern 1.

Another concept in object-oriented programming is inheritance. In a moment, I'll describe how implement inheritance in F#.

# Using a Special/Reserved Member Name

The variable name in F# can be a keyword and supports space and other special characters. You can use these special strings or characters to define the class member name as well. Listing 2-28 shows sample.

**LISTING 2-28** Using special characters and keywords in a class member definition

```
let f =
  let `else` = 99
  let `end` = 100
  let `F#` = 101
  let `my value` = 102
  let `let` = 103
()
ntype MyClass() = class
  member val `else` = 0 with get, set
  member val `end` = 0 with get, set
  member val `F#` = 0 with get, set
  member val `My Value` = 0 with get, set
  member val `let` = 0 with get, set
end

let myValue = MyClass()

printfn "put break point here"
```