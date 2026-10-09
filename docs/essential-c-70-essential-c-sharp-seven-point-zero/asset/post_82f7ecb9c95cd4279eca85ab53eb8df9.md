
## Multithreading, asynchronous tasks
- antecedent tasks, 797–798
- associating data with tasks, 795
- asynchronous continuations, 796–803
- chaining tasks, 797–798
- cold tasks, 792
- composing large tasks from smaller ones, 796–798
- continuation tasks, 797–798
- control flow, 796
- creating threads and tasks, 790–791
- hot tasks, 792
- Id property, 795
- introduction, 791–795
- invoking, 791–795
- multithreaded programming complexities, 789–790
- observing unhandled exceptions, 806–807
- polling a Task<T>, 793–794
- registering for notification of task behavior, 801–802
- registering for unhandled exceptions, 803–807
- registering listeners for events, 802–803
- returning void from an asynchronous method, 830–833
- synchronous delegates, 791
- task continuation, 796–803
- task identification, 795
- task scheduler, 790–791
- task status, getting, 794
- Task.Run(), 792
- tasks, definition, 790–791
- tasks vs. delegates, 791
- Task.WaitAll(), 793
- Task.WaitAny(), 793
- unhandled exception handling with AggregateException, 803–807
- unhandled exceptions on a thread, 803–807

## Multithreading, canceling tasks
- cooperative cancellation, definition, 810
- disposable tasks, 816
- long-running tasks, 810–814
- obtaining a task, 814–815

## Multithreading, guidelines
- aborting threads, 787
- long-running tasks, 816
- parallel loops, 849
- performance, 777, 781
- thread pooling, 789
- Thread.Sleep(), 784–785
- unhandled exceptions, 810

## Multithreading, parallel loop iterations
- breaking, 855–856
- canceling, 852–854
- exception handling with AggregateException, 851–852
- hill climbing, 850–851
- introduction, 846–850
- options, 854–855
- TPL performance tuning, 850–851
- work stealing, 850–851

## Multithreading, performance
- context switching, 777
- overview, 776–777
- switching overhead, 777
- time slicing costs, 777

## Multithreading, task-based asynchronous pattern
- with async and await, 824–829
- async and await with the Windows UI, 843–845
- async keyword, purpose of, 827
- async void method, 830–833
- asynchronous high-latency operations with the TPL, 820–824
- asynchronous lambdas, 833–835
- await keyword, 838–840
- await operators, 844–846
- awaiting non-Task<T> or values, 838–840
- control flow misconceptions, 826
- control flow within tasks, 827
- custom asynchronous methods, 835–838
- handling exceptions, 821–822
- problems addressed by, 846
- progress update, 837–838
- synchronization context, 840–842
- synchronous high-latency operations, 817–818
- task drawbacks, overview, 817–823
- task schedulers, 840–842

## Multithreading, threading problems
- atomic operations, 778
- complex memory models, 779-780
- deadlocks, 780
- lock statement, 780
- locking leading to deadlocks, 780
- race conditions, 778-779

## Multithreading, with System.Threading.Thread
- Abort(), 786-787
- aborting threads, 786-787
- asynchronous delays, 785
- asynchronous operations, 781-783
- await operator, 785
- checking threads for life, 784
- foreground threads vs. background, 783
- IsAlive property, 784
- IsBackground property, 783
- Join(), 783
- Priority property, 784
- putting threads to sleep, 784-785
- re-prioritizing threads, 783
- Task.Delay(), 785
- thread management, 783-784
- thread pooling, 787-789
- ThreadAbortException, 786-787
- Thread.Sleep() method, putting threads to sleep, 784-785
- ThreadState property, 784
- waiting for threads, 783

## N
- \n, newline character, 55, 57
- Name property, 273-274
- Named arguments, calling methods, 222
- Named parameters, attributes, 746-747
- nameof operator
  - properties, 270-271, 733-734
  - throwing exceptions, 467, 468
- Namespaces
  - aliasing, 199-200. See also using directive.
  - calling methods, 184-186
  - in the CLR (Common Language Runtime), 442
  - common, list of, 185-186
  - defining, 442-445
  - definition, 184, 195
  - dropping. See using directive.
  - eliminating. See using directive.
  - guidelines, 186, 445
  - importing types from. See using directive.
  - introduction, 442-445
  - naming conventions, 186, 442
  - nested, 196, 443-444
- Naming conventions
  - avoiding ambiguity, 254
  - class definition, 15
  - identifiers, 13-14
  - for interfaces, 355
  - local variables, 22
  - methods, 183
  - namespaces, 186, 442
  - parameters, 191, 223
  - properties, 267
  - type parameter, 498
- Native code, definition, 32
- NDoc tool, 449
- Negation operator. See NOT operator.
- Negative infinity, 119
- Negative numbers vs. positive, bitwise operators, 148
- Negative zero, 120
- Nested
  - classes, 304-306
  - delegates, 545
  - generic types, 505-506
  - if statements, 130-132
  - iterators, 714-715
  - namespaces, 196, 443-444
  - types, 306
  - using directives, 197-198

## .NET
- description, 943
- garbage collection, 450-451, 933-934

### .NET Compact Framework, 926

### .NET Core
- default .NET framework, 3
- description, 37, 925, 927-928

### .NET Framework
- description, 925
- vs. .NET framework, 927

### .NET framework
- choosing, 3
- default, 3. See also .NET Core.
- downloading, 3
- installing, 3
- vs. .NET Framework, 927
- predominant implementations, 37. See also specific frameworks.

### .NET Micro Framework, 926

## .NET Native, 942–943

## .NET standard, 928–929

## .NET versions, mapped to C# releases, 39–40

## new keyword, 94

## New line, starting
- \n (newline character), 55, 57, 64
- \r\n (newline character), 64
- strings, 55, 57
- verbatim string literals, 57
- WriteLine() method, 64

## new modifier, 330–335

## new operator
- constructors, 279, 280
- value types, 388

## NewExpression, 568

## NextId initialization, 295

## No-oping a call, 749–750

## Non-nullable value types, 511–512

## Non-serializable fields, 754

## NonSerializable, 754

## Normalized data, 633

## NOT operator, 141

## NotImplementedException, 233

## NotOnCanceled enum, 800

## NotOnFaulted enum, 799

## NotOnRanToCompletion enum, 799

## own option, 175–176

## ownarn:<warn list> option, 175–176

## NuGet packages, adding to class libraries, 436–439

## null, checking for
- arrays, 705
- collections, 705
- empty arrays or collections, 705
- guidelines, 582
- invoking delegates, 594
- multicast delegates, 580–582

## Null-conditional operator
- delegates, 146–147
- question mark, dot (?.), 144–146
- short circuiting with, 144–146

## null type
- description, 67–68
- use for, 67–68

## Nullable modifier, 80–83

## Nullable<T>, 493

## NullReferenceException
- invoking delegates, 594
- throwing exceptions, 467, 468

## Numbers, formatting as hexadecimal, 52

## Numeric conversion, exception handling, 238–239

## O
- Obfuscators, 34. See also ILDASM (IL Disassembler).
- Object graphs, expression trees as, 568–569
- Object initializers
  - calling, 281–282
  - constructors, 281–282
  - definition, 281–282
- object members, overriding, 416–419
- Object-oriented programming, definition, 242–243
- Object types. See Types.
- Objects. See also Constructors.
  - associations, 292
  - CIL (Common Intermediate Language), 940
  - definition, 246–247
  - destroying, 283
  - identity vs. equal object values, 416–419
  - instantiation, 247
- Obsolete APIs. See Deprecated APIs.
- ObsoleteAttribute, 751–752
- Obtaining a task, 814–815
- OfType<>(), 643
- One-to-many relationships, 630, 637–638
- OnFirstNameChanging(), 310–311
- OnLastNameChanging(), 310–311
- OnlyOnCanceled enum, 799
- OnlyOnFaulted enum, 800
- OnlyOnRanToCompletion enum, 800
- OnTemperatureChange event, 598–599
- OnTemperatureChanged(), 577–578
- Operational polymorphism, 218
- OperationCanceledException, 814, 854, 859–861
- Operator constraints, constraint limitations, 515–516
- Operator-only statements, C++ vs. C#, 111
- Operator order of precedence, C++ vs. C#, 124
- Operators. See also specific operators.
  - arithmetic (binary (+, -, *, /, %)), 111–112
  - assignment (=), 22
  - associativity (()) parenthesis, 112–117
  - bitwise (&, |, ^), 149–152
  - characters in arithmetic operations, 115
