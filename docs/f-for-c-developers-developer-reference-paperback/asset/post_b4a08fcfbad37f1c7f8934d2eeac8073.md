
```fsharp
// function to check that the age is between 18 and 65
let validAge =
  record.Age < 65 && record.Age > 18
```

```fsharp
// function to check that the weight is less than 200
let validWeight =
  record.Weight < 200.
```

```fsharp
// function to check that the height is greater than 120
let validHeight =
  record.Height > 120.
```

```fsharp
// function to perform the check according to parameter f
let f (record, result) =
  if not return result then
    false
  else
    record, f(record)
```

```fsharp
// create chain function
let chainOfResponsibility = check validAge >> check validWeight >> check validHeight
```

```fsharp
// define two patients' records
let john = { Name = "John"; Age = 80; Weight = 180; Height = 180. }
let dan = { Name = "Dan"; Age = 20; Weight = 160; Height = 190. }
```

```fsharp
printf "John's result = %s" (chainOfResponsibility(john, true) | snd)
printf "Dan's result = %b" (chainOfResponsibility(dan, true) | snd)
```

Execution result from the chain of responsibility sample

John's result = false
Dan's result = true

> Note: You have to execute the chainOfResponsibility function to get the result shown.

In the implementation in Listing 3-2, three functions (responsibilities) are composed into a chain and the data is passed along the chain when it is being processed. The parameter contains a Boolean variable that decides whether the data can be processed. In Listing 3-2, all the functions are effective AND-ed together. The parameter passed into the first function contains a Boolean value. The successive function can be invoked only if the Boolean value is true.

The other implementation is used for pipelining, as shown in Listing 3-3, rather than function composition. The chainTemplate higher-order function takes a process and canContinue function. The canContinue function always returns true, and the process function is a simple "increase" function. The execution result is 2.

## LISTING 3-3 Chain of responsibility sample using pipelining

```fsharp
// chain template function
let chainTemplate s processFunction canContinue s =
  if canContinue s then
    processFunction s
  else s

let canContinueF _ = true
let processF x = x + 1

// combine two functions to get a chainFunction
let chainFunction = chainTemplate processF canContinue

// use pipeline to form a chain
let s = 1 |> chainFunction

printf("%A") s
```

The other chain of responsibility implementation uses the partial pattern feature in F#. I introduced the unit of measure to make the code readable; the code goes from the first case and stops when the condition is met. The sample code is listed in Listing 3-2. The sample code checks the height and weight value for some predefined criteria. The person's data is checked against NotPassHeight and then NotPassWeight if his height passes the validation criteria. The code also demonstrates how to use the F# unit-of-measure feature, which avoids possible confusion because the unit is used. The parameter for makeCheck is #Person, which means that any object of type Person or derived from a Person type can be passed.

Listing 3-4 uses units-of-measure language constructs within a calculation. Only the number with the same unit of measure can be involved in the same calculation. Listing 3-4 shows how to define a kilogram (kg) and decorate it with a number.

## LISTING 3-4 Defining-of-measure using a kg unit of measure

```fsharp
// define unit-of-measure kg
[Measure]> type kg

// define 1kg and 2kg variables
let oneKilo = 1<kg>
let twoKilo = 2<kg>
```

The None and Some(person) syntax in the sample code in Listing 3-6 represents a Nullable-type-like data structure called an option. You can think of None as NULL. The special function `let (| NotPassHeight | _)` is called an active pattern. It takes a person parameter and decides whether the person meets criteria. If the person meets the criteria, the function returns Some(person) and triggers the match statement. Listing 3-5 shows how to use Some() syntax to check for an odd number. This sample introduced several new concepts. I will come back to these details in Chapter 5.

## LISTING 3-5 Using active pattern, option, and match to check for an odd number

```fsharp
// define an active pattern function to check for an odd number
let (| Odd | _ ) x = if x % 2 = 0 then None else Some(x)

// define a function to check for an odd number
let findOdd x =
  match x with
  | Odd x -> printf("x is odd number")
  | _ -> printf("x is not odd number")

// check odd number
findOdd 3
findOdd 4
```

Execution result
x is odd number
x is not odd number

## LISTING 3-6 Chain of responsibility pattern using partial pattern matching

```fsharp
// define two units of measure: cm and kg
<Measure> type cm
<Measure> type kg

// define a person class with its height and weight to 0cm and 0kg
type Person() =
  member val Height = 0.<cm> with get, set
  member val Weight = 0.<kg> with get, set

// define a higher order function that takes a person record as a parameter
let makeCheckingcriterion (person: #Person) =
  if ifPassingCriterion then None //if passing, say nothing, just let it
  else Some(person) //if not passing, return Some(person)

// define NotPassHeight when the height does not meet 170cm
let (| NotPassHeight | _ ) person = makeCheck (fun p -> p.Height > 170.<cm>) person

// define the NotPassWeight when weight does not fall into 100kg and 50kg range
let (| NotPassWeight | _ ) person =
  makeCheck (fun p -> p.Weight < 100.<kg> && p.Weight > 50.<kg>) person

// check incoming x
let check x =
  match x with
  | NotPassHeight x -> printf("this person is not tall enough")
  | NotPassWeight x -> printf("this person is out of weight range")
  | _ -> printf("good, this person passes")
```

* CHAPTER 3 F# and Design Patterns

```fsharp
// create a person with 180cm and 75kg
let p = Person(Height = 180.<cm>, Weight = 75.<kg>)

// perform the check
check p
```

Execution result
good, this person passes

## Working with Adapter Pattern

The adapter pattern is a design pattern that translates one interface into an interface that is compatible. In Listing 3-7, we use generic invoke to invoke incompatible types. (Note that F# you declare as inline as in the following code)

+   LISTING 3-7 GI function

```fsharp
// define a GI function
let inline canConnect (x : ^AT) = (^AT : member CanConnect : unit->bool) x
```

## LISTING 3-8 The adapter pattern (bridge pattern)

```fsharp
// define a cat class
type Cat() = =
    member this.Walk() = printf "cat walks"

// define a dog class
type Dog() = =
    member this.Walk() = printf "dog walks"

// adapter pattern
let adapterExample() =
    let cat = Cat()
    let dog = Dog()

// define the GI function to invoke the Walk function
let inline walk(x : ^AT) = (^AT: (member Walk : unit->unit) x

// invoke GI and both Cat and Dog
walk(cat)
walk(dog)
```

Execution result from adapter pattern
cat walks
dog walks

The interesting about this design implementation in Listing 3-8 is that Cat and Dog do not share any base class. However they can still be processed in a unified function. (You should note, by the way, this is a sloppy way of solving the problem and should be considered only when no other option is available.)

Imagine that you have two legacy systems that need to be integrated and that you do not have access to the source code. It would be difficult to integrate the systems in other languages, but it's possible and even easy in F# using the generic invoke technique.
