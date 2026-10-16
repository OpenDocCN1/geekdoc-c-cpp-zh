
Axioms such as these can be used to define the semantic properties of complex numbers, or the properties of the complex data type can be **derived** from those of the real data type by stating properties of the operations that lead back to properties of the real numbers. For example, complex addition can be based on real addition according to the following properties:

```
realpart(x + y) = realpart(x) + realpart(y)
imaginarypart(x + y) = imaginarypart(x) + imaginarypart(y)
```

The appropriate arithmetic properties of the complex numbers can then be proved from the corresponding properties for reals. A complete algebraic specification of type complex combines signature, variables, and equational axioms.¹

type complex imports real

# operations:

+   +   : complex × complex   complex
+   =   : complex × complex   complex
+   *   : complex × complex   complex
+   /   : complex × complex   complex
+   -   : complex   complex
+   makecomplex : real × real   complex
+   realpart : complex   real
+   imaginarypart : complex   real

# variables: x,y,z: complex; r,s: real

# axioms:

+   realpart(makecomplex(r,s)) = r
+   imaginarypart(makecomplex(r,s)) = s
+   realpart(x + y) = realpart(x) + realpart(y)
+   imaginarypart(x + y) = imaginarypart(x) + imaginarypart(y)
+   realpart(x - y) = realpart(x) - realpart(y)
+   imaginarypart(x - y) = imaginarypart(x) - imaginarypart(y)
+   ...
+   (more axioms)
+   ...

Such a specification is called an **algebraic specification** of an abstract data type. It provides a concise specification of a data type and its associated operations. The accompanying equational semantics give a clear indication of implementation behavior, often containing enough information to allow coding directly from the equations. Finding an appropriate set of equations, however, can be a difficult task. The next part of this section gives some suggestions on how to find them.

Remember the difference in the foregoing specification between **equality** as used in the axioms and the **arrow** of the syntactic specification of the functions. Equality is of values returned by functions, while the arrows separate a function’s domain and range.

> ¹The variables section of a specification is a notational convenience that simply lists the names (and their types) over which the axioms are assumed to be universally quantified in the mathematical sense. Thus, the first axiom in this algebraic specification is actually “for all real r and s, realpart(makecomplex(r,s)) = r.”

A second example of an algebraic specification of an abstract data type is the following specification of a queue:

type queue(element) imports boolean

# operations:

+   createq: queue
+   enqueue: queue × element   queue
+   dequeue: queue   queue
+   frontq: queue   element
+   emptyq: queue   boolean

variables: q: queue; x: element

# axioms:

+   emptyq(createq) = true
+   emptyq(enqueue(q,x)) = false
+   frontq(createq) = error
+   frontq(enqueue(q,x)) = if emptyq(q) then x else frontq(q)
+   dequeue(createq) = error
+   dequeue(enqueue(q,x)) = if emptyq(q) then q else enqueue(dequeue(q),x)

This specification exhibits several new features. First, the data type queue is parameterized by the data type element, which is left unspecified. Such a type parameter can be replaced by any type. You indicate it by placing its name inside parentheses, just as a function parameter would be. Second, the specification includes a constant, create, that is technically not a function. Such constants may also be a part of the algebraic specification; if desired, createq can be viewed as a function of no parameters that always returns the same value. Intuitively, we can see that createq is a new queue that has been initialized to empty. Third, we now include axioms that specify error values, such as

frontq(createq) = error

Such axioms can be called error axioms, and they provide limitations on the application of the operations. The actual error value of an error axiom is unspecified. Finally, the equations are specified using an if-then-else function, whose semantics are as follows:

if true then a else b = a
if false then a else b = b

Note also that the dequeue operation as specified does not return the front element of the queue, as in most implementations: It simply throws it away. Abstractly, this is simpler to handle and does not take away any functionality of the queue, since the frontq operation can extract the front element before a dequeue operation is performed.

The equations specifying the semantics of the operations in an algebraic specification of an abstract data type can be used as a specification of the properties of an implementation. It can also be used as a guide to the code for an implementation, and to prove specific properties about objects of the type.

For example, the following applications of axioms show that dequeuing from a queue with one element leaves an empty queue:

```
emptyq(dequeue(enqueue(createq, x)))
    = emptyq(createq)        (by the sixth axiom above)
    = true                  (by the first axiom)
```

Note that the operations and the axioms are specified in a mathematical form that includes no mention of memory or of assignment. Indeed, enqueue returns a newly constructed queue every time a new element is added. These specifications are in fact in purely functional form, with no variables and no assignment. (The variables in the specification are taken in the mathematical sense to be just names for values.) This is important, since mathematical properties, such as the semantic equations, are much easier to express with purely functional constructions. (See Chapter 4 for more on purely functional programming.) In practice, abstract data type implementations often replace the specified functional behavior with an equivalent imperative one using explicit memory allocation, as well as assignment or update operations. The question of how to infer that an imperative implementation is in some sense equivalent to a purely functional one, such as the above, is beyond the scope of our study here.

How do we find an appropriate axiom set for an algebraic specification? In general, this is a difficult question. We can, however, make some judgments about the kind and number of axioms necessary by looking at the syntax of the operations. An operation that creates a new object of the data type being defined is called a constructor, while an operation that retrieves previously constructed values is called an inspector. In the queue example, createq and enqueue are constructors, while frontq, dequeue, and emptyq are inspectors. Inspector operations can also be broken down into predicates, which return Boolean values, and selectors, which return non-Boolean values. Thus frontq and dequeue are selectors,² while emptyq is a predicate.

In general, we need one axiom for each combination of an inspector with a constructor. For the queue example, the axiom combinations are:

+   emptyq(createq)
+   emptyq(enqueue(q,x))
+   frontq(createq)
+   frontq(enqueue(q,x))
+   dequeue(createq)
+   dequeue(enqueue(q,x))

According to this scheme, there should be six rules in all, and that is in fact the case.

As a final example of an algebraic specification of an abstract data type, we give a specification for the stack abstract data type, which has many of the same features as the queue ADT:

```
type stack(element) imports boolean
```

# operations:

+   createstk: stack
+   push: stack × element  stack
+   pop: stack  stack
+   top: stack  element
+   emptystk: stack  boolean

> ²Strictly speaking, dequeue is a non-primitive constructor. We call it a selector because it acts like one in this context.

**variables:** *s*: stack; *x*: element

**axioms:**

    emptystk(createstk) = true  
    emptystk(push(s,x)) = false  
    top(createstk) = error  
    top(push(s,x)) = x  
    pop(createstk) = error  
    pop(push(s,x)) = s

In this case, the operations createstk and push are constructors, the pop and top operations are selectors, and the emptystk operation is a predicate. By our proposed scheme, therefore, there should again be six axioms.

## 11.2 Abstract Data Type Mechanisms and Modules

In this section, we explore some mechanisms for creating abstract data types and the manner in which modules represent an extension of these mechanisms.

### 11.2.1 Abstract Data Type Mechanisms

Some languages have a specific mechanism for expressing abstract data types. Such a mechanism must have a way of separating the specification or signature of the ADT (the name of the type being specified, and the names and types of the operations) from its implementation (a data structure implementing the type and a code body for each of the operations). Such a mechanism must also guarantee that any code outside the ADT definition cannot use details of the implementation but can operate on a value of the defined type only through the provided operations.

ML is an example of a language with a special ADT mechanism, called abstype. It is viewed as a kind of type definition mechanism. In Figure 11.1 it is used to specify a queue.

```
```sml
(1) abstype ’element Queue = Q of ’element list
(2) with
(3)   val createq = Q [];
(4)   fun enqueue (Q lis, elem) = Q (lis @ [elem]);
(5)   fun dequeue (Q lis) = Q (tl lis);
(6)   fun frontq (Q lis) = hd lis;
(7)   fun emptyq (Q []) = true | emptyq (Q (h::t)) = false;
(8) end;
```
```

**Figure 11.1** A queue ADT as an ML abstype, implemented as an ordinary ML list
