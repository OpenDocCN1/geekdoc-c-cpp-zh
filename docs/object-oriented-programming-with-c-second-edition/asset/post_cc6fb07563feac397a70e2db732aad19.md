
# Object Oriented Programming with C++

SECOND EDITION

Sourav Sahay
Lead Consultant
Capgemini
Detroit, Michigan

# OXFORD UNIVERSITY PRESS

# OXFORD UNIVERSITY PRESS

Oxford University Press is a department of the University of Oxford. It furthers the University's objective of excellence in research, scholarship, and education by publishing worldwide. Oxford is a registered trade mark of Oxford University Press in the UK and in certain other countries.

Published in by
Oxford University Press
YMCA Library Building, 1 Jai Singh Road, New Delhi 110001, India

© Oxford University Press 2006, 2012

The moral rights of the author/s have been asserted.

First Edition Published in 2006
Second Edition Published in 2012

All rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or by means, without the prior permission in writing of Oxford University Press, or as expressly permitted by law, by licence, or under terms agreed with the appropriate reprographic rights organization. Enquiries regarding permission outside the scope of the above should be sent to the Rights Department: Oxford University Press, at the address above.

You must not circulate this work in any other form and you must impose this same condition on any acquirer.

ISBN-13: 978-0-19-806530-2
ISBN-10: 0-19-806530-2

Typeset in Times New Roman
by Recto Graphics, Delhi 110096

Printed in India by Adage Printers (P) Ltd., Noida 201301 U.P.

# Preface to the First Edition

C++ made its advent in the early 1980s and enabled programmers to write their programs the object-oriented way. For this reason, the language quickly gained popularity and became a programming language of choice. Despite the development of a number of competing object-oriented languages including Java, C++ has successfully maintained its position of popularity.

C++ starts where C stops. C++ is a superset of C. All the language features of C language appear in C++ with little or no modification. Over and above such features, C++ provides a number of extra features, which provide the language its object-oriented character.

# About the Book

The continued popularity of C++ has led to considerable literature. Inumerable books, journals, magazines, and articles have been written on C++. So, why another book on C++?

The aim of the book is to thoroughly explain all aspects of the language constructs provided by C++, while doing full justice to the commonly explained topics of C++, the book does not neglect the advanced and new concepts of C++ that are not widely taught.

This book is a power-packed instruction guide for Object-Oriented Programming and C++.

The purpose of this book is two-fold:

- To clarify the fundamentals of the Object-Oriented Programming System
- To provide an in-depth treatment of each feature and language construct of C++

This book emphasizes the Object-Oriented Programming System—its benefits and its superiority over the conventional Procedure-Oriented Programming System.

This book starts directly with C++ since the common features of C and C++ are anyway covered in books. Each feature of C++ is covered from the practical point of view. Instead of brief introductions, this book gives an in-depth explanation of the rationale and proper use of each object-oriented feature of C++.

To help the readers assimilate the large volume of knowledge contained in this book, an adequate number of example programs, well-designed diagrams, and analogies with the real world have been given. Some program examples given in this book are abstract in nature to help readers focus on the concept discussed.

# Acknowledgements

First, I thank my parents for the value of valuable lessons of life including the value of hardwork and the value of good education (neither of which I have learnt yet!). I also thank my wife Madhvi for her patience, her encouragement, and also for having tolerated long periods of silence and temper tantrums! Thanks (rather apologies) to my little daughters, Surabhi and Sakshi, who tolerated Papa’s frequent refusals to take them on outings.

I thank Dr David Mulvaney and Dr Sekharjit Datta of the University of Loughborough for their valuable guidance, encouragement, and inspiration. My teachers always encouraged me to think big and to think independently. My sincerest gratitude to each one of them.

The editorial team of Oxford University Press deserves my heartfelt thanks for their guidance and for their timely reminders about the deadlines I would have definitely missed otherwise!

Feedback about the book is most welcome. Readers are requested and encouraged to send their feedback to the author’s mail id sourav1903@yahoo.com.

Sourav Sahay

# Preface to the Second Edition

The object-oriented programming system OOPS enables a programmer to model real-world objects. It allows the programmer to add characteristics like data security, data encapsulation, etc.

In the procedure-oriented programming system, procedures are dissociated from data and are not a part of it. Instead, they receive structure variables, or their addresses, and work upon them. This program design is centered around procedures. While this may seem obvious, this programming pattern has its drawbacks, a major one being that the data is not secure. It can be manipulated by any procedure.

It is the lack of data security of the procedure-oriented programming system that led to OOPS, in which, with the help of a new programming construct and new keywords, associated functions of the data structure can be given exclusive rights to work upon its variables. There is another characteristic of real-world objects—a guaranteed initialization of data. Programming languages that implement OOPS enable library programmers to incorporate this characteristic of real-world objects into structure variables. Library programmers can ensure a guaranteed initialization of data members of structures to the desired values. For this, application programmers do not need to write code explicitly.

OOPS further supports the following concepts:

- **Inheritance**: This feature allows a class to inherit the data and function members of an existing class.
- **Data abstraction**: Data abstraction is a virtue by which an object hides its internal operations from the rest of the program.
- **Modularity**: This feature supports dividing a program into small segments and implement those segments using different functions.
- **Polymorphism**: Through polymorphism, functions with different set of formal arguments can have the same name.

The first edition covered the fundamentals of the object oriented programming system in depth. These explanations in the first edition hold true for any programming language that supports OOPS. This second edition enhances coverage, as listed below.

# New to this Edition

- New chapter on data structures containing new and original algorithms, especially elegant and simple recursive algorithm for inserting nodes into trees. The explanations are elaborate and full of diagrams.
- New sections on explicit constructors, command line arguments, and re-throwing exceptions.
- Expanded glossary.
- Accompanying CD contains all the program codes given in the text.

# Key Features

- Simple and concise language eases the understanding of complex concepts that have made C++ powerful but enigmatic.
- Plenty of solved examples with complete program listing and test cases to reinforce learning.
- Review questions and writing exercises at the end of each chapter to provide additional practice.
- Self-tests at the end of the book to prepare the students for examinations.

# Organization of the Book

A brief knowledge of C language is a prerequisite for this book. The readers need to know how programs are written in C, data types, decision-making and looping constructs, operators, functions, header files, pointers, and structures.

Chapter 1 contains an explanation of the procedure-oriented programming system, the role played by structures in this system, its drawbacks and how these drawbacks led to the creation of OOPS. The meaning of modelling real-world objects by the object-oriented programming system has been clearly explained. The chapter explains a study of the non-object features of C++.

Chapter 2 is devoted to the study of objects and classes. It gives a thorough explanation of the class construct of C++. Superiority of the class construct of C++ over the structure of C language is explained. A description of the various types and features of functions and member data is included. Other concepts are included as namespaces, arrays of objects, arrays in objects, and nested classes.

Chapter 3 deails with dynamic memory management. It explains the use of the new and the delete operators. It also explains the method of specifying our new handler for handling out-of-memory conditions.

Chapter 4 explains constructors and destructors. It discusses their importance, their features, and the method of defining them.

Chapter 5 is devoted to inheritance. Concepts like base class, derived class, base class pointer, and derived class pointer are covered. The protected keyword and the it specifiers of deriving by different access specifiers are explained. This chapter describes various types of inheritance.

Chapter 6 gives a detailed explanation of one of the most striking features of C++dynamic polymorphism. This chapter describes the virtual functions and how it enables C++ programmers to extend class libraries. The importance of pure functions and clone classes is also explained.

Chapter 7 describes the standard C++ library for handling streams. It explains the two types of input and output—text mode and binary mode. Input and output from disk files are explained. The chapter also describes the use of error-handling routines of the C++ stream stream and manipulators.

Chapter 8 is devoted to operator overloading, type conversion, new styles, and RTTI. This chapter explains the various intricacies and the proper use of operator overloading. This chapter also explains how a C++ programmer can implement conventional type type
