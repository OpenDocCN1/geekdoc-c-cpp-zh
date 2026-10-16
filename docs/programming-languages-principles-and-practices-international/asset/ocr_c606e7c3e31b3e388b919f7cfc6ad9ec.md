The main reason for this is that the ML language has no explicit or implicit separate compilation mechanism (or other code aggregation mechanism), so there is no way to externally specify an implementation choice.[^8]

# 11.6 Modules in Earlier Languages

Historically, modules and abstract data type mechanisms began with Simula67 and made significant progress in the 1970s through language design experiments at universities and research centers. Among the languages that have contributed significantly to module mechanisms in Ada, ML, and other languages, are the languages CLU, Euclid, Modula-2, Mesa, and Cedar. To indicate how module mechanisms have developed, we sketch briefly the approaches taken by Euclid, CLU, and Modula-2.

# 11.6.1 Euclid

In the Euclid programming language, modules are types, so a complex number module is declared as a type:

```
type ComplexNumbers = module
    exports(Complex, add, subtract, multiply,
            divide, negate, makeComplex,
            realPart, imaginaryPart)
    type Complex = record
        var re, im: real
    end Complex

    procedure add (x,y: Complex, var z: Complex) =
    begin
        z.re := x.re + y.re
        z.im := x.im + y.im
    end add

    procedure makeComplex
            (x,y: real, var z:Complex) =
    begin
        z.re := x
        z.im := y
    end makeComplex
            ...
end ComplexNumbers
```

To be able to declare complex numbers, however, we need an actual object of type ComplexNumbers—a module type in itself does not exist as an object. Thus, we must declare:

```
var C: ComplexNumbers
```