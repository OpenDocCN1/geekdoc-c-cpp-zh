```
override def toString = "<"+x+", "+y+", "+z+">"
}
```

The first version of `apply` lets you index into the different coordinates. It is written using a match expression though there are certainly other ways it could be done. The second version of `apply` is more unusual. It allows you get the x, y, and z values back as a sequence by passing in a sequence of indexes.$^{2}$

With this code written, we can instantiate objects of the `Vect` type and perform the specified operations on them.

```
scala> val v1=new Vect(1,2,3)
v1: Vect = <1.0, 2.0, 3.0>
```

```
scala> val v2=new Vect(2,-4,7)
v2: Vect = <2.0, -4.0, 7.0>
```

```
scala> val v3=v1+v2
v3: Vect = <3.0, -2.0, 10.0>
```

```
scala> val v4=v3*8
v4: Vect = <24.0, -16.0, 80.0>
```

Note that with the code that we have here, we have to put the scalar on the right of the multiply. If you tried to do `8*v3` you would get an error. This is because Scala sees that as `(8).* (v3)`. The value 8 is an `Int`, it does not have a version of `*` that works on a `Vect`. It is possible to get around this, but it requires another more advanced concept called an implicit conversion which we do not want to consider at this time. For now we will be happy putting the scalar on the right.

There are two other common operations on 3-vectors: the dot product and the cross product. The dot product returns a scalar and the cross product returns a vector. When writing these, we have to make a significant decision, do we want them to be symbolic or words? We can not use just `*` for both because Scala could not figure out which one we meant to use at any given time. For that matter, people reading the code probably could not either. Scala does give us the ability to use longer symbol names with multiple operator symbols. So maybe `**` for a dot product and `**` for a cross product. You can not use `*.*` and `*x*` because `.` and `x` are not operator characters. The choice of `+` and `-` in these comes from knowledge of the formulas for dot and cross products, but neither really fits well or will read to most people as dot and cross. For that reason, we will stick with normal alphabetic method names.

```
def dot(v:Vect):Double = x*v.x+y*v.y+z*v.z
def cross(v:Vect):Vect =
    new Vect(y*v.z-z*v.y, z*v.x-x*v.z, x*v.y-y*v.x)
```

We can still use these in operator notation. The only problem is that characters have lower precedence than multiplication would so parentheses will have to be used to enforce order of operation.

There is no `update` method provided because these are immutable. You could, in theory, make them mutable and provide an `update`. You would probably also want to provide `+=`, `-=`, `**=`, and `/=` operators that mutate instead of making a new copy. Doing so is left as an exercise for the reader.

$^{2}$This type of indexing is a standard operation in $\mathrm{MATLAB}^{\circled{R}}$ where dealing with arrays and matrices is the primary usage of the language.