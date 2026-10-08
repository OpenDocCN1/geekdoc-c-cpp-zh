
## 23.9 Matching with regular expressions
880

## 23.10 References
885

# Chapter 24 Numerics
889

## 24.1 Introduction
890

## 24.2 Size, precision, and overflow
890

### 24.2.1 Numeric limits
894

## 24.3 Arrays
895

## 24.4 C-style multidimensional arrays
896

## 24.5 The Matrix library
897

### 24.5.1 Dimensions and access
898

### 24.5.2 1D Matrix
901

### 24.5.3 2D Matrix
904

### 24.5.4 Matrix I/O
907

### 24.5.5 3D Matrix
907

## 24.6 An example: solving linear equations
908

### 24.6.1 Classical Gaussian elimination
910

### 24.6.2 Pivoting
911

### 24.6.3 Testing
912

## 24.7 Random numbers
914

## 24.8 The standard mathematical functions
917

## 24.9 Complex numbers
919

## 24.10 References
920

# Chapter 25 Embedded Systems Programming
925

## 25.1 Embedded systems
926

## 25.2 Basic concepts
929

### 25.2.1 Predictability
932

### 25.2.2 Ideals
932

### 25.2.3 Living with failure
933

## 25.3 Memory management
935

### 25.3.1 Free-store problems
936

### 25.3.2 Alternatives to the general free store
939

### 25.3.3 Pool example
940

### 25.3.4 Stack example
942

## 25.4 Addresses, pointers, and arrays
943

### 25.4.1 Unchecked conversions
943

### 25.4.2 A problem: dysfunctional interfaces
944

### 25.4.3 A solution: an interface class
947

### 25.4.4 Inheritance and containers
951

## 25.5 Bits, bytes, and words
954

### 25.5.1 Bits and bit operations
955

### 25.5.2 bitset
959

### 25.5.3 Signed and unsigned
961

### 25.5.4 Bit manipulation
965

### 25.5.5 Bitfields
967

### 25.5.6 An example: simple encryption
969

## 25.6 Coding standards
974

### 25.6.1 What should a coding standard be?
975

### 25.6.2 Sample rules
977

### 25.6.3 Real coding standards
983

# Chapter 26 Testing
989

## 26.1 What we want
990

### 26.1.1 Caveat
991

## 26.2 Proofs
992

## 26.3 Testing
992

### 26.3.1 Regression tests
993

### 26.3.2 Unit tests
994

### 26.3.3 Algorithms and non-algorithms
1001

### 26.3.4 System tests
1009

### 26.3.5 Finding assumptions that do not hold
1009

## 26.4 Design for testing
1011

## 26.5 Debugging
1012

## 26.6 Performance
1012

### 26.6.1 Timing
1015

## 26.7 References
1016

# Chapter 27 The C Programming Language
1021

## 27.1 C and C++: siblings
1022

### 27.1.1 C/C++ compatibility
1024

### 27.1.2 C++ features missing from C
1025

### 27.1.3 The C standard library
1027

## 27.2 Functions
1028

### 27.2.1 No function name overloading
1028

### 27.2.2 Function argument type checking
1029

### 27.2.3 Function definitions
1031

### 27.2.4 Calling C from C++ and C++ from C
1032

### 27.2.5 Pointers to functions
1034

## 27.3 Minor language differences
1036

### 27.3.1 struct tag namespace
1036

### 27.3.2 Keywords
1037

### 27.3.3 Definitions
1038

### 27.3.4 C-style casts
1040

### 27.3.5 Conversion of void*
1041

### 27.3.6 enum
1042

### 27.3.7 Namespaces
1042

## 27.4 Free store
1043

## 27.5 C-style strings
1045

### 27.5.1 C-style strings and const
1047

### 27.5.2 Byte operations
1048

### 27.5.3 An example: strcpy()
1049

### 27.5.4 A style issue
1049

## 27.6 Input/output: stdio
1050

### 27.6.1 Output
1050

### 27.6.2 Input
1052

### 27.6.3 Files
1053

## 27.7 Constants and macros
1054

## 27.8 Macros
1055

### 27.8.1 Function-like macros
1056

### 27.8.2 Syntax macros
1058

### 27.8.3 Conditional compilation
1058

## 27.9 An example: intrusive containers
1059

# Part V **Appendices**
1071

## **Appendix A Language Summary**
1073

### A.1 General
1074

#### A.1.1 Terminology
1075

#### A.1.2 Program start and termination
1075

#### A.1.3 Comments
1076

### A.2 Literals
1077

#### A.2.1 Integer literals
1077

#### A.2.2 Floating-point literals
1079

#### A.2.3 Boolean literals
1079

#### A.2.4 Character literals
1079

#### A.2.5 String literals
1080

#### A.2.6 The pointer literal
1081

### A.3 Identifiers
1081

#### A.3.1 Keywords
1081

### A.4 Scope, storage class, and lifetime
1082

#### A.4.1 Scope
1082

#### A.4.2 Storage class
1083

#### A.4.3 Lifetime
1085

### A.5 Expressions
1086

#### A.5.1 User-defined operators
1091

#### A.5.2 Implicit type conversion
1091

#### A.5.3 Constant expressions
1093

#### A.5.4 sizeof
1093

#### A.5.5 Logical expressions
1094

#### A.5.6 new and delete
1094

#### A.5.7 Casts
1095

### A.6 Statements
1096

### A.7 Declarations
1098

#### A.7.1 Definitions
1098

### A.8 Built-in types
1099

#### A.8.1 Pointers
1100

#### A.8.2 Arrays
1101

#### A.8.3 References
1102

### A.9 Functions
1103

#### A.9.1 Overload resolution
1104

#### A.9.2 Default arguments
1105

#### A.9.3 Unspecified arguments
1105

#### A.9.4 Linkage specifications
1106

### A.10 User-defined types
1106

#### A.10.1 Operator overloading
1107

### A.11 Enumerations
1107

### A.12 Classes
1108

#### A.12.1 Member access
1108

#### A.12.2 Class member definitions
1112

#### A.12.3 Construction, destruction, and copy
1112

#### A.12.4 Derived classes
1116

#### A.12.5 Bitfields
1120

#### A.12.6 Unions
1121

### A.13 Templates
1121

#### A.13.1 Template arguments
1122

#### A.13.2 Template instantiation
1123

#### A.13.3 Template member types
1124

### A.14 Exceptions
1125

### A.15 Namespaces
1127

### A.16 Aliases
1128

### A.17 Preprocessor directives
1128

#### A.17.1 #include
1128

#### A.17.2 #define
1129

# Appendix B Standard Library Summary
1131

## B.1 Overview
1132

### B.1.1 Header files
1133

### B.1.2 Namespace std
1136

### B.1.3 Description style
1136

## B.2 Error handling
1137

### B.2.1 Exceptions
1138

## B.3 Iterators
1139

### B.3.1 Iterator model
1140

### B.3.2 Iterator categories
1142

## B.4 Containers
1144

### B.4.1 Overview
1146

### B.4.2 Member types
1147

### B.4.3 Constructors, destructors, and assignments
1148

### B.4.4 Iterators
1148

### B.4.5 Element access
1149

### B.4.6 Stack and queue operations
1149

### B.4.7 List operations
1150

### B.4.8 Size and capacity
1150

### B.4.9 Other operations
1151

### B.4.10 Associative container operations
1151

## B.5 Algorithms
1152

### B.5.1 Nonmodifying sequence algorithms
1153

### B.5.2 Modifying sequence algorithms
1154

### B.5.3 Utility algorithms
1156

### B.5.4 Sorting and searching
1157

### B.5.5 Set algorithms
1159

### B.5.6 Heaps
1160

### B.5.7 Permutations
1160

### B.5.8 min and max
1161

## B.6 STL utilities
1162

### B.6.1 Inserters
1162

### B.6.2 Function objects
1163

### B.6.3 pair and tuple
1165

### B.6.4 initializer_list
1166

### B.6.5 Resource management pointers
1167

## B.7 I/O streams
1168

### B.7.1 I/O streams hierarchy
1170

### B.7.2 Error handling
1171

### B.7.3 Input operations
1172

### B.7.4 Output operations
1173

### B.7.5 Formatting
1173

### B.7.6 Standard manipulators
1173

## B.8 String manipulation
1175

### B.8.1 Character classification
1175

### B.8.2 String
1176

### B.8.3 Regular expression matching
1177

## B.9 Numerics
1180

### B.9.1 Numerical limits
1180

### B.9.2 Standard mathematical functions
1181

### B.9.3 Complex
1182

### B.9.4 valarray
1183

### B.9.5 Generalized numerical algorithms
1183

### B.9.6 Random numbers
1184

## B.10 Time
1185

## B.11 C standard library functions
1185

### B.11.1 Files
1186

### B.11.2 The printf() family
1186

### B.11.3 C-style strings
1191

### B.11.4 Memory
1192

### B.11.5 Date and time
1193

### B.11.6 Etc.
1194

## B.12 Other libraries
1195

# Appendix C Getting Started with Visual Studio
1197

## C.1 Getting a program to run
1198

## C.2 Installing Visual Studio
1198

## C.3 Creating and running a program
1199

### C.3.1 Create a new project
1199

### C.3.2 Use the std_lib_facilities.h header file
1199

### C.3.3 Add a C++ source file to the project
1200

### C.3.4 Enter your source code
1200

### C.3.5 Build an executable program
1200

### C.3.6 Execute the program
1201

### C.3.7 Save the program
1201

## C.4 Later
1201

# Appendix D Installing FLTK
1203

## D.1 Introduction
1204

## D.2 Downloading FLTK
1204

## D.3 Installing FLTK
1205

## D.4 Using FLTK in Visual Studio
1205

## D.5 Testing if it all worked
1206

# Appendix E GUI Implementation
1207

## E.1 Callback implementation
1208

## E.2 Widget implementation
1209

## E.3 Window implementation
1210

## E.4 Vector_ref
1212

## E.5 An example: manipulating Widgets
1213

# Glossary
1217

# Bibliography
1223

# Index
1227

*This page intentionally left blank*

# Preface

> “Damn the torpedoes!  
> Full speed ahead.”  
> —— Admiral Farragut

Programming is the art of expressing solutions to problems so that a computer can execute those solutions. Much of the effort in programming is spent finding and refining solutions. Often, a problem is only fully understood through the process of programming a solution for it.

This book is for someone who has never programmed before but is willing to work hard to learn. It helps you understand the principles and acquire the practical skills of programming using the C++ programming language. My aim is for you to gain sufficient knowledge and experience to perform simple useful programming tasks using the best up-to-date techniques. How long will that take? As part of a first-year university course, you can work through this book in a semester (assuming that you have a workload of four courses of average difficulty). If you work by yourself, don't expect to spend less time than that (maybe 15 hours a week for 14 weeks).

Three months may seem a long time, but there's a lot to learn and you'll be writing your first simple programs after about an hour. Also, all learning is gradual: each chapter introduces new useful concepts and illustrates them with examples inspired by real-world uses. Your ability to express ideas in code – getting a computer to do what you want it to do – gradually and steadily increases as you go along. I never say, "Learn a month's worth of theory and then see if you can use it."
