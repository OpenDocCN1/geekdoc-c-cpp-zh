We could write procedures equal and assign and add them to the operations in the package specification (or the header file in C), but, again, there would be no guarantee that they would be appropriately applied by a client.

In Ada, however, we can use a limited private type as a mechanism for controlling the use of equality and assignment. For example:

```
package ComplexNumbers is

    type Complex is limited private;

    -- operations, including assignment and equality
    ...
    function equal(x,y: in Complex) return Boolean;
    procedure assign(x: out Complex; y: in Complex);

private
    type ComplexRec;
    type Complex is access ComplexRec;

end ComplexNumbers;
```

Now clients are prevented from using the usual assignment and equality operations, and the package body can ensure that equality is performed appropriately and that assignment deallocates garbage and/or copies values instead of pointers. Indeed, the = (and, implicitly, the inequality /=) operator can be overloaded as described in Chapter 8, so the same infix form can be used after redefinition by the package. Assignment, however, cannot be overloaded in Ada, and there is still no automatic initialization and deallocation.

C++ has an advantage here, since it allows the overloading of both assignment (=) and equality (==). Additionally, object-oriented languages solve the initialization problem by the use of constructors.

ML also is able to control equality testing by limiting the data type in an abstype or struct specification to types that do not permit the equality operation. Indeed, ML makes a distinction between types that allow equality testing and types that do not. Type parameters that allow equality testing must be written using a double apostrophe `'a instead of a single apostrophe `a, and a type definition that allows equality must be specified as an eqtype rather than just a type:

```
signature QUEUE =
    sig
    eqtype `'a Queue
    val createq: `'a Queue
    ...etc.
end;
```

Without this, equality cannot be used to test queues. Additionally, assignment in ML is much less of a problem, since standard functional programming practice does away with most uses of that operation (see Chapter 4).