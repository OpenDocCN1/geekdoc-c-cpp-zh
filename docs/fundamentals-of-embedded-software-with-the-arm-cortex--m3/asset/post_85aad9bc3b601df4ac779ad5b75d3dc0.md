
## FUNDAMENTALS OF EMBEDDED SOFTWARE
### with the ARM® Cortex-M3
### SECOND EDITION
### DANIEL W. LEWIS

## Fundamentals of Embedded Software
### with the ARM® Cortex-M3

This page intentionally left blank

## Fundamentals of Embedded Software with the ARM® Cortex-M3
### Second Edition
### Daniel W. Lewis
Santa Clara University
PEARSON

- Vice President and Editorial Director, ECS: Marcia J. Horton
- Executive Editor: Bill Zobrist
- Executive Editor, Production: Vince O'Brien
- Vice President, Marketing Manager: Tim Galligan
- Marketing Assistant: Jon Bryant
- Permissions Project Manager: Karen Sanatar
- Senior Manufacturing Coordinator: Trudy Pitts
- Production Project Manager: Scott Disanno
- Creative Director: Jayne Conte
- Cover Designer: Bruce Kenselaar
- Corporate Illustration: Greg Dulles & Alex
- Composition: Joyce India
- Full-Service Project Management: Pavithra Jayapaul, Jouve India
- Printer/Binder: Courier Westford
- Cover Printer: Lehigh-Phoenix
- Typeface: 10/12 Times-Roman

Credits and acknowledgments borrowed from other sources and reproduced, with permission, in this textbook appear on appropriate page within text.

Copyright © 2003, 2002 by Pearson Education, Inc., Upper Saddle River, NJ 07458
All rights reserved. Manufactured in the United States of America. This publication is protected by Copyright and permissions should be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. For information regarding permission(s), write to: Rights and Permissions Department.
Pearson Prentice Hall™, is a trademark of Pearson Education, Inc.
Permissions Department, One Lake Street, Upper Saddle River, NJ 07458.

Many of the designations by manufacturers and seller to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed in initial caps or all caps.
ARM is a registered trademark of ARM Ltd., 110 Fulbourn Road, Cambridge, GB-CB1 9NJ, Great Britain.
MATLAB is a registered trademark of The MathWorks, Inc., 3 Apple Hill Drive, Natick, MA 01760-2098.

The author and publisher of this book have used their best efforts in preparing this book. These efforts include the development, research, and testing of the theories and programs to determine their effectiveness. The author and publisher make no warranty of any kind, expressed or implied, with regard to these programs or the documentation contained in this book. The author and publisher shall not be liable in any event for incidental or consequential damages with, or arising out of, the furnishing, performance, or use of these programs.

- Pearson Education Ltd., London
- Pearson Education Australia Pty. Ltd.
- Pearson Education Singapore, Pte. Ltd.
- Pearson Education North Asia, Ltd.
- Pearson Education Australia, Ltd., Hong Kong
- Pearson Education de Mexico S.A. de C.V.
- Pearson Education — Japan
- Pearson Education Malaysia, Pte. Ltd.
- Pearson Education, Inc., Upper Saddle River, New Jersey

### Library of Congress Cataloging-in-Publication Data

Lewis, D.W. (Daniel Wesley)
Fundamentals of embedded software : with the ARM® Cortex-M3 / Daniel W. Lewis. — 2nd ed.
p. cm.
Includes bibliographical references and index.
ISBN-13: 978-0-13-291654-7 (alk. paper)
ISBN-10: 0-13-291654-1 (alk. paper)
1. Embedded computer systems—Programming. 2. C (Computer program language) I. Title.
TK7895.E42L49 2012
005. 13'3—dc23
2011043104

10 9 8 7 6 5 4 3 2 1
ISBN-13: 978-0-13-291654-7
ISBN-10: 0-13-291654-1
PEARSON

## Dedication

It may have been many more years ago than I would care to admit, but I do still remember what it was like to be an undergraduate. Like my own students, I too had to take an occasional class in which much of the material came from slides and handouts because the instructor was writing a textbook for the course. So, to all those students who have had to suffer through this same experience with me, who have unknowingly helped me organize and clarify the material, who have tactfully pointed out my mistakes, and who have fueled my inspiration—thank you. This book is for you and those that follow in your footsteps.

This page intentionally left blank

## Contents

- Preface xiii

## Chapter 1 Introduction 1

### 1.1 What is an Embedded System? 1
### 1.2 What Is Unique about the Design Goals for Embedded Software? 3
### 1.3 What Does "Real-Time" Mean? 5
### 1.4 What Does "Multithreading" Mean? 5
### 1.5 How Powerful Are Embedded Processors? 6
### 1.6 What Programming Languages are Used? 6
### 1.7 How Is Building an Embedded Application Different? 7
### 1.8 How Big Are Typical Embedded Programs? 9
### Problems 10

## Chapter 2 Data Representation 11

### 2.1 Fixed-Precision Binary Numbers 11
### 2.2 Positional Number Systems 13
### 2.2.1 Binary-to-Decimal Conversion 14
### 2.2.2 Decimal-to-Binary Conversion 14
### 2.2.3 Hexadecimal: A Shorthand for Binary 17
### 2.2.4 Fixed Precision, Rollover, and Overflow 18
### 2.3 Binary Representation of Integers 19
### 2.3.1 Signed Integers 20
### 2.3.2 Positive and Negative Representations of the Same Magnitude 20
### 2.3.3 Interpreting the Value of a 2's-Complement Number 21
### 2.3.4 Changing the Sign of Numbers with Integer and Fractional Parts 22
### 2.3.5 Binary Addition and Subtraction 23
### 2.3.6 Range and Overflow 25
### 2.4 Binary Representation of Real Numbers 26
### 2.4.1 Floating-Point Real Numbers 26
### 2.4.2 Fixed-Point Real Numbers 28
### 2.5 ASCII Representation of Text 28
### 2.6 Binary-Coded Decimal (BCD) 31
### Problems 32

## Chapter 3 Implementing Arithmetic 35

### 3.1 2's-Complement and Hardware Complexity 35
### 3.2 Multiplication and Division 38
### 3.2.1 Signed Versus Unsigned Multiplication 38
### 3.2.2 Shifting Instead of Multiplying or Dividing by Powers of 2 38
### 3.2.3 Multiplying by an Arbitrary Constant 40
### 3.2.4 Dividing by an Arbitrary Constant 41
### 3.3 Arithmetic for Fixed-Point Reals 41
### 3.3.1 Fixed-Point Using a Universal 16.16 Format 44
### 3.3.2 Fixed-Point Using a Universal 32.32 Format 45
### 3.3.3 Multiplication of 32.32 Fixed-Point Reals 46
### 3.3.4 Example: Multiplying two 4.4 Fixed-Point Reals 49

### Problems 50

## Chapter 4 Getting the Most out of C 52

### 4.1 Integer Data Types 52
### 4.1.1 Integer Range and the Standard Header File LIMITS.H 54
### 4.2 Boolean Data Types 56
### 4.3 Mixing Data Types 57
### 4.4 Manipulating Bits In Memory 58
### 4.4.1 Testing Bits 60
### 4.4.2 Setting, Clearing, and Inverting Bits 61
### 4.4.3 Extracting Bits 62
### 4.4.4 Inserting Bits 62
### 4.5 Manipulating Bits In Input/Output Ports 63
### 4.5.1 Write-Only I/O Devices 63
### 4.5.2 I/O Devices Differentiated by Reads Versus Writes 65
### 4.5.3 I/O Devices Differentiated by Sequential Access 65
### 4.5.4 I/O Devices Differentiated by Bits in the Written Data 66
### 4.6 Accessing Memory-Mapped I/O Devices 66
### 4.6.1 Accessing Data Using a Pointer 67
### 4.6.2 Arrays, Pointers, and the "Address of" Operator 68
### 4.7 Structures 69
### 4.7.1 Packed Structures 70
### 4.7.2 Bit Fields 71
### 4.8 Variant Access 72
### 4.8.1 Casting the Address of an Object 73
### 4.8.2 Using Unions 74

### Problems 75

## Chapter 5 Programming in Assembly Part 1: Computer Organization 80

### 5.1 Memory 82
### 5.1.1 Data Alignment 83
### 5.2 The Central Processing Unit (CPU) 85
### 5.2.1 Other Registers 86
### 5.2.2 The Fetch-Execute Cycle 86
### 5.3 Input/Output 89
### 5.4 Introduction to the ARM® Cortex™-M3 v7M Architecture 90
### 5.4.1 Internal Organization 90
### 5.4.2 Instruction Pipelining 91
### 5.4.3 Memory Model 93
### 5.4.4 Bit-Banding 93
### 5.5 ARM Assembly Language 96
### 5.5.1 Instruction Formats and Operands 96
### 5.5.2 Translating Assembly into Binary 98
### Problems 98

## Chapter 6 Programming in Assembly Part 2: Data Manipulation 102

### 6.1 Loading Constants into Registers 102
### 6.2 Loading Memory Data into Registers 103
### 6.3 Storing Data from Registers to Memory 105
### 6.4 Converting Simple C Assignment Statements into ARM Assembly 106
### 6.5 Memory Address Calculations 107
### 6.6 Memory Addressing Examples 108
### 6.6.1 Translating C Pointer Expressions to Assembly 109
### 6.6.2 Translating C Subscript Expressions to Assembly 111
### 6.6.3 Translating Structure References to Assembly 111
### 6.7 Stack Instructions 112
### 6.8 Data Processing Instructions 113
### 6.8.1 Updating the Flags in the APSR 113
### 6.8.2 Arithmetic Instructions 114
### 6.8.3 Bit Manipulation Instructions 115
### 6.8.4 Shift Instructions 116
### 6.8.5 Bit Field Manipulation Instructions 118
### 6.8.6 Miscellaneous Bit, Byte, and Half-Word Instructions 119
### Problems 120
