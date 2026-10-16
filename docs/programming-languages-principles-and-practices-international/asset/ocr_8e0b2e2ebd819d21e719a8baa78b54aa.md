Some languages allow only functions (that is, all procedures must return values). Functional languages in particular have this property; see Chapter 3.

Procedure and function declarations can be written in a form similar to constant declarations, using an equal sign, as in the following ML function declaration for a swap procedure:³

```
(* ML code *)
fun swap (x,y) =
  let val t = !x
  in
    x := !y;
    y := t
  end;
```

The use of an equal sign to declare procedures is justified, because a procedure declaration gives the procedure name a meaning that remains constant during the execution of the program. We could say that a procedure declaration creates a constant procedure value and associates a symbolic name—the name of the procedure—with that value.

A procedure communicates with the rest of the program through its parameters and also through nonlocal references, that is, references to variables declared outside of its own body. The scope rules that establish the meanings of nonlocal references were introduced in Chapter 7.

# 10.2 Procedure Semantics

From the point of view of semantics, a procedure is a block whose declaration is separated from its execution. In Chapter 7, we saw examples of blocks in C and Ada that are not procedure blocks; these blocks are always executed immediately when they are encountered. For example, in C, blocks A and B in the following code are executed as they are encountered:

```
A:
{ int x,y;
  ...
  x = y * 10;
  B:
  { int i;
    i = x / 2;
    ...
  } /* end B */
} /* end A */
```

In Chapter 7, you saw that the environment determines the allocation of memory and maintains the meaning of names during execution. In a block-structured language, when a block is encountered during execution, it causes the allocation of local variables and other objects corresponding to the declarations

> ³This procedure in ML has type 'a ref * 'a ref -> unit and is polymorphic; see Chapter 9. Note that its return type is unit, which is the equivalent of the C void type.