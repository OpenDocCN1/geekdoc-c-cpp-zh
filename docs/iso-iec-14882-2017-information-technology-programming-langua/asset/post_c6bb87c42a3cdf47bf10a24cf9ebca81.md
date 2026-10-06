
# ISO/IEC 14882:2017(E)

+ 31.7 Class template regex_traits ..................................................................... 1305
31.8 Class template basic_regex ..................................................................... 1307
31.9 Class template sub_match ....................................................................... 1313
31.10 Class template match_results ................................................................ 1318
31.11 Regular expression algorithms ............................................................... 1324
31.12 Regular expression iterations ................................................................ 1329
31.13 Modified ECMAScript regular expression grammar ................................... 1335

# 32 Atomic operations library ............................................................ 1338

+ 32.1 General ....................................................................................... 1338
32.2 Header <atomic> synopsis ................................................................ 1338
32.3 Type aliases ..................................................................................... 1338
32.4 Order and consistency ........................................................................ 1342
32.5 Lock-free property ............................................................................ 1344
32.6 Class template atomic ....................................................................... 1345
32.7 Non-member functions ........................................................................ 1352
32.8 Flag type and operations ................................................................ 1352
32.9 Fences ........................................................................................ 1353

# 33 Thread support library ....................................................... 1355

+ 33.1 General ....................................................................................... 1355
33.2 Requirements ............................................................................... 1355
33.3 Threads ........................................................................................ 1358
33.4 Mutual exclusion ........................................................................ 1363
33.5 Condition variables ....................................................................... 1384
33.6 Futures ........................................................................................ 1391

# A Grammar summary .......................................................... 1408

+ A.1 Keywords ................................................................................... 1408
A.2 Lexical conventions ........................................................................ 1408
A.3 Basic concepts ............................................................................ 1413
A.4 Expressions ................................................................................... 1413
A.5 Statements ................................................................................... 1417
A.6 Declarations ................................................................................ 1418
A.7 Declarators ................................................................................ 1422
A.8 Classes ...................................................................................... 1424
A.9 Derived classes ........................................................................ 1425
A.10 Special member functions ............................................... 1426
A.11 Overloading ................................................................... 1426
A.12 Tuples ....................................................................... 1429
A.13 Exception handling ........................................................ 1427
A.14 Preprocessing directives ............................................... 1428

# B Implementation quantities ......................................... 1430

# C Compatibility ............................................................ 1432

+ C.1 C++ and ISO C ........................................................ 1432
C.2 C++ and ISO C++ 2003 ....................................... 1441
C.3 C++ and ISO C++ 2011 ....................................... 1447
C.4 C++ and ISO C++ 2014 ....................................... 1449
C.5 C standard library ................................................ 1453

ISO/IEC 14882:2017(E)

# D Compatibility features 1456

+ D.1 Redeclaration of static constexpr data members . . . . 1456
+ D.2 Implicit declaration of copy functions . . . . 1456
+ D.3 Deprecated exception specifications . . . . . 1456
+ D.4 C++ standard library headers . . . . . . 1456
+ D.5 C standard library headers . . . . . . . 1457
+ D.6 char streams . . . . . . . . . . 1457
+ D.7 uncaught_exception . . . . . . . 1457
+ D.8 Old adaptable function bindings . . . . . 1466
+ D.9 The default allocator . . . . . . . 1471
+ D.10 Raw storage iterator . . . . . . 1472
+ D.11 Temporary buffers . . . . . . 1473
+ D.12 Deprecated type traits . . . . . . 1474
+ D.13 Deprecated iterator primitives . . 1475
+ D.14 Deprecated shared_ptr observers . . 1475
+ D.15 Deprecated standard code conversion functions 1475
+ D.16 Deprecated convenience conversion interfaces 1477

# Bibliography 1482

# Cross references from ISO C++ 2014 1483

# Index 1504

# Index of grammar productions 1506

# Index of library names 1539

# Index of implementation-defined behavior 1543

# ISO/IEC 14882:2017(E)

# Foreword

ISO (the International Organization for Standardization) is a worldwide federation of national standards bodies (member bodies). The work of preparing Standards is normally carried out by technical committees. Each member body interested in a subject for which a technical committee has established the right to be represented on that committee. International organizations, governmental and non-governmental, in liaison with ISO, collaborate closely with the International Electrotechnical Commission (IEC) on all matters of electrotechnical standardization.

This document was prepared in accordance with the editorial rules of ISO Directives. Attention is drawn to the possibility that some of the elements of this document may be subject of patent rights. ISO shall not be responsible for identifying or all such patent rights. Details of any patent rights identified in the Introduction and/or the ISO list of patent declarations (see www.iso.org/patents).

Any trade name used in this document is information given for the convenience of users and does not constitute an endorsement. For an explanation on the voluntary nature of standards, the meaning of ISO specific terms and expressions related to conformity assessment, as well as information about ISO's adherence to the World Trade Organization (WTO) principles in the Technical Barriers to Trade (TBT) see the following URL www.iso.org/foreword.html.

This document was prepared by Technical Committee ISO/IEC JTC 1, Information technology, Subcommittee 22, Programming languages, their environments and system software interfaces.

This edition cancels and replaces the previous edition as (ISO/IEC 14882:2014), which has been technically revised.

The main changes compared to the previous edition are as follows:

- evaluation order is specified in more cases
- removal of trigraphs
- adjustments to value categories resulting in copy elimination being mandatory
- additional character and floating point literals syntax
- lambdas extensions to permit capture of *this and use in constant expressions
- initializer statements for if and switch statements
- addition of constexpr if statements
- range-based for generalized to support heterogeneous begin and end types
- addition of structured bindings
- addition of inline variables
- list enumeration extended to support enumerations and aggregates with base classes
- message in static_assert is now optional
- addition of nested namespace syntax
