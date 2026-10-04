
strings
stack space, 102
checking for, 489
stack trace, 461, 462
complete, 462
constructing, 462
interpreting, 463
StackTrace property, 461
Start method (Thread class), 679
StartNew method, 710
StartsWith method, comparing strings, 325
startup time, improving, 19, 21
starvation, thread, 684
state corruption
destroying, 476
exception handling, and, 477
FailMethod, 480
managed code, and 477
mitigating, 475
terminating process for, 477
state machines, returning model, 749
stateless encoding and decoding, 356
statements, checked and unchecked, 116
static classes, 158
static constructors. See type constructors
defining on generic types, 273
static events, 152
static fields, 177
defining, 178
initializing, 189
memory leaks and, 510
static members
interfaces and, 297
MarshalByRefObject class and, 567
static methods
for arrays, 380
calling, 106
calling back, with delegates, 394
calling operator overload methods, with 194
for Char type, 318
nextension attribute, 203
Finalize method and, 526
forInt32 variables, 768
thread safety, 759, 760
volatile keyword, 767
StaticDelegateDemo method, 394
Stop method (Parallel class), 716
streaming contexts for serialization, 631
StreamReader type, 350
streams, 656
StreamWriter type, 350, 537
finalization and, 538
String class
hash table, accounting, 330
methods, 338
sealed, 323
string interning, 329
String objects. See strings
immutability of, 569
String type, 112, 320
constructing, 320
interfaces and, 300
method overloads defined by, 325
as native type, 320
StringBuilder class, 198, 345
creating objects, 366
members, 337
methods, 338
StringBuilder type, 336
StringComparer class, 329
StringComparison type, 324
StringInfo, 333
strings
base-64 encoding/decoding, 356
changing case of characters in, 325
character arrays, 337
characters, examining, 333
cloning, 335
comparing, 323
catatenating, 322
constructing, 320
constructing efficiently, 336
converting to bytes, 353
converting to Unicode to MBCS, 350
copying, 335
custom formatter, 345
date formatting, 341
ndeleting securely, 358
encodings, 350
formatting, 344, 346
formatting multiple objects into, 344
immutability, of 323
interning, 329
mapping enumerated types to, 364
in metadata, 332
number formatting, 341
as object representation, 339
parsing, 348
pooling, 332
secure, 357
in source code, 321
uses for, 324
verbatim, 322
WinRT, 647
optimizing, 795
public indexes, 797
relationships, 795
type objects and, 795
synchronization context task schedulers, 711
SynchronizationContext class, 749
synchronizing threads. See thread
synchronization
synchrous I/O operations, 752. See I/O operations
FileStream objects and, 753
System Monitor, 524
System namespace, 22, 23
System.Collections.Generic namespace, 270
System.Decimal type, 118, 198
System.Diagnostics.ConditionalAttribute
Strong Name utility (SN.exe), 68
strongly named assemblies
characteristics of, 66
components of, 68
compressing, 74
creating, 67
deploying globally, 72
deploying privately, 79
obtaining a key for, 68
referencing, 74
security of, 76
tamper-resistant nature of, 75
unique identification of, 67
verification, 76
attribute, 206
System.Exception class, state corruption and, 474
type, 460
SystemException type, 466
System.InvalidCastException type, 95
System.Object type, 26, 91
delete operator, 93
new operator, 92
protected methods, 92
public methods, 92
System.Reflection.AssemblyName class, 68
System.Runtime.ProfileOptimization class, 16
System.namespace, 97
System.Type object, type pointer, 110
Structured Exception Handling (SEH), 453. See also exceptions; handling structures.
Substring method, 335
SubstringByElements, 333
SuppressMessage attribute, 440
SurrogateSelector object, 639
surrogate types for serialization, 636
surrogates for Unicode elements, 333
suspending threads, 774
sync blocks, 794
index, 105
initialization of, 795
Task class
FromAny methods, 822
vs. thread synchronization, 814
Task Manager, 670, 675
monitoring performance with, 675
Task objects, 701
arrays of, 710
fields in, 707
ContinueWith task, 705
creation flags for, 701
CurrentId property, 708
disposing of, 708
factory for, 709
Int32 fields in, 708
status of, 708
Status property, querying, 708
supplementary state, 707
WaitingForActivation state, 709
TaskFactory type, 709, 710
TaskLogger class, 738
tasks, 700
canceling, 704
CancellationToken objects, associating with, 705
child tasks, 707
composition of, 707
constructors and, 201
deadlock situations, 702
delaying, 722
delegates, passing, 715
exceptions, detecting, 703
exceptions thrown by, 704
performance issues and, 708
reader/writer semantics, 815
returning void with, 709
starting automatically on our task completion, 705
state, 707
supplementary state, 707
synchronization context tasks, 711
task schedulers, 711, 712
vs. thread synchronization, 807
handled exceptions by, 702
unique IDs for, 708
waiting for completion, 702
Tasks namespace, 651, 700, 709
TaskScheduler objects, 711
TaskScheduler type, defining classes derived from, 712
TEB (thread environment block), 671
temporary variables, 284
terminated applications, viewing in Reliability Monitor
terminating process, 477, 574
text elements. See also characters
TextElementEnumerator method, 333
thread blocking, I/O operations and, 731
Thread class, 668
thread environment block (TEB), 671
thread kernel objects, 671
thread locks, asynchronous functions and, 734
thread pools, 692
calling methods asynchronously, 693
child tasks, 707
continuing tasks in, 705, 707
deadlock situations, 724
delaying tasks, 792
execution contexts, 695
heuristic nature of, 692
limiting number of threads in, 724
parallel performance of, 713
parallel processing, exceptions thrown when 716
performance and, 692
processing order, 725
queuing in, 693
scheduling method calls, 720
scheduling tasks in, 712
security settings and, 694
sequential method execution, 713
thread management in, 723
thread synchronization locks and, 725
worker thread management, 724
work items in, 693
thread prioritization, 754
thread-safe collection classes, 818
queues, 813
thread safety, 759
thread synchronization async functions and, 757
asynchronous, 814
auto-reset events and, 782
avoiding, 759
# ThreadAbortException exception
blocking, avoiding, 805
blocking countdown, 804
class libraries and, 759
condition variable pattern, 811
constructs, 805
double-check locking, 807
drawbacks of, 757
exception handling and, 476
hybrid, 790
hybrid constructs, creating constructs
elivelocks and deadlocks, 761
lock, 189
locks, 476, 725
lock scalability, 814
m_opCount field, 772
Mutex objects, 786
parallel execution, 805
performance issues, 758
primitive constructs, 760
priority boosting, disabling, 774
private locks, 797
properties and, 233
reader-writer locks, 801, 804
recursive locks, 786
recursive locks, avoiding, 806
specifying synchronization object, 811
spin lock logic, 774
spin locks, 773
tasks vs., 807
yielding threads when, 775
ThreadException exception, 580
Thread event, 488
threading models, 748
Threading namespace, 695, 720, 778
DispatcherTimer class, 723
Timer class, 723
ThreadTaskScheduler, 713
ThreadPool class, 693
for Windows Store apps, 694
threads, 102
in 16-bit Windows, 669
aborting, 578, 679
allocating local variables, 105
# Strong Name Utility (SN.exe)
# ThreadAbortException exception
