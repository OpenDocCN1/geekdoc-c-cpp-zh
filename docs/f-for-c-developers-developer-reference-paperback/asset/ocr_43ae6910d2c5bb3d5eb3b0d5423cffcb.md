```
module Print
// general print function
let print x = printf("%A") x

// auto open NumberPrint
[-AutoOpen]
module NumberPrint =
    // function to print int
    let printInt = printf("%d")

    // function to print float
    let printFloat = printf("%f")

module StringPrint =
    // function to print string
    let printString = printf("%s")

    // function to print char
    let printChar = printf("%c")

// invoke print functions
printFloat 4.5
printInt 2

// use module name to reference the function defined in the module
StringPrint.printChar 'c'
StringPrint.printString "abc"

// open StringPrint module
open StringPrint
printChar 'c'
printString "abc"
```

> Note The open statement must be located somewhere after the module is defined.

The RequireQualifiedAccess attribute indicates that a reference to an element in that module must specify the module name. Listing 1-91 shows how to decorate the attribute on a module and reference a function within.