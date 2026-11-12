
## SIXTH EDITION

## Data Abstraction & Problem Solving with C++

## WALLS AND MIRRORS

FRANK M. CARRANO | TIMOTHY HENRY

## C++ Reserved Keywords

C++ reserves and gives predefined meanings to the following keywords. You may not redefine keywords or use them for other purposes. Keywords that appear in color are new since C++11.

| alignas | decltype | namespace | struct |
| --- | --- | --- | --- |
| alignof | default | new | switch |
| and | delete | noexcept | template |
| and_eq | do | not | this |
| asm | double | not_eq | thread_local |
| auto | dynamic_cast | nullptr | throw |
| bitand | else | operator | true |
| bitor | enum | or | try |
| bool | explicit | or_eq | typedef |
| break | export | private | typeid |
| case | extern | protected | typename |
| catch | false | public | union |
| char | float | register | unsigned |
| char16_t | for | reinterpret_cast | using |
| char32_t | friend | return | virtual |
| class | goto | short | void |
| compl | if | signed | volatile |
| const | inline | sizeof | wchar_t |
| const_cast | int | static | while |
| constexpr | long | static_assert | xor |
| continue | mutable | static_cast | xor_eq |

| Operator | Meaning | Associativity | Usage |
|---|---|---|---|
| * | multiply | left | `expr * expr` |
| / | divide | left | `expr / expr` |
| % | modulo | left | `expr % expr` |
| + | add | left | `expr + expr` |
| - | subtract | left | `expr - expr` |
| << | bitwise shift left‡ | left | `expr << expr` |
| >> | bitwise shift right‡ | left | `expr >> expr` |
| < | less than | left | `expr < expr` |
| <= | less than or equal to | left | `expr <= expr` |
| > | greater than | left | `expr > expr` |
| >= | greater than or equal to | left | `expr >= expr` |
| == | equal | left | `expr == expr` |
| != | not equal | left | `expr != expr` |
| & | bitwise AND | left | `expr & expr` |
| ^ | bitwise EXCLUSIVE OR | left | `expr ^ expr` |
| `|` | bitwise OR | left | `expr | expr` |
| && | logical AND | left | `expr && expr` |
| || | logical OR | left | `expr || expr` |
| ? : | conditional | left | `expr ? expr : expr` |
| = | assign | left | `lvalue = expr` |
| *= | multiply and assign | left | `lvalue *= expr` |
| /= | divide and assign | left | `lvalue /= expr` |
| %= | modulo and assign | left | `lvalue %= expr` |
| += | add and assign | left | `lvalue += expr` |
| -= | subtract and assign | left | `lvalue -= expr` |
| <<= | shift left and assign | left | `lvalue <<= expr` |
| >>= | shift right and assign | left | `lvalue >>= expr` |
| &= | AND and assign | left | `lvalue &= expr` |
| |= | OR and assign | left | `lvalue |= expr` |
| ^= | EXCLUSIVE OR and assign | left | `lvalue ^= expr` |
| , | comma | left | `expr, expr` |

‡ Typically overloaded for I/O

## Data Abstraction & Problem Solving with C++

## WALLS AND MIRRORS

## SIXTH EDITION

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_3_0.png)

Frank M. Carrano
University of Rhode Island

Timothy Henry
University of Rhode Island

PEARSON

Vice President and Editorial Director, ECS: Marcia J. Horton
Executive Editor: Tracy Johnson
Associate Editor: Carole Snyder
Director of Marketing: Christy Lesko
Marketing Manager: Yez Alayan
Marketing Assistant: Jon Bryant
Director of Production: Erin Gregg
Managing Editor: Jeff Holcomb
Associate Managing Editor: Robert Engelhardt
Manufacturing Buyer: Lisa McDowell
Art Director: Anthony Gemmellaro

Cover Designer: Liz Harasymczuk
Permissions Supervisor: Michael Joyce
Permissions Administrator: Jennell Forscher
Director, Image Asset Services: Annie Atherton
Manager, Visual Research: Karen Sanatar
Cover Art: Shutterstock/SVLuma
Media Project Manager: Renata Butera
Full-Service Project Manager: Rose Kernan
Composition: Cenveo Publisher Services / Nesbitt
Printer/Binder: Edwards Brothers
Cover Printer: Lehigh-Phoenix Color/Hagerstown

Credits and acknowledgments borrowed from other sources and reproduced, with permission, in this textbook appear on the appropriate page within text.

Copyright © 2013, 2007, 2005 Pearson Education, Inc., publishing as Addison-Wesley. All rights reserved. Printed in the United States of America. This publication is protected by Copyright, and permission should be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. To obtain permission(s) to use material from this work, please submit a written request to Pearson Education, Inc., Permissions Department, One Lake Street, Upper Saddle River, New Jersey 07458, or you may fax your request to 201-236-3290.

Many of the designations by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed in initial caps or all caps.

Library of Congress Cataloging-in-Publication Data on file.

10 9 8 7 6 5 4 3 2 1

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_4_0.png)

ISBN 10: 0-13-292372-6
ISBN 13: 978-0-13-292372-9

Welcome to the sixth edition of Data Abstraction & Problem Solving with C++: Walls and Mirrors. Since the publication of the first edition, we all have gained experience with teaching data abstraction in an object-oriented way using C++. This edition reflects that experience and the many comments and suggestions received from faculty and students alike.

I am happy to introduce Dr. Timothy Henry, my co-author and colleague at the University of Rhode Island. Together, we have given this book a much needed revision and a new look. However, our goal remains to give students a superior foundation in data abstraction, object-oriented programming, and other modern problem-solving techniques. All C++ code has been rewritten with a focus on safe and secure programming practices. It also adheres to the C++11 standard.

We hope that you enjoy reading this book. Like many others before you, you can learn—or teach—data structures in an effective and sustainable way.

## Talk to Us

Walls and Mirrors continues to evolve. Your comments, suggestions, and corrections will be greatly appreciated. Here are a few ways to reach us:

- E-mail: carrano@acm.org
- Facebook: www.facebook.com/makingitreal
- Twitter: twitter.com/Frank_M_Carrano
- Blog: frank-m-carrano.com/makingitreal

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_5_0.png)

## A Note to Students

The topics that we cover in this book deal with the various ways of organizing data so that a given application can access and manipulate data in an efficient way. These topics are fundamental to your future study of computer science, as they provide you with the foundation of knowledge required to create complex and reliable software. Whether you are interested in designing video games or software for robotic-controlled surgery, the study of data structures is vital to your success. Even if you do not study all of the topics in this book now, you are likely to encounter them later. We hope that you will enjoy reading the book, and that it will serve as a useful reference tool for your future courses.

The walls and mirrors in the title represent two fundamental problem-solving techniques that appear throughout the presentation. Data abstraction isolates and hides the implementation details of a module from the rest of the program, such as a wall can isolate and hide you from your neighbor. Recursion is a repetitive technique that solves a problem by solving exactly the same but smaller problems, much as images in facing mirrors grow smaller with each reflection.

Please be sure to browse the rest of this preface to see the features that will help you in your studies. To help you learn and to review for exams, we have included such learning aids as video tutorials (VideoNotes), checkpoint questions with answers, margin notes, programming tips, chapter summaries, and a glossary. As a help during programming, you will find C++ reference material in the appendixes and inside the covers. You should review the list of this book’s features given later in this preface in the section “Features to Enhance Learning.”

The presentation makes some basic assumptions about your knowledge of C++. Some of you may need to review this language or learn it for the first time by consulting the appendixes of this book. This book covers C++ classes and other relevant aspects of the language in new C++ Interludes that occur throughout the book between certain chapters. These interludes do not assume that you already know their topics. We assume no experience with recursive functions, which are included in Chapters 2 and 5.

All of the C++ source code that appears in this book is available for your use. Later in this preface, the description of supplementary materials tells you how to obtain these files, as well as the VideoNotes and other online documents.
