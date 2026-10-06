> Note To avoid odd compile errors, make sure First and Last are aligned correctly. highly recommend installing and using the F# depth colorizer to assist with this.

The record fields can be mutable if they are decorated with the mutable keyword. Also, records can define member functions or properties to extend their functionality. See Listing 6-25.

# LISTING 6-25 A record with a mutable field and members

```
type Car =
  Make : string
  Model : string
  mutable Odometer : int
  member this.drive(mile)
    printf "you drove another %d mile"
    this.Odometer <- this + mile
    this.CurrentMileage = get() = this.Odometer
```

```
let myCar = Make = "Plymouth", Model = "Neon", Odometer = 100892
myCar.Drive(20)
printf "current mileage = %d" myCar.CurrentMileage
```

Example result
you drove another 20 miles
current mileage = 100912

> Note F# uses space indents to distinguish between language elements. If the member keyword in the record definition is not aligned correctly, you will get a compile error.

The record does not support default values on its fields. However, you can declare a static member with a default value and mutate its value using the with keyword. Listing 6-26 shows how to do this.

# LISTING 6-26 Using a static member as a base template record

```
// define a Point2D record with originalPoint = (0,0)
type Point2D =
  { x : float; y : float }
  static member OriginalPoint =
    { x = 0.; y = 0.}
```