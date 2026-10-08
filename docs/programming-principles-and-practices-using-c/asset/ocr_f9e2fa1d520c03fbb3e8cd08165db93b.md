# Drill

+   1.  Run this:

    `int v = 1; for (int i = 0; i<sizeof(v)*8; ++i) { cout << v << ' '; v <<<=1; }`

2.  Run that again with `v` declared to be an `unsigned int`.

3.  Using hexadecimal literals, define `short unsigned ints` with:
    * a.  Every bit set
    * b.  The lowest (least significant bit) set
    * c.  The highest (most significant bit) set
    * d.  The lowest byte set
    * e.  The highest byte set
    * f.  Every second bit set (and the lowest bit 1)
    * g.  Every second bit set (and the lowest bit 0)

4.  Print each as a decimal and as a hexadecimal.

5.  Do 3 and 4 using bit manipulation operations (`|`, `&`, `<<`) and (only) the literals 1 and 0.

# Review

+   1.  What is an embedded system? Give ten examples, out of which at least three should not be among those mentioned in this chapter.

2.  What is special about embedded systems? Give five concerns that are common.

3.  Define predictability in the context of embedded systems.

4.  Why can it be hard to maintain and repair an embedded system?

5.  Why can it be a poor idea to optimize a system for performance?

6.  Why do we prefer higher levels of abstraction to low-level code?

7.  What are transient errors? Why do we particularly fear them?

8.  How can we design a system to survive failure?

9.  Why can't we prevent every failure?

10. What is domain knowledge? Give examples of application domains.

11. Why do we need domain knowledge to program embedded systems?

12. What is a subsystem? Give examples.

13. From a C++ language point of view, what are the three kinds of storagee?

14. When would you like to use the free store?

15. Why is it often infeasible to use the free store in an embedded system?

16. When can you safely use `new` in an embedded system?

17. What is the potential problem with `std::vector` in the context of embedded systems?