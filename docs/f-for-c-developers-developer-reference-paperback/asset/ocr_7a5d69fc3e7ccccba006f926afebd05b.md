Add this attribute to a type or module to make it apply recursively to all the values
in the module or all the members of the type.

Listing 9-18 shows how to show the quotation expression for the function. The <@ @@ is used
to get the quotation from a function that is decorated with the ReflectedDefinition attribute.

# LISTING 9-18 Getting a quotation from a function with the ReflectedDefinition attribute

```
[<ReflectedDefinition>]
let f()
let b = 99
b*2

<@@ f @@>

Execution result
val f : unit -> int
val it : Quotations.Expr = Lambda (arg00, Call (None, f, []))
```

There are several approaches to converting F# code to CUDA. Figure 9-6 shows one of these
aches. The PTX file is an assembly-like language for the GPU. In this chapter, the path from
quotation via C to PTX file is chosen.

![](bbox=[0.125, 0.517, 0.65, 0.77])

FIGURE 9-6 Converting code from F# to GPU code

After the quotation is ready, a translation function can be applied. Listing 9-20 shows how to
tverse the tree structure and the CUDA C code. There are several ways to generate code from
a quotation tree. Listing 9-20 generates C code, which can make the quotation generation easy
to understand; the listing traverses the parse tree structure emitting C code. To support the
generation, CUDAAPointer2 is defined, as shown in Listing 9-19.