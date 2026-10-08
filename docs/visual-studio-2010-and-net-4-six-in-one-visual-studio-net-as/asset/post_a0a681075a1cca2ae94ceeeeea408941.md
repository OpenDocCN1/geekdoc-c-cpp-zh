
# Discriminated Unions

Discriminated (or tagged) unions are a form of algebraic data types that can take on a predefined set of shapes. One immediate advantage of using discriminated unions in your code is that the compiler can check that you handle all possible shapes where you operate on them, as you will see shortly in the pattern matching. However, fundamentally, even more important advantage is that they provide type-safe access to the values they carry, as opposed to the C-style unions you have encountered before. Discriminated unions are important abstractions in functional programming because they partition a value space into a set of shapes, making it easier and conceptually clearer to work on them.

Consider the following example:

```
type Expr =
  Num of float
  Var of string
  UnOp of (float -> float) * Expr
  BinOp of (float -> float -> float) * Expr * Expr
  static Member Add (el, e2) = BinOp (+), e2)
  static Member Sub (el, e2) = BinOp (-), e2)
  static Member Mul (el, e2) = BinOp (*), e2)
  static Member Div (el, e2) = BinOp ( /), e2)
  static Member Sin (el) = UnOp (Math.Sin, el)
  static Member Cos (el) = UnOp (Math.Cos, el)
```

Here you created a discriminated union to represent mathematical expressions with four basic shapes: numbers, variables and binary operations. To make it easier to construct (expressions) of this type, you have also added a few members to represent the basic arithmetic operations, sine and cosine. You can also add any number of members to represent the same way.

You now construct mathematical expressions easily. Consider the following that represents cos(x+y):

```
let num = Expr.Cos (Expr.Add (Expr.Var "x", Expr.Num Math.PI)
```

Note that you have used type name to qualify the occurrences of the basic shapes (Var and Num) — this is not required as long as the type itself is in scope. However, because you may have union cases with the same name in different unions, it is good practice to qualify them with the appropriate type name.

You can examine union values (and others) using pattern matching — a machinery used to deconstruct and bind values via patterns. You will learn more about pattern matching later in this chapter, but as a preview, here is a function that evaluates expressions of your type:

```
let rec Eval (env: Map<string, float>) = function
  Num num ->
    num
  Var v ->
    env.[v]
```

```
| UnOp (op, e) ->
  op (Eval env e)
| BinOp (op, e1, e2) ->
  op (Eval env e1) (Eval env e2)
```

You can play the evaluator in F# Interactive with a just to double-check that it works correctly:

```
> let env = ["x", 1.0] | Map.OfList;

val env : Map<string, float>

> Eval env num;
  val it : float = -0.5403023059
> Math.Cos (l + Math.PI);
  val it : float = -0.5403023059
>
```

# Using Options

Option values are a generalization of the concept of “nullables” — that is, to represent a value of some type τ is given or not. One key difference from the Nullable<T> .NET type is that F# options can be used with any arbitrary type, and not just value types. As you may expect, options can be implemented with discriminated unions. In fact, this is how it’s done in the F# standard library:

```
type Option<T> =
  Some of 'T
  None
```

You will also find type aliases (simple to define as a lowercase type) to this type in the standard library, and, in fact, this is the type you will be seeing in F# code:

```
type 'T option = Option<'T>
```

Option values play an important role in making F# programming safe. One of the drawbacks of imperative languages is that they rely heavily on nulls to represent that some computation proceed, or the result is undefined. In fact, there are plenty of standard .NET library functions returning nulls in certain situations.

Consider the following FileExtension fileName:

```
let FileExtension fileName =
  if fileName > String.IsNullOrEmptyOrEmpty | not then
    fileName.LastIndexOfOf('.')
  | function
      n when n < 1 ->
        None
      idx ->
        fileName.Substring
        | Some
  else
    None
```

This function returns the file extension from the filename parameter as an option. It will only succeed if the filename has passed a dot (.) in it, and then it will return the tail from dot as a Some value. In every other case, it will return None. A bit of F# Interactive exploration helps to test this:

```
> FileExtension "data";
val it : string option = None
> FileExtension "data";
val it : string option = Some "*
> FileExtension "data.dat";
val it : string option = Some "*.dat"
> FileExtension "*";
val it : string option = None
> FileExtension null;
val it : string option = None
>
```

# Using Records

You can define a record type by listing its fields and types inside braces:

```
type Person =
  { FirstName: string
  LastName: string
  Age: int
  Children: Person list
  mutable LastSeen: System.DateTime option }
```

You can just create a new record value by giving the values of its fields inside braces:

```
let john =
  { FirstName = "John"
  LastName = "Smith"
  Age = 32
  Children = []
  LastSeen = None }
```

In the definition and the value constructor, fields can be separated by semicolons — this comes in handy when you want to put multiple fields on the same line.

At times, you may need to copy records to create new ones, perhaps with certain fields changed:

```
let sally =
  { john with
  FirstName = "Sally"
  Age = 25 }
```

One important thing to remember is that records are not value types. Switching one of the fields to mutable will reveal this:

```
let shadowOfSally = sally
```

Now, in F# Interactive, you can experiment with what happens when you update shadowOfSally:

```
> shadowOfSally.LastSeen <- Some System.DateTime.Now;
val it : unit = ()
> sally;
val it : Person =
  {FirstName = "Sally";
  LastName = "Smith";
  Age = 25;
  Children = [];
  LastSeen = Some 12/16/2009 10:16:03
    Day = 16;
    DayOfWeek = Wednesday;
    DayOfYear = 350;
    Hour = 22;
    Kind = Local;
    Millisecond = 122;
    Minute = 16;
    Month = 12;
    Second = 53;
    Ticks = 6339659856312245330L;
    TimeOfDay = 22:16:03.1224530;
    Year = 2009;}
```

Type inference for records works by identifying fields and trying to match them to unique types. If you have multiple records types that overlap in their field names. In this case, you can prefix the labels with the record type to disambiguate — and even a single

# Using Lists

F# lists provide a hassle-free container for storing ordered sequence of values of a given type, They are implemented as linked lists, so if you need random access to the list, you should consider sets or arrays instead. Lists are at the core of functional programming, and as such, they are primary collection type as you work with F# code. They also receive extra attention in the language, which provides a clean syntax for constructing list values.

List values can be iterated, transformed, and aggregated using the static members available on the List module (defined as Microsoft.FSharp.Collections.List). Consider the following:

```
> let a = List.empty
let b = []
let c = 1 :: 2 :: 3 :: [ 4 ]
let d = [ 1; 2; 3; 4 ];
```

```
val a : 'a list
val b : 'a list
val c : int list = {1; 2; 3; 4}
val d : int list = {1; 2; 3; 4 };
```

Here, a and b contain the empty list, with a generic type that no elements have been given; c and d are also, with 1, 2, 3, 4 as elements— and, with the concrete type int list.

You can traverse (iterate) a list with List.iter, giving a "visitor" function that takes an element and returns nothing (so, a function of type 'T -> unit) and a list you want to traverse (of type 'T list):

```
> List.iter(printf "Printing a number: %d" c);

Printing a number: 1
Printing a number: 2
Printing a number: 3
Printing a number: 4
val it : unit = ()
```

# TABLE 25-10: Language Constructs

| EXPRESSION | DESCRIPTION | EXAMPLES |
| --- | --- | --- |
| [ ] | An empty list. | [ ] |
| expr :: expr | Adding an element to the head of the list ("consing"). | 1 :: [ 2; 3 ] |
| [ expr; .. expr ] | A list with its elements. | [ 1; 2; 3 ] |
| [ expr .. expr ] | A range of numbers. | [ 1 .. 100 ], [ 1.0 .. 100.0 ] |
| [ expr .. expr .. expr ] | A range of numbers using a skip value. | [ 0 .. 2 .. 100 ] |
| expr @ expr | Concatenation of lists. | [ 1; 2 ] @ [ 3; 4 ] |
| [ for x in list -> expr ] | A list comprehension. | [ for x in 1 .. 100 -> x*x ]
[/