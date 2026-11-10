
## PEARSON NEW INTERNATIONAL EDITION

## Compilers

## Principles, Techniques, and Tools

Aho   Lam   Sethi   Ullman

## Second Edition

![](img/2a44b9071782fade81f3050c3b718341_0_0.png)

## Pearson New International Edition

## Compilers  
Principles, Techniques, and Tools  
Aho Lam Sethi Ullman  
Second Edition

**Pearson Education Limited**
Edinburgh Gate
Harlow
Essex CM20 2JE
England and Associated Companies throughout the world

*Visit us on the World Wide Web at:* www.pearsoned.co.uk

© Pearson Education Limited 2014

All rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, electronic, mechanical, photocopying, recording or otherwise, without either the prior written permission of the publisher or a licence permitting restricted copying in the United Kingdom issued by the Copyright Licensing Agency Ltd, Saffron House, 6–10 Kirby Street, London EC1N 8TS.

All trademarks used herein are the property of their respective owners. The use of any trademark in this text does not vest in the author or publisher any trademark ownership rights in such trademarks, nor does the use of such trademarks imply any affiliation with or endorsement of this book by such owners.

![](img/2a44b9071782fade81f3050c3b718341_2_0.png)

ISBN 10: 1-292-02434-8  
ISBN 13: 978-1-292-02434-9

**British Library Cataloguing-in-Publication Data**  
A catalogue record for this book is available from the British Library

Printed in the United States of America

## Table of Contents

- **Chapter 1. Introduction** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 1
- **Chapter 2. A Simple Syntax-Directed Translator** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 39
- **Chapter 3. Lexical Analysis** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 109
- **Chapter 4. Syntax Analysis** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 191
- **Chapter 5. Syntax-Directed Translation** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 303
- **Chapter 6. Intermediate-Code Generation** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 357
- **Chapter 7. Run-Time Environments** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 427
- **Chapter 8. Code Generation** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 505
- **Chapter 9. Machine-Independent Optimizations** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 583
- **Chapter 10. Instruction-Level Parallelism** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 707
- **Chapter 11. Optimizing for Parallelism and Locality** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 769
- **Appendix A: A Complete Front End** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 903
- **Appendix B: Finding Linearly Independent Solutions** — Alfred V. Aho/Monica S. Lam/Ravi Sethi/Jeffrey D. Ullman — 927
- **Index** — 931

## Chapter 1. Introduction

Programming languages are notations for describing computations to people and to machines. The world as we know it depends on programming languages, because all the software running on all the computers was written in some programming language. But, before a program can be run, it first must be translated into a form in which it can be executed by a computer.

The software systems that do this translation are called *compilers*.

This book is about how to design and implement compilers. We shall discover that a few basic ideas can be used to construct translators for a wide variety of languages and machines. Besides compilers, the principles and techniques for compiler design are applicable to so many other domains that they are likely to be reused many times in the career of a computer scientist. The study of compiler writing touches upon programming languages, machine architecture, language theory, algorithms, and software engineering.

In this preliminary chapter, we introduce the different forms of language translators, give a high level overview of the structure of a typical compiler, and discuss the trends in programming languages and machine architecture that are shaping compilers. We include some observations on the relationship between compiler design and computer-science theory and an outline of the applications of compiler technology that go beyond compilation. We end with a brief outline of key programming-language concepts that will be needed for our study of compilers.

### 1.1 Language Processors

Simply stated, a compiler is a program that can read a program in one language — the *source language* — and translate it into an equivalent program in another language — the *target language*; see Fig. 1.1. An important role of the compiler is to report any errors in the source program that it detects during the translation process.

![](img/2a44b9071782fade81f3050c3b718341_6_0.png)

If the target program is an executable machine-language program, it can then be called by the user to process inputs and produce outputs; see Fig. 1.2.

![](img/2a44b9071782fade81f3050c3b718341_6_1.png)

An *interpreter* is another common kind of language processor. Instead of producing a target program as a translation, an interpreter appears to directly execute the operations specified in the source program on inputs supplied by the user, as shown in Fig. 1.3.

![](img/2a44b9071782fade81f3050c3b718341_6_2.png)

The machine-language target program produced by a compiler is usually much faster than an interpreter at mapping inputs to outputs. An interpreter, however, can usually give better error diagnostics than a compiler, because it executes the source program statement by statement.

**Example 1.1.** Java language processors combine compilation and interpretation, as shown in Fig. 1.4. A Java source program may first be compiled into an intermediate form called *bytecodes*. The bytecodes are then interpreted by a virtual machine. A benefit of this arrangement is that bytecodes compiled on one machine can be interpreted on another machine, perhaps across a network.

In order to achieve faster processing of inputs to outputs, some Java compilers, called *just-in-time* compilers, translate the bytecodes into machine language immediately before they run the intermediate program to process the input.

![](img/2a44b9071782fade81f3050c3b718341_7_0.png)

Figure 1.4: A hybrid compiler

In addition to a compiler, several other programs may be required to create an executable target program, as shown in Fig. 1.5. A source program may be divided into modules stored in separate files. The task of collecting the source program is sometimes entrusted to a separate program, called a *preprocessor*. The preprocessor may also expand shorthands, called macros, into source language statements.

The modified source program is then fed to a compiler. The compiler may produce an assembly-language program as its output, because assembly language is easier to produce as output and is easier to debug. The assembly language is then processed by a program called an *assembler* that produces relocatable machine code as its output.

Large programs are often compiled in pieces, so the relocatable machine code may have to be linked together with other relocatable object files and library files into the code that actually runs on the machine. The *linker* resolves external memory addresses, where the code in one file may refer to a location in another file. The *loader* then puts together all of the executable object files into memory for execution.

#### 1.1.1 Exercises for Section 1.1

- **Exercise 1.1.1:** What is the difference between a compiler and an interpreter?
- **Exercise 1.1.2:** What are the advantages of (a) a compiler over an interpreter (b) an interpreter over a compiler?
- **Exercise 1.1.3:** What advantages are there to a language-processing system in which the compiler produces assembly language rather than machine language?
- **Exercise 1.1.4:** A compiler that translates a high-level language into another high-level language is called a *source-to-source* translator. What advantages are there to using C as a target language for a compiler?
- **Exercise 1.1.5:** Describe some of the tasks that an assembler needs to perform.
