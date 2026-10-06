> Tip FSI is not only a good approach for debugging a program and running unit tests, it's also a quick way to check a function's definition. For example, you can type Seq.filter into the FSI window. FSI shows you the function definition, which saves you the seconds of going to the MSDN documentation.

# The Sequence, List, and Array Module Functions

Now you might be wondering someone can find functions like Seq.filter and Seq.sum. They are located inside three modules: Seq, List, and Array module. Module is a special way for organizing F# code that will be discussed in this chapter. For the convenience of list, we denote seq, list, and array as collections. The functions listed next are the most commonly used. Refer to MSDN document http://msdn.microsoft.com/en-us/library/ee353413 for a complete function list.

# length

It is easy to get the length of a list or an array using the length function. The LINQ extension method provides the same functionality. An example is shown in Listing 1-33.

LISTING 1-33 The length function

```
let myList = [1..10]
let listLength = myList |> List.length //Length is 10
let myArray = [1..10]
let arrayLength = myArray |> Array.length //arrayList is 10
let mySeq = seq { 1 . 10 }
let seqLength = mySeq |> Seq.length //10
```

> Note Seq has a length function, but keep in mind that a sequence can be of an infinite length. An infinite-length sequence can make many functions not applicable, unsafe, or both.

# exists and exists2

Seq, list, and array provide the same functions to check whether an element exists and to see whether two collections contain the same element at the same location. The exists function is used to check for a single element, and exists.2 is used for checking two collections. Listing 1-34 shows how to use Seq.exists and Seq.exists2.