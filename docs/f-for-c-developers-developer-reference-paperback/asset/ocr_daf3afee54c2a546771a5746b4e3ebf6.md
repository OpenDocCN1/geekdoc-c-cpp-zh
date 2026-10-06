In addition to the mutable-variable restriction, there is another restriction for computation
expressions. It is invalid to use base in the computation expression. (See Listing 6-95.) The workaround
isimple, just use this.

LISTING 6-95 Using this in a seq computation expression

```
type BaseClass() =
  member val X = 0 with get,

type ClassA() =
  inherit BaseClass()
  member this.F() =
    let r = seq {
      let a = 0

      // use base here to generate a compile error
      let b = this.X //base.X
      yield a
    }
```

Expanding a .NET language seems like an exciting possibility. OK, let's do it now. The first sample
is a bank system where the decimal number is rounded when calculating a customer's interest, as
shown in Listing 6-96.

LISTING 6-96 Rounding computation expression

```
// define a rounded computation expression
type RoundComputationBuilder(digits:int) =
  let round(x:decimal) = System.Math.Round(x, digits)
  member this.Bind(result, restComputation ) =
    restComputation(round result)
  member this.Return x = round x

// calculate the bank interests
let bankInterest = RoundComputationBuilder
bankInterest {
  let! x = 23231.34m * 0.002m
  return x
}
```

The RoundComputationBuilder defines two special methods: Bind and Return. These two methods
correspond to let! and return if you debug inside the code. Table 6-2 shows a full list of method names
and corresponding settings. In most cases, the method name suggests its usage.