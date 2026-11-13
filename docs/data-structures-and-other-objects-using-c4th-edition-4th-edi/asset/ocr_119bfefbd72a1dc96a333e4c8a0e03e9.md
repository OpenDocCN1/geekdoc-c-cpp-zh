# C++ Language Features

C++ is a complex language with many advanced features that will not be touched in a second-semester course. But we endeavor to provide complete coverage for those features that we do touch. In the first edition of the text, we included coverage of two features that were new to C++ at the time: the new bool data type (Figure 2.1 on page 37) and static member constants (see page 104). The requirements for using static member constants were changed in the 1998 Standard, and we have incorporated this change into the text (the constant must now be declared both inside and outside the class definition). The other primary new feature from the 1998 Standard is the use of namespaces, which were incorporated in the second edition. In each of these cases, these features might not be supported in older compilers. We provide some assistance in dealing with this (see Appendix E, “Dealing with Older Compilers”), and some assistance in downloading and installing the GNU g++ compiler (see Appendix K).

# Flexibility of Topic Ordering

This book was written to allow instructors latitude in reordering the material to meet the specific background of students or to add early emphasis to selected topics. The dependencies among the chapters are shown on page xi. A line joining two boxes indicates that the upper box should be covered before the lower box.

Here are some suggested orderings of the material:

+   **Typical course.** Start with Chapters 1–10, skipping parts of Chapter 2 if the students have a prior background in C++ classes. Most chapters can be covered in a week, but you may want more time for Chapter 5 (linked lists), Chapter 6 (templates), Chapter 9 (recursion), or Chapter 10 (trees). Typically, we cover the material in 13 weeks, including time for exams and extra time for linked lists and trees. Remaining weeks can be spent on a tree project from Chapter 11, or on binary searching (Section 12.1) and sorting (Chapter 13).

+   **Heavy OOP emphasis.** If students cover sorting and searching elsewhere, there will be time for a heavier emphasis on object-oriented programming. The first four chapters are covered in detail, and then derived classes (Section 14.1) are introduced. At this point, students can do an interesting OOP project, based on the ecosystem of Section 14.2 or the games in Section 14.3. The basic data structures are then covered (Chapters 5–8), with the queue implemented as a derived class (Section 14.3). Finish up with recursion (Chapter 9) and trees (Chapter 10), placing special emphasis on recursive member functions.

+   **Accelerated course.** Assign the first three chapters as independent reading in the first week, and start with Chapter 4 (pointers). This will leave two to three