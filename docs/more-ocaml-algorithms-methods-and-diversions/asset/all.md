![](images/calibre_cover.jpg)

MORE OCAML  Algorithms, Methods & Diversions

In More OCaml John Whitington takes a meandering tour of functional programming with OCaml, introducing various language features and describing some classic algorithms. The book ends with a large worked example dealing with the production of PDF files. There are questions for each chapter together with worked answers and hints.

More OCaml will appeal both to existing OCaml programmers who wish to brush up their skills, and to experienced programmers eager to explore functional languages such as OCaml. It is hoped that each reader will find something new, or see an old thing in a new light. For the more casual reader, or those who are used to a different functional language, a summary of basic OCaml is provided at the front of the book.

JOHN WHITINGTON founded a software company which uses OCaml extensively. He teaches functional programming to students of Computer Science at the University of Cambridge. His other books include “PDF Explained” (O’Reilly, 2012) and “OCaml from the Very Beginning” (Coherent, 2013).

> MORE OCAML
> Algorithms, Methods & Diversions

> John Whitington

> C O H E R E N T   P R E S S

> C O H E R E N T    P R E S S
> Cambridge

> Published in the United Kingdom by Coherent Press, Cambridge

> Ⓒ Coherent Press 2014
> This publication is in copyright. Subject to statutory
> exception no reproduction of any part may take place
> without the written permission of Coherent Press.
>  
> First published August 2014

> A catalogue record for this book is available from the British Library
>  
> by the same author
> PDF Explained (O’Reilly, 2012)
> OCaml from the Very Beginning (Coherent, 2013)

Contents

[Summary of Basic OCaml](#index_split_005.html_filepos10461)
[Our Working Environment](#index_split_006.html_filepos35604)
1 [Unravelling “Fold”](#index_split_007.html_filepos42586)
2 [Being Lazy](#index_split_008.html_filepos58917)
3 [Named Tuples with Records](#index_split_009.html_filepos73521)
4 [Generalized Input/Output](#index_split_010.html_filepos85748)
5 [Streams of Bits](#index_split_011.html_filepos100097)
6 [Compressing Data](#index_split_012.html_filepos116762)
7 [Labelled and Optional Arguments](#index_split_013.html_filepos147180)
8 [Formatted Printing](#index_split_014.html_filepos163032)
9 [Searching for Things](#index_split_015.html_filepos174919)
10 [Finding Permutations](#index_split_016.html_filepos191331)
11 [Making Sets](#index_split_017.html_filepos210405)
12 [Playing Games](#index_split_018.html_filepos237292)
[GENERATING PDF DOCUMENTS - AN EXTENDED EXAMPLE](#index_split_018.html_filepos248699)
13 [Representing Documents](#index_split_020.html_filepos249424)
14 [Writing Documents](#index_split_021.html_filepos263669)
15 [Pretty Pictures](#index_split_022.html_filepos282420)
16 [Adding Text](#index_split_023.html_filepos291403)
A [Answers to Questions](#index_split_024.html_filepos308584)
A [Hints for Questions](#index_split_025.html_filepos412178)
A [Coping with Errors](#index_split_026.html_filepos437648)
[Index](#index_split_026.html_filepos453073)

Preface

When I wrote “OCaml from the Very Beginning”, the intention was to have a book with no prerequisites – a bright individual, new to programming, could follow it. Because of this, and for length concerns, plenty of interesting material had to be omitted. This text, not being constrained in the same way, contains a variety of topics which require some existing experience with a functional language. Those who have read the previous text should have no problem with this one. Equally, it should be comprehensible to a functional programmer familiar with another language such as Standard ML or Haskell. The reader may need to make occasional reference to the OCaml manual.

There are, typically, two different activities when writing programs larger than a few dozen lines: firstly, dealing with the challenges of complexity inherent in the problem, by finding appropriate abstraction mechanisms and, secondly, finding and using the wide range of third-party libraries available for a given language. Most projects involve a combination of the two. In this text we concentrate wholly on the former, using nothing other than the OCaml Standard Library. Keeping up with the myriad third-party OCaml libraries is a task better suited to other media.

The book consists of sixteen short chapters falling broadly into three categories. Some introduce pieces of OCaml syntax with worked examples. Some survey practical topics such as input/output. Some cover little diversions or puzzles. The main matter of the book ends with a lengthy worked example: a program to build PDF files containing computer-generated drawings and text. There are full answers and hints for all questions in the book, and additional material in the online resources.

Acknowledgments

The quotation in Chapter 6 is taken from ISO-32000 Ⓒ International Organization for Standardization. The tables of codes in the same chapter are taken from ITU-T T.30 Ⓒ International Telecommunication Union. The presentation of the balancing operation for Red-Black trees in Chapter 11 and its functional implementation is due to Chris Okasaki, as described in the invaluable “Purely Functional Data Structures” (Cambridge University Press, ISBN 978-0521663502, 1998). Chapter 12 was inspired by a University of Cambridge Computer Science Tripos exam question set by Lawrence C. Paulson in 1999\. Question 3 of that chapter is due to Peter D. Schumer in “Mathematical Journeys” (John Wiley & Sons, ISBN 0-471-22066-3, 2004).

I am grateful to the many colleagues and friends with whom I have been able to discuss OCaml style and substance, including Mark Shinwell, Leo White, Daniel Bünzli, Anil Madhavapeddy, Stephen Dolan and many others whom I have forgotten. Helpful comments on an earlier draft were provided by Stefan Schmiedl, Manuel Cornes, Jonas Bülow, Emmanuel Delaborde, Mario Alvarez Picallo, Giannis Tsaraias, Emmanuel Oga, and André Bjärby.

Summary of Basic OCaml

This chapter contains a summary of each OCaml construct used in the book, together with some examples. Pieces of OCaml syntax not contained in this chapter will be introduced as and when they are needed throughout the rest of the book. Existing OCaml programmers may skip this chapter.

Simple Data Types

Integers `min_int` … `-3` `-2` `-1` `0` `1` `2` `3` … `max_int` of type int. Booleans `true` and `false` of type bool. Characters of type char like `'X'` and `'!'`.

Mathematical operators `+ - * / mod` which take two integers and give another.

![](images/00068.jpg)

Operators  `=  <  <=  >  >=  <>` which compare two values and evaluate to either `true` or `false`.

![](images/00125.jpg)

The conditional `if` expression1 `then` expression2 `else` expression3, where expresssion1 has type bool and expression2 and expression3 have the same type as one another.

![](images/00146.jpg)

The boolean operators `&&` (logical AND) and `||` (logical OR) which allow us to build compound boolean expressions.

![](images/00243.jpg)

Tuples to combine a fixed number of elements `(a, b)`,  `(a, b, c)` etc. with types α × β,  α × β × γ etc. For example, `(1, '1')` is a tuple of type int × char. On the screen, OCaml writes `'a` for α etc.

Strings, which are sequences of characters written between double quotes and are of type string. For example, `"one"` has type string.

Names and Functions

Assigning a name to the result of evaluating an expression using the `let` name `=` expression construct.

`let x = 5 > 2` x is new, and is `false`

Building compound expressions using `let` name1 `=` expression1 `in` `let` name2 `=` expression2 `in` …

`let x = 4 in let y = 5 in x + y`

Anonymous (un-named) functions `fun` name `->` expression.

![](images/00095.jpg)

Making operators into functions as in `( < )` and `( + )`.

`( + ) 1 2` ![](images/00227.jpg)`3`

Functions, introduced by `let` name argument1 argument2 … `=` expression. These have type α → β, α → β → γ etc. for some types α, β, γ etc. For example, `let f a b = a > b` is a function of type α → α → bool.

Recursive functions, which are introduced in the same way, but using `let rec` instead of `let`. For example, here is a function `g` which calculates the smallest power of two greater than or equal to a given positive integer, using the recursive function `f`:

`let rec f x y =`
`  if y < x then f x (2 * y) else y`

`let g z = f z 1`

Mutually recursive functions, introduced by writing `let rec f x = …  and g y = … and …`

Pattern Matching

Matching patterns using `match` expression1 `with` pattern1 `|` … `->` expression2 `|` pattern2 `|` … `->` expression3 `|`…The expressions expression2, expression3 etc. must have the same type as one another, and this is the type of the whole `match` … `with` expression. The special pattern `_` which matches anything.

`match x with`
`  0 -> 1`
`| 1 | 2 -> 3`
`| _ -> 4`

Matching two or more things at once, using commas to separate as in `match a, b with 0, 0 ->` expression1 `| x, y ->`  expression2 `|` …

`match x, y, z with`
`  0, 0, 0 -> true`
`| _, _, _ -> false`

Lists

Lists, which are ordered collections of zero or more elements of like type. They are written between square brackets, with elements separated by semicolons e.g. `[1; 2; 3; 4; 5]`. If a list is non-empty, it has a head, which is its first element, and a tail, which is the list composed of the rest of the elements.

The `::`“cons” operator, which adds an element to the front of a list. The `@` “append” operator, which concatenates two lists together.

`1 :: [2; 3]` ![](images/00218.jpg)`[1; 2; 3]`
`[1; 2] @ [3]` ![](images/00034.jpg)`[1; 2; 3]`

Lists and the `::` “cons” symbol may be used for pattern matching to distinguish lists of length zero, one, etc. and with particular contents. For example, we can calculate the length of a list:

`let rec length l =`
`  match l with`
`    [] -> 0`
`  | _::t -> 1 + length t`

Exceptions

Defining exceptions with `exception` name. They can carry extra information by adding `of` type. Raising exceptions with `raise`. Handling exceptions with `try` … `with` …

`exception Problem of int`

`let f x y =`
`  if y = 0`
`    then raise (Problem x)`
`    else x / y`

`let g x y =`
`  try f x y with Problem p -> p`

Partial Application

Partial application of functions by giving fewer than the full number of arguments. Partial application with functions built from operators.

`let add x y = x + y`

`List.map (add 3) [1; 2; 3]`
![](images/00008.jpg)`[4; 5; 6]`

`List.map (( + ) 3) [1; 2; 3]`
![](images/00054.jpg)`[4; 5; 6]`

New Data Types

New types with `type` name `=` constructor1 `of` type1 `|` constructor2 `of` type2 `|` … Pattern matching on them as with the built-in types. Polymorphic types.

`type colour =`
`  Red | Blue | Green | Grey of int`

`[Red; Blue; Grey 16]` this has type colour list

`type 'a tree =`
`   Lf`
`| Br of 'a tree * 'a * 'a tree`

For example, `Br (Lf, 'X', Br (Lf, 'Y', Lf))` has type char tree. A useful built-in data type is the option type, defined as `type 'a option = None | Some of 'a`. A type can be polymorphic in more than one type parameter, for example `('a, 'b) Hashtbl.t`, as in the Standard Library.

Basic Input / Output

The value `()` and its type unit. Input channels of type in_channel and output channels of type out_channel. Built-in functions such as `open_in`, `close_in`, `open_out`, `close_out`, `input_char`, `output_char` etc. for reading from and writing to them respectively.

Mutable State

References of type α ref. Building them using `ref`, accessing their contents using `!` and updating them using the `:=` operator.

`# let p = ref 0;;  `
`val p : int ref = {contents = 0}  `
`# p := 5;;  `
`- : unit = ()  `
`# !p;;  `
`- : int = 5`

Arrays of type α array written like `[|1; 2; 3|]`. Creating an array with the built-in function `Array.make`, finding its length with `Array.length`, accessing an element with `a.(`subscript`)`. Updating with `a.(`subscript`)` `<-` expression.

`let swap a x y =`
`  let t = a.(x) in`
`    a.(x) <- a.(y); a.(y) <- t`

Bracketing expressions together with `begin` and `end` instead of parentheses for readability.

`if x = y then`
`  begin`
`    a := b;`
`    c := d`
`  end`
`else`
`  e := f`

Performing an action many times based on a boolean condition with the `while` boolean expression `do` expression `done` construct.

`while !x < y do x := !x * 2 done`

Performing an action a fixed number of times with a varying parameter using the `for` name `=` start `to` end `do` expression `done` construct.

`for x = 1 to 10 do print_int x done`

Floating-point Numbers

Floating-point numbers `min_float` … `max_float` of type float. Floating-point operators `+. *. -. /. **` and built-in functions `sqrt log` etc.

`2. ** 0.2` ![](images/00299.jpg)`1.1486983549970351`

The OCaml Standard Library

Using functions from the OCaml Standard Library with the form Module`.`function. For example, `List.map`, `String.length`, `Array.copy` etc. The Buffer module allows the efficient collation of strings into larger ones.

Simple Modules

Writing modules in `.ml` files. Building interfaces in `.mli` files with types and the `val` keyword. For example, the `.ml` file with contents `let f x = x + 1` might have the interface `val f : int ->` `int`

Compiling Programs

The `ocamlc` and `ocamlopt` compilers. For example:

`ocamlc -o x x.ml` builds `x` (or `x.exe`) from `x.ml` with the bytecode compiler.

`ocamlopt -o x x.ml` builds `x` (or `x.exe`) from `x.ml` with the native code compiler.

Our Working Environment

Every piece of code in an example, and every answer to an end-of-chapter question can be downloaded from the book’s website at [`http://www.ocaml-book.com/`](http://www.ocaml-book.com/) and built on the reader’s machine. The programs should work on Unix (including Linux), Mac OS X, and Microsoft Windows.

Since several of our programs require tail-recursive list functions, we provide a wrapper to the Standard Library List module which provides them. In addition, three small utility functions (`take`, `drop`, and `from`) are provided in a Util module. These modules are contained in the module More. So, by writing `open More`, the Util module is available, and all functions in the List module are tail-recursive.

If using OPAM, the OCaml Package Manager, this package may be installed by writing `opam install` `more-ocaml`. Then (or by installing in another manner – see the online resources for details) our modules are available in the top level:

`        OCaml  `

`# #use "topfind";;  `
`- : unit = ()  `
`Findlib has been successfully loaded. Additional directives:  `
`  #require "package";;      to load a package  `
`  #list;;                   to list the available packages  `
`  #camlp4o;;                to load camlp4 (standard syntax)  `
`  #camlp4r;;                to load camlp4 (revised syntax)  `
`  #predicates "p,q,...";;   to set these predicates  `
`  Topfind.reset();;         to force that packages will be reloaded  `
`  #thread;;                 to enable threads  `

`- : unit = ()  `
`# #require "more";;  `
`/Users/john/.opam/4.02.0/lib/ocaml/more.cma: loaded  `
`/Users/john/.opam/4.02.0/lib/more: added to search path  `
`# open More;;  `
`# Util.take;;  `
`- : 'a list -> int -> 'a list = <fun>`

They are also available when compiling stand-alone programs with the bytecode compiler `ocamlc` or the native code compiler `ocamlopt`:

`ocamlfind ocamlc -package more program.ml -linkpkg -o program  `
`ocamlfind ocamlopt -package more program.ml -linkpkg -o program`

Further instructions, including for use on platforms where OPAM is not supported, are given in the online resources.

Timing with the Unix module

Sometimes we will wish to see how much time a piece of code takes. This can be achieved using the function `gettimeofday` from the Unix module (contrary to its name, this module also works on Windows). This function returns a floating-point number representing the time since 00:00:00 GMT, Jan. 1, 1970, in seconds:

`        OCaml  `

`# #use "topfind";;  `
`- : unit = ()  `
`Findlib has been successfully loaded. Additional directives:  `
`  #require "package";;      to load a package  `
`  #list;;                   to list the available packages  `
`  #camlp4o;;                to load camlp4 (standard syntax)  `
`  #camlp4r;;                to load camlp4 (revised syntax)  `
`  #predicates "p,q,...";;   to set these predicates  `
`  Topfind.reset();;         to force that packages will be reloaded  `
`  #thread;;                 to enable threads  `

`- : unit = ()  `
`# #require "unix";;  `
`/Users/john/.opam/4.01.0/lib/ocaml/unix.cma: loaded  `
`# Unix.gettimeofday ();;  `
`- : float = 1407679005.43897  `
`# Unix.gettimeofday ();;  `
`- : float = 1407679011.08860302`

Now, by evaluating `Unix.gettimeofday ()`, running a piece of code, and evaluating `Unix.gettimeofday ()` once more, we can calculate the elapsed time. To use the Unix module when compiling stand-alone programs:

`ocamlfind ocamlc -package more,unix program.ml -linkpkg -o program  `
`ocamlfind ocamlopt -package more,unix program.ml -linkpkg -o program`

Chapter 1
Unravelling “Fold”

The List module in OCaml’s Standard Library defines two intriguingly-named functions over lists:

> ![](images/00056.jpg)

What do they do? And why are they considered important enough to include in the Standard Library? As we shall see, they abstract the idea of recursion over lists with an accumulator in a most delightfully generic way.

Let us first examine `fold_left` and its rather complicated type. The first argument is itself a function, which takes the existing accumulator and an element from the input list, combines them in some fashion, and returns a new accumulator, ready for the next element. So, in general, the first argument has type α → β → α. Then we have an initial value for the accumulator, which must have type α, and an input list of type β list. The return value is the final accumulator, so that must have type α. We can annotate the function as follows:

> ![](images/00101.jpg)

We can find the sum of a list of numbers:

![](images/00129.jpg)

Here, α and β are both int. The function `( + )` has the right type, and we use for the initial accumulator the identity element for `( + )` which is 0 since for all x, x + 0 = x (we cannot take the initial accumulator from the list itself since our function must have a result for the sum of all the integers in an empty list.)

It might appear to the reader that this is more complicated than the simple recursive solution, but to the experienced functional programmer, using `fold_left` is in fact easier to read. Let us find the maximum number in a list using `fold_left`:

![](images/00077.jpg)

Here `max` is the built-in function for finding the larger of two things, and `min_int` is the built-in value of the smallest possible integer. We can use a similar scheme to define functions on lists of booleans:

> ![](images/00082.jpg)

The `all` function is true if and only if all items in the list are true; the `any` function if at least one is. What can happen when α and β are different? How about making the accumulator a list too? We can use `List.mem` to turn an arbitrary list into a set by consulting the existing accumulator before putting an element in:

> ![](images/00206.jpg)

We are using `List.mem` to decide whether to add each element to the accumulator or discard it.

What about `fold_right`?

Here is the function again:

> ![](images/00092.jpg)

The `fold_left` function applied the given function over the elements in the input list from the left hand side. In contrast, `fold_right` processes them from the right, by changing the evaluation order. Consider, for example, our summation example:

![](images/00263.jpg)

![](images/00103.jpg)

See how the accumulating of values starts from the right hand side. Note also that `fold_right` is not tail-recursive (the intermediate expression it builds is proportional to the size of the input). We can define `map` simply as a use of `fold_right`.

> ![](images/00106.jpg)

Who would have thought that `fold_right` was the more fundamental function? At the cost of a list reversal, we can make `fold_right` tail-recursive by defining it in terms of `fold_left`:

> ![](images/00111.jpg)

Sometimes we want to provide an initial accumulator value which is not the identity element for the computation. For example, applying `::` over an input list with `fold_right` is not very interesting, yielding a function which returns a copy of its input:

> ![](images/00116.jpg)

But if we supply a non-empty list as the initial value of the accumulator, we have the `append` function:

> ![](images/00121.jpg)

We can use a more complicated accumulator, such as a tuple. In this example, we replicate the `List.split` function which, given a list of pairs, yields a pair of lists:

> ![](images/00126.jpg)

For example, `split [(1, "one"); (2, "two")]` evaluates to `([1; 2], ["one"; "two"])`.

A word of caution

One very simple definition for the function `concat` which concatenates all lists in a list of lists is given by:

> ![](images/00131.jpg)

We use the append function to accumulate the lists into a single list one by one:

![](images/00135.jpg)

However, the order of evaluation is such that the append function `@` (which takes time proportional to the length of its first argument) is used inefficiently – we process the list again and again.

Folding over trees

For the usual definition of a binary tree, we can define a fold. There are two accumulators, one for everything from the left sub-tree, and one for everything from the right sub-tree. The supplied function combines both into a new accumulator.

> ![](images/00138.jpg)

Here is an example tree:

![](images/00142.jpg)

Functions for the size of a tree, and the sum of an integer tree are now easy, without explicit recursion:

> ![](images/00274.jpg)

The standard tree traversals can be written easily with a list accumulator. A little typographical manipulation shows the pleasing symmetry:

> ![](images/00001.jpg)

On our example list:

![](images/00006.jpg)

Questions

1.  Write a function which, given a list of integers representing expenses, removes them from a budget, again represented by an integer.
2.  Calculate the length of a list using one of the `fold_` functions.
3.  Use one of the `fold_` functions to find the last element of list, if any. Behave sensibly if the list is empty.
4.  Write a function to reverse a list, using one of the `fold_` functions.
5.  Write a version of `List.mem` using one of the `fold_` functions. Now `setify` can be defined entirely using folds.
6.  Use a fold to write a function which, given a list of non-empty strings representing words, returns a single string where the words are separated by spaces. Comment on its efficiency.
7.  Use `fold_tree` to write a function which calculates the maximum depth of a tree. What is its type?
8.  Compare the time efficiency of one or more of your functions with the system implementation of the same function (for example, our fold-based member function vs. `List.mem`) with regard to both computational complexity and actual time taken.
9.  Comment on whether the use of folds in each of Questions 1–7 is good style.

Chapter 2
Being Lazy

We can make our own data type for OCaml’s built-in lists like this:

`type 'a list = Nil | Cons of 'a * 'a list`

The constructor `Nil` represents the empty list, and `Cons` builds a list from a head and a tail. So, for example, we can write the list `[1; 2; 3]` as `Cons (1, Cons (2, Cons (3, Nil)))`. It is also possible to define an infinitely-long list, where elements are only produced when we actually need them. This is known as a lazy list. Instead of a tail, we use a tail function. This is a function which, when given a unit value, yields the tail:

`type 'a lazylist = Cons of 'a * (unit -> 'a lazylist)`

Note that we have no `Nil` constructor, because the list has no end. Our use of unit rather than another type is a choice – we could use any type, but unit is the simplest type, containing only one value. How do we use such a creature? Let us start by writing a function which, given an integer n, builds the lazy list of all integers n,n + 1,n + 2… and returns it:

> ![](images/00010.jpg)

When we type this in to the OCaml top level, here is what we see:

`        OCaml`

`# lseq 0;;`
`- : int lazylist = Cons (0, <fun>)`

We can see that the head of the list is zero – the rest is yet to be calculated. OCaml represents the tail function with `<fun>`. We can now write functions to extract items from the list. Here are lazy head and tail functions:

> ![](images/00016.jpg)

Notice that, because there is only one constructor in our data type, we can pattern match directly in the function argument. When we apply the unit `()` to the tail function, we are forcing evaluation of the tail. Here are lazy versions of the familiar `take` and `drop` functions, which take or drop the first n elements of a list:

> ![](images/00019.jpg)

The `ltake` function has to yield an ordinary list, of course. Note the use of the `as` keyword to name part of the pattern (here, `Cons (h, tf)` is named `ll`), making the base case of `ldrop` simpler. Now we can actually get at our elements:

`        OCaml`

`# ltake (lseq 0) 20;;`
`- : int list =`
`[0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10; 11; 12; 13; 14; 15; 16; 17; 18; 19]`
`# ldrop (lseq 0) 20;;`
`- : int lazylist = Cons (20, <fun>)`

Two favourite list functions have easy analogues in the lazy world:

> ![](images/00024.jpg)

Note that delaying and forcing evaluation often come together, as in both these examples. The function `map` returns almost immediately – assuming `f` is quick. The computation of the rest of the elements is, as always, delayed. The `filter` function is different – it must find at least one matching element to use as the head, before returning. If it does not find one, it will never return, so care is needed. Let us use these two functions to find the cubes divisible by five:

> ![](images/00028.jpg)

Now, using `ltake`:

`        OCaml`

`# ltake cubes 20;;`
`- : int list =`
`[125; 1000; 3375; 8000; 15625; 27000; 42875; 64000; 91125; 125000; 166375;`
` 216000; 274625; 343000; 421875; 512000; 614125; 729000; 857375; 1000000]`

Here is another example of a simple lazy list, this time the list of all primes, created by use of `lfilter` and recursion, beginning with the list of all numbers from 2, calculated with `lseq`:

> ![](images/00212.jpg)

There are plenty of list functions which cannot be adapted to lazy lists. We cannot, for example, reverse a lazy list, or append two lazy lists. But there is an analogue to `append`. We can combine two lists fairly, taking elements in turn from each:

> ![](images/00040.jpg)

For example, the list alternating between zeros and ones can be built with `interleave` and a function to build constant lists:

> ![](images/00044.jpg)

A more interesting example is to calculate the lazy list of all ordinary lists of zeros and ones. We can do this by prepending a zero and a one to the list, and interleaving the resulting lists:

> ![](images/00049.jpg)

This yields:

`        OCaml`

`# ltake allones 20;;`
`- : int list list =`
`[[]; [0]; [1]; [0; 0]; [0; 1]; [1; 0]; [1; 1]; [0; 0; 0]; [0; 0; 1];`
` [0; 1; 0]; [0; 1; 1]; [1; 0; 0]; [1; 0; 1]; [1; 1; 0]; [1; 1; 1];`
` [0; 0; 0; 0]; [0; 0; 0; 1]; [0; 0; 1; 0]; [0; 0; 1; 1]; [0; 1; 0; 0]]`

To see why, we can visualise the evaluation as a tree where each left branch prepends a zero and each right branch a one:

![](images/00025.jpg)

The interleavings are fair, and the interleavings of interleavings equally so, thus we see the results of length two in this order: `[0; 0] [0; 1] [1; 0] [1; 1]`.

Questions

1.  Write the lazy list whose elements are the numbers 1, 2, 4, 8, 16… What is its type?
2.  Write a function to return the nth element of a lazy list where element zero is the head of the list.
3.  Write a function which, given a list, returns the lazy list forming a repeated sequence taken from that list. For example, given the list `[1; 2; 3]` it should return a lazy list with elements 1, 2, 3, 1, 2, 3, 1, 2…
4.  Write a lazy list whose elements are the fibonacci numbers 0, 1, 1, 2, 3, 5, 8… whose first two elements are zero and one by definition, and each ensuing element is the sum of the previous two.
5.  Write the function `unleave` which, given a lazy list, returns two lazy lists, one containing elements at positions 0, 2, 4, 6… of the original list, and the other containing elements at positions 1, 3, 5, 7…
6.  Alphanumeric labels in documents go A,B,C,…,X,Y,Z,AA,AB,…,BA,BB,…AAA,…  Write the lazy list containing strings representing this sequence.

Chapter 3
Named Tuples with Records

Tuples can be used to combine a fixed number of elements of same or differing types. However, once we have more than two or three items, remembering the order can be difficult, especially if the types of the items are the same. Records remedy this, allowing us to name each item. Due to this naming, they have several other useful properties which distinguish them from tuples. Let us define a simple type for cartesian coordinates in two dimensions:

`type point = {x : float; y : float}`

Records are like tuples with labels. We write them between braces `{ }`. Each element of the record (called a field) has a name and a type, and the fields are separated with semicolons. We can construct a value of this type using the same syntax, but with the equals sign in place of the colons:

`let p = {x = 4.5; y = 6.0}`

We can add another field to the record, a label for the point:

`type point = {x : float; y : float; label : string}`

We can parametrize it just like a list or variant data type:

`type 'a point =`
`{x : float; y : float; label : string; content : 'a}`

So now we can have values of type int point and string point and so on. We can define one directly:

> ![](images/00059.jpg)

Notice that frequently we write something like `x = x` in a record definition, as in `make_point` here. This can be shortened to just `x`, and by doing so for all the arguments in `make_point` we obtain this simpler definition:

> ![](images/00066.jpg)

Having built record values, we now need to know how to extract the individual parts. We can use the dot notation, writing record.field like so:

> ![](images/00069.jpg)

Alternatively, we can use record syntax in patterns, here in the argument itself:

> ![](images/00075.jpg)

Notice we only had to include in the pattern the parts of the record we intended to use. This can, optionally, be made more explicit by adding the wildcard `_` to the pattern:

> ![](images/00079.jpg)

Finally, we can use the shorthand record form in patterns too:

> ![](images/00084.jpg)

Where we need a copy of a record with just one or more fields changed, we can use the `with` keyword:

> ![](images/00089.jpg)

Again, the shortened form can help:

> ![](images/00094.jpg)

Here is a function to reflect a point about the line x = y:

> ![](images/00099.jpg)

Mutable records

Individual fields of a record can be made mutable (their value may be changed – literally mutated), by use of the `mutable` keyword:

`type 'a point = {x : float; y : float; label : string;mutable content : 'a}`

In fact, OCaml’s reference type is just a record with a single, mutable field:

`        OCaml`

`# let x = ref 0;;`
`- : int ref = { contents = 0 }`

Here, the type ref is defined by `type 'a ref = {mutable contents : 'a}` and the constructor function `ref` is of type α → α ref. The value of a mutable field can be updated using the `<-` symbol like this:

`        OCaml`

`# type 'a point = {x : float; y : float; label : string; mutable content : 'a};;`
`type 'a point = {`
`  x : float;`
`  y : float;`
`  label : string;`
`  mutable content : 'a;`
`}`

`# let p = {x = 4.5; y = 6.0; label = "P"; content = [1; 3; 1]};;`
`val p : int list point = {x = 4.5; y = 6.; label = "P"; content = [1; 3; 1]}`

`# p.content <- [1];;`
`- : unit = ()`

`# p;;`
`- : int list point = {x = 4.5; y = 6.; label = "P"; content = [1]}`

Such records should be used with care, like any mutable feature, especially if they are likely to be used as part of a larger data structure.

Questions

1.  Show how to update a reference without using the `:=` operator.
2.  Using functions from the “Time Functions” section of the documentation to the Unix module, write a program which, when run, returns a string containing the time and date, for example `"It` `is 2:45 on Wednesday 8 January 2014"`.
3.  What is the difference between `type t = {x : int ref}` and `type t = {mutable x : int}`? What are the advantages and disadvantages of each?
4.  Define a record of six items a...f where a and b have the same type as one another, c and d have the same type as one another and e and f have the same type as one another.
5.  Records are used in the module Gc which controls OCaml’s garbage collector (a garbage collector is a system which automatically reclaims space the program has finished with as the program is running). Use the data structures and functions in the Gc module to write programs which:
    1.  write a summary of the state of the garbage collector to a text file; and
    2.  alter the verbosity of the garbage collector as defined in the `control` record.

Chapter 4
Generalized Input/Output

In Pervasives, OCaml’s default always-opened module, a number of functions are defined over input and output channels – representing both files in the file system and special ones such as standard output. However, it is often useful to have a more general abstraction of input and output over, for example, strings and arrays, as well as files and channels.

In this chapter, we shall develop such an abstraction, giving input and output types which work with OCaml channels and strings. It can be extended to work over other data structures, and to have more complete functionality – some of the questions at the end of the chapter involve such extensions.

A type for inputs

The fundamental operations on an input, once it has been created, will be:

*   finding the current position;
*   setting the current position;
*   reading a character, at the same time advancing the position;
*   finding the length of an input.

We need a way to group them together, and to refer to them easily. A record is ideal:

`type input =`
`     {pos_in : unit -> int;`
`      seek_in : int -> unit;`
`      input_char : unit -> char;`
`      in_channel_length : int}`

Now we can build an input from an OCaml in_channel easily (we have re-used some of the standard OCaml names):

> ![](images/00104.jpg)

Notice that the original channel is now hidden inside the input – the functions `pos_in` and `input_char` instead simply take the unit `()` as their input. Let us assure ourselves that this structure also works for abstracting over strings:

> ![](images/00107.jpg)

We allocate a local reference, `pos`, to hold the current position. It cannot be accessed directly, only manipulated through the exposed record of functions. The `pos_in` and `in_channel_length` functions are simple. The `seek_in` function needs to check that the position is positive, but we allow it to be beyond the end, for compatibility with OCaml channels. The `input_char` function checks it is not trying to read beyond the end of the string, then reads a character, advances the position, and returns the character.

Notice we use the same exception scheme as OCaml does in its own channels – raising `End_of_file` if a read is attempted beyond the last character.

Example: reading words

We should like to write a program which can extract the words from a given input, such as a string or a file. For example, given the string

`"There were four of them; more than before."`

we wish to produce

`["there"; "were"; "four"; "of"; "them"; "more"; "than"; "before"]`

removing spaces, punctuation and making the words lower case. First, let us define a function to rewind the input by one character (useful when we have read a character and decided we do not wish to consume it), and another, a predicate to determine if a character is considered a non-letter, and thus may be skipped:

> ![](images/00113.jpg)

Now, we can write a function `skip_characters` to skip any punctuation from the current point. It may raise `End_of_file`, of course. Then, we have the function `collect_characters` which, given a fresh Buffer.t and an input which has been processed by `skip_characters`, returns the string containing the next sequence of interesting characters, or raises `End_of_file` if we are at the end of the input.

> ![](images/00119.jpg)

Finally, we can write `read_word` which finds the next word, if there is one. Then `read_words` collects them all in a list, and turns them in to lower case using the Standard Library function `String.lowercase`. These functions form Figure [4.1](#index_split_010.html_filepos93769). For example:

* * *

> ![](images/00124.jpg)

> Figure 4.1:

* * *

`# read_words (input_of_string "There were four of them; more than before.");;`
`- : string list = ["there"; "were"; "four"; "of"; "them"; "more"; "than"; "before"]`

A type for outputs

What do we need for a generic output? We must have an `output_char` function to write a single character, at least. It is also useful to have an `out_channel_length` function so we know how many characters have been written. We will not allow seeking back and forth like with our input type for the sake of simplicity. Figure [4.2](#index_split_010.html_filepos95470) shows the output type, and functions to build outputs from channels and strings.

* * *

> ![](images/00127.jpg)

> Figure 4.2:

* * *

Note that whilst we have unified the interface for writing to strings and channels, they remain different things: the string has limited length, and if the length is not all used it will contain junk at the end. Let us use these functions to build a function which writes a list of integers to any output:

> ![](images/00132.jpg)

Note that `o.output_char` has an appropriate type for use with standard functions such as `String.iter`. We can test with an output built from standard output:

`# output_int_list (output_of_channel stdout) [1; 2; 3; 4; 5];;`
`[1; 2; 3; 4; 5 ]`
`- : unit = ()`

Can you find a way to suppress the extraneous space before the `]` character?

Questions

1.  Write a function to build an input from an array of characters.
2.  Write a function `input_string` of type input → int → string which returns the given number of characters from the input as a string, or fewer if the input has ended.
3.  Extend the input type to include a function `input_char_opt` which returns a value of type char option, with `None` signalling end of file. Extend the functions `input_of_channel` and `input_of_string` appropriately.
4.  Extend the input type with a function `input_byte` which returns an integer representing the next byte, or the special value -1 at end of file. Comment on the usefulness of this compared with `input_char_opt` and `input_char`.
5.  Write an input type which raises `End_of_file` if it reaches a new line (a `'\n'` character). Use this to build a program which reads a line from standard input.
6.  Write a function to build an output from a Buffer.t. Show how this can be used to retrieve a final string after output is finished.

Chapter 5
Streams of Bits

We have dealt with byte-by-byte streams of information. Often, though, we need to consider data as a stream of bits. Can we build a nice abstraction for this?

We could start with a function which builds a list of bits from a byte, and use that for each byte in the stream, building a final list. This has two disadvantages: it is inefficient in space and time (there are eight times as many bits as bytes, of course), and it processes all the bytes at once, rather than as required. Instead, let us build a bit stream based on our input type:

`type input_bits =`
`     {input : input;`
`      mutable byte : int;`
`      mutable bit : int}`

The `input` field is the input this bit stream is based upon. It will start from the most significant bit of the current byte of that input. The `byte` field holds the byte just read from the input, or an undefined value if no byte has yet been read. The `bit` field records the current bit position, but instead of 0..7 we will use 128, 64, 32, 16, 8, 4, 2, 1 so this field can be used directly to extract the bit using the built-in logical AND operator `land`, and then halved:

![](images/00136.jpg)

The expression `x land y` where `x` and `y` are integers yields an integer whose value has a bit pattern which is the bitwise logical AND of `x` and `y`. This input_bits type can be wholly abstracted, defined in the `.mli` by just `type input_bits`. Now, we can define a function to build an input_bits from an input:

> ![](images/00140.jpg)

The function to get the next bit is simple. If `bit` is zero, we must load a new `byte` from the input and return the next bit. If `bit` is non-zero, we extract the given bit, and halve `bit` ready for next time.

> ![](images/00144.jpg)

This function can raise `End_of_file`, of course, if the underlying call to `input_char` raises it. Two other functions are useful. We can align the bit stream on the next byte boundary trivially:

> ![](images/00148.jpg)

We can write a function `getval` to return a given number of bits considered as an integer, allowing us to read a data field of any width. We use the `lor` operator, which gives the bitwise logical OR of two integers, and the `lsl` or logical shift left operator, which shifts the bits in an integer left by the specified number of bits, filling zeros on the right.

> ![](images/00005.jpg)

OCaml integers are at least 31 bits (depending upon the computer), so we can read fields up to 31 bits wide with this function. This number on a particular computer can be calculated by evaluating `Sys.word_size -` `1`.

Example: decoding a TCP datagram header

Here is the layout of the header of a datagram of the TCP (Transmission Control Protocol) used for network communications:

![](images/00061.jpg)

It contains fields as small as 1 bit, and as large as 32 bits. We shall use the following 20 byte TCP datagram header as an example: `00 26 bb 14 62 b7 cc 33 58 55 1e ed 08 00 45 00 03 78 f7` `ac`.

The code in Figure [5.1](#index_split_011.html_filepos108367), to print out pertinent information from the header, uses `getbit`, `getval`, and a yet-to-be-defined function `getval_32` to read the header of a TCP datagram and print a summary. The function `getval_32` returns up to 32 bits in an Int32.t (implementing `getval_32` is one of the questions at the end of the chapter). Here is the output for our example data:

* * *

> ![](images/00013.jpg)

> Figure 5.1:

* * *

`Source port = 38  `
`Destination = 47892  `
`Sequence = 1656212531  `
`Acknowledgement Number = 1481973485  `
`Flags:  `
` Urgent = false  `
` Ack = false  `
` Push = false  `
` Reset = false  `
` Syn = false  `
` Fin = false  `
`Receive window size = 17664  `
`Checksum = 888  `
`Urgent pointer = 63404`

Note we must use `open_in_bin` for binary data files in case the program is executed on Microsoft Windows, where text and binary files are considered different and read differently.

Output bit streams

The type for output bit streams is rather similar to that for input bit streams, but it must be used rather differently.

`type output_bits =`
`     {output : output;`
`      mutable obyte : int;`
`      mutable obit : int}`

Here, `output` is the underlying output. The current output byte which is being constructed bit-by-bit is `obyte`, and a number `obit` from 7 down to 0 to represent the current shift required to add a bit to the byte in the correct place. When it is time to move on to the next byte, `obit` is -1\. We can build a fresh output_bits from an output:

> ![](images/00018.jpg)

The whole byte cannot be written to the underlying `output` until it has been completed, so we must have a `flush` function to be used when output is finished:

> ![](images/00023.jpg)

This doubles as our alignment function. We can now write `putbit`. For reasons we shall explain, it considers any non-zero input to be a `1` bit.

> ![](images/00027.jpg)

To output a value of width up to 31, we can write a function `putval o v l` which, given an output_bits, value, and length in bits, calls `putbit` on each bit in turn:

> ![](images/00030.jpg)

Now we can see why we allowed any non-zero integer to be considered a `1` bit – it avoids a test in `putval`. Now we have everything we need.

We can rebuild the datagram we took apart earlier using `putbit`, `putval`, and the yet-to-be-defined `putval_32` as shown in Figure [5.2](#index_split_011.html_filepos114203). In the questions, you are asked to implement various specializations of some of our input and output functions on bit streams.

* * *

> ![](images/00037.jpg)

> Figure 5.2:

* * *

Questions

1.  Specialize the function `getval` so that writing 8 bits at a time when the input is aligned is optimized. Benchmark this function against the naive one.
2.  Write the function `getval_32` which can get a value of type Int32.t in the same fashion as `getval`.
3.  Specialize the function `putval` so that writing 8 bits at a time when the output is aligned is optimized. Benchmark this function against the naive one.
4.  Write the function `putval_32` which can put a value of type Int32.t in the same fashion as `putval`.
5.  We said that the output_bits type needed a `flush` operation. In fact, this is not always true – for outputs built with, for example, `output_of_string`, we could write the current byte every time a bit is written, seeking back one byte each time, only moving on when the byte is actually finished. Implement this.

Chapter 6
Compressing Data

Often we need to attempt to reduce the amount of space taken by some data, for storage or transmission. If data were arbitrary, it could not be compressed – to compress data we need to recognise and exploit patterns. However, most data is not arbitrary at all, but structured and containing repeated patterns. No compression scheme can guarantee to reduce the size of all inputs, but we would like to achieve good compression on typical data.

We will look at a simple byte-by-byte compression scheme, implementing it using our input and output data types so it can be applied to different kinds of inputs and outputs. Then, we will consider a more complex but efficient scheme for compressing data on a bit-by-bit basis.

A byte-by-byte compression scheme

The following extract from ISO-32000 (the PDF standard) defines a byte-by-byte compression scheme:

> The encoded data shall be a sequence of runs, where each run shall consist of a length byte followed by 1 to 128 bytes of data. If the length byte is in the range 0 to 127, the following length + 1 (1 to 128) bytes shall be copied literally during decompression. If the length is in the range 129 to 255, the following single byte shall be copied 257 - length (2 to 128) times during decompression. A length value of 128 shall denote EOD [end of data].

For example, consider the text “`((5.000000, 4.583333), (4.500000,5.000000))`”, which can be represented in ASCII as the list of integers `[40; 40; 53; 46; 48; 48; 48; 48; 48; 48; 44; 32; 52; 46; 53; 56; 51;` `51; 51; 51; 41; 44; 32; 40; 52; 46; 53; 48; 48; 48; 48; 48; 44; 53; 46; 48; 48; 48; 48; 48; 48;` `41; 41]` of length 43\. This will be compressed as shown in Figure [6.1](#index_split_012.html_filepos120545). That is to say, as `[255; 40; 1; 53;` `46; 251; 48; 5; 44; 32; 52; 46; 53; 56; 253; 51; 6; 41; 44; 32; 40; 52; 46; 53; 252; 48; 2; 44;` `53; 46; 251; 48; 255; 41; 128]`, of length 35\. The maximum compression ratio achieved with this method (for long constant data) is 64:1\. The worst case (alternating bytes) is 127:128 – a slight expansion.

* * *

> ![](images/00043.jpg)

> Figure 6.1:

* * *

Let us begin with two utility functions to allow us to convert between strings and lists of integers – this will make it easier to understand our examples when we evaluate them in OCaml’s top level:

> ![](images/00046.jpg)

Note the use of the Standard Library function `List.iteri` which is like `List.iter`, but it passes an additional integer to the function each time, representing the position in the list, starting at 0\. Note also that we use `downto` in `int_list_of_string` to avoid a list reversal.

Now, we shall build a little abstraction to allow our compression and decompression functions to share a common basis. Our `compress` and `decompress` function will need to read from any input, and write to any output. However, for our little tests, we shall be reading from and writing to strings. Since we do not know the size of the compressed or decompressed output in advance, we cannot allocate an appropriately sized string. So, let us build an output from a Buffer.t. This way, we can write a function `process` which, given a compression or decompression function, creates a buffer, builds an output from it, calls the function to process the data, and then extracts the final string from the buffer.

> ![](images/00051.jpg)

Now, given some suitable function `decompress`, say, we can call `process` giving the function and a string, and get a new string back.

Decompression in this scheme, as is often the case, is simpler than compression, so we shall address it first. The whole thing is wrapped in a loop which terminates only upon an exception. If the input data is well-formed, that exception will be `EOD`, which we have defined for this purpose. Inside the loop, we read a byte from the input. It is either in the range 0...127, in which case it is a “different” run, and we copy some bytes from input to output. Or, it is in the range 129...255, in which case it is a “same” run, and we output a number of copies of the next byte. Otherwise, the byte must have value 128, and we raise the `EOD` exception. The `decompress_string` function is as simple as we claimed it would be, because we wrote `process`.

> ![](images/00057.jpg)

For compression, we will first write functions to recognise a “same” run and a “different” run in the input, and then a main function which uses them as appropriate. The function `get_same` returns the first character, and an integer representing the number (one or more) of “same” characters starting with the first one. It leaves the input pointing at the last “same” character. If 128 same characters have been found, we must stop early. If we are at the end of input when the function is called, `End_of_file` is raised as usual.

> ![](images/00063.jpg)

The `get_different` function is rather more awkward. It will return the non-empty list of “different” characters starting at the current position. We must stop as soon as we notice two like characters, rewinding twice and removing a character from our accumulator. So, for example, if we are reading “`An Accumulation`” we want to return `['A'; 'n'; ' '; 'A']` but we do not know this until we read the second `'c'`. Again, we must stop after 128 differing characters. As before, `End_of_file` is raised if we are at the end of the input on the initial call.

> ![](images/00090.jpg)

The compression function is now relatively simple. We repeatedly call `get_same`. If it indicates a run of length one, we call `get_different` instead. In each case we write appropriate data. Then, on `End_of_file`, we write the EOD marker. The `compress_string` function is built just like `decompress_string`.

> ![](images/00071.jpg)

Let us try with our sample data:

`       OCaml  `

`# open Examples;;  `
`# example;;  `
`- : string = "((5.000000, 4.583333), (4.500000,5.000000))"  `

`# int_list_of_string example;;  `
`- : int list =  `
`[40; 40; 53; 46; 48; 48; 48; 48; 48; 48; 44; 32; 52; 46; 53; 56; 51; 51; 51;  `
` 51; 41; 44; 32; 40; 52; 46; 53; 48; 48; 48; 48; 48; 44; 53; 46; 48; 48; 48;  `
` 48; 48; 48; 41; 41]  `

`# let smaller = compress_string example;;  `
`val smaller : string = "?(\0015.?0\005, 4.58?3\006), (4.5?0\002,5.?0?)\128"  `

`# int_list_of_string smaller;;  `
`- : int list =  `
`[255; 40; 1; 53; 46; 251; 48; 5; 44; 32; 52; 46; 53; 56; 253; 51; 6; 41; 44;  `
` 32; 40; 52; 46; 53; 252; 48; 2; 44; 53; 46; 251; 48; 255; 41; 128]  `

`# decompress_string (compress_string example) = example;;  `
`- : bool = true`

A bit-by-bit compression scheme

Our previous method required whole bytes to be equal to one another to compress well. Now we consider compression bit-by-bit, but on the same principle – encoding the lengths of runs of data. We will build a compressor and decompressor for the CCITT Group 3 compression scheme. This is the basic scheme used by the fax machines since the 1970s, and for 1 bit-per-pixel TIFF files. It is also used in the PDF format, as we shall see later in the book. Here is our example data, an 80x21, one-bit-per-pixel image of a scanned word from printed paper:

![](images/00153.jpg)

We can put it into our source file using the characters `0` and `1` to ease readability. A string can run over several lines if a backslash is added at the end of each line. Spaces at the beginning of the next line are also skipped, so we can line it up nicely:

`let input_data =`
`"00000000000000000000000000000000000000000000000000000000000000000000000000000000\`
` 00000000000000000000000000000000000000000000000000000000000000000000000001000000\`
` 00000000111111110000000000011111111100000000000000000000000000000000000111100000\`
`00000011000000011100000001110000001110000000000000000000000000000000000011000000\`
`00000110000000001110000011000000000110000000000000000000000000000000000011000000\`
`00001110000000000111000111000000000000000000000000000000000000000000000011000000\`
`00001100000000000111000110000000000000000000000000000000000000000000000011000000\`
`00001100000000000011001110000000000000000011100000000100111000011100000011000000\`
`00011100000000000011001110000000000000001111111000111111111101111110000001000000\`
`00011100000000000011101100000000000000001000011000001110001111000111000001000000\`
`00011100000000000011101100000000000000000000011000001100000110000011000001000000\`
`00011100000000000011001110000000000000000000011000001100000110000011000001000000\`
`00001100000000000011001110000000000000000111011000001100000110000011000001000000\`
`00001110000000000011000110000000000000011100011000001100000110000011000001000000\`
`00001110000000000110000111000000000000011000011000001100000110000011000011000000\`
`00000111000000000110000011100000000000011000011000001100000110000011000011100000\`
`00000011100000001100000001110000000010010001110000011000001100000110000111000000\`
`00000011111111100000000001111111111000111110111000111100011110000111001111100000\`
`00000000011100000000000000001111000000001000000000000000000000000000000000000000\`
`00000000000000000000000000000000000000000000000000000000000000000000000000000000\`
`00000000000000000000000000000000000000000000000000000000000000000000000000000000"`

You can see that it consists of runs of 0 (white) and 1 (black) pixels, 80 to each line, with 21 lines.

Preliminaries

First, we had better define a function to convert the string of zeros and ones to a string containing the actual binary data. We can do this by building an output_bits with an output built from a buffer. Then, after flushing, we can use `Buffer.contents` to extract the data we have written.

> ![](images/00181.jpg)

Note that, since the string will always be a whole number of bytes (possibly padded with zeros by `flush`) we must remember the width and height of our image (80 and 21 here) and pass one or both of them to some of our other functions. For example, we can write a function to print one of these packed binary strings. This needs the width of the image to know when to print newlines:

> ![](images/00087.jpg)

For simplicity here, we do not worry about padding at the end (in our example, since the width is 80, it will consist of whole bytes anyway).

Fax compression explained

We have said that the compression will proceed by encoding the lengths of the runs of zeros and ones in our data. How do we encode them? We need a set of binary sequences which can be distinguished from one another (i.e. no sequence can be a prefix of another sequence). In the case of fax compression, there are codes for run lengths 0 to 63, and different codes for white and black runs, as shown in Figure [6.2](#index_split_012.html_filepos137359). Shorter codes are chosen for the more common cases, based on a statistical analysis of real documents.

* * *

> ![](images/00232.jpg)

> Figure 6.2:

* * *

Notice that no white symbol is a prefix of another white symbol, and no black symbol is a prefix of another black symbol. These codes for runs from 0 to 63 are called terminating codes. When a run is longer, we use one “make-up code”, shown in Figure [6.3](#index_split_012.html_filepos138415), followed by a terminating code. Thus, the longest run is of length 1728 + 63 = 1791.

* * *

> ![](images/00096.jpg)

> Figure 6.3:

* * *

The reason for distinguishing between white and black codes is to do with error correction in unreliable transport mechanisms (such as phone lines that fax machines operate over) – otherwise we could just have one set of codes and assume runs alternate. The reason for the existence of a zero-length run is that each line is defined to begin with a white run. If it is really black, a zero-length white run is output first. No run is longer than a line. As an example, let us compress the first three lines of our example data:

`00000000000000000000000000000000000000000000000000000000000000000000000000000000  `
`00000000000000000000000000000000000000000000000000000000000000000000000001000000  `
`00000000111111110000000000011111111100000000000000000000000000000000000111100000`

We have the following:

![](images/00294.jpg)

We have reduced the data from 240 bits to 64 bits, a reduction of about three quarters.

Compressing fax data

First, we need to encode the terminating and make-up codes. We will use arrays for direct indexing, but lists for each element, since we do not need random access to each bit. This is shown in Figure [6.4](#index_split_012.html_filepos140932). Now, we can write a function which, given a length of run and a colour, gives the appropriate code as a list of bits:

* * *

> ![](images/00021.jpg)

> Figure 6.4:

* * *

> ![](images/00050.jpg)

Now, a function which, given the current colour, an input_bits, the current number of like bits read, and the width of the image, returns a pair of the number of like bits, and the colour:

> ![](images/00081.jpg)

For example, the first call to `read_up_to` will calculate (80, 0). Now we can write the main function. Given an input_bits and output_bits, and the width and height of the image, for each line we check if a zero-width white run needs to be added, and then call `encode_fax_line`.

> ![](images/00109.jpg)

Now we can write a function `process`, just like we did in the byte-by-byte example, but for `input_bits` and `output_bits`. We must be sure to flush the output. The main `compress_string_ccitt` function is then simple:

> ![](images/00137.jpg)

For our full input data, the input string is 80 × 21 = 1680 bits long, and the compressed string is 960 bits long, a compression ratio of 7:4.

Decompressing fax data

For decompression, we will write two functions for reading white and black codes. It is easiest to directly encode the decision tree:

> ![](images/00162.jpg)

Now, decoding is relatively simple. We decode runs for each line, until the width is all used up, and do this for each line. We read white and black codes alternately – each line begins on white. We can use `process` again:

> ![](images/00189.jpg)

We can verify our code by evaluating `s = decompress_string_ccitt (compress_string_ccitt s)` for our example data.

Questions

1.  How much complexity did using the input and output types add to `compress` and `decompress` in our byte-by-byte example? Rewrite the functions so they just operate over lists of integers, in functional style, and compare the two.
2.  Replace our manual tree of codes with a tree automatically generated from the lists of codes used for compression. The tree will have no data at its branches (since no code is a prefix of another), and will have data at only some of its leaves. Define a suitable data type first.
3.  What happens if we compress our data as a single line of 1680 bits instead of 21 lines of 80? What happens if we try to compress already-compressed data?
4.  Write a function which, given input data, will calculate a histogram of the frequencies of different runs of white and black. This could be used to build custom codes for each image, improving compression.

Chapter 7
Labelled and Optional Arguments

OCaml allows us to label some or all of the arguments to a function, so as to provide a little documentation, to prevent us from accidently swapping two arguments which have the same type, and to allow partial application of arguments more flexibly. Consider a function to fill in part of an array with an element:

> ![](images/00215.jpg)

The `fill` function takes four arguments: the array itself, the start position, length of the fill and the element to use to fill. However, since the start and length are both integers, it is easy to get them the wrong way round. This can be remedied by giving those two arguments labels. A label is introduced by a tilde, followed by the label name, a colon and the argument name itself. Consider the functions `fill` and `filled` below. As you can see, we have defined `fill` with labels, which appear in the type as well. In the first `filled` function, we call the `fill` function, citing the labels and giving immediate integers. In the second, we show that it works with other names (as it does, indeed, for any expression). In the third, we show that the labelled arguments may be permuted and rearranged with regard to the other arguments (unlabelled arguments must remain in the correct order relative to one another).

> ![](images/00234.jpg)

Another change we can make is to use the label for the name of the argument inside the function too. This simplifies the syntax: we can just write `~label`.

> ![](images/00083.jpg)

You can see that in `filled`, this “punning” works equally well when calling the function, if we happen to have values with the same names. These two facilities need not be used together, of course.

Labels with partial application

Another common use of labelled arguments is to give flexibility when using partial application. Consider the following function:

`let divide x y = x / y`

We can use partial application to write the function which divides ten thousand by each number in a list:

`let f = divide 10000 in [f 100; f 50; f 20]`

This yields `[100; 200; 500]`. But we cannot re-use `divide` to write the function which divides each number in a list by ten – this would involve partially applying the second argument `y` first. The design of the `divide` function has baked in which argument may be partially applied (OCaml lets us partially apply any prefix of the arguments – the first, first and second, first, second and third etc.) For example, we can apply the same function to many lists, using a partially applied `List.map` but we cannot apply many functions to a single list by providing the list to `List.map` instead. In our example, we can label the arguments to our divide function:

`let divide ~x ~y = x / y`

The type of the function reflects this:

`        OCaml  `

`# let divide ~x ~y = x / y;;  `
`val divide : x:int -> y:int -> int = <fun>`

Now we may apply the arguments in either order:

`        OCaml  `

`# let f = divide ~x:10000 in [f 100; f 50; f 20];;  `
`- : int list = [100; 200; 500]  `
`# let f = divide ~y:10000 in [f 100000; f 10000; f 1000];;  `
`- : int list = [10; 1; 0]`

We can in fact, omit the labels if we are applying arguments in order:

`        OCaml  `

`# let f = divide 10000 in [f 100; f 50; f 20];;  `
`- : int list = [100; 200; 500]`

Optional arguments

OCaml also allows us to make a labelled argument optional – that is to say, we need not supply it at all. The function which is called without one or more of its arguments can decide what to do. Consider this simple function `split` which returns a list of singleton lists from an input list, for example returning `[[1]; [2];` `[3]]` for the input list `[1; 2; 3]`:

> ![](images/00152.jpg)

We would like to extend the function to produce sub-lists of a given size, other than the default of 1\. We can add a labelled argument and adapt the function, using `take` (which takes a given number of items from the start of a list) and `drop` (which drops a given number of items from the start of a list) from the Util module described on page xiii:

> ![](images/00157.jpg)

There are two problems, though. Existing code using the function will not compile, and we must always specify the `chunksize` argument, even when it will be 1\. This can be remedied by using an optional labelled argument, introduced with a question mark instead of a tilde, and given a default value:

> ![](images/00160.jpg)

Notice the question mark appears also in the type. Notice also that in the recursive call to `split` we can write `~chunksize` instead of `~chunksize:chunksize` as usual. Now our `split` function can be called with or without this optional argument:

`        OCaml  `

`# split [1; 2; 3];;  `
`- : int list list = [[1]; [2]; [3]]  `
`# split ~chunksize:3 [1; 2; 3; 4; 5; 6; 7];;  `
`- : int list list = [[1; 2; 3]; [4; 5; 6]; [7]]`

In fact, if we do not give a default value to the optional argument in the definition of `split`, we have access to its actual implementation – as a value of the option type, either `None` or `Some`, and we can match on it:

> ![](images/00165.jpg)

This is primarily useful when there are several optional arguments.

Labels in the Standard Library

The Standard Library contains three labelled versions of other modules: ListLabels, ArrayLabels and StringLabels. For example, we can write:

`        OCaml  `

`# ListLabels.map ~f:(fun x -> x * 2) [1; 2; 3];;  `
`- : int list = [2; 4; 6]`

If we wish to use the labelled modules by default, the module StdLabels contains these labelled modules under their original names so, by writing “`open StdLabels`”, `List.map`, `Array.blit` etc. will now be labelled:

`        OCaml  `

`# open StdLabels;;  `
`# List.map ~f:(fun x -> x * 2) [1; 2; 3];;  `
`- : int list = [2; 4; 6]`

These modules do not label all arguments. Typically they just do so for arguments which are functions, and when there are multiple arguments of the same type which may be confused. For example, `ArrayLabels.sub` of type α array → pos:int → len:int → α array introduces labels to disambiguate the position and length arguments, but does not label in the input array.

Questions

1.  The function `ArrayLabels.make` is not labelled, having type int → α → α array. When might this cause confusion? Write a labelled version to correct this problem.
2.  When we wrote our `fill` function with labelled arguments, we wanted to prevent someone mistakenly swapping the start and length values. Can you find a way to do this without labelled or optional arguments?
3.  Build labelled versions of functions from the Buffer module, choosing which functions and arguments to label as appropriate.
4.  Frequently we use an accumulator to make a function tail-recursive, wrapping it up in another function to give the initial value of the accumulator. For example, we might write:

    > ![](images/00168.jpg)

    Use an optional argument to express this as a single function.

Chapter 8
Formatted Printing

OCaml provides facilities for what is called formatted printing. Consider the following function, culled from Chapter [3](#index_split_009.html_filepos73521):

> ![](images/00174.jpg)

Using the function `sprintf` (“`f`ormatted `print`ing to a `s`tring”) from the Standard Library module Printf we can build this string more easily:

> ![](images/00179.jpg)

In this example, the format string is `“%s = (%f, %f)”`. The conversion specifications `%s` and `%f` denote places for a string and the decimal representation of a floating-point number respectively to be substituted into the string. Other characters are simply reproduced from the format string to the output string. We have avoided the inefficient, repeated use of the `^` operator for string concatenation, and our new example is both shorter and easier to read. Here is a subset of the many conversion specifications available:

![](images/00184.jpg)

The `sprintf` function knows how to match up the conversion specification with the arguments following the format specification at compile time, so run-time errors are avoided:

`        OCaml`

`# Printf.sprintf "%s = (%f, %f)" "A"` `40` `65.8;;`
`Error: This expression has type int but an expression was expected of type`
`         float`

Indeed, even if we use partial application, the type of the resulting function will be calculated:

`        OCaml`

`# let f = Printf.sprintf "%s = (%f, %f)" "A" 2.45;;`
`val f : float -> string = <fun>`

You might be able to guess that there is a little magic going on here – we could not write `sprintf` ourselves, for example. We can see the rather complicated type of the `sprintf` function, used for its internal implementation:

`        OCaml`

`# Printf.sprintf;;`
`- : ('a, unit, string) format -> 'a = <fun>`

For printing numbers, there are some additional pieces of information which can be provided. The format of a conversion specifier is in fact:

`%`⟨flags⟩⟨width⟩⟨`.`precision⟩type

Fields enclosed in angle brackets are optional. So far, we have only used the `%` character and the type field. The width field defines the width of the representation of the number, and can be used to line things up in columns, here of width six:

> ![](images/00188.jpg)

This will result in the following output from `print_nums data`:

`A     | B     | C`
`------+-------+-------`
`     1|      6|      5`
`     2|     18|      4`
`     3|     31|     12`
`     4|     16|      2`

Here are some possible values of the flags field:

![](images/00193.jpg)

The optional precision field specifies the number of digits after the decimal point. For example, let us print some integers and floating-point numbers in columns with differing flags and precisions:

> ![](images/00252.jpg)

This will result in the following output from `print_nums data`:

`A     | B     | C`
`------+-------+-------`
`000001| 35.54 | 39.42`
`000002| 12.31 | 23.24`
`000003| 13.53 | 24.21`
`000004| 57.75 | 126.75`

Printing to other places

Of course, once we have calculated a string using `sprintf`, we can do with it what we may – however, for convenience and efficiency, the Printf module provides several other functions:

![](images/00100.jpg)

These all return unit. For example, to write a point to standard output, using the `%!` conversion specification to flush each time so screen update is immediate:

> ![](images/00205.jpg)

It might be argued, though, that it is better to keep `string_of_point` as the basic function, so it can be reused in other situations, writing the generated string to the screen from the calling function instead.

Questions

1.  Given a list of pairs of integers such as `[(1, 2); (5, 6); (6, 6); (7, 5)]`, write a function to return a string representation such as `"(1, 2) --> (5, 6) --> (6, 6) --> (7, 5) --> (1,` `2)"`.
2.  Write a function which, given a string, returns another string which represents the first using hexadecimal numbers. For example, the input string `Hello` should yield the output `48656c6c6f` since `'H'` has ASCII code `0x48` and so on.
3.  Why does the following code cause a type error?

    `# let mkstring () = "string";;  `
    `val mkstring : unit -> string = <fun>  `
    `# Printf.printf (mkstring ());  `
    `  ;;  `
    `Error: This expression has type string but an expression was expected of type  `
    `         ('a, out_channel, unit) format =  `
    `           ('a, out_channel, unit, unit, unit, unit) format6`

    What can be done to fix it?

4.  Use the `*` syntax described in the Printf module documentation to write a function which can print a table of integers to a given width. For example, given width 10, we might see:

    `(         1)  `
    `(        23)  `
    `(     33241)  `
    `(         0)`

Chapter 9
Searching for Things

How do we look for a sequence in another, longer sequence? Suppose we want to write a function `search_list` which, given the list `p` (the pattern) to search for in the list `l` determines if it exists (i.e. if it is a sub-list). For example, the list `[1; 2]` is found in `[2; 1; 2; 2]` but not in `[2; 1; 1]`. A list `p` is defined to be a sub-list of a list `l` if there exist lists `x` and `y` such that `l = x @ p @ y`. One, two, three, or all four of `x`, `p`, `y`, `l` can be the empty list, of course. So, for example, `[]` is a sub-list of `[1; 2; 3]` and of `[]`. A list `p` is a sub-list of `l` if:

*   The length of `p` is less than or equal to the length of `l` and either
*   The sub-list `p` is found at the beginning of `l`, or
*   The list `p` is a sub-list of the tail of `l`

We can write this out easily, using the `take` and `drop` functions from our Util module, described on page xiii:

> ![](images/00211.jpg)

(Recall that the `||` operator does not evaluate its right hand side if the left hand side evaluates to `true`, so this function will exit as soon as it finds a match.) We might be worried about the call `List.tl` failing, but if `l` is empty, the pattern must be empty from the first test, and so the condition with `Util.take` would have succeeded already. You can see that there are two inefficiencies here, the use of `List.length` on `p` and `l` each time around, and the explicit building of the list to check the pattern against with `Util.take`. Let us remove the first one:

> ![](images/00214.jpg)

Now, `List.length` is called only at the beginning. We can also remove `Util.take` to avoid the construction of intermediate lists, by writing an explicit function to test the pattern against the first `len_p` items in the lists:

> ![](images/00217.jpg)

This is now about as efficient as our simple approach can get.

Searching in strings

For practical applications, we shall often need to search within strings, or other such random-access structures. Our first list version generalizes easily:

> ![](images/00221.jpg)

This time, there is no problem with `String.length` since, unlike `List.length`, it runs in constant time. We do have the overhead of the first `String.sub`, analogous to the `Util.take` in the list version. The second `String.sub` is also a problem since, unlike `List.tl`, it creates a new string.

To solve this, we can define an auxiliary function `at` which, given pattern `p`, string `s` and the length `l` to test, together with the position in the pattern `pp` and in the main string `sp`, tests for equality. This is similar to `equal` in our lists example.

> ![](images/00226.jpg)

The `search'` function itself has a counter for how far along the main string it is. We initialize this to zero in `search`.

More flexible searches

We can make our searching function more interesting by allowing the use of some special characters. We shall introduce only these simple constructs:

*   A `?` character matches zero or one instances of the following character. For example, the pattern `?abc` matches `abc`, `bc`, and `dbc`;
*   A `*` character matches zero or more instances of the following character. So, the pattern `*abc` matches `bc`, `abc`, and `aaabc`;
*   A `+` character matches one or more instances of the following character. For example, the pattern `+abc` matches `abc` and `aaabc` but not `bc` or `dbc`.

Let us add the `?` character to begin with. First, we must alter our `search'` function’s terminating condition – we can no longer just finish when the pattern is longer than the remaining part of the string – the length of the pattern and the length of the characters matching that pattern are no longer always equal. We now continue only when the position `n` is less than the length of the string, or it is equal to the length of the string and that length is zero (the latter case is required so that the pattern `?a` matches the empty string).

> ![](images/00231.jpg)

Now we can alter the `at` function itself. We have an initial terminating condition – if the pattern has been used up entirely, we must have matched it. Otherwise, we match on the next character in the pattern, to see if the next part of the pattern matches and, if it does, calculate `jump_p` (the amount to move forward in the pattern) and `jump_s` (the amount to move forward in the string).

> ![](images/00236.jpg)

Note the behaviour of the `?` case carefully, with regard to its specification – this kind of matching code can be rather subtle. To deal with `*` we must have a way of matching zero or more instances of a character, moving as far along the string as possible. The function `swallow_all` below, given a character `ch`, a string `p` and a position `sp`, returns the number of characters which match `ch` starting at `sp`. We can then add a match case for the `*` specifier, as shown in Figure [9.1](#index_split_015.html_filepos188284).

* * *

> ![](images/00242.jpg)

> Figure 9.1:

* * *

The `+` character can be added with `swallow_all` too, but we must check that there is at least one matching character. Figure [9.2](#index_split_015.html_filepos189225) shows the whole program in one place.

* * *

> ![](images/00247.jpg)

> Figure 9.2:

* * *

Questions

1.  Write a function to return the number of matches of one string in another a) when all matches are considered and b) when only non-overlapping matches are considered.
2.  Write functions which return the position and length of the longest prefix of a string in another. That is to say, the longest initial part of the pattern which matches anywhere in the string.
3.  Compare the speed of the first two versions of `search` given in this chapter.
4.  Add the special symbol `\` to our final search program. It indicates that the following symbol is not a special symbol, but a normal character. Note that, we must write `'\\'` for that character in OCaml code.
5.  Add a labelled argument of type bool whose value, when true, indicates a case-insensitive search.

Chapter 10
Finding Permutations

How can we calculate the n! permutations of a given list of length n? For example, given the list `[1; 2; 3]` we should like to find `[[1; 2; 3]; [2; 1; 3]; [2; 3; 1]; [1; 3; 2]; [3; 1; 2]; [3; 2; 1]]` or similar (we are not concerned with the order of the list of permutations). So, we require a function of type α list → α list list.

Sometimes it is useful with a hard problem like this to simply start writing, working out what gaps there are, and then filling them in. The base case for our `perms` function is trivial: there is one permutation of the empty list, namely the empty list itself:

> ![](images/00251.jpg)

For the main case, let us try the most simple decomposition. We calculate the permutations of the tail for free with recursion, and then combine the result in some way with the head:

> ![](images/00257.jpg)

Here, `combine` is a function we have yet to concoct. It must take a list of permutations, such as `[[3;` `2]; [2; 3]]` and a single element, such as `1`, and produce `[[1; 2; 3]; [2; 1; 3]; [2; 3;` `1]; [1; 3; 2]; [3; 1; 2]; [3; 2; 1]]`. The elements of this list can be produced by placing `1` in each possible place in each list in `[[3; 2]; [2; 3]]`. So first, we will reduce the problem by using `List.map` with an as-yet-unwritten function `interleave`, combining the results with `List.concat`:

> ![](images/00261.jpg)

Now, we just need to build the function `interleave` which takes an item, such as `1` and a list such as `[2; 3]` and builds the list `[[1; 2; 3]; [2; 1; 3]; [2; 3; 1]]` by placing the item at each possible position in the list.

> ![](images/00268.jpg)

This function maintains a list of the elements already seen (which is initially empty), building each new list. When the input list is empty, the final one is generated. Thus, we avoid any kind of counter to know when we are finished. For example, consider a call to `interleave` in our example:

![](images/00273.jpg)

Now we can write the whole thing out:

> ![](images/00278.jpg)

Here are the 24 permutations of the list `[1; 3; 5; 7]`:

`# perms [1; 3; 5; 7];;`
`- : int list list =`
`[[1; 3; 5; 7]; [3; 1; 5; 7]; [3; 5; 1; 7]; [3; 5; 7; 1]; [1; 5; 3; 7];`
` [5; 1; 3; 7]; [5; 3; 1; 7]; [5; 3; 7; 1]; [1; 5; 7; 3]; [5; 1; 7; 3];`
` [5; 7; 1; 3]; [5; 7; 3; 1]; [1; 3; 7; 5]; [3; 1; 7; 5]; [3; 7; 1; 5];`
` [3; 7; 5; 1]; [1; 7; 3; 5]; [7; 1; 3; 5]; [7; 3; 1; 5]; [7; 3; 5; 1];`
` [1; 7; 5; 3]; [7; 1; 5; 3]; [7; 5; 1; 3]; [7; 5; 3; 1]]`

Note that our function does not work properly when there are duplicates in the list – it will treat each item as if it were different:

`# perms [1; 1; 2];;`
`- : int list list =`
`[[1; 1; 2]; [1; 1; 2]; [1; 2; 1]; [1; 2; 1]; [2; 1; 1]; [2; 1; 1]]`

In this implementation, we run into problems with the lack of tail recursion well before we run out of memory to store the permutations:

`# List.length (perms [1; 2; 3; 4; 5; 6; 7; 8]);;`
`- : int = 40320`
`# List.length (perms [1; 2; 3; 4; 5; 6; 7; 8; 9]);;`
`- : int = 362880`
`# List.length (perms [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]);;`
`Stack overflow during evaluation (looping recursion?).`

To fix this up, we must rewrite `interleave` to be tail recursive by adding an accumulating argument:

> ![](images/00281.jpg)

Now, we can go as far as we have time and memory (though the permutations are in a different order – can you fix that?)

Another method of finding permutations, which gives a shorter solution, is to choose each element of the input list and use that as the first element, prepending it to each of the permutations of the remaining list. First, let us define a function to remove the (first) occurrence of a given element from a list:

> ![](images/00286.jpg)

It need not be tail-recursive, since this list will always be small. Now, we can write the new `perms` function. The base case is the same. In the main case, we use `List.map` twice. The inner `map` prepends a given element to each of the permutations of the list without that element. The outer `map` uses that over each of the elements of the input, selecting each in turn as the first element. The results are then concatenated.

> ![](images/00292.jpg)

This function has the advantage of producing the items in proper lexicographic (dictionary) order:

`[[1; 2; 3]; [1; 3; 2]; [2; 1; 3]; [2; 3; 1]; [3; 1; 2]; [3; 2; 1]]`

Permutations one at a time

There is a well-known imperative algorithm for generating the lexicographically-next permutation given the current one. We can use this to build a function to generate all the permutations without the heavy recursion of our previous programs and, more interestingly, to build a lazy list of all the permutations, which requires minimal computation each time a new permutation is needed.

We begin with a sorted array, such as `[|1; 2; 3|]`. This is the first permutation. We generate new permutations until the array is in reverse-sorted order – `[|3; 2; 1|]` – this is the final permutation. In order to find the lexicographically-next permutation there are four steps:

1.  Find the right-most item which is smaller than its next item. Call this the “first” item. This is the item which must be altered to find the permutation which is the smallest distance from the current one in the lexicographic order.
2.  Find the smallest item to the right of the “first” item which is greater than it. Call this the “last” item. This is the item which will go in the position of the “first” item.
3.  Swap these two characters.
4.  Sort everything to the right of the original index of the “first” item into lexicographic order. This ensures we have selected the next permutation, not any later one.

Marking the first item with F and the last item with L, we have `[|1; 2`^(`F`)`; 3`^(`L`)`|]` -→ `[|1`^(`F`)`; 3; 2`^(`L`)`|]` -→ `[|2;` `1`^(`F`)`; 3`^(`L`)`|]` -→ `[|2`^(`F`)`; 3`^(`L`)`; 1|]` -→ `[|3; 1`^(`F`)`; 2`^(`L`)`|]` -→ `[|3; 2; 1|]`. The `first` function finds the index of the “first item” in an array:

> ![](images/00297.jpg)

The corresponding `last` function is a little more awkward, needing to check two conditions and using a special initializer, rather than simply initializing with the last element as `first` does.

> ![](images/00029.jpg)

Two simple utility functions, to swap given indices in an array, and sort a sub-array given its offset and length:

> ![](images/00009.jpg)

Now we are ready to write `next_permutation`:

> ![](images/00151.jpg)

We define a predicate for non-increasing-ness:

> ![](images/00120.jpg)

And, finally, we are finished:

> ![](images/00145.jpg)

Note that this imperative algorithm works correctly with repetitions of elements – it will include the permutation only once. We can now generate a repeating lazy list of all the permutations of a given list, using our standard lazy list type from Chapter [2](#index_split_008.html_filepos58917):

> ![](images/00169.jpg)

This very imperative algorithm has now been dressed in functional clothes.

Questions

1.  Write a function to generate all the unordered combinations of items from a list. For example, for the list `[1; 2; 3]`, the result, whose order is not important, might be `[[]; [1]; [2]; [3];` `[1; 2]; [1, 3]; [2; 3]; [1; 2; 3]]`.
2.  Generate all the “permicombinations” – that is all the permutations of all the combinations of a list. For the list `[1; 2; 3]` this might be `[[]; [1]; [2]; [3]; [1; 2]; [2; 1]; [1; 3]; [3;` `1]; [2; 3]; [3; 2]; [1; 2; 3]]`.
3.  Write a function to give the list of all possible lists of length n containing just `true` and `false`.
4.  The sorting phase of the imperative algorithm can be replaced with a simple list reversal, since the items are already in reverse lexicographic order each after the swap. Implement this.
5.  The imperative algorithm could be defined in terms of lists, in a functional fashion. Demonstrate this.

Chapter 11
Making Sets

In this chapter, we will look at various naive and sophisticated data structures for storing sets. We will look at their theoretical performance characteristics and time them against one another on various sorts of data to learn about their performance in practice. Along the way, we will learn about some of OCaml’s more advanced modular abstraction mechanisms. For each set representation, we will give the following five functions:

*   `set_of_list` which builds a set from a list (which may contain duplicates). The empty set is built with `set_of_list []`;
*   `list_of_set` which returns, in no particular order, a list of the elements in the set;
*   `insert` which inserts a given element into the set, if it is not already present;
*   `size` which returns the number of elements in the set; and
*   `member` which tests if an element is present in the set.

Simple lists

Figure [11.1](#index_split_017.html_filepos212726) exhibits these five functions by representing sets using the built-in list type. They are largely trivial, save for `set_of_list` which works by repeated insertion into the existing set.

* * *

> ![](images/00200.jpg)

> Figure 11.1:

* * *

These functions are not terribly efficient. The `member`, `size`, and `insert` functions take time proportional to the size of the set. The `set_of_list` function is worse: it takes time proportional to the square of the size of the set, since it uses `insert` for each element on a growing list. The only bright spot is `list_of_set` which (of course) runs in constant time.

We have not hidden the type of the sets – they may be manipulated by the caller as plain lists – and so the abstraction is not safe or complete. Here is an interface as a `.mli` file, abstracting the real type of the set to just α t .

> ![](images/00222.jpg)

Here is the corresponding `.ml` file with the implementation:

> ![](images/00253.jpg)

Recall that, by hiding the implementation behind an interface, we can swap implementations at will, making them more efficient, or fixing bugs.

Since we wish to build several of these set implementations, and benchmark them, it is a good time to look at OCaml’s syntax for putting several modules in a single source file. Figure [11.2](#index_split_017.html_filepos216015) exhibits a piece of OCaml which corresponds to our `.ml` and `.mli` file all in one place:

* * *

> ![](images/00283.jpg)

> Figure 11.2:

* * *

The general syntactic form is:

`module` module name `:`
`  sig`
contents of .mli file
`  end`
`=`
`  struct`
contents of .ml file
`  end`

When this code is pasted into the top level, or loaded in some other way, a new module SetList is available, with functions like `SetList.size` available through the given interface.

Since all our different implementations of sets will share the same interface as SetList, we will split this module definition up using the `module type` syntax to define the signature, and the `include` keyword to use that signature for our module:

> ![](images/00012.jpg)

Thus, we have avoided duplication of the interface. Each new set representation will just need an implementation.

Performance

Each use of the set data type is different – sometimes there is an initial phase of insertions, followed by millions of membership tests with no insertions. Sometimes insertions and membership tests are equally likely. Some functions may not be required at all. We shall consider two benchmarks for insertion:

*   the insertion of the integers 1…50000 in a randomized order; and
*   the insertion, in order, of the 50000 integers 1…50000.

Then, we will, for each of these “ordered” and “unordered” cases:

*   perform 50000 membership tests in the range of numbers 1…100000, so that half are present and half not;
*   calculate the number of elements in the set;
*   calculate the size of the set.

Here are the results:

![](images/00042.jpg)

The big difference is in the time for the membership tests, due to the balance or lack of balance in the tree, as expected. When we introduce more ways of storing sets, we will do the same tests, and compare the results.

Binary Search Trees

A binary search tree is a binary tree with the property that all elements in the left sub-tree of each node are smaller than it, and all elements in the right sub-tree are larger. If the tree is reasonably well balanced, we can reach any element in time proportional to the logarithm of the number of elements in the set.

Just like the representation of sets, there are multiple representations of sets, depending upon the order of insertion of the elements. Here are the trees corresponding to the insertion orders 123, 132, 213, 231, 312, 321:

![](images/00070.jpg)

We can see that when the items in the set are added in numerical or reverse-numerical order, this data structure is equivalent to, and has no better performance, than a simple list. The data type is the usual one for binary trees:

`type 'a t = Lf | Br of 'a t * 'a * 'a t`

The SetTree module is shown in Figure [11.3](#index_split_017.html_filepos222216).

* * *

> ![](images/00241.jpg)

> Figure 11.3:

* * *

When the tree is balanced `insert` and `member` run in logarithmic time. The `size` function runs in linear time, since it must visit every node irrespective of the balance. The same is true of `list_of_set`. When unbalanced, `insert` and `member` take linear time. We can extend our table now:

![](images/00048.jpg)

Notice that, in the unordered case, performance is dramatically increased for insertion and membership, by about two hundred times. However, if the elements are inserted in order, the unbalanced tree actually takes longer to build than its equivalent list. Finding all the elements as a list also takes a huge amount of time in the ordered insertion case.

Balanced trees

We have seen that binary search trees are only useful if they are reasonably close to balanced. In recent decades, several data structures have been developed which try to keep a binary tree “reasonably balanced”, such that operations remain efficient. “Red-Black trees” are one such commonly used and interesting data structure. Red-Black trees were invented by Rudolf Bayer, and the functional formulation presented here is due to Chris Okasaki in his landmark book “Purely Functional Data Structures” (Cambridge University Press, 1998).

A Red-Black tree is an ordinary binary tree with one addition: each node is either Red or Black. Leaf nodes are considered Black. The balance is ensured by every operation which alters the tree (in our case, just `insert`) so that the following remains true:

*   the children of each Red node are Black; and
*   each path from root to leaf contains an equal number of Black nodes.

These two rules, together, ensure that the tree is reasonably balanced – the longest path from root to leaf (Black, Red, Black, Red … Black) is no more than twice as long as the shortest path (Black, Black, Black … Black). Thus, the maximum depth of a Red-Black tree is proportional to the logarithm of the number of elements in the set. Here is an example valid Red-Black tree, with 3 black nodes in each path:

![](images/00182.jpg)

Here are the types for representing a Red-Black tree – we have just added a new colour field to each branch of the tree:

`type colour = R | B`

`type 'a t = Lf | Br of colour * 'a t * 'a * 'a t`

The `list_of_set`, `size`, and `member` functions are simple to alter: they just ignore the colour field. The `insert` function, however, must be modified to preserve the Red-Black properties.

As with ordinary binary search trees, the new node added by `insert` will be in place of a leaf node. We colour it Red, to make sure that the invariant that no path can have a differing number of black nodes in it is not broken. However, this may break the other invariant (that no Red node has a Red parent). It turns out that, by considering the parent and grandparent of the newly-inserted node, performing a simple operation, and possibly continuing this process upward, we can restore this invariant, and efficiently. The following diagrams, à la Okasaki, illustrate the process:

![](images/00022.jpg)

In each case, the nodes x,y,z and the sub-trees α,β,γ,δ remain in the same order, so the binary tree invariant is preserved. Pattern matching is particularly elegant here, since all but one of our cases have the same result:

> ![](images/00163.jpg)

Now, we can write the insertion function itself:

> ![](images/00004.jpg)

Note that we wrap it in a function to set the root of the tree to Black – balancing will not do this, since the root has no parent or grandparent to compare with, and so we may otherwise end up with a red root with a red child. The full module is shown in Figure [11.4](#index_split_017.html_filepos229499).

* * *

> ![](images/00269.jpg)

> Figure 11.4:

* * *

Since we have guaranteed that the tree will be reasonably balanced, there is no need for tail recursive functions, even for huge sets. The effect of balanced trees on performance is clear, and there appears to be little or no slow-down from the more complex Red-Black data structure:

![](images/00285.jpg)

Hash Tables

A hash table is a data structure designed to provide very fast insertion of and access to data in sets and maps. It holds a set of buckets 0...n. When we insert a value into the set, it is processed via a hash function which allocates it to a bucket, in such a manner that there should be a roughly uniform distribution of values among the buckets. When we need to test membership for an item, the same hash function is applied, and we need only search in one bucket. If the hash function works well and the number of buckets is appropriate, lookup is in constant time regardless of how many items are in the set.

For example, if the hash function is x-→x mod 23 and the data to be inserted is 34, 2, 67, 3, 4, 84, 1467, 7432, 48, 1 then the buckets would be 11, 2, 21, 3, 4, 15, 18, 3, 1, 1\. The membership test for 67 now consists of applying the hash function, and then searching in bucket 21 to see if 67 is there.

The OCaml Standard Library provides a hash table implementation in the module Hashtbl. To build a hash table for a set, we use a hash table which maps from α to unit, of type (α, unit) Hashtbl.t. It is simple to build an implementation matching our signature, using the functions `Hashtbl.mem`, `Hashtbl.add`, `Hashtbl.create`, and `Hashtbl.iter`, as shown in Figure [11.5](#index_split_017.html_filepos233285).

* * *

> ![](images/00175.jpg)

> Figure 11.5:

* * *

The disadvantage is that hash tables are mutable data structures, and so operations like `insert` mutate the structure. The result of `insert`, then, alters the set rather than creating a new set. This means that whilst the SetType interface is technically satisfied, our intended abstraction is actually broken. Such is mutability. The performance on our benchmarks, however, is clear:

![](images/00265.jpg)

The benchmarking programs may be found in the online resources.

Questions

1.  Compare our set representations with regard to the amount of memory required to create and store them. You can use the functions from the Gc module in OCaml’s Standard Library to find out how many words of memory have been allocated before and after allocating a large set in each set representation.
2.  Write functions (naive if necessary) to perform the “union” operation on sets in each representation. The union of two sets is the set of elements present in one or the other or both of them. After the operation, both inputs should still be available as sets.
3.  OCaml has a built-in Set module. It uses advanced module syntax not discussed here, but you can build a module for manipulating sets of integers like this:

    `module S = Set.Make (struct type t = int let compare = compare end)`

    This new module S provides, amongst others, a type t for sets, and `add`, `elements`, `mem`, `empty`, and `cardinal` functions, whose definitions you can find in the OCaml manual. Use these functions to build a set module with a similar interface to ours. Comment on its speed for our examples.

4.  We can save memory in the definition of Red-Black trees by having two different `Br` nodes, one for Red and one for Black, instead of storing the colour. Implement this. How much memory is saved? How much extra complexity is there in the source code?

Chapter 12
Playing Games

The childhood game of Noughts and Crosses is a combinatorial problem of a large but manageable size. Let us review the rules, and then see if we can build the game tree (that is, a structure describing all possible games), and draw some statistics from it.

A 3-by-3 grid is constructed. Two players (O and X) take turns, beginning with O, to place their piece in an empty space. The game is won if or when a player forms three pieces in a row, column, or diagonally. The game is drawn if the board is full and no such pattern has been formed. For example, in this board, player O has won, building a diagonal:

![](images/00112.jpg)

Let us consider the shape of the game tree. Clearly, at the top level, it will branch nine ways, since O can be placed in any square. Then eight ways, seven ways and so on. Once we reach the fifth level, some of the games have been won (since three pieces from player O may form a line), and so the number of branches may be reduced. The tree must end after nine levels, since the board must at least be full, even if no-one has won. A fragment of the game tree is shown in Figure 12.1. Let us begin to construct the program. We will need a type to represent X, O and the empty square:

* * *

![](images/00246.jpg)        

> Figure 12.1:

* * *

`type turn = O | X | E`

It would be natural to use a nine-tuple, since the board is of a fixed size. Then, though, we lose the ability to use the standard list-processing functions such as `List.map` over the boards. So, at the cost of a little inelegance, we will use a list of length nine instead – in other words a `turn` `list`.

We need to terminate the tree when X has won, O has won, or the board is full. Thus we will need to check all the rows, columns, and diagonals. We do not want to replicate the logic several times or build a huge pattern match, so it is easiest to write a function which takes a list of nine booleans and just checks for lines of `true`. We can then use `List.map` on the board itself to build these intermediate lists of booleans.

> ![](images/00093.jpg)

We can number the positions in our board:

![](images/00225.jpg)

Now, we can use functions from the List module to write a function to return the numbers of the positions which are currently empty:

> ![](images/00073.jpg)

This works by building the list of tuples `[(X, 1); (E, 2); (E, 3)` …`(O, 9)]`, filtering out any which are not empty, and extracting the list of empty positions `[2, 3` …`]`. It is also simple to write a function which, given a board like `[E; E; E; E; X; E; O; E; E]`, a turn like `O` and a number such as 8, will fill in the correct slot in the board to produce `[E; E; E; E; X; E; O; X; E]`. The `take` and `drop` functions from our Util module (described on page xiii) are ideal:

> ![](images/00210.jpg)

One more simple function is required before we can write the main tree-building function, and that is to change whose turn it is:

> ![](images/00053.jpg)

What should the type of the game tree be? Each node needs a list of turn elements representing the board, and a list of zero or more trees representing the game resulting from each possible move. Since the list can have zero elements, we need no separate leaf constructor:

`type tree = Move of turn list * tree list`

Now we may construct the main function. Our job is to build, given a turn (X or O) and the current board, the tree starting at that board. If the board has been won by either player, the list of next nodes is empty, and the recursion stops. If not, we calculate the empty positions, build a new board with each empty position filled in with the current turn, and then map `next_moves` over each of those.

> ![](images/00192.jpg)

Note that the recursion stops when a board is full (drawn) because `empty` returns the empty list in this case. Now we can build the game tree itself, which might take a second or so:

> ![](images/00017.jpg)

This results in the tree shown below.

> ![](images/00045.jpg)

You can see the first ending position in this game tree is `[O; X; O; X; O; X; O; E; E]`. You can also see several drawn games. We can now use this game tree to calculate how many games are won by a given player:

> ![](images/00076.jpg)

This tells us, reasonably quickly, that O wins 131184 games. The questions at the end of this chapter ask you to work out more of these numbers. Here is the full code in one place:

> ![](images/00105.jpg)

In the questions, you will extract the rest of the statistics from the tree, and build some alternative representations.

Questions

1.  In how many cases does X win? How many possible different games are there? How many end in a draw?
2.  Build a lazy version of our game tree, where nodes are only created when explored. Now write a function to work out how many times O and X win or the game is drawn if O goes first and picks the centre slot. What about if O picks a corner? The middle of a side?
3.  Another way to check if someone has won is to rearrange the board numbers into a so-called magic square, where each row, column or diagonal sums to 15:

    ![](images/00133.jpg)

    Now, a player has won if they have any three positions summing to 15\. Re-implement our game tree program using this alternative representation.

> GENERATING PDF DOCUMENTS
> an extended example

Chapter 13
Representing Documents

In this chapter we will define a data type for representing a PDF document. PDF is a structured format for describing a wide variety of graphical and textual data. The PDF file format itself is large and complex, but we will introduce only the parts required for our examples. It is relatively easy to write PDF files but rather harder to read them, so we will concentrate on creating PDF data structures in memory, and then writing them to valid files. Here is an example PDF, as it might be displayed in a PDF viewer:

![](images/00158.jpg)

Here is the corresponding code, which you would see if you opened the PDF file in a plain text editor:

`%PDF-1.1  `
`1 0 obj  `
`<</Type /Page  `
`  /Parent 3 0 R  `
`  /Resources  `
`    <</Font  `
`       <</F0  `
`          <</Type /Font /Subtype /Type1 /BaseFont /Times-Italic>>>>>>  `
`       /MediaBox [0 0 595.275590551 841.88976378]  `
`       /Rotate 0 /Contents [4 0 R] >>  `
`endobj  `
`2 0 obj  `
`<</Type /Catalog /Pages 3 0 R>>  `
`endobj  `
`3 0 obj  `
`<</Type /Pages /Kids [1 0 R] /Count 1>>  `
`endobj  `
`4 0 obj  `
`<</Length 53>>  `
`stream  `
`1 0 0 1 50 770 cm BT /F0 36 Tf (Hello, World!) Tj ET  `
`endstream  `
`endobj  `
`xref  `
`0 5  `
`0000000000 65535 f  `
`0000000015 00000 n  `
`0000000200 00000 n  `
`0000000245 00000 n  `
`0000000296 00000 n  `
`trailer  `
`<</Size 5 /Root 2 0 R>>  `
`startxref  `
`397  `
`%%EOF`

Rather complicated, as we can see. Our first job is to define a pleasant OCaml data type for PDF documents, which can then be flattened to the format above when written to a file.

The main body of a PDF file is a set of numbered objects – there are four in the example above, from `1 0` `obj` to `4 0 obj`. Each one contains some structured data, such as the dictionary `<</Type /Pages /Kids [1 0` `R] /Count 1>>` which associates the keys `/Type`, `/Kids`, and `/Count` to the name `/Pages`, the array `[1 0 R]`, and the integer `1` respectively. Before and after the main body is some ancillary data, most of which we do not need to hold in our data structure – it is generated upon writing. Here are all the kinds of data we will be using:

*   Booleans, like `true` and `false`
*   Integers, such as 4, 256, -1
*   Floating-point numbers such as 1.585
*   Strings, like `(a string)` which are sequences of characters within parentheses
*   Names, like `/Name`
*   Ordered arrays of objects such as `[1 2 4]`
*   Dictionaries, which are unordered collections of key-value pairs, where the keys are names. For example, `<</One 1 /Two 2 /Three 3>>`.
*   Streams, like object 4 in the example above, which are arbitrary sequences of bytes.
*   Indirect references, like `4 0 R` which point to another object by its number (here, object 4).

Here is an OCaml data type to hold such data:

`type pdfobject =`
`  Boolean of bool`
`| Integer of int`
`| Float of float`
`| String of string`
`| Name of string`
`| Array of pdfobject list`
`| Dictionary of (string * pdfobject) list`
`| Stream of pdfobject * string`
`| Indirect of int`

Note that it is recursive, mirroring the structure of the data. For example, object 3 in the example above, that is `<</Type /Pages /Kids [1 0 R] /Count 1>>`, will be represented as:

`Dictionary`
`  [("/Type", Name "/Pages"); ("/Kids", Array [Indirect 1]); ("/Count", Integer 1)]`

Now, we need a type to represent the whole document, which contains a list of these objects, the PDF version number (1.1 in the example above), and the trailer dictionary (`<</Size 5 /Root 2 0 R>>` above). Everything else is generated upon writing. It is traditional to name the main type of a module t:

`type t =`
`  {version : int * int;`
`   objects : (int * pdfobject) list;`
`   trailer : pdfobject}`

We put these two types into `pdf.ml` and `pdf.mli`. Here is how we might build an instance of this data type representing our example PDF:

`let objects =`
`  [(1,`
`     Pdf.Dictionary`
`       [("/Type", Pdf.Name "/Page");`
`        ("/Parent", Pdf.Indirect 3);`
`        ("/Resources",`
`           Pdf.Dictionary`
`             [("/Font",`
`              Pdf.Dictionary`
`                [("/F0",`
`                  Pdf.Dictionary`
`                    [("/Type", Pdf.Name "/Font");`
`                     ("/Subtype", Pdf.Name "/Type1");`
`                     ("/BaseFont", Pdf.Name "/Times-Italic")])])]);`
`        ("/MediaBox",`
`          Pdf.Array`
`            [Pdf.Float 0.; Pdf.Float 0.;`
`             Pdf.Float 595.275590551; Pdf.Float 841.88976378]);`
`        ("/Rotate", Pdf.Integer 0);`
`        ("/Contents", Pdf.Array [Pdf.Indirect 4])]);`
`   (2,`
`     Pdf.Dictionary`
`       [("/Type", Pdf.Name "/Catalog");`
`        ("/Pages", Pdf.Indirect 3)]);`
`   (3,`
`     Pdf.Dictionary`
`       [("/Type", Pdf.Name "/Pages");`
`        ("/Kids", Pdf.Array [Pdf.Indirect 1]);`
`        ("/Count", Pdf.Integer 1)]);`
`   (4,`
`     Pdf.Stream`
`       (Pdf.Dictionary [("/Length", Pdf.Integer 53)],`
`        "1 0 0 1 50 770 cm BT /F0 36 Tf (Hello, World!) Tj ET"))]`

`let hello =`
`  {Pdf.version = (1, 1);`
`   Pdf.objects = objects;`
`   Pdf.trailer =`
`   Pdf.Dictionary`
`    [("/Size", Pdf.Integer 5);`
`     ("/Root", Pdf.Indirect 2)]}`

The advantage of using this data structure as opposed to generating the PDF file directly is that it may be programmatically manipulated with ease, using pattern matching and other standard OCaml techniques. Note that the content of the page itself `"1 0 0 1 50 770 cm BT /F0 36 Tf (Hello, World!) Tj ET"` remains a plain string. We shall look at this separate language soon.

In the next three chapters, we will learn how to write this representation to a file, and add our own text and graphics to the page.

Questions

1.  Draw the graph of the relationships, via indirect references such as `3 0 R`, of the objects 1, 2, 3, 4 and the trailer dictionary.
2.  Represent the following PDF objects using our data type:
    *   `/Name`
    *   `(Quartz Crystal)`
    *   `<</Type /ObjStm /N 100 /First 807 /Length 1836 /Filter /FlateDecode>>`
    *   `[1 2 1.5 (black)]`
    *   `[1 2 0 R]`
3.  PDF files can contain arbitrary objects, which will be ignored by a PDF reader if they are not understood. Design a way of representing items of the following type using one or more PDF objects:

     `type tree = Lf | Br of tree * int * tree`

4.  Write a function of type pdfobject → pdfobject which, given an object, replaces the value of any dictionary entry with key `/Rotate` to `90`.

Chapter 14
Writing Documents

We have built a representation for PDF documents to be held in memory, and defined an example document. Now, we must build functions to write this to file. Recall our example file from the last chapter:

`%PDF-1.1  `
`1 0 obj  `
`<</Type /Page  `
`  /Parent 3 0 R  `
`  /Resources  `
`    <</Font  `
`       <</F0  `
`          <</Type /Font /Subtype /Type1 /BaseFont /Times-Italic>>>>>>  `
`       /MediaBox [0 0 595.275590551 841.88976378]  `
`       /Rotate 0 /Contents [4 0 R] >>  `
`endobj  `
`2 0 obj  `
`<</Type /Catalog /Pages 3 0 R>>  `
`endobj  `
`3 0 obj  `
`<</Type /Pages /Kids [1 0 R] /Count 1>>  `
`endobj  `
`4 0 obj  `
`<</Length 53>>  `
`stream  `
`1 0 0 1 50 770 cm BT /F0 36 Tf (Hello, World!) Tj ET  `
`endstream  `
`endobj  `
`xref  `
`0 5  `
`0000000000 65535 f  `
`0000000015 00000 n  `
`0000000200 00000 n  `
`0000000245 00000 n  `
`0000000296 00000 n  `
`trailer  `
`<</Size 5 /Root 2 0 R>>  `
`startxref  `
`397  `
`%%EOF`

It consists, we remember, of a header, then some objects (here, four), and a trailer. We will need four functions:

1.  The function `string_of_pdfobject` to make a string from a Pdf.pdfobject, for example making the string `"<</Type /Pages /Kids [1 0 R] /Count 1>>"` from the pdfobject `Dictionary` `[("/Type", Name "/Pages"); ("/Kids", Array [Indirect 1]); ("/Count", Integer 1)]`;
2.  The function `write_header` to write the header (i.e. everything before the objects);
3.  The function `write_trailer` to write the trailer (i.e. everything after the objects); and
4.  The main function `pdf_to_file` which uses these three functions to write a Pdf.t to a file under the given file name.

The function `string_of_pdfobject` is best expressed as a set of mutually-recursive functions introduced with the `let rec … and …` construct. To give it as a single function is possible, but would be rather large, and so harder to read and edit. Let us present it piece-by-piece and then all at once.

First, the main part. Given an object we wish to produce its string, assuming that `string_of_array`, `string_of_dictionary`, and `string_of_stream` exist:

> ![](images/00185.jpg)

The cases are all simple, except for the ones we have put aside to be implemented separately. Strings must be put between parentheses, indirect references are printed as `2 0 R` etc.

To build a string from an `Array`, we need to start with an open square bracket, add the string for each Pdf.pdfobject in the array (which may be arbitrarily complex, of course), and put spaces between them. Then we end with a close square bracket:

> ![](images/00233.jpg)

It is natural to use the Buffer module from the Standard Library to collect these strings together. It is also more efficient than using string concatenation. Notice we do not add an initial space after the square bracket, but do before the closing square bracket, for symmetry. The `string_of_dictionary` function is somewhat similar:

> ![](images/00237.jpg)

Now for `string_of_stream`. A stream in PDF is written like this:

stream dictionary
`stream`
stream data
`endstream`

This is simple with the Buffer module too:

> ![](images/00270.jpg)

* * *

> ![](images/00060.jpg)

> Figure 14.1: Our mutually recursive functions to build a string from a Pdf.pdfobject

* * *

The code for these four functions is collected together in Figure [14.1](#index_split_021.html_filepos271214). Now that we can build a string from any Pdf.pdfobject, we can proceed to build the `write_header`, `write_trailer`, and `write_objects` functions, so that we have everything we need for the final `pdf_to_file` function.

The PDF header consists of `%%PDF-`m`.`n where m and n are the major and minor version numbers. This is easy to build with `Printf.sprintf`:

> ![](images/00199.jpg)

The `write_objects` function, which is given a list of (int × Pdf.pdfobject) pairs, sorts the objects by their number, and then outputs each object using `string_of_pdfobject`. For example, the pair

`(3,  `
`  Dictionary  `
`    [("/Type", Name "/Pages"); ("/Kids", Array [Indirect 1]); ("/Count", Integer 1)])`

will be written to file like this:

`3 0 obj  `
`<< /Type /Pages /Kids [1 0 R] /Count 1 >>  `
`endobj`

The function collects and returns a list of the byte offsets of the objects written, since this will be needed to write the trailer section, which we shall describe in a moment.

> ![](images/00147.jpg)

Now, we can write the trailer. That is to say, this section:

`xref  `
`0 5  `
`0000000000 65535 f  `
`0000000015 00000 n  `
`0000000230 00000 n  `
`0000000279 00000 n  `
`0000000338 00000 n  `
`trailer  `
`<< /Size 5 /Root 2 0 R >>  `
`startxref  `
`440  `
`%%EOF`

This consists largely of a list of the byte offsets of the four objects in the file (15, 230, 279, 338), the trailer dictionary, and so on. It is not necessary to understand it in detail. This is the first section which would be read by a PDF reader, to find the actual objects in the file.

> ![](images/00085.jpg)

Now the main function is simple. We open the file, write the header, objects, and trailer, and close the file. In the event of an exception, we close the file to clean up, and re-raise it.

> ![](images/00114.jpg)

This code goes into `pdfwrite.ml`. The interface `pdfwrite.mli` is very simple. We expose only
`pdf_to_file`:

> ![](images/00141.jpg)

Here is the output of our program on the example Pdfhello.hello:

`%PDF-1.1 `
`1 0 obj `
`<< /Type /Page /Parent 3 0 R /Resources << /Font << /F0 << /Type /Font /Subtype /Type1 /BaseFont /Times-Italic >> >> >> /MediaBox [ 0. 0. 595.275590551 841.88976378 ] /Rotate 0 /Contents [ 4 0 R ] >> `
`endobj `
`2 0 obj `
`<< /Type /Catalog /Pages 3 0 R >> `
`endobj `
`3 0 obj `
`<< /Type /Pages /Kids [ 1 0 R ] /Count 1 >> `
`endobj `
`4 0 obj `
`<< /Length 53 >> `
`stream `
`1 0 0 1 50 770 cm BT /F0 36 Tf (Hello, World!) Tj ET `
`endstream `
`endobj `
`xref `
`0 5 `
`0000000000 65535 f `
`0000000015 00000 n `
`0000000230 00000 n `
`0000000279 00000 n `
`0000000338 00000 n `
`trailer `
`<< /Size 5 /Root 2 0 R >> `
`startxref `
`440 `
`%%EOF`

This loads correctly into a PDF viewer. Notice that some of the spacing is different from the specimen PDF we had at the top of the chapter – this does not matter. Now we can move on to putting more interesting content on the page of our PDF documents.

Questions

1.  Modify the code so that arrays and dictionaries do not have spaces at either end of them (these spaces are not required). For example, we should see `[2 0 R]` rather than `[ 2 0 R ]`.
2.  Build an example PDF with three pages. This will have three entries in its `/Kids` array, and three page objects. The page contents may be shared by the three pages if desired. You will need to number the additional objects carefully.
3.  Modify the program to use our byte-by-byte compression algorithm from Chapter 6 to compress the content stream in the “Hello, World” program. You will need to fix the `/Length` and add `/Filter /RunLengthDecode` to the stream dictionary. Now modify the program to use our bit-by-bit compression algorithm from the same chapter with `/Filter /CCITTFaxDecode`. You will need to add the following entry to the stream dictionary, in addition to altering the `/Filter` entry:

    `("/DecodeParms",  `
    `    Pdf.Dictionary  `
    `      [("/Rows", Pdf.Integer 1);  `
    `       ("/Columns", Pdf.Integer (52 * 8));  `
    `       ("/BlackIs1", Pdf.Boolean true);  `
    `       ("/EndOfBlock", Pdf.Boolean false)])`

    The number 52 is the number of bytes of data in our example.

Chapter 15
Pretty Pictures

We have not yet explained the structure of the code which put “Hello, World!” on the page. Here it is again:

`1 0 0 1 50 770 cm BT /F0 36 Tf (Hello, World!) Tj ET`

It is a list of operator-operand sequences. Each sequence consists of zero or more operands and one operator. The sequences in our example are:

![](images/00166.jpg)

In this chapter we will introduce a few simple operators for drawing lines and filling shapes (in the next chapter we discuss adding text and build a basic typesetter). Here are the operators we will be using to start with:

![](images/00194.jpg)

Here is a data type, which forms part of the new Pdfpage module, which encodes these operators. We will extend it with new operators when required.

`type t =`
`    Move of float * float`
`  | Line of float * float`
`  | Close`
`  | Stroke`
`  | Fill`
`  | FillColour of float`
`  | StrokeColour of float`

In order to put these into the PDF document, we will need to convert each set of operands and operator to a string. This is simple:

> ![](images/00284.jpg)

Now we can put them together into a single string by using functions from the Buffer module, putting a space character after each.

> ![](images/00248.jpg)

Here is a very simple example – we move to (100, 100), make three lines and close the path. Then we use the `Fill` operator. Coordinates in PDF have the origin at the bottom left of the page.

> ![](images/00279.jpg)

Our page looks like this:

![](images/00007.jpg)

Not all sequences of operators are valid, and our data type makes no checks to ensure our list is correct. This could be solved by building a higher-level data type which would then be flattened down to a list of Pdfpage.t elements. In our examples, and in the questions at the end of the chapter, it is sufficient to stick to the pattern above – one `Move`, one or more `Line`s, a `Close` (if filling), and a `Fill` or `Stroke`.

As an example, we will build a function to make a single line, and use it to build a function which, given the page dimensions, draws a page of graph paper. First, a function to build a single line from (x,y) to (x1,y1):

> ![](images/00035.jpg)

Now, a function to return a set of equally spaced floating-point values from 0…n given a step:

> ![](images/00067.jpg)

Note that we have been careful to avoid repeated addition of floating-point values – this can accumulate errors. We can build all the lines:

> ![](images/00080.jpg)

Here is the result of `graph_string 595.28 841.89 10\.` on a page of A4 paper:

![](images/00072.jpg)

Questions

1.  Write a function which, given a centre point and radius, returns a list of `Move`, `Line`, and `Close` elements which represent a circle. Use a number of lines appropriate to the size of the circle.
2.  Use the function from the previous question to write a program which outputs a page covered in pseudo-random sized and filled grey circles.
3.  The sequences `red green blue` `rg` and `red green blue` `RG` are the colour analogues to the sequences `grey` `g` and `grey` `G`. Add them to our data type, and redo the circles program to use colour.
4.  The sequence `width` `w` sets the line width. Add this to our data type and use it to draw a single large unfilled circle over the centre of the page.
5.  The operator `W` in place of a stroke or paint operator is used to set up a clipping path. Add this to our data type. Turn your big circle into a clipping path for the random circles pattern, so you now have circles within a circle.

Chapter 16
Adding Text

In this chapter, we will develop a very simple typesetter. Given a string representing the page content, it will split it into words, break them across lines and place them on the page. In the questions at the end of the chapter, the typesetter will be extended to use full justification, to indent paragraphs, and to produce multi-page documents.

To begin with, some of our numbers (lines per page, margins etc.) will be hard coded – we will then factor them out as we generalize the code. But let us define names for the page width and height for an A4 page first, to prevent excessive duplication:

> ![](images/00149.jpg)

We first need to split our text into words. For our purposes, a word is anything separated from another word by one or more spaces. To preserve the paragraph breaks, the new line character `\n` will be considered a word also. So, for example, the string `"He stopped.\n Looking around, he saw he was enveloped in smoke."` would be split into the list of words `["He"; "stopped."; "\n"; "Looking"; "around,"; "he"; "saw";` `"he"; "was"; "enveloped"; "in"; "smoke."]`.

The function `consume_spaces`, given an input, places the input position at the first non-space character at or after its current position. If the end of the input is reached, no exception is raised.

> ![](images/00176.jpg)

Now we can write a function to read a word. First, we consume any spaces present. Then, we repeatedly read characters into a buffer until either a space occurs, a newline occurs, or we reach the end of a file. If a space occurs, we have finished reading the word. If a newline occurs, we have finished also, but we rewind so the newline will be picked up as its own word next time. If we reach the end of the input, we return the contents of the buffer so far.

> ![](images/00202.jpg)

Now it is simple to collect all the words in an input by repeatedly calling `read_word`, and accumulating the result is a list.

> ![](images/00032.jpg)

We shall consider the opening paragraphs of Kafka’s “Metamorphosis”:

`One morning, when Gregor Samsa woke from troubled dreams, he found  `
`himself transformed in his bed into a horrible vermin.  He lay on  `
`his armour-like back, and if he lifted his head a little he could  `
`see his brown belly, slightly domed and divided by arches into stiff  `
`sections.  The bedding was hardly able to cover it and seemed ready  `
`to slide off any moment.  His many legs, pitifully thin compared  `
`with the size of the rest of him, waved about helplessly as he  `
`looked.  `
`        "What's happened to me?" he thought. It wasn't a dream. His  `
`room, a proper human room although a little too small, lay peacefully  `
`between its four familiar walls. A collection of textile samples lay  `
`spread out on the table - Samsa was a travelling salesman - and above  `
`it there hung a picture that he had recently cut out of an  `
`illustrated magazine and housed in a nice, gilded frame. It showed a  `
`lady fitted out with a fur hat and fur boa who sat upright, raising a  `
`heavy fur muff that covered the whole of her lower arm towards the  `
`viewer.`

So, for our text, we get:

`["One"; "morning,"; "when"; "Gregor"; "Samsa"; "woke"; "from"; "troubled";  `
` "dreams,"; "he"; "found"; "himself"; "transformed"; "in"; "his"; "bed";  `
` "into"; "a"; "horrible"; "vermin."; "He"; "lay"; "on"; "his"; "armour-like";  `
` "back,"; "and"; "if"; "he"; "lifted"; "his"; "head"; "a"; "little"; "he";  `
` "could"; "see"; "his"; "brown"; "belly,"; "slightly"; "domed"; "and";  `
` "divided"; "by"; "arches"; "into"; "stiff"; "sections."; "The"; "bedding";  `
` "was"; "hardly"; "able"; "to"; "cover"; "it"; "and"; "seemed"; "ready";  `
` "to"; "slide"; "off"; "any"; "moment."; "His"; "many"; "legs,"; "pitifully";  `
` "thin"; "compared"; "with"; "the"; "size"; "of"; "the"; "rest"; "of";  `
` "him,"; "waved"; "about"; "helplessly"; "as"; "he"; "looked."; "\n";  `
` "\"What's"; "happened"; "to"; "me?\""; "he"; "thought."; "It"; ...]`

Notice the newline as a word on its own. Our next task is to break this sequence of words into lines of a given width. We will have two kinds of line. A `Full` line is one we had to break at the end of. A `Partial` line is one which ended because of a newline or end-of-input. In our first example, we will not need to distinguish these two, but when it comes to justification and more advanced examples, it will be invaluable. The type is trivial:

`type line =`
`     Full of string`
`   | Partial of string`

Now the line breaking function. The function `lines` takes a maximum width in characters, and a list of words, and returns a line list. There are three cases in the `lines_inner` function:

1.  If we have reached the end of the list of words, return the list of collected `line`s, adding one for anything in the current line buffer, if it is non-empty.
2.  If we have a newline word, create a `Partial` line from the current buffer (even if it is empty – this allows blank lines to be inserted using multiple newlines), and carry on.
3.  If we have any other word, see how long it and the buffer are. If the word is longer than the whole line and we are at the beginning of that line, we output an over-sized line (an alternative would be to wrap or hyphenate the word in some way). Otherwise, we see if the current word will fit. If it will, we add it and a space to the buffer and carry on. It not, we output a `Full` line, and start with the word on the next line.

> ![](images/00258.jpg)

For example, here is our text split into lines of no more than twenty characters each:

`[Text.Full "One morning, when "; Text.Full "Samsa woke from ";  `
` Text.Full "dreams, he found "; Text.Full "transformed in his ";  `
` Text.Full "into a horrible "; Text.Full "He lay on his ";  `
` Text.Full "back, and if he "; Text.Full "his head a little ";  `
` Text.Full "could see his brown "; Text.Full "slightly domed and ";  `
` Text.Full "by arches into "; Text.Full "sections. The ";  `
` Text.Full "was hardly able to "; Text.Full "it and seemed ready ";  `
` Text.Full "slide off any "; Text.Full "His many legs, ";  `
` Text.Full "thin compared with "; Text.Full "size of the rest of ";  `
` Text.Full "waved about "; Text.Partial "as he looked. ";  `
` Text.Full "\"What's happened to "; Text.Full "he thought. It ";  `
` Text.Full "a dream. His room, "; Text.Full "proper human room ";  `
` Text.Full "a little too small, "; Text.Full "peacefully between "; ...]`

Now we need to add appropriate text-showing operators to our Pdfpage module, and then produce a list of operators for showing a line, using it repeatedly to show the whole page. A text section in a PDF operator stream looks something like this:

`BT 1 0 0 1 40 50 Tm /F0 12 Tf (The text) Tj ET`

This contains the following operators and operands:

![](images/00287.jpg)

Here are the fragments added to the Pdfpage.t type…

`  | BeginText`
`  | EndText`
`  | SetTextPosition of float * float`
`  | SetFontAndSize of string * float`
`  | ShowText of string`

…and the `string_of_op` function:

`  | BeginText -> "BT"`
`  | EndText -> "ET"`
`  | SetTextPosition (x, y) -> Printf.sprintf "1 0 0 1 %f %f Tm" x y`
`  | SetFontAndSize (font, size) -> Printf.sprintf "%s %f Tf" font size`
`  | ShowText t -> Printf.sprintf "(%s) Tj" t`

Consider Figure [16.1](#index_split_023.html_filepos305915). The function `typeset_line_at` builds a single line at x position 20 and a given y coordinate. The function `downfrom` builds a list of y positions for a number of lines. The utility function `clean_lines` makes plain strings from a list of `line`s, and the function `typeset_page` puts it all together, generating a big list of Pdfpage.t operations. The resulting PDF is shown in Figure [16.2](#index_split_023.html_filepos306494). The full code for this chapter is included in the online resources – it should be consulted before attempting the questions.

* * *

> ![](images/00272.jpg)

> Figure 16.1:

* * *

* * *

> ![](images/00118.jpg)

> Figure 16.2:

* * *

Questions

1.  Factor out the font size, line height, margin height and automatically calculate the number of characters in a line (the number of characters in a line can be calculated by the formula 5w∕3f where w is the width of a line and f is the font size). The program should now work for any page size.
2.  The first line of each paragraph (save for the first) should be indented by eight characters. Implement this.
3.  Implement full justification. This gives a clean left and right margin except for the left margin of the first line in a paragraph and the right margin of the last line of a paragraph. This can be done by altering the spacing between characters and words. Of course, `Partial` lines should not be stretched.
4.  Allow the program to generate multiple pages, should the length of the text demand it. This can be done by extending the `/Kids` entry in the PDF file, and producing multiple page objects.

Answers to Questions

Hints may be found on page [309](#index_split_025.html_filepos412178).

1 (Unravelling “Fold”)

1

This can be achieved by folding the subtraction operator over the deductions, with the starting accumulator set to the budget:

> ![](images/00250.jpg)

Partial application can be used, as in the second definition.

2

We can use an accumulator starting at zero, and increment it once for each element processed:

> ![](images/00026.jpg)

Since we ignore the element itself, the function is polymorphic.

3

If the list is empty, we return `None`, otherwise we use a left fold which simply replaces the accumulator with each successive element from the list. We must initialize the accumulator, so we pick the first element for that (we have already eliminated the case where there are no elements, so `List.hd` will succeed).

> ![](images/00134.jpg)

Not quite idiomatic.

4

If we start from the left, consing each element to the accumulator (which is initially the empty list), the list will be reversed.

> ![](images/00228.jpg)

Since the accumulator is the empty list (which has type α list), the function remains polymorphic, having the type we would expect.

5

The accumulator begins set to `false`. For each element, we calculate the logical OR of the element tested for equality and the accumulator. If at least one `true` occurs, the result will be `true`.

> ![](images/00036.jpg)

Note that this is less efficient than `List.mem` because there is no early exit – the whole list is processed in every case.

6

This is a classic problem. We either need to

*   add a space after each word except for the last; or
*   add a space before each word except for the first.

With `fold_left` we can detect when we are at the first word, by inspecting the accumulator, and use the second method.

> ![](images/00203.jpg)

Note that the requirement that the words be non-empty is important here. The efficiency is poor, however, since each string concatenation builds a new string. The Standard Library Buffer module is a better approach here.

7

We can use the built-in `max` function to update the accumulator.

> ![](images/00220.jpg)

The current element is ignored.

8

We can compare the speed of `List.mem` and `member` with the help of the `Unix.gettimeofday` function, as shown in Figure [A.1](#index_split_024.html_filepos315703). On the Author’s machine, this results in:

* * *

> ![](images/00041.jpg)

> Figure A.1:

* * *

`Our member took 2.513232 seconds  `
`List.mem took 1.162159 seconds`

There is a significant speed penalty in our version of the member function, at least for this scenario.

2 (Being Lazy)

1

This is similar to the `lseq` function in the text, but we double every time instead of adding one.

> ![](images/00180.jpg)

Having written the function which, given a number, doubles from that point, we then just code the list itself by starting at 1.

2

If we are asked to fetch the 0th element, we already have it – as the head of the lazy list. If not, we force evaluation of the tail, and recurse.

> ![](images/00256.jpg)

Of course, this does not terminate on bad inputs (when n < 0). Error detection should be added.

3

Below, the function `lrepeating_inner` takes the current list `c` and the original list `l`. Matching on `c`, we build the lazy list. If we reach the last element of the input list, we start again, with the original list, which is always retained.

> ![](images/00064.jpg)

Note that we cannot build from an empty list, since there could be no head.

4

The first two fibonacci numbers are defined to be 0 and 1\. Thereafter, we keep the current and previous number, and generate the lazy list.

> ![](images/00003.jpg)

5

This is slightly delicate. We must force the tail twice, to reveal new elements for the heads of the two output lists, and the final tail for the next time each list is forced.

> ![](images/00266.jpg)

Note that we cannot hoist the calculation of `unleave t` into a `let` so as to do it once, since to do so would not delay evaluation.

6

If we write a function which, given a number, gives the correct string, then the lazy list itself is easy to build with `lmap` and `lseq`.

> ![](images/00260.jpg)

3 (Named Tuples with Records)

1

Since a reference is just a record with a mutable field `contents`, we can use the `<-` construct:

`        OCaml`

`# let x = ref 0;;`
`val x : int ref = {contents = 0}`
`# x.contents <- 1;;`
`- : unit = ()`
`# x;;`
`- : int ref = {contents = 1}`

There is no reason to use this rather than `:=` of course.

2

The function `Unix.time` returns the current time. The function `Unix.localtime` builds from this a record of type Unix.tm. First we will need two ancillary functions:

> ![](images/00130.jpg)

Now the main function, which both uses the shortened form of a record pattern, and names only the fields we need:

> ![](images/00264.jpg)

Note that the names bound by the pattern do not include the `Unix` prefix.

3

The construct `type t = {x : int ref}` is a record type containing a reference to an integer. We can build it using an existing reference, and can extract the reference for use elsewhere. We can share a single reference between two or more instances of this data type. The construct `type t = {mutable x : int}` is a record with a single, mutable field. We must use `<-` rather than `:=` to mutate it, and it may not be shared.

4

We can use multiple type parameters (which are written with parentheses and commas) and then use these types for the fields in the appropriate way:

`type ('a, 'b, 'c) t =`
`  {a : 'a;`
`   b : 'a;`
`   c : 'b;`
`   d : 'b;`
`   e : 'c;`
`   f : 'c}`

5

For the first part, we can use the function `Gc.stat` to return a Gc.stat record. Then we can write various components to the given file (here, we have chosen just a few):

> ![](images/00110.jpg)

For the second part, we define names for the magic numbers given in the documentation. We can then write a function `change_verbosity` which adds them up to make the new flags field, and uses `Gc.get` together with the `with` syntax to build a new record to be passed to `Gc.set`:

> ![](images/00245.jpg)

4 (Generalized Input/Output)

1

This is a simple modification of `input_of_string` from the text, replacing string operators with array ones.

> ![](images/00291.jpg)

Note that an array of characters like this requires much more space as a string.

2

We create a Buffer.t, attempt to read the specified number of characters, and then return the contents. If one of the calls to `i.input_char ()` raises the `End_of_file` exception, we return the buffer contents anyway – it will contain the characters read so far.

> ![](images/00224.jpg)

3

We add a function of the expected type to the input. The option `None` will represent the end of the file.

`type input =`
`  {pos_in : unit -> int;`
`   seek_in : int -> unit;`
`   input_char : unit -> char;`
`   input_char_opt : unit -> char option;`
`   in_channel_length : int}`

Now for a new `input_of_channel`. We try to build the `Some` option, returning `None` if the `End_of_file` exception is raised.

> ![](images/00198.jpg)

The `input_of_string` function is another similar modification. This time, there is no need for exception handling.

> ![](images/00209.jpg)

4

We add the function of type unit → int.

`type input =`
`  {pos_in : unit -> int;`
`   seek_in : int -> unit;`
`   input_char : unit -> char;`
`   input_byte : unit -> int;`
`   in_channel_length : int}`

Now, having defined as a convenience, the name `no_more` for the -1, we can modify `input_of_channel` and `input_of_string` easily:

> ![](images/00052.jpg)

These functions have none of the advantages of the exception-raising or option-returning ones, but they are very fast indeed.

5

We alter `input_of_channel` to check for a newline and raise `End_of_file` in that case.

> ![](images/00191.jpg)

Now we can create one of these special inputs from standard input, and use our `input_string` function to build a string from the user’s input, ending when the return key is pressed. For example:

`# input_string (single_line_input_of_channel stdin) max_int;;`
`Some input`
`- : string = "Some input"`

6

Ideal functions to use when defining the new type already exist in the Buffer module. Then, we can build an example, where we give a name to the buffer, build an input from it and process it, retrieving its contents afterwards.

> ![](images/00031.jpg)

5 (Streams of Bits)

1

We can read quickly if the number of bits wanted is 8 and we happen to be at the beginning of a byte. In this case we can call the underlying output’s `input_char` function directly.

> ![](images/00172.jpg)

If the conditions are not met, we fall back to the old `getval` function. This will be faster if we frequently read data aligned-byte-by-aligned-byte, but we still need the flexibility of a stream of bits when required.

2

We simply replace the int operators with those for Int32.t:

> ![](images/00015.jpg)

3

Our precondition this time is that the number of bits to be written is 8 and the `obit` field is set to its initial value, 7\. Then we can use the `output_char` function of the underlying output.

> ![](images/00156.jpg)

Otherwise, we fall back to the old `putval` function.

4

The integer functions are replaced by ones from the Int32 module:

> ![](images/00296.jpg)

5

We add a field `rewind` which will move the position in the output backwards one byte, if possible. This is the new type:

`type output =`
`     {output_char : char -> unit;`
`      rewind : unit -> unit;`
`      out_channel_length : unit -> int}`

Now we can rewrite, for example, `output_of_string` for this new type:

> ![](images/00102.jpg)

We alter `putbit` appropriately:

> ![](images/00098.jpg)

6 (Compressing Data)

1

We will need to look through the input list of integers (bytes), finding same and different runs and building a new list. For clarity, we will produce the output runs using a new type, producing the actual bytes later:

`type run = Same of int * int | Diff of int list`

The `Same` case holds a (length, value) pair and `Diff` just a list of bytes. Now we can write a function `get_same` which, given the first value, the current count, and the list, returns a pair of the final count of like characters, and the remaining list:

> ![](images/00230.jpg)

Similarly, we can define a function to read a different run into an accumulator, returning the run and the remaining list. This function will be called only when `get_same` returned a run of length one.

> ![](images/00078.jpg)

Now we can write a function which uses both of these functions to get a single run, creating an instance of our new data type:

> ![](images/00038.jpg)

Now, we use the defined rules to build a function which makes a list of bytes from a run:

> ![](images/00143.jpg)

With all this done, it is easy to define the compression function itself, which accumulates runs, concatenating them when all the data has been processed. We must be sure to add the EOD marker at the end.

> ![](images/00239.jpg)

Decompression is rather simpler, making use of our `take` and `drop` functions from the Util module described on page xiii. We read each run and expand it to a list of bytes, accumulating them until end of data.

> ![](images/00047.jpg)

Note a little cheat – we use functions from the Array module to expand the `Same` run.

2

The tree carries no information in its branches (since no code can be a prefix of another code). Leaves can carry or not carry information, depending on whether there is a code there. In order to avoid option types, we can just split into three cases, `Lf` for empty leaves, `Code` for full ones, and `Br` for a branch, where 0 goes left and 1 goes right.

`type tree = Lf | Code of int | Br of tree * tree`

Now, we can define the function to add a code to an existing tree. For example, `add_elt Lf ([0; 1], 67)` adds the code `[0; 1]` for the run length 67\. This will build the tree `Br (Br (Lf, Code 67), Lf)`. We match on the code, building the tree as we go left or right.

> ![](images/00065.jpg)

Now, to build the whole tree, we just use repeated insertion with `fold_left`, having built the (code, run length) pairs:

> ![](images/00020.jpg)

Now, for example, we can build the white terminating codes as a tree:

> ![](images/00161.jpg)

(`Util.from a b` gives the list of numbers starting at `a` and ending at `b` in ascending order). The function succeeds, verifying that there are no collisions, and yields:

`  Br  `
`   (Br  `
`     (Br  `
`       (Br  `
`         (Br  `
`           (Br (Br (Lf, Br (Code 29, Code 30)),  `
`             Br (Br (Code 45, Code 46), Code 22)),  `
`           Br (Br (Code 23, Br (Code 47, Code 48)), Code 13)),  `
`         Br  `
`          (Br (Br (Code 20, Br (Code 33, Code 34)),  `
`            Br (Br (Code 35, Code 36), Br (Code 37, Code 38))),  `
`          Br (Br (Code 19, Br (Code 31, Code 32)), Code 1))),  `
`       Br  `
`        (Br (Br (Code 12, Br (Br (Code 53, Code 54), Code 26)),  `
`          Br (Br (Br (Code 39, Code 40), Br (Code 41, Code 42)),  `
`           Br (Br (Code 43, Code 44), Code 21))),  `
`        Br  `
`         (Br (Br (Code 28, Br (Code 61, Code 62)),  `
`           Br (Br (Code 63, Code 0), Lf)),  `
`         Code 10))),  `
`     Br  `
`      (Br  `
`        (Br (Code 11,  `
`          Br (Br (Code 27, Br (Code 59, Code 60)), Br (Lf, Code 18))),  `
`        Br  `
`         (Br (Br (Code 24, Br (Code 49, Code 50)),  `
`           Br (Br (Code 51, Code 52), Code 25)),  `
`         Br (Br (Br (Code 55, Code 56), Br (Code 57, Code 58)), Lf))),  `
`      Br (Lf, Code 2))),  `
`   Br  `
`    (Br (Br (Code 3, Br (Lf, Code 8)),  `
`      Br (Br (Code 9, Br (Code 16, Code 17)), Code 4)),  `
`    Br (Br (Code 5, Br (Br (Code 14, Code 15), Lf)), Br (Code 6, Code 7))))`

3

Compressing our data with `compress_string input_data 1680 1` instead of `compress_string input_data` `80 21` generates a string of length 110 bytes rather than 120 bytes. This is because we could generate one run for the white section at the end of one line followed by a white section at the beginning of the next, instead of splitting at line boundaries.

If we try to re-compress this data, with `compress_string compressed 880 1`, the data size increases to 197 bytes. This is unsurprising, since the job of the white and black codes is to be information-dense and the compression algorithm works best on data which is information-sparse.

4

We can re-use the `read_up_to` function to build our histogram. Given white and black arrays, each of length 1792 and with elements initialized to zero, the input bits and the width and height, we can repeatedly call `read_up_to`. We must maintain a count of how many pixels are left to be read, and an additional count of how many are left in this line, so the correct width can be passed to the `read_up_to` function.

> ![](images/00002.jpg)

Now it is easy to build two histograms – one for white and one for black, and return them:

> ![](images/00267.jpg)

We can define a simple function to print the histogram, eliding any zero counts:

> ![](images/00074.jpg)

Here is the histogram for white runs on our example data:

`# print_histogram white;;  `
`5 runs of length 1  `
`7 runs of length 2  `
`15 runs of length 3  `
`15 runs of length 4  `
`34 runs of length 5  `
`20 runs of length 6  `
`4 runs of length 7  `
`4 runs of length 8  `
`4 runs of length 9  `
`3 runs of length 10  `
`3 runs of length 11  `
`7 runs of length 12  `
`1 runs of length 13  `
`1 runs of length 14  `
`1 runs of length 15  `
`3 runs of length 16  `
`1 runs of length 17  `
`1 runs of length 20  `
`1 runs of length 21  `
`3 runs of length 35  `
`1 runs of length 39  `
`1 runs of length 46  `
`1 runs of length 47  `
`1 runs of length 73  `
`3 runs of length 80  `
`- : unit = ()`

And here is the histogram for black runs:

`# print_histogram black;;  `
`12 runs of length 1  `
`55 runs of length 2  `
`38 runs of length 3  `
`5 runs of length 4  `
`2 runs of length 5  `
`1 runs of length 6  `
`1 runs of length 7  `
`1 runs of length 8  `
`2 runs of length 9  `
`2 runs of length 10  `
`- : unit = ()`

7 (Labelled and Optional Arguments)

1

If α is int then the first and second argument can be confused. We can fix this by adding labels and calling `Array.make`. Notice the use of punning here.

> ![](images/00173.jpg)

Now the function can be called without confusion:

`        OCaml  `

`# make ~len:5 ~elt:4;;  `
`- : int array = [|4; 4; 4; 4; 4|]`

Of course, it can still be called without labels.

2

We can define separate types for the start and length so that their names must be mentioned when calling the function.

> ![](images/00277.jpg)

Not nearly as convenient as labels, though.

3

There are three functions where confusion may arise, and we can label them with simple wrappers. They are the functions where multiple arguments have the same type, and so may be confused.

> ![](images/00235.jpg)

4

We can make the accumulator an optional argument. Now the caller can call the function as if it were the same as `List.map`.

> ![](images/00244.jpg)

The optional argument must still appear in the interface, of course, so we might still prefer the old approach of wrapping it up and only exposing the wrapper.

8 (Formatted Printing)

1

We can use `Printf.bprintf` to accumulate the individual parts, making sure to deal with the final element specially. The outer function sets everything up.

> ![](images/00091.jpg)

2

Again, `Printf.bprintf` is the key. This time, we can calculate the initial buffer size exactly.

> ![](images/00223.jpg)

We have used a width specifier of `2` and the `0` flag to make sure that characters with code 0..15 are padded with a zero.

3

The format string for `Printf.printf` must be known at compile time. The solution for printing the result of `mkstring` using `printf` is the `%s` format specification:

`Printf.printf "%s" (mkstring ())`

4

The `*` character can be used as a width or precision specifier, to indicate that the width or precision is given as an argument. We use `*` for the width, and pass in 10.

`Printf.sprintf "(%*i)" 10 1`

So, the result is:

`(         1)`

We can use `List.iter` to print a table by applying this to each of a list of numbers in turn.

> ![](images/00293.jpg)

9 (Searching for Things)

1

For the first part, where all matches are considered, we can rewrite `search` with an extra argument to count the matches, restructuring its logic so as not to finish upon the first match.

> ![](images/00208.jpg)

There is no need to rewrite the `at` function. Now, for the version which considers only non-overlapping matches, we just jump by the length of the pattern `ss` upon a match:

> ![](images/00108.jpg)

2

It is simple to write a function which returns the length of the longest matching prefix at the beginning of a list:

> ![](images/00190.jpg)

Now, we can write a function which keeps track of the position and length of the longest prefix found, returning them when the whole list has been searched.

> ![](images/00011.jpg)

Here, `currpos` is the current position, `bestpos` the position of the longest matching prefix found so far, and `bestlen` the length of the longest prefix so far.

3

We can write a simple profiling function which, given a search function, measures its running time. This allows us to compare the naive and better versions of `search` we wrote for searching in strings:

> ![](images/00171.jpg)

Compiling with `ocamlc` on the Author’s machine:

`Naive version took 7.608291 seconds  `
`Better version tool 3.388830 seconds`

Now, compiling with `ocamlopt`:

`Naive version took 2.966211 seconds  `
`Better version tool 0.450546 seconds`

4

We can add a case to the main search. We must check the character following the backslash for a match, assuming there is such a next character. If so, we move two positions in the pattern and one in the string. Otherwise, the match has failed.

`| '\\'->`
`    if`
`      sp < String.length s &&`
`      ssp < String.length ss - 1 &&`
`      ss.[ssp + 1] = s.[sp]`
`    then`
`      Some (2, 1)`
`    else`
`      None`

5

The Standard Library function `String.uppercase` can be used, in conjunction with the optional boolean argument:

> ![](images/00014.jpg)

Both the pattern and string must be upper case, of course.

10 (Finding Permutations)

1

The combinations of a list can be generated by calculating the combinations of the tail. Then consider two possibilities – the head is included in this combination, or it is not:

> ![](images/00155.jpg)

Note the base case is the list containing the empty list, not just the empty list.

2

We build this from `perms` and the `combinations` function we just wrote:

> ![](images/00197.jpg)

We used the tail-recursive version of `perms`, of course.

3

This has roughly the same shape as `combinations`, with two differences: we keep a counter to make sure the computation ends, and we always add something to the list – either `true` or `false`.

> ![](images/00139.jpg)

4

We repeatedly swap elements from opposite ends of the sub-array, given an array, offset and length:

> ![](images/00276.jpg)

It is important to make sure it works for the empty range, an even-length sub-array and an odd-length sub-array. You could add detection of invalid arguments to this function.

5

The two functions `first` and `last` turn out to be even more awkward than their imperative counterparts. The function `first`, given a list, returns a tuple of three things: the elements before the “first” item, the first item itself, and those afterward. This is done by reversing the input list and looking for the first appropriate item, since this is easier than looking for the last appropriate item in the original input:

> ![](images/00122.jpg)

The `last` function is still more verbose: we locate the correct item by sorting and finding the smallest item greater than `f`. Then we can call `split_at` to return the item before and after the instance of `f`.

> ![](images/00154.jpg)

Now, the `next_permutation` function calls `first` and `last`, and stitches everything together:

> ![](images/00159.jpg)

Here is the equivalent `non_increasing` function, which is simple:

> ![](images/00164.jpg)

The final `all_permutations` function is now easy.

> ![](images/00167.jpg)

Conclusion: converting an imperative algorithm mechanically to a functional style is not always useful.

11 (Making Sets)

1

It is not possible to measure directly the memory used by an OCaml data structure (though one could calculate it by reading the section in the OCaml manual about data representation), but we can use the Gc module to measure the number of words allocated whilst building the structure, by using the data in `Gc.counters` before and after building each structure, and the given formula “memory used since start of program = minor words + major words - promoted words”:

![](images/00170.jpg)

Notice that a huge amount more is required for the tree structures, because every time a new element is inserted, part of the tree is rewritten. In the case of the Red-Black tree, rotations involve allocating new memory too.

2

We can add the type for the `union` function to our signature:

> ![](images/00177.jpg)

For lists, the `union` function is easy, we just insert each element of `b` into the list `a`. Duplicates will be removed correctly:

`let union a b = List.fold_left (fun x y -> insert y x) a b`

For trees and Red-Black trees, we must turn `b` into a list first, so `fold_left` can be used, but the solution is broadly the same.

`let union a b = List.fold_left (fun x y -> insert y x) a (list_of_set b)`

For hash tables, to preserve the previous tables, we must build lists from both sets, and then build a new set from the concatenation of those too lists:

`let union a b = set_of_list (list_of_set a @ list_of_set b)`

The built-in Set module, which is considered in Question 3, provides a particularly efficient union operation.

3

We write a version of our set signature which is specialized to integers. Then, we use the syntax given in the question to build the module S. This contains the type S.t, the value `S.empty` and the functions `S.elements`, `S.add`, `S.mem`, and `S.cardinal`, which we can use to write the functions to match our signature.

> ![](images/00183.jpg)

Now the benchmarking for insertion and membership is simple:

> ![](images/00186.jpg)

Here is the output:

`For ordered, insertion took 0.056586, membership 0.019593`
`For unordered, insertion took 0.087148, membership 0.021295`

4

We can change the type thus, with `BrR` for red and `BrB` for black:

`type 'a t =`
`  Lf`
`| BrR of 'a t * 'a * 'a t`
`| BrB of 'a t * 'a * 'a t`

Now, the solutions are tedious to write out, but not difficult. The result is Figure [A.2](#index_split_024.html_filepos379432).

* * *

> ![](images/00298.jpg)

> Figure A.2:

* * *

12 (Playing Games)

1

We already know that O wins 131184 times. By a similar use of `num_wins` we find that X wins 77904 times. So, as expected, going first is an advantage. We must write another function to find how many draws there are. A board is drawn if it is full but does not contain a winning configuration of either X or O:

> ![](images/00195.jpg)

This tells us that there are 46080 drawn games. Since each game must be either won or drawn, the total number of possible games is 131184 + 77904 + 46080 = 255168\. We can check this by writing a function to find the terminal nodes directly:

> ![](images/00201.jpg)

This gives 255168 too.

2

We need make only two small changes. Delaying evaluation in the type…

`type tree = Move of turn list * (unit -> tree list)`

…and altering `next_moves` to insert that delay:

> ![](images/00204.jpg)

Now, we can carefully write a function `select_case` which, given a starting board such as `[E; E; E; E; O;` `E; E; E; E]` and the game tree, returns the portion of the game tree matching that board. Due to laziness, the rest of the tree is now not explored.

We can now alter `num_wins` easily for the delayed case, and write a function `pos_wins` which returns the number of wins starting from a position like `[E; E; E; E; O; E; E; E; E]`.

> ![](images/00240.jpg)

Similarly, we can modify the `drawn` function to work with the new lazy structure, and write a new function `draws` to count the drawn positions from a given starting board such as `[E; E; E; E; O; E; E; E;` `E]`:

> ![](images/00213.jpg)

Now we can define starting boards for the centre spot, the middle of a side, and a corner. We can now use `pos_wins` and `draws`, taking account of symmetry to enumerate all the cases:

> ![](images/00216.jpg)

This gives the following:

`val centre_x_wins : int = 5616  `
`val centre_o_wins : int = 15648  `
`val centre_drawn : int = 4608  `
`val side_x_wins : int = 40704  `
`val side_o_wins : int = 56928  `
`val side_drawn : int = 20736  `
`val corner_x_wins : int = 31584  `
`val corner_o_wins : int = 58608  `
`val corner_drawn : int = 20736`

The total is 255168, of course.

3

The strategy of using the magic square representation is to build a problem which is isomorphic (has the same essential characteristics – literally the same shape) to the original one, but is easier to work with. Before building the tree tree, we will need five little functions:

*   `sum`, which checks if a list sums to 15;
*   `threes`, which finds all the combinations of numbers from a list of numbers which are of length three (the `combinations` function is from Chapter [10](#index_split_016.html_filepos191331));
*   `won`, which uses `threes` to check if a list of integers contains a combination of three numbers which sum to 15;
*   `drawn` which, given the integer lists for X and O, works out if the game has been drawn; and
*   `possibles` which, given all the non-empty squares, lists the empty ones.

> ![](images/00086.jpg)

Now, the type contains a list of X positions, a list of O positions, and the list of child nodes:

`type tree = Move of int list * int list * tree list`

We do not need a type for the turn this time – we can just use a boolean. The function `next_moves` follows the usual pattern – if the game is won or drawn, the list of child nodes is empty. Otherwise, we build child nodes for each possible position the next player could place his piece.

> ![](images/00219.jpg)

* * *

> ![](images/00229.jpg)

> Figure A.3:

* * *

The game tree is shown in Figure [A.3](#index_split_024.html_filepos388565). We can write a simple `xwins` function to test our new function returns the same result as the original.

> ![](images/00088.jpg)

13 (Representing Documents)

1

Writing `T` for the trailer dictionary, we have the graph `T` → `2` → `3` ←→ `1` → `4`.

2

These can be written out by reference to the data structure:

*   `Name "/Name"`
*   `String "Quartz Crystal"`
*   `Dictionary [("/Type", Name "/ObjStm"); ("/N", Integer 100); ("/First", Integer` `807); ("/Last", Integer 1836); ("/Filter", Name "/FlateDecode")]`
*   `Array [Integer 1; Integer 2; Float 1.5; String "black"]`
*   `Array [Integer 1; Indirect 2]`

In the last two examples, we assumed integer where appropriate. Notice that in the last example, the parsing is somewhat ambiguous – we would need to read all the way to the `R` to be sure it was not an array of several integers.

3

Consider the tree `Br (Br (Lf, 1, Lf), 2, Br (Lf, 3, Lf))`. We will represent it by using nested PDF dictionaries. A branch will have a `/Type` key with value `/Br`. It will have `/Left` and `/Right` entries for the sub-trees. A leaf is indicated simply by `/Lf`. In the PDF file we would write it like this:

`<</Type /Br  `
`  /Value 2  `
`  /Left <</Type /Br /Value 1 /Left /Lf /Right /Lf>>  `
`  /Right <</Type /Br /Value 3 /Left /Lf /Right /Lf>>>>`

To construct it from our data type in OCaml:

`let tree =`
`  Pdf.Dictionary`
`    [("/Type", Pdf.Name "/Br");`
`     ("/Value", Pdf.Integer 2);`
`     ("/Left",`
`        Pdf.Dictionary`
`          [("/Type", Pdf.Name "/Br");`
`           ("/Value", Pdf.Integer 1);`
`           ("/Left", Pdf.Name "/Lf");`
`           ("/Right", Pdf.Name "/Lf")]);`
`     ("/Right",`
`         Pdf.Dictionary`
`           [("/Type", Pdf.Name "/Br");`
`            ("/Value", Pdf.Integer 3);`
`            ("/Left", Pdf.Name "/Lf");`
`            ("/Right", Pdf.Name "/Lf")])]`

4

We must search for dictionary entries inside `Pdf.Dictionary`, of course, but also inside `Pdf.Stream`, which contains a dictionary, and `Pdf.Array` which may do so too. Two mutually-recursive functions will do:

> ![](images/00238.jpg)

14 (Writing Documents)

1

We can alter the functions `string_of_array` and `string_of_dictionary` to simply not output the space preceding the closing bracket. To remove the initial space requires a little trick. We inspect the length of the buffer to determine if we are about to output the first item. In that case, no space is written. This is shown in Figure [A.4](#index_split_024.html_filepos395818).

* * *

> ![](images/00123.jpg)

> Figure A.4:

* * *

2

The full code can be found in the online resources. We make the following changes:

*   Change `/Count` from `1` to `3`.
*   Move the `/Resources` to its own object, number `5`.
*   Write two new pages, objects `6` and `7`.
*   Write two new page content streams, `8` and `9`.
*   Change the `/Size` from `5` to `10` to account for the new objects.

3

The full code can be found in the online resources. See the hint for a little more help.

15 (Pretty Pictures)

1

Since we are working with circles, let us define π:

> ![](images/00249.jpg)

We can write a simple function to return the point at a given angle, distance `r` from point (`x`, `y`):

> ![](images/00255.jpg)

Now, we can build a list of all these points, remembering to stop before we have been around the whole circle. The argument `step` is the angle between successive points.

> ![](images/00259.jpg)

Finally, we generate a `Move` to the first points, `Line`s to the rest, and a final `Close`.

> ![](images/00150.jpg)

For our example, we made a filled circle of radius 100 centred at (300, 300) with `Pdfpage.Fill`:

![](images/00271.jpg)

2

First, a function to build a pseudo-random circle somewhere on our page, making sure to overlap the edges:

> ![](images/00275.jpg)

Now, a little utility function to build a list of n things when given a function which generates them, such as `random_circle`:

> ![](images/00280.jpg)

Now it is simple to build a hundred random grey filled circles and append them all together with `List.concat`:

> ![](images/00117.jpg)

![](images/00289.jpg)

3

We can add `FillColourRGB of float * float * float` and `StrokeColourRGB of float * float * float` to the data type and associated functions, and then modify our previous example:

> ![](images/00295.jpg)

If you are reading the PDF ebook version of this book, the following image is in colour:

![](images/00058.jpg)

4

We add `LineWidth of float` to the data type and associated functions. Now we set the line width and stroke colour and draw the large circle:

> ![](images/00055.jpg)

![](images/00039.jpg)

5

We add `SetClip` to the data type and associated functions. Then we set the clip before stroking.

> ![](images/00178.jpg)

The single path is used both for clipping and for the stroke:

![](images/00254.jpg)

16 (Adding Text)

1

We can pull out font size, line spacing and margin easily, defining them at the top of the page. The text width is derived from the page width and margin. The maximum number of characters in a line can be calculated using the formula given in the question:

`let font_size = 10.0`

`let line_spacing = 1.1`

`let margin = 40.0`

`let text_width = page_width -. margin -. margin`

`let max_chars = int_of_float (text_width /. font_size *. (5. /. 3))`

We can now insert these new names into `typeset_line_at`:

`Pdfpage.SetTextPosition (margin, y);`
`Pdfpage.SetFontAndSize ("/F0", font_size);`

We pass `max_chars` to `clean_lines` and alter our call to `downfrom`:

`let ls = clean_lines (lines max_chars words) in`

`downfrom`
`  (font_size *. line_spacing)`
`  (page_height -. margin -. line_spacing) (List.length ls) 0`

Here is an example of the new program, with text typeset on a much smaller page (it runs off the bottom, of course):

![](images/00062.jpg)

2

We can implement this by manually inserting space characters into the buffer in `lines_inner` following every newline (i.e. at the beginning of the second and subsequent paragraphs). This is shown in Figure [A.5](#index_split_024.html_filepos407599).

* * *

> ![](images/00115.jpg)

> Figure A.5:

* * *

Notice the use of an optional argument in `lines`. We can now alter one line in `typeset_page`:

`let ls = clean_lines (lines max_chars ~indent:8 words) in`

The result is shown in Figure A.6.

* * *

> ![](images/00288.jpg)

> Figure A.6:

* * *

3

The page height can be calculated easily:

`let text_height = page_height -. margin -. margin`

Now, we can use `Pdfpage.SetCharacterSpacing` in `typeset_line_at`, adding an extra argument for the spacing:

> ![](images/00282.jpg)

The spacing is calculated as prescribed, only for `Full` lines:

> ![](images/00128.jpg)

In a revised `typeset_page`, we can calculate the correct spacings, passing them to `typeset_line_at`:

> ![](images/00262.jpg)

Here is an example page. You can see that the lines are fully justified – flush to the left and right margins.

![](images/00033.jpg)

4

The answer to this question is too long to be contained in the text. Consult the online resources for the program itself. An example multi-page output is shown in Figure [A.7](#index_split_024.html_filepos411487).

* * *

![](images/00187.jpg) ![](images/00290.jpg)

![](images/00097.jpg) ![](images/00196.jpg)

![](images/00207.jpg)

> Figure A.7:

* * *

Hints for Questions

1
Unravelling “Fold”

1

What must the accumulator start at? What operation must we perform each time? Consider the `sum` function from the text as a starting point.

2

We need to ignore each element, just incrementing an accumulator when we see each one. The final value of the accumulator will then be the length of the list. What is the initial accumulator?

3

A good way to deal with the fact that an empty list has no last element would be to return an option type.

4

These sorts of folds producing lists have an accumulator which is a list type – you might start at the empty list.

5

The type will be the same as for `List.mem`. How do we keep track of whether or not we have seen a matching element? What is the initial accumulator?

6

This will involve a string accumulator and the string concatenation operator. How to we ensure there is not an excess space before or after the sentence?

7

The built-in `max` operator returns the larger of two values.

8

You can use the Standard Library function `Unix.gettimeofday` to help time the functions.

2
Being Lazy

1

This is very similar to `lseq` in the text.

2

Construct by analogy to the same function on ordinary lists. Remember one needs to force evaluation to get at the tail.

3

How do we know when we have reached the end of the input list and must start again? What do we do if the input list is empty?

4

Consider the definition of fibonacci numbers. Split into a function which builds the lazy list given two numbers, and the construction of the list itself.

5

The type of the function will be α lazylist → α lazylist × α lazylist. You will need to force the evaluation of the tail of the input list twice to yield the heads of the two output lists, and then work out how to produce the tails.

6

Write a function which builds the alphabetic string from a number. Then, some of the generic lazy list handling functions from the text can be used to build the lazy list itself.

3
Named Tuples with Records

1

What is a reference really?

2

Look at the functions `Unix.time` and `Unix.localtime`. You will need to deal with conversion of day-of-week and month from integers to strings yourself, but this is not difficult.

4

Records types can be parametrized, just like other data types.

5

See the documentation for a) `Gc.stat` and b) `Gc.set` and `Gc.get`.

4
Generalized Input/Output

1

A simple modification of `input_of_string`.

2

Use a Buffer.t to accumulate the characters.

3

The new field will have type unit → char option.

4

The new field will have type unit → int. For `input_of_channel` and `input_of_string`, use exception handling to return the special value. Consider giving the special value -1 a name.

5

Check for a newline character on each `input_char`, raising `End_of_file`. Can you use `input_string` with the new channel you have created to return the user input?

6

The Buffer module already contains ideal functions for this.

5
Streams of Bits

1

What is the test for being able to read a whole byte at a time? What do we do if the condition is met? If it is not?

2

Just replace the integer functions with ones from the Int32 module.

3

What is the test for being able to write a whole byte at a time? What do we do if the condition is met? If it is not?

4

Just replace the integer functions with ones from the Int32 module.

5

Try adding a `rewind` method to your `output` type, which goes back one byte. Now extend `output_of_string` appropriately.

6
Compressing Data

1

Use list processing functions over a list of integers representing the data. For testing purposes, re-use our `int_list_of_string` and `string_of_int_list` functions.

2

Carefully define a suitable data type for the tree – the data will all be at the fringes of the tree, since no code is a prefix of another. Write a function to add a code to the tree. Now, repeated insertion can be used to build the whole tree.

4

We can re-use the `read_up_to` function, building up two histograms – one for white runs and one for black runs.

7
Labelled and Optional
Arguments

1

Consider what happens if α is int.

2

Perhaps define one or more new types.

3

Consider which functions have two or more arguments of the same type. We can add labels to those arguments only and wrap the function up.

4

We can use an optional argument for the accumulator.

8
Formatted Printing

1

Consider `Printf.bprintf` as a way to accumulate the parts. What is special about the last element? What if there is no last element?

2

There is a format specifier for hexadecimal numbers. Consider what happens with very small character codes.

9
Searching for Things

1

The `at` function from the chapter may be re-used here, in both parts of the question.

2

Start by writing a function which gives the length of the longest prefix of a pattern at the beginning of a list. Now wrap it in another which works through the whole list.

3

The expression `Unix.gettimeofday ()` gives a floating-point number representing the current time.

4

Add a case to the inner match. It must manually check the next letter in the pattern matches the next letter in the string (if it exists).

5

This does not require altering the search code itself – one can just preprocess the pattern and string. There is a function `String.uppercase` in the Standard Library.

10
Finding Permutations

1

What is the base case? For the main case, first calculate the combinations of the tail by recursion. What can you do now?

2

You can build this from functions we have already written.

3

What is the base case? You will need to keep a counter to make sure we only generate lists of the given length.

4

Consider using the `swap` function we defined in the main text.

5

Instead of using indices for the “first” and “last”, use the values themselves. Pull the list representing the old permutation apart, and rearrange it until you have the next.

11
Making Sets

1

In the documentation for the Gc module, you will find the function `Gc.counters` and a description of how to calculate the total amount of memory allocated since the program began.

2

Add a `union` function to the signature, with the type α t → α t → α t and then a `union` function to the struct for each set representation.

3

You can include the given code inside the structure of the new module. Now, you can set the type t to be equal to S.t, the type of these new sets.

4

Alter the type first. The changes to each function then follow relatively easily.

12
Playing Games

1

We already have code to find the number of X wins. What are the conditions for a game being drawn?

2

It is only necessary to alter the type tree and the function `next_moves`, and only a little. Now we need a function to extract the part of the tree which begins with O in the centre slot. Once we have this, simple modifications of our functions for counting wins and draws will do the job.

3

There is no need to worry about the order of the numbers in the square – the tree will have the same essential characteristics regardless.

13
Representing Documents

3

A structure built from nested dictionaries would be suitable.

4

Consider everywhere a dictionary entry might appear. The function or functions will be recursive, following the general pattern of the data structure.

14
Writing Documents

1

Removing the space at the end is simple. How can we detect if we are about to output the first item, and thus do not want a space?

2

Remember to alter the `/Size` entry, and to change `/Indirect` entries as required to reflect the new structure.

3

For the content stream in the “Hello, World!” file, one long row is sufficient. However, when encoding other example content streams, consult the PDF specification to ensure the file is still valid. To test, open in your favourite PDF reader.

15
Pretty Pictures

1

We need to generate a set of points on the circle, and then they can be built into a path with `Move`, `Line`, and `Close`. This path can then be used with `Fill` to build the final page content.

2

First write a function to generate a path for a pseudo-random circle using a function we have previously written. Now `FillColour` and `Fill` can be added for each one, and the final list of operators produced.

3

We add `FillColourRGB` and `StrokeColourRGB` items to the data type and its associated functions. Then we can substitute them into the previous answer.

16
Adding Text

1

You need to alter `typeset_line_at`, `clean_lines`, and `downfrom` once you have defined the new values.

2

Try just adding eight space characters after each new line in `lines_inner`.

3

If there are n characters, we must insert n - 1 pieces of space between them, each of equal size.

4

To make the construction of the multipage document simpler, consider choosing carefully the order (and hence numbering) of the objects in the file.

Coping with Errors

It is very hard to write even small programs correctly the first time. An unfortunate but inevitable part of programming is the location and fixing of mistakes. OCaml has a range of messages to help you with this process.

Here are descriptions of the common messages OCaml prints when a program cannot be accepted or when running it causes a problem (a so-called “run-time error”). We also describe warnings OCaml prints to alert the programmer to a program which, though it can be accepted for evaluation, might contain mistakes.

ERRORS

These are messages printed when an expression could not be accepted for evaluation, due to being malformed in some way. No evaluation is attempted. You must fix the expression and try again.

Syntax error

This error occurs when OCaml finds that the program text contains things which are not valid words (such as `if`, `let` etc.) or other basic parts of the language, or when they exist in invalid combinations – this is known as syntax. Check carefully and try again.

`        OCaml`

`#1 +``;;`
`Error: syntax error`

OCaml has underlined where it thinks the error is. Since this error occurs for a wide range of different mistakes and problems, the underlining may not pinpoint the exact position of your mistake.

Unbound value …

This error occurs when you have mentioned a name which has not been defined (technically “bound to a value”). This might happen if you have mistyped the name.

`        OCaml`

`#` `x` `+ 1;;`
`Error: Unbound value x`

In our example `x` is not defined, so it has been underlined.

This expression has type … but an expression was expected of type …

You will see this error very frequently. It occurs when the expression’s syntax is correct (i.e. it is made up of valid words and constructs), and OCaml has moved on to type-checking the expression prior to evaluation. If there is a problem with type-checking, OCaml shows you where a mismatch between the expected and actual type occurred.

`        OCaml`

`# 1 +` `true``;;`
`Error: This expression has type bool but an expression was expected of type`
`int`

In this example, OCaml is looking for an integer on the right hand side of the `+` operator, and finds something of type bool instead.

It is not always as easy to spot the real source of the problem, especially if the function is recursive. Nevertheless, a careful look at the program will often shine light on the problem – look at each function and its arguments, and try to find your mistake.

This function is applied to too many arguments

Exactly what it says. The function name is underlined.

`        OCaml`

`# let f x = x + 1;;`
`val f : int -> int = <fun>`
`#` `f` `x y;;`
`Error: This function is applied to too many arguments;`
`maybe you forgot a` `‘;'`

The phrase “maybe you forgot a ‘;’ ” applies to imperative programs where accidently missing out a ‘;’ between successive function applications might commonly lead to this error.

Unbound constructor …

This occurs when a constructor name is used which is not defined.

`        OCaml`

`# type t = Roof | Wall | Floor;;`
`type t = Roof | Wall | Floor`
`#` `Window``;;`
`Error: Unbound constructor Window`

OCaml knows it is a constructor name because it has an initial capital letter.

The constructor … expects … argument(s), but is applied here to … argument(s)

This error occurs when the wrong kind of data is given to a constructor for a type. It is just another type error, but we get a specialized message.

`        OCaml`

`# type p = A of int | B of bool;;`
`type p = A of int | B of bool`
`# A;;`
`Error: The constructor A expects 1 argument(s),`
`but is applied here to 0 argument(s)`

RUN-TIME ERRORS

In any programming language powerful enough to be of use, some errors cannot be detected before attempting evaluation of an expression (until “run-time”). The exception mechanism is for handling and recovering from these kinds of problems.

Stack overflow during evaluation (looping recursion?)

This occurs if the function builds up a working expression which is too big. This might occur if the function is never going to stop because of a programming error, or if the argument is just too big.

`        OCaml`

`# let rec f x = 1 + f (x + 1);;`
`val f : int -> int = <fun>`
`# f 0;;`
`Stack overflow during evaluation (looping recursion?).`

Find the cause of the unbounded recursion, and try again. If it is really not a mistake, rewrite the function to use an accumulating argument (and so, to be tail recursive).

Exception: Match_failure …

This occurs when a pattern match cannot find anything to match against. You would have been warned about this possibility when the program was originally entered. For example, if the following function `f` were defined as

`let f x = match x with 0 -> 1`

then using the function with `1` as an argument would produce:

`        OCaml`

`# f 1;;`
`Exception: Match_failure ("//toplevel//", 1, 10).`

In this example, the match failure occurred in the top level (i.e. the interactive OCaml we are using), at line one, character ten.

Exception: …

This is printed if an un-handled exception reaches OCaml.

`        OCaml`

`# exception Exp of string;;`
`exception Exp of string`
`# raise (Exp "Failed");;`
`Exception: Exp "Failed".`

This can occur for built-in exceptions like `Division_by_Zero` or `Not_found` or ones the user has defined like `Exp` above.

WARNINGS

Warnings do not stop an expression being accepted or evaluated. They are printed after an expression is accepted but before the expression is evaluated. Warnings are for occasions where OCaml is concerned you may have made a mistake, even though the expression is not actually malformed. You should check each new warning in a program carefully.

This pattern-matching is not exhaustive

This warning is printed when OCaml has determined that you have missed out one or more cases in a pattern match. This could result in a `Match_failure` exception being raised at run-time.

`        OCaml`

`# let f x =` `match x with 0 -> 1``;;`
`Warning 8: this pattern-matching is not exhaustive.`
`Here is an example of a value that is not matched:`
`1`
`val f : int -> int = <fun>`

Helpfully, it is able to generate an example of something the pattern match does not cover, so this should give you a hint about what has been missed out. You may ignore the warning if you are sure that, for other reasons, this case can never occur.

This match case is unused

This occurs when two parts of the pattern match cover the same case. In this situation, the second one could never be reached, so it is almost certain the programmer has made a mistake.

`        OCaml`

`# let f x = match x with _ -> 1 |` `0` `-> 0;;`
`Warning 11: this match case is unused.`
`val f : int -> int = <fun>`

In this case, the first case matches everything, so the second cannot ever match.

This expression should have type unit

Sometimes when writing imperative programs, we ignore the result of some side-effect-producing function. However, this can indicate a mistake.

`        OCaml`

`#` `f 1``; 2;;`
`Warning 10: this expression should have type unit.`
`- : int = 2`

It is better to use the built-in `ignore` function in these cases, to avoid this warning:

`        OCaml`

`#` `ignore (f 1)``; 2;;`
`- : int = 2`

The ignore function has type α → unit. It has no side-effect.