
## Accessing Instructor and Student Resource Materials

The following items are available on the publisher's website at www.pearsonhighered.com/carrano

- C++ code as it appears in the book
- A link to any misprints that have been discovered since the book was published
- Links to additional online content, which is described next

### Instructor Resources

The following protected material is available to instructors who adopt this book by logging onto Pearson's Instructor Resource Center, accessible from www.pearsonhighered.com/carrano

- PowerPoint lecture slides
- Test bank
- Instructor solutions manual
- Figures from the book

Additionally, instructors can access the book's Companion Website for the following online premium content, also accessible from www.pearsonhighered.com/carrano

- Instructional VideoNotes
- Answers to the Checkpoint Questions
- A glossary of terms

Please contact your Pearson sales representative for an instructor access code. Contact information is available at www.pearsonhighered.com/replocator.

### Student Resources

The following material is available to students by logging onto the book's Companion Website accessible from www.pearsonhighered.com/carrano:

- Instructional VideoNotes
- Answers to the Checkpoint Questions
- A glossary of terms

Students must use the access card located in the front of the book to register for and then enter the Companion Website. Students without an access code can purchase access from the Companion Website by following the instructions listed there.

## Chapter Overview

Readers of this book should have completed a programming course, preferably in C++. Appendix A covers the essentials of C++ that we assume readers will know. You can use this appendix as a review or as the basis for making the transition to C++ from another programming language. Note that Appendices K and L offer some help for those who are transitioning from Java or Python, respectively.

- Chapters 1 through 5: Chapter 1 introduces object-oriented concepts and focuses on the specification of abstract data types (ADTs). Our ADTs now store data whose data type is chosen by the client. To accomplish this, each specification of an ADT includes a C++ template interface. As an example, Chapter 1 introduces the ADT bag. Much of the software engineering material that was in Chapter 1 is now in the appendices.

Next in C++ Interlude 1, which presents C++ classes. It gives more details about template interfaces—like the one presented in Chapter 1—and shows how to use inheritance to define a class derived from an interface.

As it did in earlier editions, Chapter 2 introduces recursion, and Chapter 5 develops it as a problem-solving tool. Recursion is revisited often throughout the book.

We clearly separate the specification, use, and implementation of the bag by dividing the material across several chapters. For example, Chapter 1 specifies the bag and provides several examples of its use. Chapter 3 covers implementations that use arrays. Just before Chapter 4 introduces chains of linked nodes and uses one in the definition of a class of bags, C++ Interlude 2 covers pointers, polymorphism, and dynamic memory allocation. Both Chapters 3 and 4 include recursion in their presentation.

In a similar fashion, we separate specification from implementation throughout most of the book when we discuss various other ADTs. You can choose to cover the chapters that specify and use the ADTs and then later cover the chapters that implement them. Or you can cover the chapters as they appear, implementing each ADT right after studying its specification and use. A list of chapter prerequisites appears later in this preface to help you plan your path through the book.

Chapter 3 does more than simply implement the ADT bag. It shows how to approach the implementation of a class by initially focusing on core methods. When defining a class, it is often useful to implement and test these core methods first and to leave definitions of the other methods for later. Chapter 4 follows this approach in its development of a link-based implementation of the ADT bag.

- Chapters 6 and 7: Chapter 6 discusses stacks, giving examples of their use, and Chapter 7 implements the stack using an array and then again using a chain. Between these chapters is C++ Interlude 3, which discusses C++ exceptions. Chapter 7 then shows how to use an exception in the implementation of the ADT stack, when a client violates a method’s precondition.

- Chapters 8 and 9: The next two chapters introduce the ADT list. We discuss this container abstractly and then implement it by using an array and then a chain of linked nodes. Once again, we use exceptions to enforce method preconditions.

- Chapters 10 and 11: Chapter 10 introduces the complexity of algorithms, a topic that we integrate into future chapters. Chapter 11 discusses various sorting techniques and their relative complexities. We consider both iterative and recursive versions of these algorithms.

- Chapter 12: Chapter 12 introduces the sorted list, looking at a linked implementation and its efficiency. We then talk about the relationship between a list and a sorted list and show how to use the list as a base class for the sorted list. Note that Chapter 12 is preceded by C++ Interlude 4 that discusses class relationships and the various ways a class can be reused. Chapter 12 puts that discussion into immediate use.

- Chapters 13 and 14: Chapter 13 presents the ADTs of queue and priority queue, along with some uses of these containers. In doing so, we give an example of simulation that uses both ADTs, and finally summarize the difference between position oriented and value oriented ADTs. Chapter 14 implements the queue, and introduces tail pointers, circularly linked chains, and circular arrays. We offer an implementation of a priority queue by using a sorted list, but note that a better approach will come later when we introduce the ADT heap.

- Chapters 15 through 17: Before we begin the next chapter, C++ Interlude 5 introduces overloaded operators and friend access. We overload operators when we define classes of trees in this group of chapters. Chapter 15 discusses trees—binary, binary search, and general—and their possible uses. Chapter 16 considers implementations of these trees, and briefly introduces the tree sort. C++ Interlude 6 presents iterators in the context of a list. Chapter 17 introduces the ADT heap and shows how to implement it by using an array. We then use a heap to implement the priority queue and to sort an array.

- Chapter 18: This chapter covers the specification and use of the ADT dictionary (formerly called the table in the previous edition). We look at implementations of the dictionary that use an array or a binary search tree. We then introduce hashing and use it as a dictionary implementation.

- Chapter 19: Chapter 19 introduces balanced search trees. Included in this chapter are the 2-3, 2-4, and red-black trees, as well as AVL trees. These trees are considered as implementations of the ADT dictionary.

- Chapter 20: Next, we discuss graphs, suggest two ways to implement them, and look at several applications.

- Chapter 21: This last chapter considers data storage in external direct access files. Merge sort is modified to sort such data, and external hashing and B-tree indexes are used to search it. These searching algorithms are generalizations of the internal hashing schemes and 2-3 trees already developed. Finally, C++ Interlude 7 ends the main presentation by discussing the containers and algorithms available in the C++ Standard Template Library (STL).

- Appendices A through L: The appendices provide supplemental information. As we mentioned earlier, Appendix A reviews C++ up to but not including classes. Appendices B, C, D, and F contain sections that were in Chapter 1 of the previous edition, namely important aspects of programming, the Unified Modeling Language (UML), the software life cycle, and algorithm verification. Appendix E covers mathematical induction, and Appendix G covers input and output with external files. Appendix H provides a list of C++ header files and standard functions, and Appendix I considers the javadoc commenting style and defines the tags that we use in this book. Appendix J is simply a chart of the ASCII character codes. Finally, Appendices K and L are brief transition guides to C++ for those who know Java or Python, respectively.
