+   2.2 switch with Initialization ................................................... 23
+   2.3 Afternotes ............................................................... 24
+   
+   3 Inline Variables .............................................................. 25
+   3.1 Motivation for Inline Variables .............................................. 25
+   3.2 Using Inline Variables ...................................................... 27
+   3.3 constexpr Now Implies inline For Static Members ................................ 28
+   3.4 Inline Variables and thread_local ............................................ 29
+   3.5 Afternotes ............................................................... 31
+   
+   4 Aggregate Extensions ........................................................... 33
+   4.1 Motivation for Extended Aggregate Initialization .............................. 34
+   4.2 Using Extended Aggregate Initialization ...................................... 34
+   4.3 Definition of Aggregates ..................................................... 36
+   4.4 Backward Incompatibilities ................................................... 36
+   4.5 Afternotes ............................................................... 37
+   
+   5 Mandatory Copy Elision or Passing Unmaterialized Objects ....................... 39
+   5.1 Motivation for Mandatory Copy Elision for Temporaries ....................... 39
+   5.2 Benefit of Mandatory Copy Elision for Temporaries ............................ 41
+   5.3 Clarified Value Categories ................................................... 42
+   5.3.1 Value Categories ....................................................... 42
+   5.3.2 Value Categories Since C++17 ............................................ 44
+   5.4 Unmaterialized Return Value Passing .......................................... 45
+   5.5 Afternotes ............................................................... 46
+   
+   6 Lambda Extensions .............................................................. 47
+   6.1 constexpr Lambdas ........................................................... 47
+   6.1.1 Using constexpr Lambdas .................................................. 49
+   6.2 Passing Copies of this to Lambdas ............................................ 50
+   6.3 Capturing by const Reference ................................................ 53
+   6.4 Afternotes ............................................................... 53
+   
+   7 New Attributes and Attribute Features .......................................... 55
+   7.1 Attribute [[nodiscard]] ..................................................... 55