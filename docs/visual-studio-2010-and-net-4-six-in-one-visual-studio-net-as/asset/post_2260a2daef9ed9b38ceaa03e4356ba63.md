
# Object Expressions

You can instantiate interfaces using *object expressions*:

```
let aud2000 =
    new ICar with
        member this.Name = "Audi"
        member this.Year = 2000
```

Object expressions are used for implementing interfaces on-the-fly. Any given expression must give the implementation for all interface members:

```
let bmw525i2004 =
    new ICarModel with
        member this.Name = "BMW"
        member this.Year = 2004
        member this.Model = "525i"
```

You can also define new classes that implement interfaces, as many as you prefer:

```
type Citroen(model: string, year: int) =
    interface ICar with
        member this.Name = "Citroen"
        member this.Year = year
        member this.Model = model
```

# Objects

Ordinary classes can be instantiated using their constructors and the optional *new* keyword.

```
let aud2000 = Car("Audi", 2000)
let bmw525i2004 = new BMW("525i", 2004)
```

# Object State via Binding

Now that you have how to define classes and interfaces, object expressions work, and you can instantiate both to create objects, there are a few additional details you should be aware of.

Foremost, you can add constructor-time state to your objects using *let* bindings in the class definition:

```
type Rectangle(height, width) =
    let area = height*width
    let diagonal = Math.Sqrt(height**2.0 + width**2.0)
    member this.Area = area
    member this.Diagonal = diagonal
```

These *let* bindings, similar to the type/constructor arguments, are visible in the entire type definition, and they are computed only once the object is being constructed. They need to be placed before the members; otherwise, you will get a compiler error.

# Object Initialization

You can also add initialization code to your classes using the do keyword. This code can be added before or after the let bindings. Usually, you can use initialization code to check various constraints that must hold for the object to be constructed. Here is an example of refusing to construct rectangles with negative dimensions:

```
type Rectangle2(height, width) =
    do if height < 0. || width < 0. then
        failwith("Can't construct rectangle with negative dimensions")

    let area = height*width
    let diagonal = Math.Sqrt(height**2.0 + width**2.0)

    member this.Area = area
    member this.Diagonal = diagonal
```

# Setters and Getters

In all previous class examples, the properties you defined were read-only. Another way to write these properties would be to use the getter explicitly:

```
...
member this.Area with get () = area
```

Because there is no setter defined by default, if you tried to set them, you would get an error:

```
let r2 = Rectangle2(100,100)
r2.Area <- 100
// Error
```

Adding a setter is straightforward, and it usually comes together with the getter (unless you want only a setter):

```
type Rectangle2(height, width) =
    let mutable colorCode = 0
    ...
member this.ColorCode
    with get () = colorCode
    and set cc = colorCode <- cc
```

# Indexers

You can add dot notation to your objects in the form of object.[index] and object.[index] <- expr. These indexer properties are special properties that take arguments, and can be defined with getters and setters as shown previously to a special property called Item.

For example, you may want to provide a mechanism to read the coordinates in a polygon by an index (starting at zero). You can implement this by creating a Polygon class with an indexer property:

```
type Polygon(coords:int list) =
    ...
member self.Item
    with get idx =
        if Seq.length <= idx then
            failwith "Index out of bound"
        else
            Seq.nth idx coords
```

You can test the indexer property in F# Interactive:

```
> let p = new Polygon([1;2;3;4;5;6;7]);
val p : Polygon

> p.[2] | printfn "%d"
val it : unit
```

# Named and Optional Arguments

You can make your code more readable by naming arguments and setting properties in your constructor. For example, you can construct a new rectangle like this:

```
let r2 = Rectangle(height=100., width=100., ColorCode=5)
```

You can verify that this initialized the object properly:

```
> r2.ColorCode;
val it : int = 5
> r2.Area;
val it : float = 100.0
> r2.Diagonal;
val it : float = 141.421...
```

You can also add optional arguments to your constructors:

```
type Circle(radius, x, y, ?color) =
    let setColor =
        match color with
        | None -> 
        | Some c -> c
    member self.Everything = (radius, y)
```

Here, ?color defines an optional argument to Circle. This is modeled as receiving an option value, which you can check as part of the object initialization, and assign appropriately. You can test this in F# Interactive:

```
> let c1 = new Circle(radius=10, x=5, y=5);
val c1 : Circle

> let c2 = new Circle(10, 5, 5);
val c2 : Circle

> c1.Everything;
val it : int * int = (10, 5)
> c2.Everything;
val it : int * int = (10, 5)
```

# Anonymous Functions

You can create an anonymous function (a lambda expression in C#)—that is, a new unnamed function using the fun keyword, listing the formal parameters and the body of the function:

```
fun x y -> Math.Sqrt(x + y)
```

You can name functions by binding them to a name:

```
let diag = fun x y -> Math.Sqrt(x + y)
```

This is equivalent to the following:

```
let diag x y = Math.Sqrt(x + y)
```

If you need a single argument that pattern matches its argument (you will learn by pattern matching in this chapter), you can use the function keyword:

```
let onlyOne = function 1 -> 0
```

This defines a function that takes an integer and returns 1 if it was 1, and 0 otherwise. By convention, each pattern match starts with a pipe (|), the first case.

The function values can be passed or returned from other functions. One particularly useful application of anonymous functions is writing continuations, also known as continuation style (CPS). You will see continuations in this chapter that deals with asynchronous programming, where an expression that is evaluated takes place via registering a callback function (that is, a continuation that will receive the computed value and proceed with the result of the computation).

For an example of explicit continuations, consider a CPS version of an evaluator (more of which will be later in this chapter in the chapter on discriminated unions):

```
type Expr =
    | Number of float
    | Binop of (float -> float -> float) * Expr * Expr

static member Add (e1, e2) = Binop (+), e1, e2)
static member Sub (e1, e2) = Binop (-), e1, e2)
static member Mul (e1, e2) = Binop (*), e1, e2)
static member Prod (e1, e2) = Binop (/), e1, e2)

let rec Eval cont =
    match e with
    | Number n ->
        cont n
    | Binop (f, e1, e2) ->
        Eval (fun i1 ->
            Eval e2 (fun i2 ->
                f i1 i2 cont))
```

The Eval function receives an expression and an explicit continuation that takes the result of the expression. When the expression is a number, you simply pass it to the continuation. If the expression is a binary operation, you evaluate the first operand with a continuation function that evaluates the second operand, which itself gets a continuation that takes both of the evaluated results, applies the binary operation on them, and passes the overall result to the original continuation.

CPS is a common functional pattern, used for translating between different representations or traversing data types.

# Using Tuples

Tuples are a fundamental functional data structure, another wellknown of F# development. They are a versatile data type that .NET 4.0 finally included them as a system type as System.Tuple, pioneered and inspired by F#.

Tuples are also referred to as product types, because they constitute the Cartesian product of their parts, and also because, in theory, they are denoted by a star symbol (such as T1*T2*T3). As you saw earlier, in F# type signatures, tuples are marked with the star symbol (such as T1*T2*T3).

You can construct tuples by connecting values with a comma:

- 1, "my string", 3

Often, you must parenthesize to avoid precedence errors — for example, when you call a function that takes a tuple, argument, as you saw in the beginning of this chapter:

```
(1, "my string", 3) | MyFunction
```

Here, the function call (or the pipe operator) has higher precedence than a comma, and without parentheses, it would only apply to the value in the intended tuple.

Tuples are also called n-tuples for any n, where the tuple groups n separate values. You can nest tuples in tuples, so the following are different values:

```
(1, "my string", 3)
(1, ("my string", 3))
((1, "my string"), 3)
```

You can use pattern matching to deconstruct tuples, as you will see later in this chapter. F# also provides some utility functions to work with pairs:

```
> fst (1, 2);
val it : int = 1
> snd (1, 2);
val it : int = 2
```
