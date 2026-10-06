
```fsharp
// pizza module that defines all recipes
-[AutoOpen]-
module PizzaModule = {
    let makeNormalDough() = printfn "make normal dough"
    let makePanBakedDough() = printfn "make pan baked dough"
    let makeCrossDough() = printfn "make cross dough"

    let makeHotSauce() = printfn "make hot sauce"
    let makeMildSauce() = printfn "make mild sauce"
    let makeLightSauce() = printfn "make light sauce"

    let makePepperoniTopping() = printfn "make pepperoni topping"
    let makeFiveCheeseTopping() = printfn "make five cheese topping"
    let makeBaconHamTopping() = printfn "make bacon ham topping"
}

// define a pepperoni pizza recipe
let pepperoniPizza = {
    new IPizza = {
        member Name = "Pepperoni Pizza"
        member this.MakeDough() = makeNormalDough()
        member this.MakeSauce() = makeHotSauce()
        member this.MakeTopping() = makePepperoniTopping()
    }
}

// cook takes pizza recipe and makes the pizza
let cook(pizza: IPPizza) =
    printfn "making %s" pizza.Name
    pizza.MakeDough()
    pizza.MakeSauce()
    pizza.MakeTopping()

// cook pepperoni pizza
cook pepperoniPizza
```

Execution result from the builder pattern sample
making pizza Pepperoni Pizza
make normal dough
make hot sauce
make pepperoni topping

The interface and object expression give the program a good structure, but it makes things unnecessarily complicated. The builder pattern requires the actual processing function or functions to be passed in, which is a perfect use of higher-order functions. Listing 3-30 uses a higher-order function to eliminate the interface and object expression.

## LISTING 3-30 Builder pattern implementation using a higher-order function

```fsharp
// pizza module that defines all recipes
<AutoOpen>
module PizzaModule =
  let makeNormalDough() = printf "make normal dough"
  let makePanBakedDough() = printf "make pan baked dough"
  let makeCrossDough() = printf "make cross dough"

  let makeHotSauce() = printf "make hot sauce"
  let makeMildSauce() = printf "make mild sauce"
  let makeLightSauce() = printf "make light sauce"

  let makePepperoniTopping() = printf "make pepperoni topping"
  let makeFiveCheeseTopping() = printf "make five cheese topping"
  let makeBaconHamTopping() = printf "make bacon ham topping"

// cook the recipe and ingredients
let cook pizza recipeSteps =
  printf "making recipe %s" pizza
  recipeSteps
  |> List.iter(fun f -> f())

  [ makeNormalDough; makeMildSauce
  makePepperoniTopping]
  |> cook "pepperoni pizza"
```

## Working with the Façade Pattern

The façade pattern provides a higher-level interface that makes invoking an underlying class library easier, readable, or both. Listing 3-31 shows how to perform an employment background check.

## LISTING 3-31 Example of a façade pattern

```fsharp
// define Applicant record
type Applicant = { Name : string }

// library to perform various checks
<AutoOpen>
module SubOperationModule =
  let checkCriminalRecord(applicant) =
    printf "checking %s criminal record..." applicant.Name
    true

  let checkPastEmployment(applicant) =
    printf "checking %s past employment..." applicant.Name
    true

  let securityClearance(applicant, securityLevel) =
    printf "security clearance for %s..." applicant.Name
    true
```

```fsharp
// façade function to perform the background check
let isBackgroundCheckPassed(applicant, securityLevel) =
  checkCriminalRecord applicant
  && checkPastEmployment applicant
  && securityClearance(applicant, securityLevel)

// create an applicant
let jenny = { Name = "Jenny" }

// print out background check result
if isBackgroundCheckPassed(jenny, 2) then printf("%s passed background check", jenny.Name)
else printf("%s failed background check", jenny.Name)
```

Execution result from the façade pattern sample
checking Jenny criminal record...
checking Jenny past employment...
security clearance for Jenny ...
Jenny passed background check

## Working with the Memento Pattern

The memento pattern saves an object's internal state so that it can be used later. In Listing 3-32, the particle class saves its location information and later restores information back to the saved location. If the state data is relatively small, a list store can easily turn the memento pattern into a redo-undo framework.

**LISTING 3-32** Example of the memento pattern

```fsharp
// define location record
type Location = { X : float; Y : float }

// define a particle class with a location property
type Particle() =
    let mutable loc = { X = 0.; Y = 0. }
    member this.Loc
        with get() = loc
        and private set v = loc <- v
    member this.GetMemento = this.Loc
    member this.Restore = loc <- v
    member this.MoveXY(newX, newY) = loc <- { X = newX; Y = newY }
```

```fsharp
// create a particle
let particle = Particle()
```

```fsharp
// save current state
let currentState = particle.GetMemento
printf "current state: %A" currentState

// move particle to new location
particle.MoveXY(2, 3)
printf "new location: %A" particle.Loc

// restore particle to previous state
particle.Restore(currentState)
printf "restored location: %A" particle.Loc
```

## Writing Design Patterns: Additional Notes

As mentioned in the beginning of this chapter, design patterns have been criticized since their birth. Many functional programmers believe that design patterns are unnecessary. However, when a program becomes large, a tested approach is needed. 

Both functional programming and object-oriented programming have their own way of reusing the code. Object-oriented programming uses inheritance, while functional programming uses higher order functions. Both approaches have loyal followers, and you might already be convinced that one is superior to the other. I say that both approaches have their own advantages under certain circumstances. Unfortunately, neither is a silver bullet that can solve all problems. Using the right tool for the right job is the key. F#, which supports both OO and functional programming, provides both approaches, and gives the developer to use the best way to perform the system design.

Functional programming can still have a structure to encapsulate logic into a unit. Functions that can be treated like data, be encapsulated in a class or inside a closure, and more importantly, the application of object expressions provides an even simpler way to organize the code. Listing 3-33 shows different ways to encapsulate the data.

## LISTING 3-33 Data encapsulation

```fsharp
Object expression

let obj = 
    let ctor = printf "constructor code"
    let field = ref 8
    new IA with
        member this.F() = printf "%A" !field
        interface System.IDisposable with
        member this.Dispose() = ()
```
