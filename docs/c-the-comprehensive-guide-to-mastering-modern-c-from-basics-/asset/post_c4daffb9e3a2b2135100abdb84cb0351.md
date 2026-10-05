
## 23.7.7 Automatically Merged

## 23.7.8 Unicode Literals

## Part IV The Standard Library

## 24 CONTAINERS

### 24.1 Basics
- 24.1.1 Recurring
- 24.1.2 Abstract
- 24.1.3 Operations
- 24.1.4 Complexity
- 24.1.5 Containers and Their Iterators
- 24.1.6 Ranges Simplify Iterators
- 24.1.7 Ranges, Views, Concepts, Adapters, Generators, and Algorithms
- 24.1.8 Algorithms

### 24.2 Iterator Basics
- 24.2.1 Iterators from Containers
- 24.2.2 More Functionality with Iterators

### 24.3 Allocators: Memory Issues

### 24.4 Container Commonalities

### 24.5 An Overview of the Standard Container Classes
- 24.5.1 Type Aliases of Containers

### 24.6 The Sequential Container Classes
- 24.6.1 Commonalities and Differences
- 24.6.2 Methods of Sequence Containers
- 24.6.3 "vector"
- 24.6.4 "array"
- 24.6.5 "deque"
- 24.6.6 "list"
- 24.6.7 "forward_list"

### 24.7 Associative and Ordered
- 24.7.1 Commonalities and Differences
- 24.7.2 Methods of Ordered Associative Containers
- 24.7.3 "set"
- 24.7.4 "map"
- 24.7.5 "multiset"
- 24.7.6 "multimap"

### 24.8 Only Associative and Not Guaranteed
- 24.8.1 Hash Tables
- 24.8.2 Commonalities and Differences
- 24.8.3 Methods of Unordered Associative Containers
- 24.8.4 "unordered_set"
- 24.8.5 "unordered_map"
- 24.8.6 "unordered_multiset"
- 24.8.7 "unordered_multimap"

### 24.9 Container Adapters

### 24.10 Special Cases: "string", "basic_string", and "vector<char>"
### 24.11 Special Cases: "vector<bool>", "array<bool,n>", and "bitset<n>"
- 24.11.1 Dynamic and Compact: "vector<bool>"
- 24.11.2 Static: "array<bool,n>" and bitset<n>"

### 24.12 Special Case: Value Array with valarray<>
- 24.12.1 Element Properties
- 24.12.2 Initialize
- 24.12.3 Assignment
- 24.12.4 Insert and Delete
- 24.12.5 Accessing
- 24.12.6 Specialty: Manipulate All Data
- 24.12.7 Specialty: Slicing and Masking

## 25 CONTAINER SUPPORT
- 25.1 Algorithms
- 25.2 Iterators and Ranges
- 25.3 Iterator Adapter
- 25.4 Algorithms of the Standard Library
- 25.5 Parallel Execution
- 25.6 Lists of Algorithm Functions and Range Adapters
- 25.6.1 Range Adapters and Views
- 25.6.2 Ranges as Parameters (and More)
- 25.6.3 List of Nonmodifying Algorithms
- 25.6.4 Inherently Modifying Algorithms
- 25.6.5 Algorithms for Partitions
- 25.6.6 Algorithms for Sorting and Fast Searching in Sorted Ranges
- 25.6.7 Set Algorithms Represented by a Sorted Range
- 25.6.8 Heap Algorithms
- 25.6.9 Minimum and Maximum Algorithms
- 25.6.10 Various Algorithms
- 25.7 Element-Linking Algorithms from "<numeric>" and "<ranges>"
- 25.8 Copy instead of Assignment: Values in Uninitialized Memory Areas
- 25.9 Custom Algorithms
- 25.10 Writing Custom Views and Range Adapters

## 26 GOOD CODE, 6TH DAN: THE RIGHT CONTAINER FOR EACH TASK

### 26.1 All Containers Arranged by Aspects
- 26.1.1 When Is a "vector" Not the Best Choice?
- 26.1.2 Always Sorted: "set", "map", "multiset", and "multimap"
- 26.1.3 In Memory Contiguously: "vector", "array"
- 26.1.4 Cheap Insertion: "list"
- 26.1.5 Low Memory Overhead: "vector", "array"
- 26.1.6 Size Dynamic: All Except "array"

### 26.2 Recipes for Containers
- 26.2.1 Two Phases? "vector" as a Good "set" Replacement
- 26.2.2 Output the Contents of a Container to a Stream
- 26.2.3 So "array" Is Not That Static

### 26.3 Implementing Algorithms That Are Specialized Depending on the Container
![](img/290cf954dfcaad53865de6b98cca8e6f_33_0)

### 27.1 Input and Output
- 27.2 Global, Predefined Standard Streams
- 27.3 Methods for Stream Input and Output
- 27.4 Error Handling and Stream States
- 27.5 Manipulating and Formatting
- 27.6 Streams for File Input and Output
- 27.7 Streams for Strings
- 27.8 Stream Buffers
- 27.9 filesystem
- 27.10 Formatting

### 28.1 pair and tuple
- 28.2 Regular Expressions
- 28.3 Randomness
- 28.4 Mathematical
- 28.5 System Handling
- 28.6 Runtime Type Information: <typeinfo> and <typeindex>
- 28.7 Helper Classes around Functors: <functional>
- 28.8 "optional" for a Single Value
- 28.9 "variant" for One of Several Types
- 28.10 "any" Holds Any Type
- 28.11 Special Mathematical Functions
- 28.12 Fast Conversion with <charconv>

## 29 THREADS: PROGRAMMING WITH CONCURRENCY

### 29.1 C++ Threading Basics
- 29.1.1 Starting Pure Threads
- 29.1.2 Terminating a Thread Prematurely
- 29.1.3 Waiting for a Thread
- 29.1.4 Consider Exceptions in the Starting Thread
- 29.1.5 Passing Parameters to a Thread
- 29.1.6 Moving a Thread
- 29.1.7 How Many Threads to Start?
- 29.1.8 Which Thread Am I?

### 29.2 Shared Data
- 29.2.1 Data Races
- 29.2.2 Latch
- 29.2.3 Barriers
- 29.2.4 Mutexes
- 29.2.5 Interface Design for Multithreading
- 29.2.6 Locks Can Lead to Deadlock
- 29.2.7 More Flexible Locking with unique_lock

### 29.3 Other Synchronization Options
- 29.3.1 Call Only Once with "once_flag" and call_once
- 29.3.2 Locking with "recursive_mutex"

### 29.4 In Its Own Storage with "thread_local"

### 29.5 Waiting for Events with condition_variable
- 29.5.1 notify_all
- 29.5.2 Synchronize Output

### 29.6 Waiting Once with "future"
- 29.6.1 Launch Policies
- 29.6.2 Wait Until a Certain Time
- 29.6.3 Exception Handling with "future"
- 29.6.4 "promise"

### 29.7 Atomics
- 29.7.1 Overview of the Operations
- 29.7.2 Memory Order
- 29.7.3 Example

### 29.8 Coroutines
- 29.8.1 Coroutines in the Compiler
- 29.8.2 Generator
- 29.8.3 Coroutines with "promise_type"

### 29.9 Summary
- 29.9.1 <thread> Header
- 29.9.2 <latch> and <barrier> Headers
- 29.9.3 <mutex> and <shared mutex> Headers
- 29.9.4 <condition variable> Header
- 29.9.5 <future> Header
- 29.9.6 <atomic> Header
- 29.9.7 <coroutine> Header

![](img/290cf954dfcaad53865de6b98cca8e6f_39_0)

## 30 Guideline Support

### 30.2 C++ Guidelines
- 30.2.1 Motivation
- 30.2.2 Type Safety
- 30.2.3 Use RAII
- 30.2.4 Class Hierarchies
- 30.2.5 Generic Programming
- 30.2.6 Not Be Confused by Anachronisms
