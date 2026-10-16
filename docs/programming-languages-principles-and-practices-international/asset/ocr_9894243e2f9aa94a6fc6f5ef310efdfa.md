(continued)

```
(16)    fq := enqueue(fq,2.3);
(17)    iq := enqueue(iq,3);
(18)    iq := enqueue(iq,2);
(19)    put(frontq(iq)); -- prints 3
(20)    new_line;
(21)    fq := dequeue(fq);
(22)    put(frontq(fq)); -- prints 2.3
(23)    new_line;
(24) end Quser;
```

Figure 11.14 Sample Ada client code that uses the Queues generic package of Figures 11.12 and 11.13

We note the following about the code in Figure 11.14. First, lines 1–5 import and dereference standard Ada library IO functions. Line 6 imports the Queues package. Lines 8 and 10 create two different instantiations of the Queues generic package, one for integers and one for floating-point numbers; these are given the package names IntQueues and FloatQueues. These two packages are then dereferenced by the use declarations in lines 9 and 11. Note that this creates name ambiguities, since all of the names from each of these packages conflict with the names from the other package. Ada’s overloading mechanism can, however, resolve most of these ambiguities, based on the data types of the parameters and results. Thus, it is still possible to use the simple names, such as enqueue, instead of the qualified names IntQueues.enqueue and FloatQueues.enqueue. However, it is impossible to disambiguate the names when the data type Queue is used in the definitions of fq and iq (lines 12 and 13). In this case, the qualified names IntQueues.Queue and FloatQueues.Queue are used to provide the necessary disambiguation.

# 11.5 Modules in ML

In Section 11.2, we demonstrated the ML abstype definition, which allows easy definition of abstract types with associated operations. ML also has a more general module facility, which consists of three mechanisms: signatures, structures, and functors. The signature mechanism is essentially an interface definition (it even adopts the name signature from the mathematical description of the syntax of an ADT as in Section 11.1). A structure is essentially an implementation of a signature; viewed another way, the signature is essentially the type of the structure. Functors are essentially functions from structures to structures, with the structure parameters having “types” given by signatures. Functors allow for the parameterization of structures by other structures. For more on functors, see Section 11.7.4.

Figure 11.15 shows an ML signature for a queue ADT. The sig ... end expression (lines 2 and 9) produces a value of type signature by listing the types of the identifiers being defined by the signature. This signature value is then stored as the name QUEUE. Since a signature is not a type as such, we must export the type Queue as one of the identifiers; this is done in line 3 with the declaration type 'a Queue, which identifies the name Queue as an exported type, parameterized by the type variable 'a. Thus, this signature allows queues to contain elements of arbitrary type (but each queue can only contain elements of a single type). The type Queue may be either a type synonym for a previously existing type, or a new type; making it a previously existing type can result in a loss of protection, however (see Exercise 11.29); thus, in our examples we will always use a new type.