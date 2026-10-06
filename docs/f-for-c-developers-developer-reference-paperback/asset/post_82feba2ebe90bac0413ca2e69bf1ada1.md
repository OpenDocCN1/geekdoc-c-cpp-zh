
```
compare duRecord1 duRecord2
compare duRecord1 duRecord3
compare duRecord2 duRecord3
compare duRecord1 duRecord4
```

```f
// create DU Case4 instances
let duTuple1 = Case4(tuple1)
let duTuple2 = Case4(tuple2)
let duTuple3 = Case4(tuple3)
let duTuple4 = Case4(tuple4)
```

```f
compare duTuple1 duTuple2
compare duTuple1 duTuple3
compare duTuple2 duTuple3
compare duTuple1 duTuple4
```

```f
// compare Case4 with Case3
compare duTuple1 duRecord1
```

Execution result from the record, tuple, and DU comparison code

```
{X = 1; Y = "1"; < {X = 1; Y = "2";}
{X = 1; Y = "1"; < {X = 2; Y = "1";}
{X = 1; Y = "2"; < {X = 2; Y = "1";}
{X = 1; Y = "1"; < {X = 1; Y = "1";}}
```

```
(1, "1") < (1, "2")
(1, "1") < (2, "1")
(1, "2") < (2, "1")
(1, "1") = (1, "1")
```

```
Case 1 < Case 2
Case 1 = Case 1
Case 2 > Case 1
```

```
Case3 {X = 1; Y = "1";} < Case3 {X = 1; Y = "2";}
Case3 {X = 1; Y = "1";} < Case3 {X = 2; Y = "1";}
Case3 {X = 1; Y = "2";} < Case3 {X = 2; Y = "1";}
Case3 {X = 1; Y = "1";} = Case3 {X = 1; Y = "1";}}
```

```f
Case4 (1, "1") < Case4 (1, "2")
Case4 (1, "1") < Case4 (2, "1")
Case4 (1, "2") < Case4 (2, "1")
Case4 (1, "1") = Case4 (1, "1")
Case4 (1, "1") > Case3 {X = 1; Y = "1";}
```

> Some returns and extra spaces are removed to increase the readability.

# Using Pattern Matching

We used pattern matching in various examples in Chapter 1, such as in Listing 1-10. At that time, your understanding of pattern matching was that it is something similar to a C# switch statement. Although this is true, pattern matching is much more powerful.

Let's start by defining patterns. Patterns are simply rules used to transform data. According to this definition, you can use pattern matching to match input data with some patterns and trigger corresponding actions, such as actions that transform data. What's more, the pattern also provides a way to decompose input data. Listing 6-38 uses pattern matching to rewrite the odd-number program from Chapter 1. The function transformEvenToZero converts all even numbers to zero and then sums the elements in the transformed sequence.

Pattern matching comes in several flavors. Listing 6-38 is the simplest pattern-matching example; it matches the input data against a constant value. This is called a constant pattern.

LISTING 6-38 Pattern-matching example

```fsharp
let isEvenNumber = x % 2 = 0
let transformEvenToZero x =
    match isEvenNumber x with
    | true -> 0
    | false -> x

// sum of odd number from 0 to 100
let r = seq {0..100} |> Seq.sum transformEvenToZero
```

Before I introduce more complex patterns, I should briefly introduce the function keyword. Listing 6-39 shows how to use the function to simplify the match expression, which is the match x with in the sample code. The function keyword implicitly appends a parameter to the containing function.

LISTING 6-39 Using the function keyword

```fsharp
Using match in a function
let matchSample x =
    match x with
    | 1 -> printf "this is one"
    | 2 -> printf "this is two"
    | 3 -> printf "this is three"
    | _ -> printf "other value"
```

```fsharp
Using function to represent match
let functionSample x =
    match x
    | 1 -> printf "this is one"
    | 2 -> printf "this is two"
    | 3 -> printf "this is three"
    | _ -> printf "other value"
```

# Using the Tuple Pattern

A more complex pattern is the tuple pattern, which is used to match a pair. Listing 6-40 implements the OR function. The first version returns false when both inputs are false. The simplified version implements this by using (_, _), which can match anything. Note that the tuple can have more than two values. Listing 6-65 uses tuple to decompose a triple in the list.

**LISTING 40 Tuple pattern**

```fsharp
OR function with tuple matching
let orFunction (x, y) =
    match x, y with
    | true, true -> true
    | true, false -> true
    | false, false -> false

Simplified OR function with tuple matching
let orFunction2 (x, y) =
    match x, y with
    | false, false -> false
    | _, _ -> true
```

> Note The _, _ can be further simplified as _. The _, _ is used to match any tuple value, while _ is used to match any value.

Listing 6-41 shows how to use pattern matching to work with a tuple that is returned from TryGetValue.

LISTING 41 Using the tuple pattern to work with Dictionary function

```fsharp
let f x =
    let dict = System.Collections.Generic.Dictionary()
    dict.[0] <- "0"
    dict.[1] <- "1"

    match dict.TryGetValue x with
    | true, v -> sprintf("%A mapped to %A") v
    | false, _ -> "cannot find"

printf("%A" (f 0))
printf("%A" (f 1))
printf("%A" (f 2))
```

Execution result
"found 0 mapped to "0"
"found 1 mapped to "1"
"cannot find"

One nice feature about pattern matching is that F# can generate a warning if one possible pattern is missing in the match expression. For example, when sending the code to FSI, F# warns you about this problem.

LISTING 42 Missing one pattern in the match expression

```fsharp
let orFunction (x, y) =
    match x, y with
    | true, true -> true
    // true, false -> true // miss one pattern
    | false, true -> true
    | false, false -> false

stdin(2,15): warning FS0025: Incomplete pattern matches on this expression. For example, the value (_,false)' may be covered by the pattern(s).

# Using the List and Array Patterns

Like a tuple, patterns can also decompose a list or array into values. Listing 6-43 decomposes an array and gets the array length.

LISTING 43 An array pattern

```fsharp
let arrayLength array =
    match array with
    | [|] -> 0
    | [ _ | _ ] -> 2
    | [ _ ; _ ; _ ] -> 3
    | _ -> Array.length array
```

Listing 6-44 shows how to use a recursive function to decompose a list into a head and tail, the length of that list. The cons operator (:) decomposes the list into a head part and a tail part.

LISTING 44 An example of the cons pattern

```fsharp
let rec listList list =
    match list with
    | head :: tail -> 1 + (listList tail)
    | [] -> 0
```

> **Note** The preceding code can cause a stack overflow because it is not tail recursive. The following code provides a version that is tail recursive:

```fsharp
let rec listList acc list =
    match list with
    | head :: tail -> listLength (acc + 1) tail
    | [] -> acc
```

There are some interesting examples in Listing 6-45 for the list pattern matching. The first code snippet matches the list and decomposes it into two elements, and it contains a list that represents the tail. The second snippet checks the element type and converts the element back to the type, as it was prior to boxing.

LISTING 6-45 Pattern matching for list

```fsharp
let list = [1;2;3;4];
match list with
| h0::h1::t -> printfn "two elements %A and tail %A" h0 h1 t
| _ -> ()

let objList = [box(1); box("a"); box("c")]
match objList with
| [| ?: int as i; ?: string as str; ?: char as ch |] ->
    printf("values are %A %A %A") i str (ch)
| _ -> ()
```

> **Note** The code: ? Int as i is a type of pattern match that will be discussed later in this section.

## Using the NULL Pattern

As mentioned in the "Working with Options" section earlier in the chapter, option is generally a better choice than using a NULL value. The first code snippet in Listing 6-46 shows a match expression that uses the option type.

Another option is to match against a NULL. This is known as the NULL pattern, and an example of this is shown in the second code snippet in Listing 6-46. An important application of the NULL pattern is to convert a NULL from an option or vice versa.

**LISTING 6-46** NULL pattern

```fsharp
Using an identifier pattern to test and extract an option value
let extractOption x =
    match x with
    | Some a -> printf("option has value %A") a
    | None -> printf("option has no value")
```

```fsharp
Using a NULL pattern to convert a nullable .NET value to an F# code
let toOption x =
    match x with
    | null -> None
    | _ -> Some x
```

## Using the Record and Identifier Patterns

Listing 6-47 shows how to use the identifier pattern to decompose a discriminated union. The second code snippet shows how to use the record pattern to decompose a record.
