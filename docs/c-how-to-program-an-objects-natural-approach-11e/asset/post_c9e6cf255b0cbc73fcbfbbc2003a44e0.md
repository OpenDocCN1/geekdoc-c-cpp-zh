
### 17.4 Launching Tasks with `std::jthread` — 1003
- 17.4.1 Defining a Task to Perform in a Thread — 1003
- 17.4.2 Executing a Task in a `jthread` — 1005
- 17.4.3 How `jthread` Fixes `thread` — 1007

### 17.5 Producer–Consumer Relationship: A First Attempt — 1008

### 17.6 Producer–Consumer: Synchronizing Access to Shared Mutable Data — 1015
- 17.6.1 Class SynchronizedBuffer: Mutexes, Locks and Condition Variables — 1017
- 17.6.2 Testing SynchronizedBuffer — 1023

### 17.7 Producer–Consumer: Minimizing Waits with a Circular Buffer — 1027

### 17.8 Readers and Writers — 1036

### 17.9 Cooperatively Canceling `jthreads` — 1037

### 17.10 Launching Tasks with `std::async` — 1040

### 17.11 Thread-Safe, One-Time Initialization — 1047

### 17.12 A Brief Introduction to Atomics — 1048

### 17.13 Coordinating Threads with C++20 Latches and Barriers — 1052
- 17.13.1 C++20 `std::latch` — 1052
- 17.13.2 C++20 `std::barrier` — 1055

### 17.14 C++20 Semaphores — 1058

### 17.15 C++23: A Look to the Future of C++ Concurrency — 1062
- 17.15.1 Parallel Ranges Algorithms — 1062
- 17.15.2 Concurrent Containers — 1062
- 17.15.3 Other Concurrency-Related Proposals — 1063

### 17.16 Wrap-Up — 1063

## 18 C++20 Coroutines — 1073
### 18.1 Introduction — 1074
### 18.2 Coroutine Support Libraries — 1075
### 18.3 Installing the concurrentpp and generator Libraries — 1077
### 18.4 Creating a Generator Coroutine with `co_yield` and the generator Library — 1077
### 18.5 Launching Tasks with concurrentpp — 1081
### 18.6 Creating a Coroutine with `co_await` and `co_return` — 1085
### 18.7 Low-Level Coroutines Concepts — 1093
### 18.8 Future Coroutines Enhancements — 1096
### 18.9 Wrap-Up — 1096

## 19 Stream I/O & C++20 Text Formatting — 1101
### 19.1 Introduction — 1102
### 19.2 Streams — 1102
- 19.2.1 Classic Streams vs. Standard Streams — 1103
- 19.2.2 `iostream` Library Headers — 1103
- 19.2.3 Stream Input/Output Classes and Objects — 1103

### 19.3 Stream Output — 1104
- 19.3.1 Output of `char*` Variables — 1105
- 19.3.2 Character Output Using Member Function `put` — 1106

### 19.4 Stream Input — 1106
- 19.4.1 `get` and `getline` Member Functions — 1106
- 19.4.2 `istream` Member Functions `peek`, `putback` and `ignore` — 1109

### 19.5 Unformatted I/O Using `read`, `write` and `gcount` — 1110

### 19.6 Stream Manipulators — 1111
- 19.6.1 Integral Stream Base: `dec`, `oct`, `hex` and `setbase` — 1112
- 19.6.2 Floating-Point Precision (`setprecision`, `precision`) — 1112
- 19.6.3 Field Width (`width`, `setw`) — 1114
- 19.6.4 User-Defined Output Stream Manipulators — 1115
- 19.6.5 Trailing Zeros and Decimal Points (`showpoint`) — 1116
- 19.6.6 Alignment (`left`, `right` and `internal`) — 1117
- 19.6.7 Padding (`fill`, `setfill`) — 1118
- 19.6.8 Integral Stream Base (`dec`, `oct`, `hex`, `showbase`) — 1119
- 19.6.9 Floating-Point Numbers; Scientific and Fixed Notation (`scientific`, `fixed`) — 1120
- 19.6.10 Uppercase/Lowercase Control (`uppercase`) — 1121
- 19.6.11 Specifying Boolean Format (`boolalpha`) — 1122
- 19.6.12 Setting and Resetting the Format State via Member Function `flags` — 1123

### 19.7 Stream Error States — 1124

### 19.8 Tying an Output Stream to an Input Stream — 1127

### 19.9 C++20 Text Formatting — 1127
- 19.9.1 C++20 `std::format` Presentation Types — 1128
- 19.9.2 C++20 `std::format` Field Widths and Alignment — 1130
- 19.9.3 C++20 `std::format` Numeric Formatting — 1131
- 19.9.4 C++20 `std::format` Field Width and Precision Placeholders — 1132

### 19.10 Wrap-Up — 1133

## 20 Other Topics and a Look Toward the Future of C++ — 1141
### 20.1 Introduction — 1142
### 20.2 `shared_ptr` and `weak_ptr` Smart Pointers — 1143
- 20.2.1 Reference Counted `shared_ptr` — 1143
- 20.2.2 `weak_ptr`: `shared_ptr` Observer — 1147

### 20.3 Runtime Polymorphism with `std::variant` and `std::visit` — 1154

### 20.4 protected Class Members: A Deeper Look — 1160

### 20.5 Non-Virtual Interface (NVI) Idiom — 1161

### 20.6 Inheriting Base-Class Constructors — 1168

### 20.7 Multiple Inheritance — 1169
- 20.7.1 Diamond Inheritance — 1174
- 20.7.2 Eliminating Duplicate Subobjects with `virtual` Base-Class Inheritance — 1176

### 20.8 public, protected and private Inheritance — 1177

### 20.9 namespaces: A Deeper Look — 1179
- 20.9.1 Defining namespaces — 1180
- 20.9.2 Accessing namespace Members with Qualified Names — 1181
- 20.9.3 using Directives Should Not Be Placed in Headers — 1181
- 20.9.4 Nested Namespaces — 1181
- 20.9.5 Aliases for namespace Names — 1181

### 20.10 Storage Classes and Storage Duration — 1182
- 20.10.1 Storage Duration — 1182
- 20.10.2 Local Variables and Automatic Storage Duration — 1182
- 20.10.3 Static Storage Duration — 1183
- 20.10.4 mutable Class Members — 1184

### 20.11 Operator Keywords — 1185

### 20.12 decltype Operator — 1186

### 20.13 Trailing Return Types for Functions — 1187

### 20.14 [[nodiscard]] Attribute — 1187

### 20.15 Some Key C++23 Features — 1189

### 20.16 Wrap-Up — 1194

## 21 Computer Science Thinking: Searching, Sorting and Big O — 1197
### 21.1 Introduction — 1198
### 21.2 Efficiency of Algorithms: Big O — 1199
- 21.2.1 O(1) Algorithms — 1199
- 21.2.2 O(n) Algorithms — 1199
- 21.2.3 O(n²) Algorithms — 1200

### 21.3 Linear Search — 1201
- 21.3.1 Implementation — 1201
- 21.3.2 Efficiency of Linear Search — 1202

### 21.4 Binary Search — 1203
- 21.4.1 Implementation — 1203
- 21.4.2 Efficiency of Binary Search — 1207

### 21.5 Insertion Sort — 1208
- 21.5.1 Implementation — 1209
- 21.5.2 Efficiency of Insertion Sort — 1210

### 21.6 Selection Sort — 1210
- 21.6.1 Implementation — 1211
- 21.6.2 Efficiency of Selection Sort — 1213

### 21.7 Merge Sort (A Recursive Implementation) — 1213
- 21.7.1 Implementation — 1214
- 21.7.2 Efficiency of Merge Sort — 1219
- 21.7.3 Summarizing Various Algorithms’ Big O Notations — 1219

### 21.8 Wrap-Up — 1221

## Index — 1225
