
## 7.3. ACCESS TO NONLOCAL DATA ON THE STACK

```text
1) fun sort(inputFile, outputFile) =
       let
2)         val a = array(11,0);
3)         fun readArray(inputFile) = ...
4)             ... a ... ;
5)         fun exchange(i,j) =
6)             ... a ... ;
7)         fun quicksort(m,n) =
               let
8)                   val v = ... ;
9)                   fun partition(y,z) =
10)                      ... a ... v ... exchange ...
                      in
11)                      ... a ... v ... partition ... quicksort
                      end
               in
12)          ... a ... readArray ... quicksort ...
       end;
```

Figure 7.10: A version of quicksort, in ML style, using nested functions

(11) suggests that *quicksort* accesses variables *a* and *v*, the function *partition*, and itself recursively.

Line (12) suggests that the outer function *sort* accesses *a* and calls the two procedures *readArray* and *quicksort*.

### 7.3.5 Access Links

A direct implementation of the normal static scope rule for nested functions is obtained by adding a pointer called the *access link* to each activation record. If procedure *p* is nested immediately within procedure *q* in the source code, then the access link in any activation of *p* points to the most recent activation of *q*. Note that the nesting depth of *q* must be exactly one less than the nesting depth of *p*. Access links form a chain from the activation record at the top of the stack to a sequence of activations at progressively lower nesting depths. Along this chain are all the activations whose data and procedures are accessible to the currently executing procedure.

Suppose that the procedure *p* at the top of the stack is at nesting depth *nₚ*, and *p* needs to access *x*, which is an element defined within some procedure *q* that surrounds *p* and has nesting depth *n_q*. Note that *n_q* ≤ *nₚ*, with equality only if *p* and *q* are the same procedure. To find *x*, we start at the activation record for *p* at the top of the stack and follow the access link *nₚ − n_q* times, from activation record to activation record. Finally, we wind up at an activation record for *q*, and it will always be the most recent (highest) activation record for *q* that currently appears on the stack. This activation record contains the element *x* that we want. Since the compiler knows the layout of activation records, *x* will be found at some fixed offset from the position in *q*’s activation record that we can reach by following the last access link.

**Example 7.6:** Figure 7.11 shows a sequence of stacks that might result from execution of the function *sort* of Fig. 7.10. As before, we represent function names by their first letters, and we show some of the data that might appear in the various activation records, as well as the access link for each activation. In Fig. 7.11(a), we see the situation after *sort* has called *readArray* to load input into the array *a* and then called *quicksort(1, 9)* to sort the array. The access link from *quicksort(1, 9)* points to the activation record for *sort*, not because *sort* called *quicksort* but because *sort* is the most closely nested function surrounding *quicksort* in the program of Fig. 7.10.

![](img/2a44b9071782fade81f3050c3b718341_450_0.png)

Figure 7.11: Access links for finding nonlocal data

In successive steps of Fig. 7.11 we see a recursive call to *quicksort(1, 3)*, followed by a call to *partition*, which calls *exchange*. Notice that *quicksort(1, 3)*’s access link points to *sort*, for the same reason that *quicksort(1, 9)*’s does.

In Fig. 7.11(d), the access link for *exchange* bypasses the activation records for *quicksort* and *partition*, since *exchange* is nested immediately within *sort*. That arrangement is fine, since *exchange* needs to access only the array *a*, and the two elements it must swap are indicated by its own parameters *i* and *j*. □

### 7.3.6 Manipulating Access Links

How are access links determined? The simple case occurs when a procedure call is to a particular procedure whose name is given explicitly in the procedure call. The harder case is when the call is to a procedure-parameter; in that case, the particular procedure being called is not known until run time, and the nesting depth of the called procedure may differ in different executions of the call. Thus, let us first consider what should happen when a procedure q calls procedure p, explicitly. There are two cases:

- 1. Procedure *p* is at a higher nesting depth than *q*. Then *p* must be defined immediately within *q*, or the call by *q* would not be at a position that is within the scope of the procedure name *p*. Thus, the nesting depth of *p* is exactly one greater than that of *q*, and the access link from *p* must lead to *q*. It is a simple matter for the calling sequence to include a step that places in the access link for *p* a pointer to the activation record of *q*. Examples include the call of *quicksort* by *sort* to set up Fig. 7.11(a), and the call of *partition* by *quicksort* to create Fig. 7.11(c).
- 2. The nesting depth *nₚ* of *p* is less than or equal to the nesting depth *n_q* of *q*. In order for the call to be within *q* to be in the scope of name *p*, procedure *q* must be nested within some procedure *r*, while *p* is a procedure defined immediately within *r*. The top activation record for *r* can therefore be found by following the chain of access links, starting in the activation record for *q*, for *n_q − nₚ + 1* hops. Then, the access link for *p* must go to this activation of *r*. This case includes recursive calls, where *p = q*. In that case, the chain of access links is followed for one hop, and the access links for *p* and *q* are the same. An example is the call of *quicksort*(1, 3) by *quicksort*(1, 9) to set up Fig. 7.11(b). It also includes the case of mutually recursive calls, where two or more procedures are defined within a common parent.

**Example 7.7:** For an example of case (2), notice how we go from Fig. 7.11(c) to Fig. 7.11(d). The nesting depth 2 of the called function *exchange* is one less than the depth 3 of the calling function *partition*. Thus, we start at the activation record for *partition* and follow 3 − 2 + 1 = 2 access links, which takes us from *partition*’s activation record to that of *quicksort*(1, 3) to that of *sort*. The access link for *exchange* therefore goes to the activation record for *sort*, as we see in Fig. 7.11(d).

An equivalent way to discover this access link is simply to follow access links for *n_q − n_p* hops, and copy the access link found in that record. In our example, we would go one hop to the activation record for *quicksort*(1, 3) and copy its access link to *sort*. Notice that this access link is correct for *exchange*, even though *exchange* is not in the scope of *quicksort*, these being sibling functions nested within *sort*. □

### 7.3.7 Access Links for Procedure Parameters

When a procedure *p* is passed to another procedure *q* as a parameter, and *q* then calls its parameter (and therefore calls *p* in this activation of *q*), it is possible that *q* does not know the context in which *p* appears in the program. If so, it is impossible for *q* to know how to set the access link for *p*. The solution to this problem is as follows: when procedures are used as parameters, the caller needs to pass, along with the name of the procedure-parameter, the proper access link for that parameter.

The caller always knows the link, since if *p* is passed by procedure *r* as an actual parameter, then *p* must be a name accessible to *r*, and therefore, *r* can determine the access link for *p* exactly as if *p* were being called by *r* directly. That is, we use the rules for constructing access links given in Section 7.3.6.

**Example 7.8:** In Fig. 7.12 we see a sketch of an ML function *a* that has functions *b* and *c* nested within it. Function *b* has a function-valued parameter *f*, which it calls. Function *c* defines within it a function *d*, and *c* then calls *b* with actual parameter *d*.

```text
fun a(x) =
    let
        fun b(f) =
            ... f ... ;
        fun c(y) =
            let
                fun d(z) = ...
                in
                    ... b(d) ...
                end
    in
        ... c(1) ...
    end;
```

Figure 7.12: Sketch of ML program that uses function-parameters

Let us trace what happens when *a* is executed. First, *a* calls *c*, so we place an activation record for *c* above that for *a* on the stack. The access link for *c* points to the record for *a*, since *c* is defined immediately within *a*. Then *c* calls *b(d)*. The calling sequence sets up an activation record for *b*, as shown in Fig. 7.13(a).

Within this activation record is the actual parameter *d* and its access link, which together form the value of formal parameter *f* in the activation record for *b*. Notice that *c* knows about *d*, since *d* is defined within *c*, and therefore *c* passes a pointer to its own activation record as the access link. No matter where *d* was defined, if *c* is in the scope of that definition, then one of the three rules of Section 7.3.6 must apply, and *c* can provide the link.
