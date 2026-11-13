
### 2.2 Constructors 45
- The Throttle's Constructor 46
- What Happens If You Write a Class with No Constructors? 49
- Programming Tip: Always Provide Constructors 49
- Revising the Throttle's Member Functions 49
- Inline Member Functions 49
- Programming Tip: When to Use an Inline Member Function 50
- Self-Test Exercises for Section 2.2 51

### 2.3 Using a Namespace, Header File, and Implementation File 51
- Creating a Namespace 51
- The Header File 52
- Describing the Value Semantics of a Class Within the Header File 56
- Programming Tip: Document the Value Semantics 57
- The Implementation File 57
- Using Namespaces in a Namespace 59
- Pitfall: Never Write a Using Statement Actually in a Header File 60
- Self-Test Exercises for Section 2.3 62

### 2.4 Classes and Parameters 63
- Programming Example: The Point Class 63
- Default Arguments 65
- Programming Tip: A Default Constructor Can Be Provided by Using Default Arguments 66
- Arguments 66
- Pitfall: Using Wrong Argument Type for a Reference Parameter 70
- Clarifying the Const Keyword
- Part 3: Const Reference Parameters 72
- Programming Tip: Use const Consistently 73
- When the Type of a Function's Return Value Is a Class 73
- Self-Test Exercises for Section 2.4 74

### 2.5 Operator Overloading 74
- Overloading Binary Comparison Operators 75
- Overloading Binary Arithmetic Operators 76
- Overloading Output and Input Operators 77
- Friend Functions 80
- Programming Tip: When to Use a Friend Function 81
- The Point Class: Putting Things Together 82
- Summary of Operator Overloading 85
- Self-Test Exercises for Section 2.5 85

### 2.6 The Standard Template Library and the Pair Class 86
- Chapter Summary 87
- Solutions to Self-Test Exercises 88
- Programming Projects 90

## CHAPTER 3 CONTAINER CLASSES

### 3.1 The Bag Class 97
- The Bag Class—Specification 98
- C++ Feature: Typedef Statements Within a Class Definition 99
- C++ Feature: The std::size_t Data Type 100
- Clarifying the Const Keyword
- Part 4: Static Member Constants 104
- Older Compilers Do Not Support Initialization of Static Member Constants 105
- The Bag Class—Documentation 105
- Do Not Change the Value Semantics 107
- The Bag Class—Implementation 107
- The Bag Class—Design 109
- Pitfall: The value_type Must Have a Default Constructor 110
- The Invariant of a Class 110
- The Bag Class—Implementation 111
- Pitfall: Needing to Use the Full Type Name bag::size_type 112
- Programming Tip: Make Assertions Meaningful 112
- C++ Feature: The Copy Function from the C++ Standard Library 116
- The Bag Class—Testing the Pieces Together 117
- Programming Tip: Document the Class Invariant in the Implementation File 117
- The Bag Class—Testing 121
- Pitfall: An Object Can Be an Argument to Its Own Member Function 121
- The Bag Class—Analysis 122
- Self-Test Exercises for Section 3.1 123

### 3.2 Programming Project: The Sequence Class 124
- The Sequence Class—Specification 124
- The Sequence Class—Documentation 127
- The Sequence Class—Design 127
- The Sequence Class—Pseudocode for the Implementation 130
- Self-Test Exercises for Section 3.2 132

### 3.3 Interactive Test Programs 133
- C++ Feature: Converting Input to Uppercase Letters 134
- C++ Feature: The Switch Statement 138
- Self-Test Exercises for Section 3.3 138

### 3.4 The STL Multiset Class and Its Iterator 139
- The Multiset Template Class 139
- Some Multiset Members 140
- Iterators and the [...] Pattern 140
- Pitfall: Do Not Access an Iterator's Item After Reaching end() 142
- Testing Iterators for Equality 143
- Other Multiset Operations 143
- Invalid Iterators 144
- Clarifying the Const Keyword
- Part 5: Const Iterators 144
- Pitfall: Changing a Container Object Can Invalidate Its Iterators 144
- Self-Test Exercises for Section 3.4 145

- Chapter Summary 146
- Solutions to Self-Test Exercises 146
- Programming Projects 149

## CHAPTER 4 POINTERS AND DYNAMIC ARRAYS

### 4.1 Pointers and Dynamic Memory 155
- Pointer Variables 156
- Using the Assignment Operator with Pointers 158
- Dynamic Variables and the new Operator 159
- Using new to Allocate Dynamic Arrays 160
- The Heap and the bad_alloc Exception 163
- The delete Operator 163
- Programming Tip: Define Pointer Types 164
- Self-Test Exercises for Section 4.1 165

### 4.2 Pointers and Arrays as Parameters 166
- Clarifying the const Keyword 166
- Self-Test Exercise: Constant Parameters That Are Pointers or Arrays 171
- Self-Test Exercises for Section 4.2 173

### 4.3 The Bag Class with a Dynamic Array 176
- Pointer Member Variables 176
- Member Functions Allocate Dynamic Memory as Needed 177
- Programming Tip: Provide Documentation about Possible Dynamic Memory Failure 181
- Value Semantics 181
- The Destructor 181
- The Revised Bag Class—Class Definition 185
- The Revised Bag Class—Implementation 187
- Programming Tip: How to Check for Self-Assignment 188
- Programming Tip: How to Allocate Memory in a Member Function 191
- The Revised Bag Class—Putting the Pieces Together 192
- Self-Test Exercises for Section 4.3 194

### 4.4 Prescription for a Dynamic Class 195
- Four Rules 195
- Special Importance of the Copy Constructor 195
- Pitfall: Using Dynamic Memory Requires a Destructor, a Copy Constructor, and an Overloaded Assignment Operator 196
- Self-Test Exercises for Section 4.4 197

### 4.5 The STL String Class and a Project 197
- Null-Terminated Strings 197
- Initializing a String Variable 198
- The Empty String 198
- Reading and Writing String Variables 199
- Pitfall: Using = and == with Strings 199
- The strcat Function 199
- The strcat Function 200
- Pitfall: Dangers of strcpy, strcat, and Reading Strings 200
- The strlen Function 201
- The strcmp Function 201
- The String Class Specification 201
- Constructors and the Destructor 201
- Constant Member Functions 203
- Overloading the Operator [] 204
- Some Further Overloading 204
- Other Operations for the String Class 205
- The String Class—Design 205
- The String Class—Implementation 206
- Demonstration Program for the String Class 208
- Chaining the Output Operator 210
- Declaring Constant Objects 210
- Constant Member Functions 210
- Using Overloaded Operations in Expressions 211
- Our String Class Versus the C++ Library String Class 211
- Self-Test Exercises for Section 4.5 211

### 4.6 Programming Project: The Polynomial 212
- Chapter Summary 216
- Solutions to Self-Test Exercises 216
- Programming Projects 218

## CHAPTER 5 LINKED LISTS

### 5.1 A Fundamental Node Class for Linked Lists 221
- Declaring a Class for Nodes 221
- Using a Typedef Statement with Linked-List Nodes 222
- Head Pointers, Tail Pointers 223
- The Null Pointer 224
- The Meaning of a Null Head Pointer or Tail Pointer 224
- The Node Constructor 224
- The Node Member Functions 225
- The Member Selection Operator 226
- Clarifying the Syntax
- Part 7: The Constructor with a Pointer to a Node, and the Need for Two Versions of Some Member Functions 227
- Programming Tip: A Rule for a Node's Constant Member Functions 228
- Pitfall: Dereferencing the Null Pointer 230
- Self-Test Exercises for Section 5.1 230

### 5.2 A Linked-List Toolkit 231
- Linked-List Toolkit—Header File 232
- Computing the Length of a Linked List 232
- Programming Tip: How to Traverse a Linked List 235
- Pitfall: Forgetting to Test the Empty List 236
- Parameters for Linked Lists 236
- Inserting a New Node at the Head of a Linked List 238
- Inserting a New Node That Is Not at the Head 240
- Pitfall: Unintended Calls to delete and new 243
- Searching for an Item in a Linked List 245
- Finding a Node by Its Position in a Linked List 246
- Copying a Linked List 247
- Removing a Node That Is Not the Head of a Linked List 250
- Removing a Node That Is Not at the Head 251
- Clearing a Linked List 252
- Linked-List Toolkit—Putting the Pieces Together 253
- Using the Linked-List Toolkit 254
- Self-Test Exercises for Section 5.2 258

### 5.3 The Bag Class with a Linked List 259
- Our Third Bag—Specification 259
- Our Third Bag—Class Definition 259
- How to Make the Bag value_type Match the Node value_type 260
- Reusing the Code for Dynamic Memory Usage in a Class 263
- The Third Bag Class Implementation 264
- Pitfall: The Assignment Operator Causes Trouble with Linked Lists 265
- Programming Tip: How to Choose Between Approaches 267
- The Third Bag Class—Putting the Pieces Together 271
- Self-Test Exercises for Section 5.3 272

### 5.4 Programming Project: The Sequence Class with a Linked List 275
- The Revised Sequence Class—Design Suggestions 275
- The Revised Sequence Class—Value Semantics 276
- Self-Test Exercises for Section 5.4 277

### 5.5 Dynamic Arrays vs. Linked Lists vs. Doubly Linked Lists 277
- Making the Decision 279
- Self-Test Exercises for Section 5.5 279

### 5.6 STL Vectors vs. STL Lists vs. STL Deques 280
- Self-Test Exercises for Section 5.6 282

- Chapter Summary 283
- Solutions to Self-Test Exercises 283
- Programming Projects 287
