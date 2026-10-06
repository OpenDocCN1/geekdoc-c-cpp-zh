multiple attributes are put into [< >] and separated by semi-colons. Listing 6-110 shows how apply one or more attributes to a class definition. There is little difference between applying attributes to a class and to an interface/struct. I will leave this exercise to you.

# LISTING 6-110 Applying an attribute to a class and class members

```
// define an attribute
type MyAttribute() =
inherit System.Attribute())

// define an attribute
type MyAttribute2() =
inherit System.Attribute()

// define a class with one attribute
[<MyAttribute>
type MyClassWithOneAttribute() = class

end

// define a class with two attributes applied separately
[<MyAttribute> [<MyAttribute2>
type MyClassWithTwoAttributes() = class

end

// define a class with two attributes applied as a group
[<MyAttribute; MyAttribute2>
type MyClassWithGroupedAttribute() = class

end

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

end
```

356 PART II F#'s Unique Features