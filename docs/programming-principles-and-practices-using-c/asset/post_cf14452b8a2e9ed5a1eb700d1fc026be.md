
## Drill

- 1. Run this:
    ```cpp
    int v = 1; for (int i = 0; i < sizeof(v) * 8; ++i) { cout << v << ' '; v <<= 1; }
    ```
- 2. Run that again with `v` declared to be an `unsigned int`.
- 3. Using hexadecimal literals, define `short unsigned ints` with:
    - a. Every bit set
    - b. The lowest (least significant bit) set
    - c. The highest (most significant bit) set
    - d. The lowest byte set
    - e. The highest byte set
    - f. Every second bit set (and the lowest bit 1)
    - g. Every second bit set (and the lowest bit 0)
- 4. Print each as a decimal and as a hexadecimal.
- 5. Do 3 and 4 using bit manipulation operations (`|`, `&`, `<<`) and (only) the literals 1 and 0.

## Review

- 1. What is an embedded system? Give ten examples, out of which at least three should not be among those mentioned in this chapter.
- 2. What is special about embedded systems? Give five concerns that are common.
- 3. Define predictability in the context of embedded systems.
- 4. Why can it be hard to maintain and repair an embedded system?
- 5. Why can it be a poor idea to optimize a system for performance?
- 6. Why do we prefer higher levels of abstraction to low-level code?
- 7. What are transient errors? Why do we particularly fear them?
- 8. How can we design a system to survive failure?
- 9. Why can't we prevent every failure?
- 10. What is domain knowledge? Give examples of application domains.
- 11. Why do we need domain knowledge to program embedded systems?
- 12. What is a subsystem? Give examples.
- 13. From a C++ language point of view, what are the three kinds of storage?
- 14. When would you like to use the free store?
- 15. Why is it often infeasible to use the free store in an embedded system?
- 16. When can you safely use `new` in an embedded system?
- 17. What is the potential problem with `std::vector` in the context of embedded systems?
- 18. What is the potential problem with exceptions in the context of embedded systems?
- 19. What is a recursive function call? Why do some embedded systems programmers avoid them? What do they use instead?
- 20. What is memory fragmentation?
- 21. What is a garbage collector (in the context of programming)?
- 22. What is a memory leak? Why can it be a problem?
- 23. What is a resource? Give examples.
- 24. What is a resource leak and how can we systematically prevent it?
- 25. Why can’t we easily move objects from one place in memory to another?
- 26. What is a stack?
- 27. What is a pool?
- 28. Why doesn’t the use of stacks and pools lead to memory fragmentation?
- 29. Why is `reinterpret_cast` necessary? Why is it nasty?
- 30. Why are pointers dangerous as function arguments? Give examples.
- 31. What problems can arise from using pointers and arrays? Give examples.
- 32. What are alternatives to using pointers (to arrays) in interfaces?
- 33. What is “the first law of computer science”?
- 34. What is a bit?
- 35. What is a byte?
- 36. What is the usual number of bits in a byte?
- 37. What operations do we have on sets of bits?
- 38. What is an “exclusive or” and why is it useful?
- 39. How can we represent a set (sequence, whatever) of bits?
- 40. How do we conventionally number bits in a word?
- 41. How do we conventionally number bytes in a word?
- 42. What is a word?
- 43. What is the usual number of bits in a word?
- 44. What is the decimal value of `0xf`?
- 45. What sequence of bits is `0xab`?
- 46. What is a `bitset` and when would you need one?
- 47. How does an `unsigned int` differ from a `signed int`?
- 48. When would you prefer an `unsigned int` to a `signed int`?
- 49. How would you write a loop if the number of elements to be looped over was very high?
- 50. What is the value of an `unsigned int` after you assign `-3` to it?
- 51. Why would we want to manipulate bits and bytes (rather than higher-level types)?
- 52. What is a bitfield?
- 53. For what are bitfields used?
- 54. What is encryption (enciphering)? Why do we use it?
- 55. Can you encrypt a photo?
- 56. What does TEA stand for?
- 57. How do you write a number to output in hexadecimal notation?
- 58. What is the purpose of coding standards? List reasons for having them.
- 59. Why can’t we have a universal coding standard?
- 60. List some properties of a good coding standard.
- 61. How can a coding standard do harm?
- 62. Make a list of at least ten coding rules that you like (have found useful). Why are they useful?
- 63. Why do we avoid ALL_CAPITAL identifiers?

## Terms

- address
- encryption
- pool
- bit
- exclusive or
- predictability
- bitfield
- gadget
- real time
- bitset
- garbage collector
- resource
- coding standard
- hard real time
- soft real time
- embedded system
- leak
- unsigned

## Exercises

- 1. If you haven’t already, do the **Try** this exercises in this chapter.
- 2. Make a list of words that can be spelled with hexadecimal notation. Read 0 as o, read 1 as l, read 2 as to, etc.; for example, Fool and Beef. Kindly eliminate vulgarities from the list before submitting it for grading.
- 3. Initialize a 32-bit signed integer with the bit patterns and print the result: all zeros, all ones, alternating ones and zeros (starting with a left-most one), alternating zeros and ones (starting with a leftmost zero), the 110011001100... pattern, the 001100110011... pattern, the pattern of all-one bytes and all-zero bytes starting with an all-one byte, the pattern of all-one bytes and all-zero bytes starting with an all-zero byte. Repeat that exercise with a 32-bit unsigned integer.
- 4. Add the bitwise logical operators `&`, `|`, `^`, and `~` to the calculator from Chapter 7.
- 5. Write an infinite loop. Execute it.
- 6. Write an infinite loop that is hard to recognize as an infinite loop. A loop that isn’t really infinite because it terminates after completely consuming some resource is acceptable.
- 7. Write out the hexadecimal values from 0 to 400; write out the hexadecimal values from −200 to 200.
- 8. Write out the numerical values of each character on your keyboard.
- 9. Without using any standard headers (such as `<limits>`) or documentation, compute the number of bits in an `int` and determine whether `char` is signed or unsigned on your implementation.
- 10. Look at the bitfield example from §25.5.5. Write an example that initializes a PPN, then reads and prints each field value, then changes each field value (by assigning to the field) and prints the result. Repeat this exercise, but store the PPN information in a 32-bit unsigned integer and use bit manipulation operators (§25.5.4) to access the bits in the word.
- 11. Repeat the previous exercise, but keep the bits in a `bitset<32>`.
- 12. Write out the clear text of the example from §25.5.6.
- 13. Use TEA (§25.5.6) to communicate “securely” between two computers. Email is minimally acceptable.
- 14. Implement a simple vector that can hold at most N elements allocated from a pool. Test it for N==1000 and integer elements.
- 15. Measure the time (§26.6.1) it takes to allocate 10,000 objects of random sizes in the [1000:0]-byte range using `new`; then measure the time it takes to deallocate them using `delete`. Do this twice, once deallocating in the reverse order of allocation and once deallocating in random order. Then, do the equivalent for allocating 10,000 objects of size 500 bytes from a pool and freeing them. Then, do the equivalent of allocating 10,000 objects of random sizes in the [1000:0]-byte range on a stack and then free them (in reverse order). Compare the measurements. Do each measurement at least three times to make sure the results are consistent.
- 16. Formulate 20 coding style rules (don’t just copy those in §25.6). Apply them to a program of more than 300 lines that you recently wrote. Write a short (a page or two) comment on the experience of applying those rules. Did you find errors in the code? Did the code get clearer? Did some code get less clear? Now modify the set of rules based on this experience.
- 17. In §25.4.3–4 we provided a class `Array_ref` claimed to make access to elements of an array simpler and safer. In particular, we claimed to handle inheritance correctly. Try a variety of ways to get a `Rectangle*` into a `vector<Circle*>` using an `Array_ref<Shape*>` but no casts or other operations involving undefined behavior. This ought to be impossible.

## Postscript

So, is embedded systems programming basically “bit fiddling”? Not at all, especially if you deliberately try to minimize bit fiddling as a potential problem with correctness. However, somewhere in a system bits and bytes have “to be fiddled”; the question is just where and how. In most systems, the low-level code can and should be localized. Many of the most interesting systems we deal with are embedded, and some of the most interesting and challenging programming tasks are in this field.
