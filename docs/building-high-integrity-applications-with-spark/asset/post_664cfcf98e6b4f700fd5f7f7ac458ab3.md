
```ada
(for all J in Items'Range =>
    (for all K in J + 1 .. Items'Last => Items(J) <= Items(K)));
end Searchers;
```

The precondition uses two nested for-all quantified expressions to assert that each item of the array comes before (or is the same as) all the items that follow it. The SPARK tools will, as usual, create a verification condition at each place where `Binary_Search` is called to prove that the precondition is satisfied.

It bears repeating that assertions in Ada are executable. With that in mind, notice that the precondition given for `Binary_Search` runs in `$O(n^2)$` time. In contrast, the binary search algorithm itself runs in only `$O(\log n)$` time.

An alternative way of expressing that the array is sorted is

```ada
Pre => (for all J in Items'First .. Items'Last - 1 =>
            Items (J) <= Items (J+1))
```

This has the advantage of running in only `$O(n)$` time, and it might also be considered clearer. However, it is still asymptotically slower than the algorithm to which it is attached. Because assertions can use quantified expressions over large arrays, and even call recursive functions, they can consume large amounts of space and time. Expressive assertions thus have the potential to render unusable a program that would otherwise have acceptable performance characteristics. We discuss this issue further in Section 6.8.

### 6.2.2 *Postconditions*

A *postcondition* is a condition that is asserted to be true when a subprogram completes its actions and returns control to the caller. It describes the effects of the subprogram. Postconditions are, thus, formal statements derived from the functional requirements that our program must meet.

Postconditions are introduced with the `Post` aspect. As an example, consider the `Searchers` package again. A version of that package follows, where the `Binary_Search` procedure has been given a postcondition:

```ada
package Searchers2
   with SPARK_Mode => On
is
   subtype Index_Type is Positive range 1 .. 100;
   type Array_Type is array (Index_Type) of Integer;

   procedure Binary_Search (Search_Item : in  Integer;
                            Items       : in  Array_Type;
                            Found       : out Boolean;
                            Result      : out Index_Type)
      with
         Pre  => (for all J in Items'Range =>
                     (for all K in J + 1 .. Items'Last => Items(J) <= Items(K))),
         Post => (if Found then Search_Item = Items (Result)
                     else (for all J in Items'Range => Search_Item /= Items(J)));
end Searchers2;
```

The postcondition says that if the procedure reports it has found the search item, then that item exists at the reported position in the array. The else clause says that if the procedure does not find the search item, the item does not exist at any location in the array.

Preconditions and postconditions have a dual relationship. A precondition is an obligation on the caller to show, either by runtime testing or proof, that the condition is true before calling a subprogram. Inside the subprogram the precondition can be used in the hypotheses of verification conditions, being taken as a given in the context of the subprogram's body.

Postconditions, on the other hand, are obligations on the subprogram itself to show that the condition is true when the subprogram returns. The calling context can use the postcondition in the hypotheses of verification conditions that appear past the point of the call.

Callers are interested in weak preconditions that are easy to prove but strong postconditions that provide a lot of information they can use after the call. In contrast, implementers want strong preconditions that provide a lot of information in the subprograms being implemented but weak postconditions that are easy to prove. Both sides of the call want to make as few promises as possible but get as many promises as they can.

Of course in real programs, just as in real life, a balance must be struck. Postconditions describe what it means for a subprogram to be correct and thus would ideally be written as part of the subprogram's design. The more specific (stronger) a postcondition is, the more information about the subprogram's behavior it captures. Preconditions often need to be provided to support the postcondition.

For example, in the case of `Binary_Search`, the implementation has no chance of proving the postcondition unless it "knows" the array is already sorted. The algorithm depends on that. Thus, the precondition is necessary if the postcondition is to be proved.

The `Binary_Search` procedure has only `in` and `out` parameters. In the case of `in out` parameters (or `In_Out` global items), it is sometimes necessary to reference the original value of the parameter (or global item) in the postcondition. As an example, consider a procedure that finds the smallest prime factor of a natural number and returns both the factor and the original number after the factor has been divided out:

```ada
procedure Smallest_Factor (N     : in out Positive;
                           Factor :    out Positive)
   with
      Post => Is_Prime(Factor) and
              (N = N'Old / Factor) and
              (N'Old rem Factor = 0);
```

Here we make use of a function `Is_Prime` that returns true if and only if its argument is a prime number.

The procedure changes the value of `N`. However, we can reference its original value in the postcondition using the `'Old` attribute. This implies that the compiler must maintain a copy of the value of `N` before the procedure is called so it can use that copy when the postcondition is evaluated. Here, `N` is just an integer so keeping a copy of it is not expensive. Yet this is another example of how assertions can potentially consume significant resources; consider the case when the parameter is a large data structure.

In general, we can talk about the *prestate* of a subprogram as the state of the entire program just before the subprogram begins executing. Similarly, we can talk about the *poststate* of a subprogram as the state of the entire program after the subprogram returns. In these terms, the `'Old` attribute can be said to make a copy of a part of the prestate for use in the evaluation of the postcondition.

Care is needed when using `'Old` with arrays. Consider the following four expressions. Here, `A` is an array and `Index` is a variable of the array's index subtype.

- `A'Old(Index)` accesses the original array element at the position given by the current `Index`. Here *original* means part of the prestate, and *current* means the value when the postcondition is executing, that is, part of the poststate.
- `A(Index'Old)` accesses the current array element at the position given by the original `Index`.
- `A'Old(Index'Old)` accesses the original array element at the position given by the original `Index`. Both the original array (in its entirety) and the original `Index` are saved when the subprogram is entered.
- `A(Index)'Old` is largely the same as `A'Old(Index'Old)`. In particular, it refers to the original value of the expression `A(Index)`. However, only the original value of `A(Index)`, not the entire array, is saved when the subprogram is entered.

The last case illustrates a general rule. The prefix of `'Old` can be an arbitrary expression, the value of which is saved when the subprogram is entered. For example, `(X + Y)'Old` in a postcondition causes the original value of the expression `X + Y` to be saved and used when evaluating the postcondition. Each usage of `'Old` in a postcondition implies the creation of a separate saved value. We also note that because the expression used as a prefix to `'Old` is copied, it cannot have a limited type.⁷

The postcondition of `Smallest_Factor` shown earlier does not fully describe the intended behavior of the procedure. It only says that `Factor` is some prime factor of the original value of `N`, but not necessarily the smallest one. Although the postcondition is not as strong as it could be, it still conveys useful information into the calling context. Proving that the postcondition will always be satisfied is a partial proof of the correctness of the procedure. The remaining properties could be explored with testing. We describe the interplay between proof and testing in more detail in Section 8.4.

The postcondition can be strengthened as follows:

```ada
procedure Smallest_Factor (N      : in out Positive;
                           Factor : out Positive)
   with
      Post => (N = N'Old / Factor) and
              (N'Old rem Factor = 0) and
              (for all J in 2 .. Factor - 1 => N'Old rem J /= 0);
```

The additional quantified expression says there are no other factors of the original `N` that are smaller than `Factor`. It is no longer necessary to directly assert that `Factor` is prime because it is a mathematical fact that the smallest factor of a number will always be prime. Notice that now the postcondition relies on a mathematical property that is proved outside the scope of the program. This is an example of the interplay between design and implementation. Although SPARK allows you to formalize the construction of your software, it is not by itself a complete formal design methodology.

Function results are normally anonymous, so to reference them in a postcondition for a function, it is necessary to use the `'Result` attribute. Consider a function version of `Smallest_Factor` that returns the smallest factor of a natural number:

```ada
function Smallest_Factor (N : in Positive) return Positive
   with
      Post => (N rem Smallest_Factor'Result = 0) and
              (for all J in 2 .. Smallest_Factor'Result - 1 => N rem J /= 0);
```
