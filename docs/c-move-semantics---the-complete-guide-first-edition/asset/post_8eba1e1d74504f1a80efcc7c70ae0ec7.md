
## C++ Move Semantics

### The Complete Guide

Nicolai M. Josuttis

## C++ Move Semantics - The Complete Guide

### First Edition

Nicolai M. Josuttis

This version was published on **2020-12-19**.

© 2020 by Nicolai Josuttis. All rights reserved.

This publication is protected by copyright, and permission must be obtained from the author prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise.

This book was typeset by Nicolai M. Josuttis using the LaTeX document processing system.

This book is for sale at [http://leanpub.com/cppmove](http://leanpub.com/cppmove).

This is a Leanpub book. Leanpub empowers authors and publishers with the Lean Publishing process. Lean Publishing is the act of publishing an in-progress ebook using lightweight tools and many iterations to get reader feedback, pivot until you have the right book, and build traction once you do.

## Contents

- **Preface** ........................................................ xi
  - An Experiment ..................................................... xi
  - Versions of This Book ............................................. xii
  - Acknowledgments .................................................... xiii

- **About This Book** ................................................ xv
  - What You Should Know Before Reading This Book ..................... xv
  - Overall Structure of the Book ..................................... xv
  - How to Read This Book ............................................. xvi
  - The Way I Implement ................................................ xvi
  - The C++ Standards .................................................. xvii
  - Example Code and Additional Information ........................... xviii
  - Feedback ........................................................... xviii

- Part I: Basic Features of Move Semantics ................................ 1

- 1 The Power of Move Semantics ........................................... 3
  - 1.1 Motivation for Move Semantics ...................................... 3
    - 1.1.1 Example with C++03 (Before Move Semantics) ....................... 3
    - 1.1.2 Example Since C++11 (Using Move Semantics) ...................... 11
  - 1.2 Implementing Move Semantics ......................................... 18
    - 1.2.1 Using the Copy Constructor ...................................... 19
    - 1.2.2 Using the Move Constructor ...................................... 20
  - 1.3 Copying as a Fallback ............................................... 21
  - 1.4 Move Semantics for const Objects .................................... 22
    - 1.4.1 const Return Values ............................................. 23
  - 1.5 Summary ..... 23

- **2 Core Features of Move Semantics** ..... 25
  - 2.1 Rvalue References ..... 25
    - 2.1.1 Rvalue References in Detail ..... 25
    - 2.1.2 Rvalue References as Parameters ..... 26
  - 2.2 `std::move()` ..... 27
    - 2.2.1 Header File for `std::move()` ..... 27
    - 2.2.2 Implementation of `std::move()` ..... 28
  - 2.3 Moved-From Objects ..... 28
    - 2.3.1 Valid but Unspecified State ..... 28
    - 2.3.2 Reusing Moved-From Objects ..... 29
    - 2.3.3 Move Assignments of Objects to Themselves ..... 30
  - 2.4 Overloading by Different References ..... 30
    - 2.4.1 `const` Rvalue References ..... 31
  - 2.5 Passing by Value ..... 31
  - 2.6 Summary ..... 32

- **3 Move Semantics in Classes** ..... 35
  - 3.1 Move Semantics in Ordinary Classes ..... 35
    - 3.1.1 When Is Move Semantics Automatically Enabled in Classes? ..... 38
    - 3.1.2 When Generated Move Operations Are Broken ..... 39
  - 3.2 Implementing Special Copy/Move Member Functions ..... 40
    - 3.2.1 Copy Constructor ..... 41
    - 3.2.2 Move Constructor ..... 42
    - 3.2.3 Copy Assignment Operator ..... 43
    - 3.2.4 Move Assignment Operator ..... 44
    - 3.2.5 Using the Special Copy/Move Member Functions ..... 46
  - 3.3 Rules for Special Member Functions ..... 48
    - 3.3.1 Special Member Functions ..... 49
    - 3.3.2 By Default, We Have Copying and Moving ..... 50
    - 3.3.3 Declared Copying Disables Moving (Fallback Enabled) ..... 50
    - 3.3.4 Declared Moving Disables Copying ..... 51
    - 3.3.5 Deleting Moving Makes No Sense ..... 52
    - 3.3.6 Disabling Move Semantics with Enabled Copy Semantics ..... 53
    - 3.3.7 Moving for Members with Disabled Move Semantics ................................ 54
    - 3.3.8 Exact Rules for Generated Special Member Functions ............................ 54
  - 3.4 The Rule of Five or Three ........................................................ 57
  - 3.5 Summary ........................................................................... 58

- **4 How to Benefit From Move Semantics** ............................................. 59
  - 4.1 Avoid Objects with Names ....................................................... 59
    - 4.1.1 When You Cannot Avoid Using Names ......................................... 60
  - 4.2 Avoid Unnecessary `std::move()` ................................................ 60
  - 4.3 Initialize Members with Move Semantics ......................................... 61
    - 4.3.1 Initialize Members the Classical Way ...................................... 61
    - 4.3.2 Initialize Members via Moved Parameters Passed by Value ................... 63
    - 4.3.3 Initialize Members via Rvalue References .................................. 66
    - 4.3.4 Compare the Different Approaches ........................................... 70
    - 4.3.5 Summary for Member Initialization ......................................... 72
    - 4.3.6 Should We Now Always Pass by Value and Move? ............................... 73
  - 4.4 Move Semantics in Class Hierarchies ............................................. 75
    - 4.4.1 Implementing a Polymorphic Base Class ...................................... 75
    - 4.4.2 Implementing a Polymorphic Derived Class ................................... 77
  - 4.5 Summary ........................................................................... 78

- **5 Overloading on Reference Qualifiers** .............................................. 79
  - 5.1 Return Type of Getters ........................................................... 79
    - 5.1.1 Return by Value .............................................................. 79
    - 5.1.2 Return by Reference ......................................................... 80
    - 5.1.3 Using Move Semantics to Solve the Dilemma .................................. 81
  - 5.2 Overloading on Qualifiers ......................................................... 83
  - 5.3 When to Use Reference Qualifiers .................................................. 84
    - 5.3.1 Reference Qualifiers for Assignment Operators .............................. 84
    - 5.3.2 Reference Qualifiers for Other Member Functions ............................ 86
  - 5.4 Summary ........................................................................... 87

- **6 Moved-From States** ................................................................. 89
  - 6.1 Required and Guaranteed States of Moved-From Objects .............................. 89
    - 6.1.1 Required States of Moved-From Objects ...................................... 90
