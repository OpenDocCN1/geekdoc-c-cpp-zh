ML determines the type of this list to be **int list**. ML’s strong typing dictates that lists may only contain elements that all have the same type. Here is an example structure that violates this restriction by mixing types of elements in a list:

```
```text
> [1,2,3.1];
Error: operator and operand don't agree [literal]
   operator domain: int * int list
   operand:        int * real list
   in expression:
      2 :: 3.1 :: nil
```
```

If we want to mix data of different types, we must use a **tuple**:

```
```text
> (1,2,3.1);
val it = (1,2,3.1) : int * int * real
```
```

The error message generated in the earlier example also gives us a hint as to how ML constructs lists, which is similar to the way Scheme constructs lists. That is, the operator `::` corresponds to cons in Scheme, and constructs a list out of an element (which becomes the head of the list) and a previously constructed list (which becomes the tail of the list). For example:

```
```text
> op :: ;
val it = fn : 'a * 'a list -> 'a list
> 2 :: [3,4];
val it = [2,3,4] : int list
```
```

Note that the type of the `::` operator contains a **type variable** `'a`, because `::` can be applied to a list containing values of any type. Thus, `::` is a function from any type `'a` and any list of the same type `'a` to a list of the same type `'a`.

In ML, every list is constructed by a series of applications of the `::` operator:

```
```text
> 1 :: 2 :: 3 :: [];
val it = [1,2,3] : int list
```
```

Here `[]` is the empty list, which can also be written as the keyword **nil**.

ML has operations corresponding to Scheme’s car and cdr operators as well, except that they are called **hd** and **tl** (for **head** and **tail**). For example:

```
```text
> hd [1,2,3];
val it = 1 : int
> tl [1,2,3];
val it = [2,3] : int list
```
```