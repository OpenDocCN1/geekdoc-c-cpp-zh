

## Wiley Finance Series

### Financial Instrument Pricing Using C++

Second Edition

DANIEL J. DUFFY

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_0_0.png)

### Financial Instrument Pricing Using C++ 2e

Founded in 1807, John Wiley & Sons is the oldest independent publishing company in the United States. With offices in North America, Europe, Australia and Asia, Wiley is globally committed to developing and marketing print and electronic products and services for our customers’ professional and personal knowledge and understanding.

The Wiley Finance series contains books written specifically for finance and investment professionals as well as sophisticated individual investors and their financial advisors. Book topics range from portfolio management to e-commerce, risk management, financial engineering, valuation and financial instrument analysis, as well as much more.

For a list of available titles, visit our website at www.WileyFinance.com.

### Financial Instrument Pricing Using C++ 2e

DANIEL J. DUFFY

WILEY

This edition first published 2018  
© 2018 John Wiley & Sons, Ltd

### Registered Office

John Wiley & Sons Ltd, The Atrium, Southern Gate, Chichester, West Sussex, PO19 8SQ, United Kingdom

For details of our global editorial offices, for customer services and for information about how to apply for permission to reuse the copyright material in this book please see our website at www.wiley.com.

All rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or by any means, electronic, mechanical, photocopying, recording or otherwise, except as permitted by the UK Copyright, Designs and Patents Act 1988, without the prior permission of the publisher.

Wiley publishes in a variety of print and electronic formats and by print-on-demand. Some material included with standard print versions of this book may not be included in e-books or in print-on-demand. If this book refers to media such as a CD or DVD that is not included in the version you purchased, you may download this material at http://booksupport.wiley.com. For more information about Wiley products, visit www.wiley.com.

Designations used by companies to distinguish their products are often claimed as trademarks. All brand names and product names used in this book are trade names, service marks, trademarks or registered trademarks of their respective owners. The publisher is not associated with any product or vendor mentioned in this book.

Limit of Liability/Disclaimer of Warranty: While the publisher and author have used their best efforts in preparing this book, they make no representations or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaim any implied warranties of merchantability or fitness for a particular purpose. It is sold on the understanding that the publisher is not engaged in rendering professional services and neither the publisher nor the author shall be liable for damages arising therefrom. If professional advice or other expert assistance is required, the services of a competent professional should be sought.

### Library of Congress Cataloging-in-Publication Data

**Names:** Duffy, Daniel J., author.  
**Title:** Financial instrument pricing using C++ / Daniel J. Duffy.  
**Description:** Second Edition. | Hoboken : Wiley, [2018] | Series: Wiley finance series | Revised and updated edition of the author’s Financial instrument pricing using C++, c2004. | Includes bibliographical references and index.  
**Identifiers:** LCCN 2018017672 (print) | LCCN 2018019643 (ebook) | ISBN 9781119170495 (Adobe PDF) | ISBN 9781119170488 (ePub) | ISBN 9780470971192 (hardcover) | ISBN 9781119170495 (ePDF) | ISBN 9781119170518 (Obook)  
**Subjects:** LCSH: Investments–Mathematical models. | Financial engineering. | C++ (Computer program language)  
**Classification:** LCC HG4515.2 (ebook) | LCC HG4515.2 .D85 2018 (print) | DDC 332.602851/533–dc23  
LC record available at https://lccn.loc.gov/2018017672

A catalogue record for this book is available from the British Library.

ISBN 978-0-470-97119-2 (hardback)    ISBN 978-1-119-17049-5 (ePDF)  
ISBN 978-1-119-17048-8 (ePub)       ISBN 978-1-119-17051-8 (Obook)

10  9  8  7  6  5  4  3  2  1

Cover design: Wiley  
Cover images: © whiteMocca/Shutterstock

Set in 10/12pt Times by Aptara Inc., New Delhi, India  
Printed in Great Britain by TJ International Ltd, Padstow, Cornwall, UK

## Contents

### CHAPTER 1 A Tour of C++ and Environs 1

- 1.1 Introduction and Objectives 1
- 1.2 What is C++? 1
- 1.3 C++ as a Multiparadigm Programming Language 2
- 1.4 The Structure and Contents of this Book: Overview 4
- 1.5 A Tour of C++11: Black–Scholes and Environs 6
  - 1.5.1 System Architecture 6
  - 1.5.2 Detailed Design 7
  - 1.5.3 Libraries and Algorithms 8
  - 1.5.4 Configuration and Execution 10
- 1.6 Parallel Programming in C++ and Parallel C++ Libraries 12
- 1.7 Writing C++ Applications; Where and How to Start? 14
- 1.8 For Whom is this Book Intended? 16
- 1.9 Next-Generation Design and Design Patterns in C++ 16
- 1.10 Some Useful Guidelines and Developer Folklore 17
- 1.11 About the Author 18
- 1.12 The Source Code and Getting the Source Code 19

### CHAPTER 2 New and Improved C++ Fundamentals 21

- 2.1 Introduction and Objectives 21
- 2.2 The C++ Smart Pointers 21
  - 2.2.1 An Introduction to Memory Management 22
- 2.3 Using Smart Pointers in Code 23
  - 2.3.1 Class `std::shared_ptr` 23
  - 2.3.2 Class `std::unique_ptr` 26
  - 2.3.3 `std::weak_ptr` 28
  - 2.3.4 Should We Use Smart Pointers and When? 29
- 2.4 Extended Examples of Smart Pointers Usage 30
  - 2.4.1 Classes with Embedded Pointers 30
  - 2.4.2 Re-engineering Object-Oriented Design Patterns 31
- 2.5 Move Semantics and Rvalue References 34
  - 2.5.1 A Quick Overview of Value Categories 34
  - 2.5.2 Why Some Classes Need Move Semantics 35
  - 2.5.3 Move Semantics and Performance 37
  - 2.5.4 Move Semantics and Shared Pointers 38
- 2.6 Other Bits and Pieces: Usability Enhancements 39
  - 2.6.1 Type Alias and Alias Templates 39
  - 2.6.2 Automatic Type Deduction and the `auto` Specifier 41
  - 2.6.3 Range-Based for Loops 42
  - 2.6.4 `nullptr` 43
  - 2.6.5 New Fundamental Data Types 44
  - 2.6.6 Scoped and Strongly Typed Enumerations 44
  - 2.6.7 The Attribute `[[deprecated]]` 45
  - 2.6.8 Digit Separators 47
  - 2.6.9 Unrestricted Unions 47
  - 2.6.10 `std::variant` (C++17) and `boost::variant` 49
- 2.7 Summary and Conclusions 52
- 2.8 Exercises and Projects 52

### CHAPTER 3 Modelling Functions in C++

- 3.1 Introduction and Objectives 59
- 3.2 Analysing and Classifying Functions 60
  - 3.2.1 An Introduction to Functional Programming 60
  - 3.2.2 Function Closure 61
  - 3.2.3 Currying 62
  - 3.2.4 Partial Function Application 62
  - 3.2.5 Lambda (Anonymous) Functions 62
  - 3.2.6 Eager and Lazy Evaluation 63
  - 3.2.7 Fold 63
  - 3.2.8 Continuation 63
- 3.3 New Functionality in C++: `std::function<>` 64
- 3.4 New Functionality in C++: Lambda Functions and Lambda Expressions 65
  - 3.4.1 Basic Syntax 65
  - 3.4.2 Initial Examples 66
  - 3.4.3 Lambda Functions and Classes: Capturing Member Data 68
  - 3.4.4 Storing Lambda Functions 69
- 3.5 Callable Objects 69
- 3.6 Function Adapters and Binders 70
  - 3.6.1 Binding and Function Objects 72
  - 3.6.2 Binding and Free Functions 73
  - 3.6.3 Binding and Subtype Polymorphism 74
- 3.7 Application Areas 75
- 3.8 An Example: Strategy Pattern New Style 75
- 3.9 Migrating from Traditional Object-Oriented Solutions: Numerical Quadrature 78
- 3.10 Summary and Conclusions 81
- 3.11 Exercises and Projects 82

### CHAPTER 4 Advanced C++ Template Programming

- 4.1 Introduction and Objectives 89
- 4.2 Preliminaries 91
  - 4.2.1 Arithmetic Operators and Implicit Conversions 91
  - 4.2.2 A Primer on Variadic Functions 93
  - 4.2.3 Value Categories 94
- 4.3 `decltype` Specifier 94
  - 4.3.1 Initial Examples 94
  - 4.3.2 Extended Examples 96
  - 4.3.3 The Auxiliary Trait `std::declval` 98
  - 4.3.4 Expressions, *lvalues*, *rvalues* and *xvalues* 99
- 4.4 Life Before and After `decltype` 101
  - 4.4.1 Extending the STL to Support Heterogeneous Data Types 103
- 4.5 `std::result_of` and SFINAE 106
- 4.6 `std::enable_if` 108
- 4.7 Boost `enable_if` 112
- 4.8 `std::decay` Trait 114
- 4.9 A Small Application: Quantities and Units 115
- 4.10 Conclusions and Summary 118
- 4.11 Exercises and Projects 118

### CHAPTER 5 Tuples in C++ and their Applications

- 5.1 Introduction and Objectives 123
- 5.2 An `std::pair` Refresher and New Extensions 123
- 5.3 Mathematical and Computer Science Background 128
- 5.4 Tuple Fundamentals and Simple Examples 130
- 5.5 Advanced Tuples 130
  - 5.5.1 Tuple Nesting 130
  - 5.5.2 Variadic Tuples 132
- 5.6 Using Tuples in Code 133
  - 5.6.1 Function Return Types 133
  - 5.6.2 Function Input Arguments 136
- 5.7 Other Related Libraries 138
  - 5.7.1 Boost Tuple 138
  - 5.7.2 Boost Fusion 139
- 5.8 Tuples and Run-Time Efficiency 140
- 5.9 Advantages and Applications of Tuples 142
- 5.10 Summary and Conclusions 143
- 5.11 Exercises and Projects 143

### CHAPTER 6 Type Traits, Advanced Lambdas and Multiparadigm Design in C++

- 6.1 Introduction and Objectives 147
- 6.2 Some Building Blocks 149

