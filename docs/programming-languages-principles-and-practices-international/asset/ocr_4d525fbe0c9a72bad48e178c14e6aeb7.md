*(continued)*

```
```sml
(10)        | dequeue (Enqueue(q,elem))
(11)                    = Enqueue(dequeue q, elem);
(12)        fun emptyq Createq = true | emptyq _ = false;
(13)        end;
```
```

**Figure 11.17** An ML structure Queue2 implementing the QUEUE signature as a user-defined linked list

The Queue2 structure of Figure 11.17 can be used exactly as the Queue1 structure of Figure 11.16:

```
```sml
- open Queue2;
opening Queue2
  datatype 'a Queue = ...
  val createq : 'a Queue
  val enqueue : 'a Queue * 'a -> 'a Queue
  val frontq : 'a Queue -> 'a
  val dequeue : 'a Queue -> 'a Queue
  val emptyq : 'a Queue -> bool
- val q = enqueue(createq,3);
val q = Enqueue(Createq,3) : int Queue
- frontq q;
val it = 3 : int
- val q1 = dequeue q;
val q1 = Createq : int Queue
- emptyq q1;
val it = true : bool
```
```

ML signatures and structures satisfy most of the requirements of criteria 1 and 2 for abstract data types from this chapter’s introduction. A signature collects a type and its associated operations in one place. The definitions do not depend on any implementation details. A structure collects the implementation details in one place and only exports the information contained in the associated signature. The main difficulty with the ML module mechanism from the point of view of abstract data types is that client code must explicitly state the implementation that is to be used in terms of the module name: Code cannot be written to depend only on the signature, with the actual implementation structure to be supplied externally to the code. Thus, we cannot write:

```
```sml
val x = QUEUE.createq;
```
```

Instead, we must write:

```
```sml
val x = Queue1.createq;
```
```

or

```
```sml
val x = Queue2.createq;
```
```