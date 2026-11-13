# # CHAPTER 3 CONTAINER CLASSES

+   3.1 The Bag Class 97
+       The Bag Class—Specification 98
+       C++ Feature: Typedef Statements Within a Class Definition 99
+       C++ Feature: The std::size_t Data Type 100
+       Clarifying the Const Keyword
+           Part 4: Static Member Constants 104
+       Older Compilers Do Not Support Initialization of Static Member Constants 105
+       The Bag Class—Documentation 105
+       Do Not Change the Value Semantics 107
+       The Bag Class—Implementation 107
+       The Bag Class—Design 109
+       Pitfall: The value_type Must Have a Default Constructor 110
+       The Invariant of a Class 110
+       The Bag Class—Implementation 111
+       Pitfall: Needing to Use the Full Type Name bag::size_type 112
+       Programming Tip: Make Assertions Meaningful 112
+       C++ Feature: The Copy Function from the C++ Standard Library 116
+       The Bag Class—Testing the Pieces Together 117
+       Programming Tip: Document the Class Invariant in the Implementation File 117
+       The Bag Class—Testing 121
+       Pitfall: An Object Can Be an Argument to Its Own Member Function 121
+       The Bag Class—Analysis 122
+       Self-Test Exercises for Section 3.1 123

+   3.2 Programming Project: The Sequence Class 124
+       The Sequence Class—Specification 124
+       The Sequence Class—Documentation 127
+       The Sequence Class—Design 127
+       The Sequence Class—Pseudocode for the Implementation 130
+       Self-Test Exercises for Section 3.2 132

+   3.3 Interactive Test Programs 133
+       C++ Feature: Converting Input to Uppercase Letters 134
+       C++ Feature: The Switch Statement 138
+       Self-Test Exercises for Section 3.3 138

+   3.4 The STL Multiset Class and Its Iterator 139
+       The Multiset Template Class 139
+       Some Multiset Members 140
+       Iterators and the [...] Pattern 140
+       Pitfall: Do Not Access an Iterator's Item After Reaching end( ) 142
+       Testing Iterators for Equality 143
+       Other Multiset Operations 143
+       Invalid Iterators 144
+       Clarifying the Const Keyword
+           Part 5: Const Iterators 144
+       Pitfall: Changing a Container Object Can Invalidate Its Iterators 144
+       Self-Test Exercises for Section 3.4 145

+   Chapter Summary 146
+   Solutions to Self-Test Exercises 146
+   Programming Projects 149