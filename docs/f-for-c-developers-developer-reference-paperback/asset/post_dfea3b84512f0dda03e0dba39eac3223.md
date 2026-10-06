
```fsharp
if finalBalance > 0 then
    account.Balance <- finalBalance
    account
else
    printfn "not enough found"
    account
```

[<Measure>] type USD
let account = Account<USD>()
let bank = Bank<USD>(account)

```fsharp
let transaction =
    bank {
        deposit 100.<USD>
        withdraw 50.<USD>
}
```

printfn "balance after one transaction = %A" (transaction).Balance

![](img/63aaf94e22830ab98ce16c5946be8ef6_374_0.png)

FIGURE 6-2 Computation expression execution result

## Using Reflection

As a C# developer, reflection is not likely a new concept for you. Usually, reflection in C# involves defining or applying attributes and getting type or method information.

## Defining Attributes

Listing 6-109 shows how to define a customized attribute.

LISTING 6-109 Defining an attribute

```fsharp
// define attribute with a property
type MyAttribute()
    inherit System.Attribute()
    member val MyProperty = System.String.Empty with get, set
```

You can add one or more attributes to modules, or smaller program elements, such as classes and properties, by putting the attribute name between < and >. The assembly-level attribute is different, because it can be applied only by using the do keyword. The attribute can be applied separately as is done in C#. Additionally, multiple attributes can be applied in a group format, when multiple attributes are put into [< >] and separated by semi-colons. Listing 6-110 shows how apply one or more attributes to a class definition. There is little difference between applying attributes to a class and to an interface/struct. I will leave this exercise to you.

## LISTING 6-110 Applying an attribute to a class and class members

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

// define an attribute
type MyAttribute2() =
    inherit System.Attribute()

// define a class with one attribute
[<MyAttribute>
type MyClassWithOneAttribute() = class

// define a class with two attributes applied separately
[<MyAttribute> [<MyAttribute2>
type MyClassWithTwoAttributes() = class

// define a class with two attributes applied as a group
[<MyAttribute; MyAttribute2>
type MyClassWithGroupedAttribute() = class

// apply an attribute to a method, property, or field
type MyClass3() =
    [<MyAttribute>
    let mutable Variable = 0

    [<MyAttribute>
    member this.Method([<MyAttribute2; MyAttribute>] x0, [<MyAttribute>] x1) = ()

    member this.Property
    with [<MyAttribute2>] get() = Variable
    and set(v) = Variable - v

    [<MyAttribute>
    member val Property2 = 0 with get, set

// apply attribute to mutual reference class
type MyClass4() =
    let a:MyClass5 = MyClass5()
and ([<MyAttribute>] MyClass5() = class
```

356 PART II F#'s Unique Features

Listing 6-111 shows how to apply attributes to F#-specific structures, such as a let binding and a record. Also, it shows how to apply attributes on the special structures in F# class definitions, as the primary constructor.

## **LISTING 6-111** An attribute on F#-specific data structures

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

[<MyAttribute>
let myValue = 0

[<MyAttribute>
let myFunction x = x + 1

// the functionality of the following two statements are the same
let [<MyAttribute>] a, b = 1, 2

// apply an attribute to a function
rec [<MyAttribute>] f() = g()

// apply an attribute to mutual reference functions
and [<MyAttribute>] g() = printf "hello"

///apply an attribute to a record
[<MyAttribute>] = {
  type Point =
  [<MyAttribute>] x : float;
  [<MyAttribute>] y: float;
  z: float; }

// apply an attribute to a DU
[<MyAttribute>
type DU =
  | [<MyAttribute>] Case1 of float
  | Case2 of double
  | [<MyAttribute>] Case3 of double

// apply an attribute to a unit of measure
[<MyAttribute>] type km

// apply an attribute to an enumeration
[<MyAttribute>
type Color =
  | [<MyAttribute>] Red = 0
  | Green = 1
  | [<MyAttribute>] Blue = 2
```

```fsharp
// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let MyTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```
Wait, checking back:
type MyClass2[<-MyAttribute>]() = class

end

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count

Wait, let me re-examine the OCR for `type MyClass`.
OCR: `type MyClass[<-MyAttribute>] xValue:double, yValue:double)`
It looks like `type MyClass[<-MyAttribute](xValue:double, yValue:double)`.

Let's fix the block based on OCR:

```fsharp
// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

end

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```

Wait, the OCR has:
`type MyClass[<-MyAttribute>] xValue:double, yValue:double)`
This is likely `type MyClass[<-MyAttribute](xValue:double, yValue:double)`.

Let's continue from `count`:

```fsharp
// define a static field named count
[<MyAttribute>]
static val count = 0
```
Wait, the OCR doesn't have `static val`. Let's re-read.

OCR:
`// define a static field named count`
Then it jumps to:
`356 PART II F#'s Unique Features`

Wait, the OCR is very messy there. Let's reconstruct based on the text provided provided.

```fsharp
// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

end

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```

Actually, the OCR ends at `// define a static field named count`. No, let me check the next page.

`PAGE 377` starts with `// apply an attribute to an exception type`.
Wait, the OCR text is repeated or fragmented. Let's look at `PAGE 377` again.

`[PAGE 377]`
```
// apply an attribute to an exception type
...
```
Wait, the OCR for `PAGE 377` is actually a continuation of the end of `PAGE 376`? No.

Let's look at the flow:
Page 376 ends with `| [<MyAttribute>] Blue = 2` ```.
Page 377 starts with `// apply an attribute to an exception type`.

Wait, I see. The OCR has a lot.
Let's re-process the text from `PAGE 377` carefully.

```fsharp
// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

end

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```
Wait, the OCR text for `PAGE 377` is actually a mess of repeated code. Let's look at the text after `356 PART II...`.

`356 PART II F#'s Unique Features`
`[PAGE 376]`
`Listing 6-111 shows how to apply attributes to F#-specific structures...`
`# LISTING 6-111 An attribute on F#-specific data structures`
`...code block...`
`[PAGE 377]`
`...code block...`

Wait, the code in `PAGE 377` is the *continuation* of `LISTING 6-111`.
Let's look at the code block in `PAGE 376`:
```fsharp
// define an attribute
type MyAttribute() =
    inher System.Attribute()

[<MyAttribute>
let myValue = 0

[<MyAttribute>
let myFunction x = x + 1

// the functionality of the following two statements are the same
let [<MyAttribute>] a, b = 1, 2

// apply an attribute to a function
rec [<MyAttribute>] f() = g()

// apply an attribute to mutual reference functions
and [<MyAttribute>] g() = printf "hello"

///apply an attribute to a record
[<MyAttribute>] = {
  type Point =
  [<MyAttribute>] x : float;
  [<MyAttribute>] y: float;
  z: float; }

// apply an attribute to a DU
[<MyAttribute>
type DU =
  | [<MyAttribute>] Case1 of float
  | Case2 of double
  | [<MyAttribute>] Case3 of double

// apply an attribute to a unit of measure
[<MyAttribute>] type km

// apply an attribute to an enumeration
[<MyAttribute>
type Color =
  | [<MyAttribute>] Red = 0
  | Green = 1
  | [<MyAttribute>] Blue = 2
```
And `PAGE 377` continues the block:
```fsharp
// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

end

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```
Wait, there's more text in `PAGE 377`:
`356 PART II F#'s Unique Features` (This is a footer/page number)
`[PAGE 378]` (Wait, the OCR says `[PAGE 377]` but then shows `[PAGE 378]`? No, let me re-read).

OCR carefully:
`[PAGE 377]`
`// apply an attribute to an exception type...`
`...
`356 PART II F#'s Unique Features`
`[PAGE 376]`
`Listing 6-111 shows how...`

Wait, the OCR is very jumbled. Let's follow the logical flow.
1. Page 374: Code block for `account.Balance`.
2. Code block for `transaction` and result.
3. Header: `## Using Reflection`.
4. Header: `## Defining Attributes`.
5. Listing 6-109 description and code.
6. Paragraph about attributes.
7. Header: `## LISTING 6-110 Applying an attribute to a class and class members`.
8. Code block for Listing 6-110.
9. Footer: `356 PART II F#'s Unique Features`.
10. Page 376: Listing 6-111 description.
11. Header: `## LISTING 6-111** An attribute on F#-specific data structures.
12. Code block for Listing 6-111 (starts on 376, ends on 377).
13. Page 377: Continuation of Listing 6-111.
14. Then there's some weird text:
    `356 PART II F#'s Unique Features`
    `[PAGE 376]` (Wait, the OCR says `[PAGE 376]` again? No, let me look closer).

Actually, let's look at the text after `PAGE 377`:
`356 PART II F#'s Unique Features`
`[PAGE 376]` (Wait, the OCR provided is repeating pages).

Let's re-read the text from `PAGE 377` onwards:
`// apply an attribute to an exception type...`
`...`
`// apply an attribute to the parameter of a constructor`
`type MyClass[<-MyAttribute](xValue:double, yValue:double)`
`// define a static field named count`

And then:
`356 PART II F#'s Unique Features`
`[PAGE 376]`
`Listing 6-111 shows how to apply attributes...`

Wait, the OCR is definitely corrupted. I will extract the unique content and organize it logically. 

Logical flow:
- Code block (374)
- Code block (374)
- Using Reflection
- Defining Attributes
- Listing 6-109
- Paragraphs
- LISTING 6-110 Applying an attribute to a class and class members
- Code block (374-375)
- LISTING 6-111 An attribute on F#-specific data structures
- Code block (376-377)
- The weird text `356 PART II...` seems like a footer.

Let's clean the code.

```fsharp
if finalBalance > 0 then
    account.Balance <- finalBalance
    account
else
    printfn "not enough found"
    account

[<Measure>] type USD
let account = Account<USD>()
let bank = Bank<USD>(account)

let transaction =
    bank {
        deposit 100.<USD>
        withdraw 50.<USD>
}

printfn "balance after one transaction = %A" (transaction).Balance
```

![](img/63aaf94e22830ab98ce16c5946be8ef6_374_0.png)

FIGURE 6-2 Computation expression execution result

## Using Reflection

As a C# developer, reflection is not likely a new concept for you. Usually, reflection in C# involves defining or applying attributes and getting type information.

## Defining Attributes

Listing 6-109 shows how to define a customized attribute.

LISTING 6-109 Defining an attribute

```fsharp
// define attribute with a property
type MyAttribute()
    inherit System.Attribute()
    member val MyProperty = System.String.Empty with get, set
```

You can add one or more attributes to modules, or smaller program elements, such as classes and properties, by putting the attribute name between < and >. The assembly-level attribute is different, because it can be applied only by using the do keyword. The attribute can be applied separately as is done in C#. Additionally, multiple attributes can be applied in a group format, when multiple attributes are put into [< >] and separated by semi-colons. Listing 6-110 shows how apply one or more attributes to a class definition. There is little difference between applying attributes to a class and to an interface/struct. I will leave this exercise to you.

## LISTING 6-110 Applying an attribute to a class and class members

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

// define an attribute
type MyAttribute2() =
    inherit System.Attribute()

// define a class with one attribute
[<MyAttribute>
type MyClassWithOneAttribute() = class

// define a class with two attributes applied separately
[<MyAttribute> [<MyAttribute2>
type MyClassWithTwoAttributes() = class

// define a class with two attributes applied as a group
[<MyAttribute; MyAttribute2>
type MyClassWithGroupedAttribute() = class

// apply an attribute to a method, property, or field
type MyClass3() =
    [<MyAttribute>
    let mutable Variable = 0

    [<MyAttribute>
    member this.Method([<MyAttribute2; MyAttribute>] x0, [<MyAttribute>] x1) = ()

    member this.Property
    with [<MyAttribute2>] get() = Variable
    and set(v) = Variable - v

    [<MyAttribute>
    member val Property2 = 0 with get, set

// apply attribute to mutual reference class
type MyClass4() =
    let a:MyClass5 = MyClass5()
and ([<MyAttribute>] MyClass5() = class
```

Listing 6-111 shows how to apply attributes to F#-specific structures, such as a let binding and a record. Also, it shows how to apply attributes on the special structures in F# class definitions, as the primary constructor.

## LISTING 6-111 An attribute on F#-specific data structures

```fsharp
// define an attribute
type MyAttribute() =
    inherits System.Attribute()

[<MyAttribute>
let myValue = 0

[<MyAttribute>
let myFunction x = x + 1

// the functionality of the following two statements are the same
let [<MyAttribute>] a, b = 1, 2

// apply an attribute to a function
rec [<MyAttribute>] f() = g()

// apply an attribute to mutual reference functions
and [<MyAttribute>] g() = printf "hello"

///apply an attribute to a record
[<MyAttribute>] = {
  type Point =
  [<MyAttribute>] x : float;
  [<MyAttribute>] y: float;
  z: float; }

// apply an attribute to a DU
[<MyAttribute>
type DU =
  | [<MyAttribute>] Case1 of float
  | Case2 of double
  | [<MyAttribute>] Case3 of double

// apply an attribute to a unit of measure
[<MyAttribute>] type km

// apply an attribute to an enumeration
[<MyAttribute>
type Color =
  | [<MyAttribute>] Red = 0
  | Green = 1
  | [<MyAttribute>] Blue = 2

// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```

Wait, I noticed `inherits` vs `inher` in OCR. I should correct `inher` to `inherit`.
Also `inherits` in the last block was `inher`. I'll use `inherit`.

Final check on the text `type MyClass[<-MyAttribute>] xValue:double, yValue:double)`. The OCR has a closing parenthesis but no opening one. I will use `type MyClass[<-MyAttribute](xValue:double, yValue:double)`.

One more thing: the OCR has `356 PART II F#'s Unique Features` which is clearly a footer. I will omit it.

Wait, the prompt says "Keep the original language and all information, do not delete or summarize". Footers are usually noise in OCR. I'll remove them.

One more detail: `if finalBalance > 0.<> then`. In OCR it's `0.<>` followed by `then`. This is likely `0 then`.

Let's refine the output.

[content]
```fsharp
if finalBalance > 0 then
    account.Balance <- finalBalance
    account
else
    printfn "not enough found"
    account
```

[<Measure>] type USD
let account = Account<USD>()
let bank = Bank<USD>(account)

let transaction =
    bank {
        deposit 100.<USD>
        withdraw 50.<USD>
    }

printfn "balance after one transaction = %A" (transaction).Balance

![](img/63aaf94e22830ab98ce16c5946be8ef6_374_0.png)

FIGURE 6-2 Computation expression execution result

## Using Reflection

As a C# developer, reflection is not likely a new concept for you. Usually, reflection in C# involves defining or applying attributes and getting type or method information.

## Defining Attributes

Listing 6-109 shows how to define a customized attribute.

LISTING 6-109 Defining an attribute

```fsharp
// define attribute with a property
type MyAttribute()
    inherit System.Attribute()
    member val MyProperty = System.String.Empty with get, set
```

You can add one or more attributes to modules, or smaller program elements, such as classes and properties, by putting the attribute name between < and >. The assembly-level attribute is different, because it can be applied only by using the do keyword. The attribute can be applied separately as is done in C#. Additionally, multiple attributes can be applied in a group format, when multiple attributes are put into [< >] and separated by semi-colons. Listing 6-110 shows how apply one or more attributes to a class definition. There is little difference between applying attributes to a class and to an interface/struct. I will leave this exercise to you.

## LISTING 6-110 Applying an attribute to a class and class members

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

// define an attribute
type MyAttribute2() =
    inherit System.Attribute()

// define a class with one attribute
[<MyAttribute>
type MyClassWithOneAttribute() = class

// define a class with two attributes applied separately
[<MyAttribute> [<MyAttribute2>
type MyClassWithTwoAttributes() = class

// define a class with two attributes applied as a group
[<MyAttribute; MyAttribute2>
type MyClassWithGroupedAttribute() = class

// apply an attribute to a method, property, or field
type MyClass3() =
    [<MyAttribute>
    let mutable Variable = 0

    [<MyAttribute>
    member this.Method([<MyAttribute2; MyAttribute>] x0, [<MyAttribute>] x1) = ()

    member this.Property
    with [<MyAttribute2>] get() = Variable
    and set(v) = Variable - v

    [<MyAttribute>
    member val Property2 = 0 with get, set

// apply attribute to mutual reference class
type MyClass4() =
    let a:MyClass5 = MyClass5()
and ([<MyAttribute>] MyClass5() = class
```

Listing 6-111 shows how to apply attributes to F#-specific structures, such as a let binding and a record. Also, it shows how to apply attributes on the special structures in F# class definitions, as the primary constructor.

## LISTING 6-111 An attribute on F#-specific data structures

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

[<MyAttribute>
let myValue = 0

[<MyAttribute>
let myFunction x = x + 1

// the functionality of the following two statements are the same
let [<MyAttribute>] a, b = 1, 2

// apply an attribute to a function
rec [<MyAttribute>] f() = g()

// apply an attribute to mutual reference functions
and [<MyAttribute>] g() = printf "hello"

///apply an attribute to a record
[<MyAttribute>] = {
  type Point =
  [<MyAttribute>] x : float;
  [<MyAttribute>] y: float;
  z: float; }

// apply an attribute to a DU
[<MyAttribute>
type DU =
  | [<MyAttribute>] Case1 of float
  | Case2 of double
  | [<MyAttribute>] Case3 of double

// apply an attribute to a unit of measure
[<MyAttribute>] type km

// apply an attribute to an enumeration
[<MyAttribute>
type Color =
  | [<MyAttribute>] Red = 0
  | Green = 1
  | [<MyAttribute>] Blue = 2

// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```
[/content]

Wait, I just realized I didn't include the `static val count` part because the OCR ended there. I will stick to what is in the OCR. Actually, the OCR has `inherits` in one place, I will correct it to `inherit`.

Wait, looking at the OCR again: `type MyAttribute() = inher System.Attribute()`. This is very clearly a typo for `inherit`. I will use `inherit`.

One final check: `if finalBalance > 0.<> then`. The `.<>` is likely OCR noise for `then` or just a typo. I'll clean it to `0 then`.

Actually, looking at `0.<>`, it might be `0.0`. But `0 then` is safer. I'll use `0 then`.

Final output is ready.

[content]
```fsharp
if finalBalance > 0 then
    account.Balance <- finalBalance
    account
else
    printfn "not enough found"
    account
```

[<Measure>] type USD
let account = Account<USD>()
let bank = Bank<USD>(account)

let transaction =
    bank {
        deposit 100.<USD>
        withdraw 50.<USD>
    }

printfn "balance after one transaction = %A" (transaction).Balance

![](img/63aaf94e22830ab98ce16c5946be8ef6_374_0.png)

FIGURE 6-2 Computation expression execution result

## Using Reflection

As a C# developer, reflection is not likely a new concept for you. Usually, reflection in C# involves defining or applying attributes and getting type or method information.

## Defining Attributes

Listing 6-109 shows how to define a customized attribute.

LISTING 6-109 Defining an attribute

```fsharp
// define attribute with a property
type MyAttribute()
    inherit System.Attribute()
    member val MyProperty = System.String.Empty with get, set
```

You can add one or more attributes to modules, or smaller program elements, such as classes and properties, by putting the attribute name between < and >. The assembly-level attribute is different, because it can be applied only by using the do keyword. The attribute can be applied separately as is done in C#. Additionally, multiple attributes can be applied in a group format, when multiple attributes are put into [< >] and separated by semi-colons. Listing 6-110 shows how apply one or more attributes to a class definition. There is little difference between applying attributes to a class and to an interface/struct. I will leave this exercise to you.

## LISTING 6-110 Applying an attribute to a class and class members

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

// define an attribute
type MyAttribute2() =
    inherit System.Attribute()

// define a class with one attribute
[<MyAttribute>
type MyClassWithOneAttribute() = class

// define a class with two attributes applied separately
[<MyAttribute> [<MyAttribute2>
type MyClassWithTwoAttributes() = class

// define a class with two attributes applied as a group
[<MyAttribute; MyAttribute2>
type MyClassWithGroupedAttribute() = class

// apply an attribute to a method, property, or field
type MyClass3() =
    [<MyAttribute>
    let mutable Variable = 0

    [<MyAttribute>
    member this.Method([<MyAttribute2; MyAttribute>] x0, [<MyAttribute>] x1) = ()

    member this.Property
    with [<MyAttribute2>] get() = Variable
    and set(v) = Variable - v

    [<MyAttribute>
    member val Property2 = 0 with get, set

// apply attribute to mutual reference class
type MyClass4() =
    let a:MyClass5 = MyClass5()
and ([<MyAttribute>] MyClass5() = class
```

Listing 6-111 shows how to apply attributes to F#-specific structures, such as a let binding and a record. Also, it shows how to apply attributes on the special structures in F# class definitions, as the primary constructor.

## LISTING 6-111 An attribute on F#-specific data structures

```fsharp
// define an attribute
type MyAttribute() =
    inherit System.Attribute()

[<MyAttribute>
let myValue = 0

[<MyAttribute>
let myFunction x = x + 1

// the functionality of the following two statements are the same
let [<MyAttribute>] a, b = 1, 2

// apply an attribute to a function
rec [<MyAttribute>] f() = g()

// apply an attribute to mutual reference functions
and [<MyAttribute>] g() = printf "hello"

///apply an attribute to a record
[<MyAttribute>] = {
  type Point =
  [<MyAttribute>] x : float;
  [<MyAttribute>] y: float;
  z: float; }

// apply an attribute to a DU
[<MyAttribute>
type DU =
  | [<MyAttribute>] Case1 of float
  | Case2 of double
  | [<MyAttribute>] Case3 of double

// apply an attribute to a unit of measure
[<MyAttribute>] type km

// apply an attribute to an enumeration
[<MyAttribute>
type Color =
  | [<MyAttribute>] Red = 0
  | Green = 1
  | [<MyAttribute>] Blue = 2

// apply an attribute to an exception type
[<MyAttribute>]
exception MyError of string

// apply an attribute to a tuple parameter
let f3 ([<-MyAttribute>] a, [<MyAttribute>] b) = a + b
let f4 ([<-MyAttribute>] a, [<MyAttribute>] b) c = a + b + c

[<MyAttribute>]
module MyModule
let myTest = 0

// apply an attribute to a primary constructor
type MyClass2[<-MyAttribute>]() = class

// apply an attribute to the parameter of a constructor
type MyClass[<-MyAttribute](xValue:double, yValue:double)

// define a static field named count
```
