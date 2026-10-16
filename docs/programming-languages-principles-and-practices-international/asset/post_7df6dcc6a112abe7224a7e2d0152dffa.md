
ML also has a feature that allows structures to be explicitly parameterized by other structures; this feature is called a functor, because it is essentially a function on structures (albeit one that operates only statically). Given two signatures such as ORDER and ORDERED_LIST (lines 1–5 and 6–13 of Figure 11.18), a functor that takes an ORDER structure as an argument and produces an ORDERED_LIST structure as a result can be defined as follows (for a complete example, see lines 14–28 of Figure 11.18):

```
functor OListFUN (structure Order: ORDER):
ORDERED_LIST =
    struct
    ..
    end;
```

Then, given an actual ORDER structure value, such as IntOrder (lines 29–33), the functor can be applied to create a new ORDERED_LIST structure IntOList:

```
structure IntOList =
    OListFUN(structure Order = IntOrder);
```

This makes explicit the appropriate dependencies, but at the cost of requiring an extra structure (IntOrder) to be defined that encapsulates the required features.

```
(1) signature ORDER =
(2)   sig
(3)   type Elem
(4)   val lt: Elem * Elem -> bool
(5)   end;

(6) signature ORDERED_LIST =
(7)   sig
(8)   type Elem
(9)   type OList
(10)  val create: OList
(11)  val insert: OList * Elem -> OList
(12)  val lookup: OList * Elem -> bool
(13)  end;
(14) functor OListFUN (structure Order: ORDER):
(15) ORDERED_LIST =
(16)   struct
(17)   type Elem = Order.Elem;
(18)   type OList = Order.Elem list;
(19)   val create = [];
(20)   fun insert ([], x) = [x]
(21)   | insert (h::t, x) = if Order.lt(x,h) then x::h::t
(22)                     else h:: insert (t, x);
(23)   fun lookup ([], x) = false
```

Figure 11.18 The use of a functor in ML to define an ordered list (continues)

```
```ml
(24)  lookup (h::t, x) =
(25)      if Order.lt(x,h) then false
(26)      else if Order.lt(h,x) then lookup (t,x)
(27)      else true;
(28)  end;

(29)  structure IntOrder: ORDER =
(30)      struct
(31)      type Elem = int;
(32)      val lt = (op <);
(33)      end;

(34)  structure IntOList =
(35)      OListFUN(structure Order = IntOrder);
```
```

**Figure 11.18** The use of a functor in ML to define an ordered list

With the code of Figure 11.18, the **IntOList** structure can be used as follows:

```
```ml
- open IntOList;
opening IntOList
type Elem = IntOrder.Elem
type OList = IntOrder.Elem list
val create : OList
val insert : OList * Elem -> OList
val lookup : OList * Elem -> bool
- val ol = insert(create,2);
val ol = [2] : OList
- val ol2 = insert(ol,3);
val ol2 = [2,3] : OList
- lookup (ol2,3);
val it = true : bool
- lookup (ol,3);
val it = false : bool
```
```

## 11.7.5 Module Definitions Include No Specification of the Semantics of the Provided Operations

In the algebraic specification of an abstract data type, equations are given that specify the behavior of the operations. Yet in almost all languages no specification of the behavior of the available operations is required. Some experiments have been conducted with systems that require semantic specification and then attempt to determine whether a provided implementation agrees with its specification, but such languages and systems are still unusual and experimental.

One example of a language that does allow the specification of semantics is Eiffel, an object-oriented language. In Eiffel, semantic specifications are given by preconditions, postconditions, and invariants. Preconditions and postconditions establish what must be true before and after the execution of a procedure or function. Invariants establish what must be true about the internal state of the data in an abstract data type. For more on such conditions, see Chapter 13 on formal semantics. For more on Eiffel, see the Notes and References.

A brief example of the way Eiffel establishes semantics is as follows. In a queue ADT as described in Section 11.1, the enqueue operation is defined as follows in Eiffel:

```
enqueue (x:element) is
require
             not full
ensure
             if old empty then front = x
             else front = old front;
             not empty
end; -- enqueue
```

The require section establishes preconditions—in this case, to execute the enqueue operation correctly, the queue must not be full (this is not part of the algebraic specification as given in Section 11.1; see Exercise 11.24). The ensure section establishes postconditions, which in the case of the enqueue operation are that the newly enqueued element becomes the front of the queue only if the queue was previously empty and that the queue is now not empty. These requirements correspond to the algebraic axioms

> frontq(enqueue(q,x)) = if emptyq(q) then x else frontq(q)
> emptyq(enqueue(q,x)) = false

of Section 11.1.

In most languages, we are confined to giving indications of the semantic content of operations inside comments.

## 11.8 The Mathematics of Abstract Data Types

In the algebraic specification of an abstract data type, a data type, a set of operations, and a set of axioms in equational form are specified. Nothing is said, however, about the actual existence of such a type, which is hypothetical until an actual type is constructed that meets all the requirements. In the parlance of programming language theory, an abstract data type is said to have existential type—it asserts the existence of an actual type that meets its requirements. Such an actual type is a set with operations of the appropriate form that satisfy the given equations. A set and operations that meet the specification are a model for the specification. Given an algebraic specification, it is possible for no model to exist, or many models. Therefore, it is necessary to distinguish an actual type (a model) from a potential type (an algebraic specification). Potential types are called sorts, and potential sets of operations are called

signatures. (Note that this agrees with our previous use of the term signature to denote the syntax of prospective operations.) Thus, a sort is the name of a type, which is not yet associated with any actual set of values. Similarly, a signature is the name and type of an operation or set of operations, which exists only in theory, having no actual operations yet associated with it. A model is then an actualization of a sort and its signature and is called an algebra (since it has operations).

For this reason, algebraic specifications are often written using the sort-signature terminology:

```
sort queue(element) imports boolean
```

# signature:

+   - createq: queue
+   - enqueue: queue × element   queue
+   - dequeue: queue   queue
+   - frontq: queue   element
+   - emptyq: queue   boolean

# axioms:

+   - emptyq(createq) = true
+   - emptyq (enqueue (q, x)) = false
+   - frontq(createq) = error
+   - frontq(enqueue(q,x)) = if emptyq(q) then x else frontq(q)
+   - dequeue(createq) = error
+   - dequeue(enqueue(q,x)) = if emptyq(q) then q else enqueue(dequeue(q), x)

Given a sort, a signature, and axioms, we would, of course, like to know that an actual type exists for that specification. In fact, we would like to be able to construct a unique algebra for the specification that we would then take to be the type represented by the specification.

How does one construct such an algebra? A standard mathematical method is to construct the free algebra of terms for a sort and signature and then to form the quotient algebra of the equivalence relation generated by the equational axioms. The free algebra of terms consists of all the legal combinations of operations. For example, the free algebra for sort queue(integer) and signature as above has terms such as the following:

+   - createq
+   - enqueue (createq, 2)
+   - enqueue (enqueue(createq, 2), 1)
+   - dequeue (enqueue (createq, 2))
+   - dequeue (enqueue(enqueue (createq, 2), -1))
+   - dequeue (dequeue (enqueue (createq, 3)))
+   - etc.

Note that the axioms for a queue imply that some of these terms are actually equal, for example,

```
dequeue (enqueue (createq, 2)) = createq
```
