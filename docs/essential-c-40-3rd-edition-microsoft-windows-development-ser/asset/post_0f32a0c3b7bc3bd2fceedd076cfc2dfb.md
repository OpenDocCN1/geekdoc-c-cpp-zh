
## C# 4.0 Topics

| TOPIC TITLE | PAGE NUMBER |
| --- | --- |
| Asynchronous Delegate Invocation | 797-798 |
| calling APMs (Asynchronous Programming Models) using TPL (Task Parallel Library) | 791-796 |
| canceling parallel loops | 729-734 |
| common namespaces | 153-154 |
| concurrent collection classes | 773-774 |
| executing iterations in Parallel | 724-734 |
| generics | |
| enabling contravariance | 460-462 |
| enabling covariance | 458-460 |
| lazy loading with | 401-402 |
| support for covariance and contravariance | 462-463 |
| lock keyword | 757 |
| ManualResetEvent and semaphores over AutoReset Event | 772 |
| Monitor class synchronization | 754-757 |
| multithreading, unhandled exceptions on AppDomain | 744-746 |
| optional parameters | 182-185 |
| parallel exception handling with System.AggregateException | 728-729 |
| Parallel LINQ (PLINQ) | 559-560 |
| programming with dynamic objects | 688-699 |
| reset events | 768-771 |
| running LINQ queries in parallel | 734-738 |
| running threads | 706-738 |
| canceling tasks | 718-722 |
| disposing tasks | 723-724 |
| long-running threads | 722-723 |
| unhandled exception handling on Task | 715-718 |
| System-defined delegates: Func | 483-485 |
| thread local storage | 774-775 |
| Tuple generic types | 437-438 |
| use of System.Exception | 412 |

## Index

16-bit characters, 41
42 as strings versus as integers, 187
; (semicolons)
  statements without, 10-11
  whitespace, 11-12
~ (bitwise complement)
  operator, 120
# (hash) symbol, 139
- (minus) operator, 84-92
+ (plus) operator, 84-92
= (assignment) operator
  (see operator overloading), 14
_ (underscore), 15
!= (inequality) operator, 110, 370
! (logical notation) operator, 113
% (remainder) operator, 85
&& (AND) operator, 112, 373
(single quote), 42
' (cast operator), 375-376
* (multiplication) operator, 85
+ (addition) operator, 85, 371-373
++ (increment) operator, 94-97
-- (decrement) operator, 94-97
/ (division) operator, 85

// (three-forward-slash), 387
< (less than) operator, 110
<= (less than or equal to) operator, 110
== (equality) operator, 110, 370
> (greater than) operator, 110
>= (greater than or equal to) operator, 110
? (conditional) operator, 113-114
?? (null coalescing) operator, 114-115
@ symbol, 45
\ (backslash) character, 42
\n (newline) character, 42, 48
^ (exclusive OR) operator, 112
{ } (code blocks), 105-107
|| (OR) operator, 111-112, 373
constraints, 450

### A
abstract classes, inheritance, 293-299
abstract members, 294
  declaring, 297
accessibility modifiers, 381
accessing
  arrays, 70

CAS (Code Access Security), 659, 852
class instances with this keyword, 214
instance fields, 210-211
members, reference types, 839
metadata, reflection, 652-662
security code, 25
access modifiers, 220-222
circumventing, 852
classes, 380-381
on getters and setters, 222-223
private, 275
protected, 276
pronounced, common acronyms, common C#, 862-863
actions, System.Action, 483-484
Active Template Library (ATL), 278
adding comments, 20-23
items to Dictionary<TKey, TValue>, 623
operators, 371-373
addition (+) operator, 85, 371-373
Add() method, 543
addresses, pointers and, 830-839

- aggregation
  - multiple inheritance, 280
  - single inheritance, 279
- aliasing, 164-165
  - qualifiers, namespaces, 384-385
- allocating data on call stacks, 836
- AllowMultiple parameter, 674
- ambiguity, avoiding, 213-217
- AND operator (&&), 112, 373
- anonymous functions, 486
- anonymous methods, 480-482
  - internals, 494-495
  - parameterless, 482
- anonymous types, 245-246
  - arrays, initializing, 545-546
  - collecting interfaces, 536-538
  - generating, 542-543
  - implicit local variables, 54
  - projection to, 558
  - within query expressions, 593
- APIs (application programming interfaces)
  - encapsulation, 826-828
  - VirtualAllocEx(), declaring, 818-819
  - wrappers, simplifying calls with, 828-829
- APMs (Asynchronous Programming Models), 783-797
  - TPL (Task Parallel Library), calling, 791-796
- AppDomain, unhandled exceptions on, 744-746
- applicable calls, 185
- applications
  - domains
    - CLI (Common Language Infrastructure), 854-855
  - HelloWorld program, 2-4, 28-30
- single instance, 766-767
- task-related finalization
  - exceptions suppressed during shutdown, 717
- applying
  - arrays, 70-76
  - bitwise operators, 118
  - characters in arithmetic operations, 88-89
  - factory inheritance, 451
  - FlagsAttribute, 354-355
  - generic classes, 427-429
  - lambda expressions as data, 498-499
  - post-increment operators, 95
  - pre-increment operators, 96
  - SafeHandle, 823-824
  - strings, 50
  - Structure
    - for LayoutAttribute
    - for sequential layout, 820-821
  - System.Threading.Interlocked class, 761-763
  - validation to properties, 228-229
  - variables, 12-16
  - variance in delegates, 485
  - weak references, 391-393
- ArgumentNullException, 407
- arithmetic operators, 85
- arrays, 64-80
  - accessing, 70
  - anonymous types, initializing, 545-546
  - applying, 70-76
  - assigning, 66-70
  - common errors, 78-80
  - declaring, 65-66, 70
  - errors, 69
  - foreach loops, 546-547
  - for each loops, 75-76
  - instance methods
    - length of, 66-70
    - length of, 72
  - methods, 73-75
  - parameters, 173-176
  - redimensioning, 75
  - strings as, 76-78
  - support for covariance and contravariance in, 462-463
  - as operators, 302
- assemblies, 3
- attributes, 665
- CLI (Common Language Infrastructure), 855-858
- metadata reflection, 652-662
- multithreading, building, 856n5
- referencing, 377-381
- targets, modifying, 378-379
- Assert() methods, 91
- assigning
  - arrays, 66-70
  - property names, indexers, 632-633
  - null to strings, 51
  - pointers, 834-837
  - variables, 13, 14-16
- assignment operators, 92-98
- binary operators, combining, 373
- bitwise, 120
- associating
  - data in classes, 250
  - XML comments with programming constructs, 386-388
- associativity, order of, 86
- Asynchronous Delegate Invocation, 797-801
- asynchronous operations
  - with System.Threading.Thread, 738-740
- Asynchronous Programming Models
  - Async property, 710
- ATL (Active Template Library), 278
- atomicity, 704-705, 752
- attributes, 663-688
  - command-line, 881-888
  - constructors, initializing, 668-673
  - custom, 666-667
  - FlagAttribute, 354-355, 675
  - limiting, 674
  - metadata reflection, 652-662
  - predefined, 676-677
  - return, specifying, 666
  - searching, 667-668
  - serialization, 680-682
  - System.ConditionalAttribute, 677-679
  - System.NonSerializableAttribute, 682-683
  - System.ObsoleteAttribute, 677-680
  - System.Runtime.Serialization.Formatters.Binary, optional FieldAttribute, 686
  - ThreadStaticAttribute, 775-777
- assemblies, 665
- automatically implemented properties, 225-227
- AutoResetEvent, semaphores over, 772
- availability of types, 380
- Average function, 585
- avoiding ambiguity, 213-217
- copying, 345
- deadlock, 759, 764-765
- equality conditionals, 91
- string types, 759-760
- synchronization, 760
- this type, 759-760
- typeof types, 759-760
- unboxing, 345
- unnecessary locking, 765-766

### B
Backgroundworker class patterns
  terms, 804-809
\ (backslash) character, 42
base classes, 204
  constraints, 444-445
  overriding, 281-293
  refactoring, 271
Base Class Library. See BCL
base interfaces, using in class declarations, 320
base members, 291-292
base types, casting between derived types, 272-273
BCL (Base Class Library), 25
CLI (Common Language Infrastructure), 860
behaviors, dynamic data type, 690-693
benefits of generics, 430-431
best practices, synchronization design, 674
binary operators, 85, 371-373
BinarySearch() method, 75, 620
Binary Tree and Pair, full source code listings, 876-881
BinaryTree<T> class with no constraints, declaring, 439
binding, dynamic, 694
bits, 115
bitwise operators, 115-121
  assignment, 120
  complement (~) operator, 120
catch blocks, general, 409-410
code blocks, 831
code blocks (), 105-107
System.Exception, 195-196
unchecked, 418
Boolean expressions, 109-115
Boolean types, 40-41
boxing, 339-346
break statements, 132-135
Bubblesort() method, 470-472
buffer overflows, 72
overruns, 72
building custom collections, 611-612
multimode assemblies, 856n5
bytes, 115

### C
C#
  acronyms, 862-863
  CLI (Common Language Infrastructure)
    compiling to machine code, 847-849
  compilers downloading, 865
  installing, 865-867
  custom collection interfaces, 612-613
  delegate instantiation, 477-480
  general catch blocks in, 409-410
  LINQ, projection using query expressions, 592-593
  overview of, 1-2
  preprocessor directives, 138-145
  properties, 48
  syntax fundamentals, 4-12
  VirtualAllocEx() APIs, declaring, 818-819
  without generics, 422-439
C++
  array declaration, 66
  buffer overflow bugs, 72
  delete operator, 208
  deterministic destruction, 399, 850
  dispatch method calls during construction, 286
  global methods, 158
  global variables and functions, 248
  header files, 160
  implicit overriding, 283
  multiple inheritance, 278
  operators, errors, 110
  pointers, declaring, 833
  preprocessing, 138
  pure virtual functions, 297
