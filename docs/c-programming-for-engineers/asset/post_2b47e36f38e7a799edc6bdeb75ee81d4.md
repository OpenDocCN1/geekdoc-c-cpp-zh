
# Contents

10.2.5 Function Prototypes . . . . . . . . . . . . . . . . . . 145
10.3 Variable Scope and Storage Classes . . . . . . . . . . . . 147
10.4 Type Conversion During Function Calls . . . . . . . . . . . . 151
10.5 Passing Arrays to Functions . . . . . . . . . . . . 152
10.5.1 Passing Array Size as a Separate Parameter . 152
10.5.2 Using First Element as Size Indicator . . 153
10.5.3 Using Sentinels . . . . . . . . . . . . . . . . 154
10.5.4 Processing Strings . . . . . . . . . . . . 155
10.6 Recursive Functions . . . . . . . . . . . . 156
10.6.1 Principles of Recursion . . . . . . . 156
10.6.2 Advantages of Recursion . . . . . . 156
10.7 More Examples . . . . . . . . . . . . . 157
10.7.1 Checking if a Number is Even . . . . 157
10.7.2 Printing Binary Representation . . . 157
10.7.3 Counting Bits in Binary Representation . . 158
10.7.4 An Improved Approach: Brian Kernighan's Algorithm 158
10.7.5 Checking if a Number is a Power of Two . 159
10.8 Library Functions . . . . . . . . . . . . 160
10.8.1 Math Library . . . . . . . . . . . 160
10.8.2 String Library . . . . . . . . . . . 161
10.8.3 Standard Library . . . . . . . 164

## 11 File Input/Output . . . . . . . . . . . 169
11.1 Opening and Closing Files . . . . . . . 169
11.2 Reading from Files . . . . . . . . . . . . . . . 170
11.2.1 Functions for Reading from Files . 170
11.2.2 Handling Different Data Types when Reading from Files . 171
11.2.3 Error Handling when Reading from Files . 171
11.3 Writing to Files . . . . . . . . . . . . 172
11.3.1 Functions for Writing to Files . . . 172
11.3.2 Writing Different Data Types to Files . . 173
11.3.3 Error Handling when Writing to Files . . . 173
11.4 File Positioning . . . . . . . . . 174
11.5 Working with Text Files . . . . . . . 174
11.5.1 Manipulating Text Files using C . . . 175
11.5.2 Reading and Writing CSV Files . . 175
11.6 Working with Binary Files . . . . . . . 176

## 12 Pointers . . . . . . . . . . . . . . . . . 179
12.1 Introduction to Pointers . . . . . . . . 179
12.1.1 Definition and Purpose of Pointers . . . 179
12.1.2 Pointer Declaration and Initialization . . 180
12.1.3 Understanding Memory Addresses . . 180
12.1.4 Accessing the Value Stored at a Pointer Address . 181
12.2 Pointer Arithmetic . . . . . . . . . . . . . . . . . . . . 182
12.3 Pointers and Arrays . . . . . . . . . . . . . . . . . . . . . 183
12.4 Pointers and Strings . . . . . . . . . . . . . . . . . . . . 184
12.5 Pointers and Functions . . . . . . . . . . . . . . . . . . . . 186
12.5.1 Pointer to Functions . . . . . . . . . . . . . . . . . . . . 186
12.5.2 Exchanging Data with Functions . . . . . . . . 186
12.6 Dynamic Memory Allocation . . . . . . . . . . . . . . . . . 188
12.7 Null Pointers . . . . . . . . . . . . . . . . . . . . . . . . 189
12.8 Advanced Pointer Concepts . . . . . . . . . . . . . . . . 191
12.8.1 Void Pointers . . . . . . . . . . . . . . . . . . . . . . . 191
12.8.2 Pointer Casting . . . . . . . . . . . . . . . . . . . . 192
12.8.3 Dangling Pointers . . . . . . . . . . . . . . . . . . . . 192
12.8.4 Wild Pointers . . . . . . . . . . . . . . . . . . . . . 194
12.8.5 Pointers to Pointers . . . . . . . . . . . . . . . 194
12.9 Hardware Access in Raspberry Pi . . . . . . . . . . 196

# Structured Data 199
13.1 Structs: Defining Custom Data Types . . . . . . . 199
13.1.1 Syntax and Declaration of Structs . . . . . . . . 199
13.1.2 Accessing Struct Members . . . . . . . . . . . . . . 200
13.1.3 Pointers to Structures . . . . . . . . . . . . . 201
13.1.4 Nested Structs . . . . . . . . . . . . . . . . . . . . 202
13.1.5 Passing Structs to Functions . . . . . . . . 203
13.1.6 Returning Structs from Functions . . . 203
13.2 Unions: A Special Kind of Struct . . . . . . . . . . 203
13.3 Typedef: Simplifying Data Type Declarations . . . . 205
13.4 Enums: Improving Program Readability . . . . . . . 206
13.5 Bit Fields . . . . . . . . . . . . . . . . . . . . . . . . . . . 207
13.6 Data Structures . . . . . . . . . . . . . . . . . . . . . . 208
13.6.1 Linked Lists . . . . . . . . . . . . . . . . . . . . . 209
13.6.2 Queues . . . . . . . . . . . . . . . . . . . . . 212
13.6.3 Stacks . . . . . . . . . . . . . . . . . . . . . . 215

## 14 Preprocessor 219
14.1 Introduction . . . . . . . . . 219
14.2 File Inclusion . . . . . . . . . . . . . . . 219
14.3 Substitution . . . . . . . . . . . . . . 221
14.3.1 How Macros Work . . . . . . . . . . . . 221
14.3.2 Predefined Macros . . . . . . . . . . . . 222
14.3.3 Side Effects and Pitfalls . . . . . . . . . . 222
14.4 Conditional Compilation . . . . . . . . . . . . 224
14.5 Miscellaneous Preprocessor . . . . . . . . . . . 225
14.5.1 The #pragma Directive . . . . . . . . . . . . . . . 225
14.5.2 The #error Directive . . . . . . . . . . . . . . . 225
14.5.3 The #line Directive . . . . . . . . . . . . . . . 226

## 15 Engineering . . . . . . . . . . . . . . 227
15.1 What You Need . . . . . . . . . . . . . . 227
15.2 Engineering vs Regular C . . . . . . . . . . . . . 228
15.3 Embedded Boards . . . . . . . . . . . . . . . 230
15.3.1 Unique Data . . . . . . . . . . . . . . . . 231
15.3.2 Practical I/O . . . . . . . . . . . . . . . . 232
15.3.3 Standard Library . . . . . . . . . . . . . . . 235
15.4 Hello World . . . . . . . . . . . . . . . . 236
15.5 Resource-constrained . . . . . . . . . . . . . . . 238
15.6 Multitasking . . . . . . . . . . . . . . . . . 241
15.7 Sequence . . . . . . . . . . . . . . . . . . . 242
15.8 Reading from . . . . . . . . . . . . . . . . . . 244
15.9 Switch . . . . . . . . . . . . . . . . . . . . 244
