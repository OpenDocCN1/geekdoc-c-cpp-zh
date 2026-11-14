
## Discovering Modern C++

An Intensive Course for Scientists, Engineers, and Programmers

Peter Gottschling

![](img/ba4defb7bf504868bf19451f3cd4b9bb_0_0.png)

C++ In-Depth Series Bjarne Stroustrup

Digitized by the Internet Archive in 2023 with funding from Kahle/Austin Foundation

## C++ In-Depth Series

## Discovering Modern C++

## C++ In-Depth Series

Bjarne Stroustrup, Consulting Editor

![](img/ba4defb7bf504868bf19451f3cd4b9bb_3_0.png)

Visit informit.com/series/indepth for a complete list of available publications.

The C++ In-Depth Series is a collection of concise and focused books that provide real-world programmers with reliable information about the C++ programming language. Selected by the designer and original implementer of C++, Bjarne Stroustrup, and written by carefully chosen experts in the field, each book in this series presents either a single topic, at a technical level appropriate to that topic, or a fast-paced overview, for a quick understanding of broader language features. In either case, the series' practical approach is designed to lift professionals (and aspiring professionals) to the next level of programming skill or knowledge.

Make sure to connect with us informit.com/socialconnect

informit.com Addison-Wesley Safari

## Discovering Modern C++

### An Intensive Course for Scientists, Engineers, and Programmers

Peter Gottschling

### Addison-Wesley

Boston • Columbus • Indianapolis • New York • San Francisco • Amsterdam • Cape Town
Dubai • London • Madrid • Milan • Munich • Paris • Montreal • Toronto • Delhi • Mexico City
Sao Paulo • Sidney • Hong Kong • Seoul • Singapore • Taipei • Tokyo

## Contents

### Preface

- Reasons to Learn C++ ... xvii
- Reasons to Read This Book ... xvii
- The Beauty and the Beast ... xviii
- Languages in Science and Engineering ... xix
- Typographical Conventions ... xx

### Acknowledgments ... xxiii

### About the Author ... xxv

### Chapter 1 C++ Basics ... 1

- 1.1 Our First Program ... 1
- 1.2 Variables ... 3
  - 1.2.1 Constants ... 5
  - 1.2.2 Literals ... 6
  - 1.2.3 Non-narrowing Initialization ... 7
  - 1.2.4 Scopes ... 8
- 1.3 Operators ... 10
  - 1.3.1 Arithmetic Operators ... 11
  - 1.3.2 Boolean Operators ... 14
  - 1.3.3 Bitwise Operators ... 15
  - 1.3.4 Assignment ... 15
  - 1.3.5 Program Flow ... 16
  - 1.3.6 Memory Handling ... 17
  - 1.3.7 Access Operators ... 17
  - 1.3.8 Type Handling ... 17
  - 1.3.9 Error Handling ... 18
  - 1.3.10 Overloading ... 18
  - 1.3.11 Operator Precedence ... 18
  - 1.3.12 Avoid Side Effects! ... 18
- 1.4 Expressions and Statements ... 21
  - 1.4.1 Expressions ... 21
  - 1.4.2 Statements ... 21
  - 1.4.3 Branching ... 22
  - 1.4.4 Loops ... 24
  - 1.4.5 goto ... 27
- 1.5 Functions ... 28
  - 1.5.1 Arguments ... 28
  - 1.5.2 Returning Results ... 30
  - 1.5.3 Inlining ... 31
  - 1.5.4 Overloading ... 31
  - 1.5.5 main Function ... 33
- 1.6 Error Handling ... 34
  - 1.6.1 Assertions ... 34
  - 1.6.2 Exceptions ... 35
  - 1.6.3 Static Assertions ... 40
- 1.7 I/O ... 40
  - 1.7.1 Standard Output ... 40
  - 1.7.2 Standard Input ... 41
  - 1.7.3 Input/Output with Files ... 41
  - 1.7.4 Generic Stream Concept ... 42
  - 1.7.5 Formatting ... 43
  - 1.7.6 Dealing with I/O Errors ... 44
- 1.8 Arrays, Pointers, and References ... 47
  - 1.8.1 Arrays ... 47
  - 1.8.2 Pointers ... 49
  - 1.8.3 Smart Pointers ... 51
  - 1.8.4 References ... 55
  - 1.8.5 Comparison between Pointers and References ... 55
  - 1.8.6 Do Not Refer to Outdated Data! ... 55
  - 1.8.7 Containers for Arrays ... 56
- 1.9 Structuring Software Projects ... 58
  - 1.9.1 Comments ... 59
  - 1.9.2 Preprocessor Directives ... 60
- 1.10 Exercises ... 63
  - 1.10.1 Age ... 63
  - 1.10.2 Arrays and Pointers ... 64
  - 1.10.3 Read the Header of a Matrix Market File ... 64

### Chapter 2 Classes ... 65

- 2.1 Program for Universal Meaning Not for Technical Details ... 65
- 2.2 Members ... 67
  - 2.2.1 Member Variables ... 67
  - 2.2.2 Accessibility ... 68
  - 2.2.3 Access Operators ... 70
  - 2.2.4 The Static Declarator for Classes ... 70
  - 2.2.5 Member Functions ... 71
- 2.3 Setting Values: Constructors and Assignments ... 72
  - 2.3.1 Constructors ... 72
  - 2.3.2 Assignment ... 81
  - 2.3.3 Initializer Lists ... 82
  - 2.3.4 Uniform Initialization ... 83
  - 2.3.5 Move Semantics ... 85
- 2.4 Destructors ... 89
  - 2.4.1 Implementation Rules ... 89
  - 2.4.2 Dealing with Resources Properly ... 90
- 2.5 Method Generation Résumé ... 95
- 2.6 Accessing Member Variables ... 96
  - 2.6.1 Access Functions ... 96
  - 2.6.2 Subscription Operator ... 97
  - 2.6.3 Constant Member Functions ... 98
  - 2.6.4 Reference-Qualified Members ... 99
- 2.7 Operator Overloading Design ... 100
  - 2.7.1 Be Consistent! ... 101
  - 2.7.2 Respect the Priority ... 101
  - 2.7.3 Member or Free Function ... 102
- 2.8 Exercises ... 104
  - 2.8.1 Polynomial ... 104
  - 2.8.2 Move Assignment ... 104
  - 2.8.3 Initializer List ... 105
  - 2.8.4 Resource Rescue ... 105

### Chapter 3 Generic Programming ... 107

- 3.1 Function Templates ... 107
  - 3.1.1 Instantiation ... 108
  - 3.1.2 Parameter Type Deduction ... 109
  - 3.1.3 Dealing with Errors in Templates ... 113
  - 3.1.4 Mixing Types ... 113
  - 3.1.5 Uniform Initialization ... 115
  - 3.1.6 Automatic return Type ... 115
- 3.2 Namespaces and Function Lookup ... 115
  - 3.2.1 Namespaces ... 115
  - 3.2.2 Argument-Dependent Lookup ... 118
  - 3.2.3 Namespace Qualification or ADL ... 122
- 3.3 Class Templates ... 123
  - 3.3.1 A Container Example ... 124
  - 3.3.2 Designing Uniform Class and Function Interfaces ... 125
- 3.4 Type Deduction and Definition ... 131
  - 3.4.1 Automatic Variable Type ... 131
  - 3.4.2 Type of an Expression ... 132
  - 3.4.3 decltype(auto) ... 133
  - 3.4.4 Defining Types ... 134
- 3.5 A Bit of Theory on Templates: Concepts ... 136
- 3.6 Template Specialization ... 136
  - 3.6.1 Specializing a Class for One Type ... 137
  - 3.6.2 Specializing and Overloading Functions ... 139
  - 3.6.3 Partial Specialization ... 141
  - 3.6.4 Partially Specializing Functions ... 142
- 3.7 Non-Type Parameters for Templates ... 144
- 3.8 Functors ... 146
  - 3.8.1 Function-like Parameters ... 148
  - 3.8.2 Composing Functors ... 149
  - 3.8.3 Recursion ... 150
  - 3.8.4 Generic Reduction ... 153
- 3.9 Lambda ... 154
  - 3.9.1 Capture ... 155
  - 3.9.2 Capture by Value ... 156
  - 3.9.3 Capture by Reference ... 157
  - 3.9.4 Generalized Capture ... 158
  - 3.9.5 Generic Lambdas ... 159
- 3.10 Variadic Templates ... 159
- 3.11 Exercises ... 161
  - 3.11.1 String Representation ... 161
  - 3.11.2 String Representation of Tuples ... 161
  - 3.11.3 Generic Stack ... 161
  - 3.11.4 Iterator of a Vector ... 162
  - 3.11.5 Odd Iterator ... 162
  - 3.11.6 Odd Range ... 162
  - 3.11.7 Stack of bool ... 162
  - 3.11.8 Stack with Custom Size ... 163
  - 3.11.9 Deducing Non-type Template Arguments ... 163
  - 3.11.10 Trapezoid Rule ... 163
  - 3.11.11 Functor ... 164
  - 3.11.12 Lambda ... 164
  - 3.11.13 Implement make_unique ... 164

### Chapter 4 Libraries ... 165

- 4.1 Standard Template Library ... 165
  - 4.1.1 Introductory Example ... 166
  - 4.1.2 Iterators ... 166
  - 4.1.3 Containers ... 171
  - 4.1.4 Algorithms ... 179
  - 4.1.5 Beyond Iterators ... 185
- 4.2 Numerics ... 186
  - 4.2.1 Complex Numbers ... 186
  - 4.2.2 Random Number Generators ... 189
- 4.3 Meta-programming ... 198
  - 4.3.1 Limits ... 198
  - 4.3.2 Type Traits ... 200
- 4.4 Utilities ... 202
  - 4.4.1 Tuple ... 202
  - 4.4.2 function ... 205
  - 4.4.3 Reference Wrapper ... 207
- 4.5 The Time Is Now ... 209
- 4.6 Concurrency ... 211
- 4.7 Scientific Libraries Beyond the Standard ... 213
  - 4.7.1 Other Arithmetics ... 214
  - 4.7.2 Interval Arithmetic ... 214
  - 4.7.3 Linear Algebra ... 214
  - 4.7.4 Ordinary Differential Equations ... 215
  - 4.7.5 Partial Differential Equations ... 215
  - 4.7.6 Graph Algorithms ... 215
- 4.8 Exercises ... 215
  - 4.8.1 Sorting by Magnitude ... 215
  - 4.8.2 STL Container ... 216
  - 4.8.3 Complex Numbers ... 216

### Chapter 5 Meta-Programming ... 219

- 5.1 Let the Compiler Compute ... 219
  - 5.1.1 Compile-Time Functions ... 219
  - 5.1.2 Extended Compile-Time Functions ... 221
  - 5.1.3 Primeness ... 223
  - 5.1.4 How Constant Are Our Constants? ... 225
- 5.2 Providing and Using Type Information ... 226
  - 5.2.1 Type Traits ... 226
  - 5.2.2 Conditional Exception Handling ... 229
  - 5.2.3 A const-Clean View Example ... 230
  - 5.2.4 Standard Type Traits ... 237
  - 5.2.5 Domain-Specific Type Properties ... 237
  - 5.2.6 enable-if ... 239
  - 5.2.7 Variadic Templates Revised ... 242
- 5.3 Expression Templates ... 245
  - 5.3.1 Simple Operator Implementation ... 245
  - 5.3.2 An Expression Template Class ... 248
  - 5.3.3 Generic Expression Templates ... 251
- 5.4 Meta-Tuning: Write Your Own Compiler Optimization ... 253
  - 5.4.1 Classical Fixed-Size Unrolling ... 254
  - 5.4.2 Nested Unrolling ... 257
  - 5.4.3 Dynamic Unrolling-Warm-up ... 263
  - 5.4.4 Unrolling Vector Expressions ... 265
  - 5.4.5 Tuning an Expression Template ... 266
  - 5.4.6 Tuning Reduction Operations ... 269
  - 5.4.7 Tuning Nested Loops ... 276
  - 5.4.8 Tuning Résumé ... 282
- 5.5 Exercises ... 283
  - 5.5.1 Type Traits ... 283
  - 5.5.2 Fibonacci Sequence ... 283
  - 5.5.3 Meta-Program for Greatest Common Divisor ... 283
  - 5.5.4 Vector Expression Template ... 284
  - 5.5.5 Meta-List ... 285

### Chapter 6 Object-Oriented Programming ... 287

- 6.1 Basic Principles ... 287
  - 6.1.1 Base and Derived Classes ... 288
  - 6.1.2 Inheriting Constructors ... 291
  - 6.1.3 Virtual Functions and Polymorphic Classes ... 292
  - 6.1.4 Functors via Inheritance ... 297
