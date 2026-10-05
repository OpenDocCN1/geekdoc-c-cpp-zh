choose a different implementation language, for example C, we would have many more issues to contend with. Nevertheless, it is possible to build this kind of interpreter in any language.

+   The use of the g: prefix in g:apply and other names serves to identify those names as specific to this “generic” interpreter. In later sections we introduce different versions of the interpreter, each of which has its own prefix.

+   Reals are usually represented in the computer as floating-point numbers. The parts of a Scheme complex number may be integers or rational fractions, as well as reals.

+   The understanding of quotation and its relationship to evaluation has deep consequences in analytic philosophy. One good exposition of this is in the 1982 PhD thesis of Brian Cantwell Smith [112].

+   A symbol is an atomic object that is named by a string of characters. What makes a symbol interesting is that it is unique; any two instances of a symbol with the same character-string name may be presumed to be identical (they are eq).

+   Many of the Scheme primitives found this way will work, such as car or +. However, primitives that take procedures as arguments, such as map or filter, will not accept nonprimitive procedures (i.e., those created by this interpreter from lambda expressions). This is addressed in exercise 5.5 on page 249.

+   The real problem with macros is that they can introduce bindings that can inadvertently conflict with existing bindings, making them referentially opaque. There are several attacks on the development of Scheme referential-opacity problem, leading to development of hygienic macro systems. See [73, 74, 8, 31]. Also, drastically modifying a language by introducing special forms makes it harder for a reader to understand a program—the reader must learn the new special forms before reading the program that uses them.

+   MIT/GNU Scheme allows a more general syntax for definitions, with recursive expansion of the cadr of the define form (see page