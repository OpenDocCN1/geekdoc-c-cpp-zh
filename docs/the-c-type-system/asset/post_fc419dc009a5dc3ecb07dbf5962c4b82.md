
# THE C# TYPE SYSTEM

BUILD ROBUST, PERFORMANT, AND EFFICIENT PROGRAMS

STEVE LOVE

![](img/47f0004b0ac0322f285ca59a19bca333_0_0.png)

no starch press

# THE C# TYPE SYSTEM

# THE C# TYPE SYSTEM. Copyright © 2024 by Steve Love.

All rights reserved. No part of this work may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system, without the prior written permission of the copyright owner and the publisher.

First printing
27 26 25 24 23     1 2 3 4 5
ISBN-13: 978-1-7185-0158-4 (print)
ISBN-13: 978-1-7185-0159-1 (ebook)

Published by No Starch Press® Inc.
245 8th Street, San Francisco, CA 94103
phone: +1.415.863.9900
www.nostarch.com; info@nostarch.com

+   Publisher: William Pollock
+   Managing Editor: Jill Franklin
+   Production Manager: Sabrina Plomitallo-González
+   Production Editor: Sydney Cromwell
+   Developmental Editor: Rachel Monaghan
+   Interior Design: Octopod Studios
+   Cover Illustrator: Gina Redman
+   Technical Reviewer: Jon Skeet
+   Copyeditor: Sharon Wilkey
+   Proofreader: Carl Quesnel
+   Indexer: BIM Creatives, LLC

Library of Congress Control Number: 2023012406

For customer service inquiries, please contact info@nostarch.com. For information on distribution, bulk sales, corporate sales, or translations: sales@nostarch.com. For permission to translate this work: rights@nostarch.com. To report counterfeit copies or piracy: counterfeit@nostarch.com.

No Starch Press and the No Starch Press logo are registered trademarks of No Starch Press, Inc. Other product and company names mentioned herein may be the trademarks of their respective owners. Rather than use a trademark symbol with every occurrence of a trademarked name, we are using the names only in an editorial fashion and to the benefit of the trademark owner, with no intention of infringement of the trademark.

The information in this book is distributed on an “As Is” basis, without warranty. While every precaution has been taken in the preparation of this work, neither the author nor No Starch Press, Inc. shall have any liability to any person or entity with respect to any loss or damage caused or alleged to be caused directly or indirectly by the information contained in it.

For my wife, Fran: best friend, fiercest critic, and staunchest supporter

# About the Author

Steve Love is a professional developer with over 20 years of experience using C# in a wide range of industries, including logistics, public services, and finance. He is the editor of *C Vu*—the members’ journal of the ACCU (https://accu.org)—as well as a frequent speaker at conferences.

# About the Technical Reviewer

Jon Skeet is a staff software engineer for Google, working on the .NET client libraries for Google Cloud Platform. He’s a regular contributor to Stack Overflow, the creator of the .NET date/time library Noda Time, and the author of *C# in Depth*, now in its fourth edition. Jon loves diving into all aspects of C# and occasionally twisting it horribly out of shape.

# BRIEF CONTENTS

Acknowledgments ........................................................... xvii

Introduction ............................................................... xix

Chapter 1: Making the Most of the Type System ................................... 1

The importance of user-defined value types and accurate names

Chapter 2: Value and Reference Types ........................................... 31

Why C# has both value and reference types and how they compare

Chapter 3: Reference and Value Parameters ...................................... 69

Four kinds of method parameters and how to pass arguments to them

Chapter 4: Implicit and Explicit Copying ....................................... 105

How values are copied in a program and copying-related hazards

Chapter 5: Types of Equality .................................................. 139

Various ways to compare values for equality

Chapter 6: The Nature of Values ............................................... 175

The characteristics and roles of different types in an application

Chapter 7: Value Types and Polymorphism ....................................... 211

Why inheritance isn't appropriate for value types

Chapter 8: Performance and Efficiency ......................................... 249

How different types affect an application’s performance

Afterword ............................................................... 287

Appendix: Further Reading ................................................... 289

Index ................................................................... 301

# CONTENTS IN DETAIL

# ACKNOWLEDGMENTS                                      xvii

# INTRODUCTION                                          xix

- Who Should Read This Book? ................................. xx
- Organization and Requirements ............................... xxi
- Modern Features ........................................... xxiii
- Why Value Types? .......................................... xxiii

# 1
MAKING THE MOST OF THE TYPE SYSTEM                                      1

- The Value of Good Names ................................... 2
- Adding Clarity Through Types ................................. 4
  - Named Arguments ........................................... 4
  - Custom Types .............................................. 5
  - Encapsulation ............................................. 6
  - Immutability .............................................. 7
  - Value Validation ........................................... 8
  - Testing ................................................... 9
- Refactoring .................................................. 9
  - Replacing Magic Numbers with Named Constants .............. 10
  - Simplifying Properties and Values ........................ 11
  - Overloading Arithmetic Operators ......................... 14
  - Determining a Need for New Types ........................ 15
- Encoding Units .............................................. 18
  - Itemizing Units with enums ............................... 19
  - Static Creation Methods .................................. 22
  - Symmetry in Design ....................................... 23
  - Making Units Explicit .................................... 24
  - Choosing the Most Natural Usage .......................... 25
  - Returning Types Implied by Units ........................ 27
- A Fully Formed Encapsulated Value .......................... 28
- Deciding Whether to Abstract Types ........................ 29
- Summary .................................................... 30

# 2
VALUE AND REFERENCE TYPES                                      31

- User-Defined Types ........................................ 32
  - Structs and Classes ...................................... 32
  - Records and Record Structs ................................ 33
  - Inheritance .............................................. 34
  - Type Instance Lifetimes .................................. 36
- Variables ................................................... 37
  - Variables vs. Values ..................................... 38
  - Definite Assignment ...................................... 39
- Instances and Storage ........................................ 39
  - Embedded Values ............................................. 40
  - Boxed Values ................................................ 44
- Semantics and Type ........................................... 45
  - The Common Type System ...................................... 45
  - Copy Semantics .............................................. 46
  - Records, Structs, and Value Semantics ....................... 48
- Construction and Initialization .............................. 49
  - Default Initialization ...................................... 50
  - Instance Constructors ....................................... 51
  - Field Initializers .......................................... 58
  - Object Initializers ......................................... 58
- null Values and Default Values ................................ 60
  - Generics and null ........................................... 61
  - Generics and Default Values ................................ 62
  - Nullable Value Types ........................................ 63
  - Nullable Reference Types .................................... 64
  - The Null-Forgiving Operator ................................ 66
- Summary ....................................................... 67

# 3
REFERENCE AND VALUE PARAMETERS

- Method Parameters and Arguments ............................. 70
  - Reference Types vs. By-Reference Parameters ................ 70
  - Value Types and Parameters .................................. 71
  - The Value of a Reference .................................... 73
  - Reference Variables and Aliasing ............................ 74
- Mutable By-Reference Parameters ................................ 76
  - Passing References by Reference ............................. 77
  - Passing Values by Reference .................................. 78
  - Working with Output Parameters .............................. 79
- Limitations of By-Reference Parameters ........................ 82
  - Property Values ............................................. 82
  - Overloading on By-Reference Parameters ...................... 83
  - Using Fields ................................................ 84
  - Extension Methods ........................................... 87
- Side Effects and Direct Effects ............................... 88
  - Mutation vs. Creation ....................................... 89
  - Declarative Code and Performance ............................ 91
- Read-Only References and Returning by Reference ................ 92
  - Returning Values by Reference ............................... 94
  - Preventing Modifications to Data ............................ 95
  - Keeping By-Reference Variables Within Scope .................. 97
  - Considering Performance vs. Simplicity ...................... 101
- Final Word on Mutable By-Reference Parameters ................ 102
- Summary ....................................................... 103
