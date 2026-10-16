
together with the implementation of the operations. Further, a client is prevented from using any of the details in the IMPLEMENTATION MODULE.

Since the DEFINITION MODULE is independent of any of the details of the IMPLEMENTATION MODULE, the implementation can be rewritten without affecting any use of the module by clients, in a similar manner to Ada and C.

## 11.7 Problems with Abstract Data Type Mechanisms

Abstract data type mechanisms in programming languages use separate compilation facilities to meet protection and implementation independence requirements. The specification part of the ADT mechanism is used as an interface to guarantee consistency of use and implementation. However, ADT mechanisms are used to create types and associate operations to types, while separate compilation facilities are providers of services, which may include variables, constants, or any other programming language entities. Thus, compilation units are in one sense more general than ADT mechanisms. At the same time they are less general, however, in that the use of a compilation unit to define a type does not identify the type with the unit and, thus, is not a true type declaration. Furthermore, units are static entities—that is, they retain their identity only before linking, which can result in allocation and initialization problems. Thus, the use of separate compilation units, such as modules or packages, to implement abstract data types is a compromise in language design. However, it is a useful compromise, because it reduces the implementation question for ADTs to one of consistency checking and linkage.

In this section, we catalog some of the major drawbacks of the ADT mechanisms we have studied (and others we have not). Of course, not all languages suffer from all the drawbacks listed here. Many, but not all, of these drawbacks have been corrected in object-oriented languages. Thus, this section serves as an indication of what to look for in object-oriented languages.

### 11.7.1 Modules Are Not Types

In C, Ada, and ML, difficulties can arise because a module must export a type as well as operations. It would be helpful instead to define a module to be a type. This prevents the need to arrange to protect the implementation details of the type with an ad hoc mechanism such as incomplete or private declarations; the details are all contained in the implementation section of the type.

The fact that ML contains both an abstype and a module mechanism emphasizes this distinction. The module mechanism is more general, and it allows the clean separation of specification (signature) from implementation (structure), but a type must be exported. On the other hand, an abstype is a type, but the implementation of an abstype cannot be separated from its specification (although access to the details of the implementation is prevented), and clients of the abstype implicitly depend on the implementation.

### 11.7.2 Modules Are Static Entities

An attractive possibility for implementing an abstract data type is to simply not reveal a type at all, thus avoiding all possibility of clients depending in any way on implementation details, as well as preventing clients from any misuse of a type. For example, in Ada we could write a Queue package specification as follows. In the following example, note how the operations must change so that they never return a queue. This is pure imperative programming.

```ada
generic
   type T is private;
package Queues is
   procedure enqueue(elem:T);
   function frontq return T;
   procedure dequeue;
   function emptyq return Boolean;
end Queues;
```

The actual queue data structure is then buried in the implementation:

```ada
package body Queues is

   type Queuerep;
   type Queue is access Queuerep;

   type Queuerep is
   record
      data: T;
      next: Queue;
   end record;

   q: Queue;

   procedure enqueue(elem:T) is
      temp: Queue;
   begin
      temp := new Queuerep;
      temp.data := elem;

      if (q /= null) then
         temp.next := q.next;
         q.next := temp;
      else
         temp.next := temp;
      end if;
      q := temp;
   end enqueue;

   function frontq return T is
   begin
      return q.next.data;
   end frontq;

   procedure dequeue is
   begin
      if q = q.next then
         q := null;
      else
         q.next := q.next.next;
         q := q.next;
      end if;
   end dequeue;

   function emptyq return Boolean is
   begin
      return q = null;
   end emptyq;

begin
   q := null;
end Queues;
```

Note that this allows us to write initialization code internally within the package body (the last three lines of the above code), which is executed on “elaboration,” or allocation time (at the beginning of execution). This eliminates the need for user-supplied code to initialize a queue, and so there is no createq procedure.

Normally this would imply that there can only be one queue in a client, since otherwise the entire code must be replicated (try this using a C++ namespace—see Exercise 11.28). This results from the static nature of most module mechanisms (including those of Ada and ML). In Ada, however, the generic package mechanism offers a convenient way to obtain several different queues (even for the same stored type) by using multiple instantiations of the same generic package:

```ada
with Ada.Text_IO; use Ada.Text_IO;
with Ada.Integer_Text_IO;
use Ada.Integer_Text_IO;
with Queues;

procedure Quser is

   package Queue1 is new Queues(Integer);
   package Queue2 is new Queues(Integer);

begin
   Queue1.enqueue(3);
   Queue1.enqueue(4);
   Queue2.enqueue(1);
   Queue2.enqueue(2);
   put(Queue1.frontq); -- prints 3
```

We could write procedures equal and assign and add them to the operations in the package specification (or the header file in C), but, again, there would be no guarantee that they would be appropriately applied by a client.

In Ada, however, we can use a limited private type as a mechanism for controlling the use of equality and assignment. For example:

```ada
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

ML also is able to control equality testing by limiting the data type in an abstype or struct specification to types that do not permit the equality operation. Indeed, ML makes a distinction between types that allow equality testing and types that do not. Type parameters that allow equality testing must be written using a double apostrophe ''a instead of a single apostrophe 'a, and a type definition that allows equality must be specified as an eqtype rather than just a type:

```sml
signature QUEUE =
    sig
    eqtype ''a Queue
    val createq: ''a Queue
    ...etc.
end;
```

Without this, equality cannot be used to test queues. Additionally, assignment in ML is much less of a problem, since standard functional programming practice does away with most uses of that operation (see Chapter 4).

### 11.7.4 Modules Do Not Always Adequately Represent Their Dependency on Imported Types

Aside from assignment and equality testing, modules often depend on the existence of certain operations on type parameters and may also call functions whose existence is not made explicit in the module specification. A typical example is a data structure such as a binary search tree, priority queue, or ordered list. These data structures all require that the type of the stored values have an order operation such as the less-than arithmetic operation “<” available. Frequently this is not made explicit in a module specification.

For example, C++ templates mask such dependencies in specifications. A simple example is of a template min function, which depends on an order operation. In C++ this could be specified as:

```cpp
template <typename T>
T min( T x, T y);
```

Naturally, the implementation of this function shows the dependency on the order operation (but the specification does not):

```cpp
// C++ code
template <typename T>
T min( T x, T y)
// requires an available < operation on T
{ return x < y ? x : y;
}
```

(See Chapter 9 for a discussion on how to make this dependency explicit in C++.)

In Ada it is possible to specify this requirement using additional declarations in the generic part of a package declaration:

```ada
generic
type Element is private;
with function lessThan (x,y: Element) return Boolean;
package OrderedList is
...
end OrderedList;
```

Now an OrderedList package can be instantiated only by providing a suitable lessThan function, as in

```ada
package IntOrderedList is new
  OrderedList (Integer,"<");
```

Such a requirement is called constrained parameterization. Without explicit constraints in Ada, no operations are assumed for the type parameter except equality, inequality, and assignment (and, as noted in the previous section, even these are not assumed if the type is declared limited private).
