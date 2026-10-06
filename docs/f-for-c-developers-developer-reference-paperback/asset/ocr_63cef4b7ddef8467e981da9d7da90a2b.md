> Note As mentioned in the previous note, a unit of measure is a compile-time feature that cannot be accessed at runtime. Any attempt to access the unit at runtime will not work. ToString() cannot print out any unit information.

A unit of measure can have static members, as shown in Listing 6-19.

# LISTING 6-19 Adding static members to unit-of-measure types

```
<<Measure>
type m =
    static member C = 3.28<foot/m>
    static member FromFoot(x:float<foot>) = x / m.C
    static member ToFoot(x:float<m>) = x * m.C

and [<Measure]> foot =
    static member FromMeter = m.ToFoot
    static member ToMeter = m.FromFoot

m.FromFoot(3.28<foot>)
```

```
Execution result
val it : float<m> = 1.0
```

A unit of measure is defined as a type, so it can be used in generic functions. Listing 6-20 defines a generic unit function that can add any two numbers. The function makes that numbers with different units of measure cannot be processed together. The execution result is result1 = 10.0, result2 = 5.0.

# LISTING 6-20 A generic function using a unit of measure

```
// define units of measure
[<Measure>] type lb
[<Measure>] type inch

// generic function
let add (x : float<u>) (y : float<u>) = x + y * 2.

let result1 = add 4.<lb> 3.<lb>
let result2 = add 1.<inch> 2.<inch>

printf "result1 = %A, result2 = %A" result1 result2
```