
```
char *EXP_COM[] = {
char *RV_TIME[] = {


int summary(void *arg, void *arg)
```

## C PROGRAMMING

### POCKET PRIMER

![](img/f65c0e06799cea6adc38157c506f310f_0_0.png)

![](img/f65c0e06799cea6adc38157c506f310f_0_1.png)

OSWALD CAMPESATO

## C PROGRAMMING

### *Pocket Primer*

(except for defective materials used in manufacturing the book or due to faulty workmanship).

The author, developers, and the publisher of any accompanying content, and anyone involved in the composition, production, and manufacturing of this work will not be liable for damages of any kind arising out of the use of (or the inability to use) the algorithms, source code, computer programs, or textual material contained in this publication. This includes, but is not limited to, loss of revenue or profit, or other incidental, physical, or consequential damages arising out of the use of this Work.

The sole remedy in the event of a claim of any kind is expressly limited to replacement of the book and/or disc, and only at the discretion of the Publisher. The use of "implied warranty" and certain "exclusions" vary from state to state, and might not apply to the purchaser of this product.

## C Programming

### Pocket Primer

Oswald Campesato

![](img/f65c0e06799cea6adc38157c506f310f_4_0.png)

MERCURY LEARNING AND INFORMATION  
Dulles, Virginia  
Boston, Massachusetts  
New Delhi

Copyright © 2015 by MERCURY LEARNING AND INFORMATION LLC.  
All rights reserved.

This publication, portions of it, or any accompanying software may not be reproduced in any way, stored in a retrieval system of any type, or transmitted by any means, media, electronic display or mechanical display, including, but not limited to, photocopy, recording, Internet postings, or scanning, without prior permission in writing from the publisher.

Publisher: David Pallai  
MERCURY LEARNING AND INFORMATION  
22841 Quicksilver Drive  
Dulles, VA 20166  
info@merclearning.com  
www.merclearning.com  
(800) 232-0223

O. Campesato. C Programming Pocket Primer.  
ISBN: 978-1-68392-388-6

The publisher recognizes and respects all marks used by companies, manufacturers, and developers as a means to distinguish their products. All brand names and product names mentioned in this book are trademarks or service marks of their respective companies. Any omission or misuse (of any kind) of service marks or trademarks, etc. is not an attempt to infringe on the property of others.

Library of Congress Control Number: 2018964991

19 20 21 3 2 1  This book is printed on acid-free paper in the United States of America.

Our titles are available for adoption, license, or bulk purchase by institutions, corporations, etc.

For additional information, please contact the Customer Service Dept. at 800-232-0223 (toll free).

All of our titles are available in digital format at authorcloudware.com and other digital vendors. Companion files (figures and code listings) for this title are available by contacting info@merclearning.com. The sole obligation of MERCURY LEARNING AND INFORMATION to the purchaser is to replace the disc, based on defective materials or faulty workmanship, but not based on the operation or functionality of the product.

> *I'd like to dedicate this book to my parents—may this bring joy and happiness into their lives.*

## CONTENTS

- *Preface*
- **Chapter 1 Introduction to C**
  - Command Line Tools
    - The gcc Compiler
    - Useful Switches for the gcc Command (optional)
    - The lint-related Utilities (optional)
    - Editors and IDEs
  - What is C?
    - What is Special About C?
    - Major Revisions to C
  - A High-Level View of C Programs
    - The Structure of C Programs
    - Coding Guidelines
    - Keywords in C
  - A Hello World Program in C
    - C Header Files and Libraries
    - Valid Syntax for the main() Function
    - C Program Syntax
    - Compiling C Programs
  - Variable Names in C
    - Assignment Statements
  - Indentation and Code Format
  - The printf() Function
  - Data Types in C
    - The sizeof() Operator in C
  - Operators in C
    - Arithmetic Operators
    - Increment/Decrement Operators
    - Ternary Operator
  - Calculating Ceiling and Floor Values
  - Calculating Absolute Values
  - Calculating Trigonometric Values in C
  - Working with Different Bases in C
  - Working with the char Type in C
  - What are C Arrays?
  - Adding the Numbers in an Array
  - Summary
- **Chapter 2 Conditional Logic and Simple Tasks**
  - Comments in C Programs
  - Simple Conditional Logic
  - Conditional Logic with Logical Errors
  - Arithmetic Operators and Conditional Logic
  - Compound if-else Statements
    - What is “Short Circuiting”?
  - Ranking Numbers with if-else Statements
  - Sequential if Statements
  - Nested if-else Statements
  - Scope of Variables in C
    - Global Variables in C Programs
  - Global Versus Local Variables
  - Type Casting in C
    - Integer Promotion
  - The strcpy() and strncpy() Functions in C
  - Strings and String-related Functions
    - The strcpy() Function
  - Handling User Input in C
    - The getchar() & putchar() Functions: Single Character Functions
    - The scanf() and printf() Functions: Multiple Characters
  - C11 Compliance
    - Checking for C11 Compliance
    - What about C17 Compliance?
  - The fgets() Function (C11 Compliant)
  - The gets() Function (not C11 Compliant)
  - Reading a Single Character from the Command Line
  - Reading an Unformatted Line from the Command Line
  - Reading a Formatted Line from the Command Line
  - The Behavior of the scanf() Function (optional)
  - Reading Multiple Strings from the Command Line
  - User Input for Numeric Calculations
  - Stdin, Stdout, and Stderr
  - Summary
- **Chapter 3 Loops and Arrays**
  - Working with for Loops
  - Working with Break and Continue in for Loops
  - Checking for Leap Years
  - Checking Alphabetic Types
  - Counting Uppercase and Lowercase Characters
  - Checking Character Types
  - Working with Arrays
  - Initializing Arrays
  - Array Values
  - C Functions and Arrays
  - Multi-Dimensional Arrays
  - Calculating the Transpose of a Square Matrix
  - Linear Search in Arrays
  - Reversing an Array of Numbers
  - Finding the Maximum and Minimum in Arrays
  - Deleting an Element from an Array
  - Strings and for Loops
  - Counting Words in a Line of Text
  - Working with Nested for Loops
  - Working with while Loops
  - Reading an Entire Line from the Command Line
  - The switch Statement
  - Working with Arrays of Numbers
  - Working with Arrays of Strings
  - Using a while loop to Find the Divisors of a Number
  - Using a while loop to Find Prime Numbers
  - Summary
- **Chapter 4 Functions in C**
  - Working with Built-in Functions in C
  - Pass by Reference versus Pass by Value
  - Built-in Character Functions
  - Converting Between Data Types
  - Defining a Simple Custom Function
    - Function Prototypes
  - Function Parameters in C Functions
  - C99 Syntax for User-Defined Functions in C
  - K&R Style Function Definitions
  - Converting Strings to Integers and Float Values
  - Printing a String to a Buffer with sprintf()
    - Buffer Manipulation Functions
  - Passing a One-Dimensional Array as an Argument
  - Finding a Character in a String
  - Converting Strings to Decimal Values
  - Display a List of Prime Numbers
  - What is Recursion?
    - Calculating Factorial Values
    - Calculating Fibonacci Numbers via Recursion
    - Calculating the Power of a Number via Recursion
    - Calculating the Number of Digits of a Number via Recursion
    - Calculating the Sum of the Digits of a Number via Recursion
    - Calculating the GCD of Two Numbers via Recursion
    - Calculating the LCM of Two Numbers via Recursion
  - Summary
- **Chapter 5 Working with Pointers in C**
  - What are Pointers?
    - Simple Examples of Pointers
    - const Pointers
