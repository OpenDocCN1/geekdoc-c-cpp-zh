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
        member this.Model = "525i" )
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