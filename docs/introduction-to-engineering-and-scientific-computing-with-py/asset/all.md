![](images/9781000648300.jpg)

![Cover: Introduction to Engineering and Scientific Computing with Python, Written by David E. Clough and Steven C. Chapra, published by CRC Press, Taylor and Francis Group.](images/9781000648300.jpg)

MATLAB® is a trademark of The MathWorks, Inc. and is used with permission. The MathWorks does not warrant the accuracy of the text or exercises in this book. This book’s use or discussion of MATLAB® software or related products does not constitute endorsement or sponsorship by The MathWorks of a particular pedagogical approach or particular use of the MATLAB® software.

First edition published 2023

by CRC Press

6000 Broken Sound Parkway NW, Suite 300, Boca Raton, FL 33487-2742

and by CRC Press

4 Park Square, Milton Park, Abingdon, Oxon, OX14 4RN

CRC Press is an imprint of Taylor & Francis Group, LLC

© 2023 David E. Clough and Steven C. Chapra

Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of their use. The authors and publishers have attempted to trace the copyright holders of all material reproduced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any copyright material has not been acknowledged, please write and let us know so we may rectify in any future reprint.

Except as permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

For permission to photocopy or use material electronically from this work, access [www.copyright.com](http://www.copyright.com) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Danvers, MA 01923, 978-750-8400\. For works that are not available on CCC please contact [mpkbookspermissions@tandf.co.uk](mailto:mpkbookspermissions@tandf.co.uk)

*Trademark notice*: Product or corporate names may be trademarks or registered trademarks and are used only for identification and explanation without intent to infringe.

*Library of Congress Cataloging‑in‑Publication Data*

Names: Clough, David E., author. | Chapra, Steven C., author.

Title: Introduction to engineering and scientific computing with Python / David E. Clough, Steven C. Chapra.

Description: First edition. | Boca Raton : CRC Press, 2023\. |

Includes bibliographical references and index.

Identifiers: LCCN 2022012776 (print) | LCCN 2022012777 (ebook) |

ISBN 9781032188942 (hardback) | ISBN 9781032188973 (paperback) | ISBN 9781003256861 (ebook)

Subjects: LCSH: Engineering mathematics—Data processing. |

Science—Mathematics—Data processing. | Python (Computer program language)

Classification: LCC TA345 .C584 2023 (print) | LCC TA345 (ebook) |

DDC 620.001/51—dc23/eng/20220706

LC record available at [https://lccn.loc.gov/2022012776](https://lccn.loc.gov/2022012776)

LC ebook record available at [https://lccn.loc.gov/2022012777](https://lccn.loc.gov/2022012777)

ISBN: 9781032188942 (hbk)

ISBN: 9781032188973 (pbk)

ISBN: 9781003256861 (ebk)

DOI: [10.1201/9781003256861](https://doi.org/10.1201/9781003256861)

Typeset in Times

by codeMantra

*This book is dedicated to the thousands of our former students at the University of Colorado, Tufts University, and Texas A&M University. Go Buffs, Go Jumbos, and Gig ‘Em Aggies!*

# List of Examples

**Chapter 1** Engineering and Scientific Calculations

1.  [1.1 What is the Volume of the Earth?](#ch01.xhtml_exa1_1)
2.  [1.2 Catenary Cable](#ch01.xhtml_exa1_2)
3.  [1.3 Engineering Units in Calculations](#ch01.xhtml_exa1_3)
4.  [1.4 Engineering and Scientific Problem Solving](#ch01.xhtml_exa1_4)

**Chapter 2** Computer-Based Calculations

1.  [2.1 What is the Radius of the Earth—Expressed in Binary?](#ch02.xhtml_exa2_1)
2.  [2.2 IEEE 754 Representation of π](#ch02.xhtml_exa2_2)

**Chapter 3** Python Basics

1.  [3.1 Calculating the Great Circle Distance between Two Points on the Earth](#ch03.xhtml_exa3_1)
2.  [3.2 Using Variable Names with the Great Circle Formula](#ch03.xhtml_exa3_2)
3.  [3.3 Creating a Script for the Great Circle Calculation](#ch03.xhtml_exa3_3)

**Chapter 4** Structured Programming with Python

1.  [4.1 Converting Thermocouple Millivolt Readings to Temperature](#ch04.xhtml_exa4_1)
2.  [4.2 Using the `while` Structure for Input Validation](#ch04.xhtml_exa4_2)
3.  [4.3 Using a `for` Loop to Limit Iterations](#ch04.xhtml_exa4_3)
4.  [4.4 Using a `for` Loop to Vary Subscripts of an Array](#ch04.xhtml_exa4_4)
5.  [4.5 Carrying Out a Set of Calculations Based on a Sequence of Values](#ch04.xhtml_exa4_5)

**Chapter 5** Graphics—Matplotlib

1.  [5.1 Freezing Point of Aqueous Ethylene Glycol Solutions](#ch05.xhtml_exa5_1)
2.  [5.2 Sunspot Observations](#ch05.xhtml_exa5_2)
3.  [5.3 Plotting the Densities of Salt and Mag Chloride Solutions](#ch05.xhtml_exa5_3)
4.  [5.4 Plotting Weather Data—Temperature and Relative Humidity](#ch05.xhtml_exa5_4)
5.  [5.5 Worldwide Wind Power Generation](#ch05.xhtml_exa5_5)
6.  [5.6 Plotting the Vapor Pressure of Water versus Temperature](#ch05.xhtml_exa5_6)
7.  [5.7 Creating a Pie Chart for World Energy Production by Source](#ch05.xhtml_exa5_7)
8.  [5.8 Contour Plot from Data of Salt Solution Density](#ch05.xhtml_exa5_8)

**Chapter 6** Array and Matrix Operations

1.  [6.1 Using Arrays in a Case Study](#ch06.xhtml_exa6_1)
2.  [6.2 Solving a Set of Linear Equations with Vector/Matrix Operations](#ch06.xhtml_exa6_2)

**Chapter 7** Solving Single Algebraic Equations

1.  [7.1 Finding the Depth of Liquid in a Spherical Tank Given the Volume](#ch07.xhtml_exa7_1)
2.  [7.2 Calibrating the Depth/Volume Relationship of Liquid in a Spherical Tank](#ch07.xhtml_exa7_2)
3.  [7.3 Solving the van der Waals Equation for Volume with Brent’s Method](#ch07.xhtml_exa7_3)

**Chapter 8** Solving Sets of Algebraic Equations

1.  [8.1 Linear Equations and Engineering/Science Problem Solving](#ch08.xhtml_exa8_1)
2.  [8.2 Determinants](#ch08.xhtml_exa8_2)
3.  [8.3 Cramer’s Rule](#ch08.xhtml_exa8_3)
4.  [8.4 Elimination of Unknowns](#ch08.xhtml_exa8_4)
5.  [8.5 Naive Gaussian Elimination](#ch08.xhtml_exa8_5)
6.  [8.6 Construction Materials: A Blending Problem with Linear Equations](#ch08.xhtml_exa8_6)
7.  [8.7 Equilibrium between Water Liquid and Vapor in a Boiler Vessel](#ch08.xhtml_exa8_7)

**Chapter 9** Solving Differential Equations

1.  [9.1 Computing Probability for the Gaussian Distribution](#ch09.xhtml_exa9_1)
2.  [9.2 Trajectory of a Projectile with Air Resistance](#ch09.xhtml_exa9_2)

**Chapter 10** Working with Data

1.  [10.1 Simulating a Noisy Signal with Random Number Generation](#ch10.xhtml_exa10_1)
2.  [10.2 Fitting a Straight Line to U.S. CO[2] Emissions from Fossil Fuels](#ch10.xhtml_exa10_2)
3.  [10.3 Fitting a Polynomial to Data on the Density of Water versus Temperature](#ch10.xhtml_exa10_3)

# Preface

The primary purpose of this text is to provide background and experience in numerical problem solving by computing with the Python language. It is intended for first-year students in the engineering and science disciplines, but it may find utility for students at other levels such as advanced students at the pre-college level, students in pre-engineering programs in 2-year colleges, students transferring into engineering and science disciplines, and professionals seeking a review of numerical problem solving and wishing to learn the Python language for this purpose. We intend that this text provides the tools and knowledge that students can use in subsequent academic courses as the need for computer-based numerical problem solving arises.

This text is not designed to provide a broad, in-depth education in the Python programming language. Python has many capabilities that fall outside our focus on numerical problem solving. We do recommend, however, that students complement the learning from this text with further study of Python, if that suits their educational goals and interests. It is our intention that this book serve as an oft-utilized reference as students proceed through their academic careers and beyond.

For instructors considering this text for their students, we would like to address the question: Why this book? First, there is a growing audience that wants to use Python as their computing language, and few texts address this topic from an engineering and science perspective. Second, the authors have a decades long track record teaching introductory computing to thousands of students and have incorporated their experience in writing the text. Third, we have written the text keeping the students and their diverse backgrounds in mind. We believe the text is approachable by students. We have intently included basic explanations and examples along with elements that will challenge students.

The next question is Why Python? First, Python is a computing language that has gained a great deal of interest over the past few years. Second, from a practical stance, Python is available at no cost to the student, including down the road when access to institution-licensed software may not be available. Although Python is a broad-based, object-oriented computing language, there is a question whether it is well suited to the numerical problem solving commonly faced by engineers and scientists. By approaching Python with some care, and by not overwhelming the students with aspects of the language not needed in problem solving, we believe we have answered this concern in the affirmative. We chose the Spyder integrated development environment (IDE) because it is well suited to engineering computing and presents an interface similar to other dedicated software packages such as MATLAB^â. Spyder’s tools for developing and debugging Python scripts are excellent and of great aid to the student.

By illustrating how students can find information and answer questions about the use of Python, often via the Internet, we intend to equip students with the ability to extend their Python capabilities on their own. We illustrate this frequently in the text. We also encourage students to expand their general knowledge of Python, but outside the scope of the text and course they might be taking.

You might wonder what experience we the authors bring to the writing of this text. Together, in 1986 at the University of Colorado, we introduced the course, Introduction to Engineering Computing, and together, or subsequently on our own at different institutions, we taught the course over three decades. This course is still taught at the University of Colorado and Tufts. Of course, over the years, the computing tools used in the course have changed, but the general content and learning goals have not. For the first 15 years, the course was taught utilizing the Fortran and BASIC computer languages. Since then, the computing vehicles have included Excel, Excel VBA, Mathcad, MATLAB, and now Python. As a consequence of these years of experience, we have learned what works and is pertinent for students early in their academic careers (and what doesn’t!). This background has brought us to the writing of this text.

For more than a decade, we taught as a team and learned from each other. Additionally, we have taught numerical methods to students later in their academic careers. Our collaboration has yielded a recent text in numerical methods with Python ([Chapra & Clough, 2022](#ch11_ref.xhtml_r3)), and teaching the implementation of numerical methods with Python has provided us with a comfort level of experience to be able to write this text for students earlier in their academic careers.

Our pedagogical approach tends to be more inductive rather than deductive. We like to present examples frequently and then generalize those to provide broader, extensible knowledge. This book uses what we call a “crawl-walk-run” approach. We illustrate methods using Python in the chapters and encourage students to replicate those on their own. Then we provide end-of-chapter problems to challenge the students and encourage independent work. It is our intention that students will be well equipped to handle numerical problem-solving scenarios they encounter after studying this text. Among the problems we include with each chapter are those which illustrate practical applications in the engineering disciplines, as well as from the sciences. The organization of the problems at the end of each chapter follows two strategies. First, the problems tend to follow the organization of the chapter chronologically. Second, the problems become more challenging toward the end.

As far as mathematical background required of the student, we do include content involving algebra, transcendental functions, and elementary calculus (derivatives and integrals). The text could still be used by instructors who have students with little to no background in calculus, if approached with some care. We do provide review material in the first chapter, and our use of examples should help those students with little or meager knowledge of calculus.

The arrangement of the material in the text is designed to provide a well-structured course curriculum. As depicted in [Table P1](#ch00_fm07_preface.xhtml_tP1), the first two chapters on numerical and computer-based calculations are general and not dependent on the use of computers or Python. The intent of these chapters is to level the playing field for a group of students with diverse backgrounds. Also, many students may have seen similar material in the past but will benefit from a review. It has been our experience that students often have gaps in their learning when it comes to the content of these two chapters.

[**TABLE P1**](#ch00_fm07_preface.xhtml_tP1b)Organization of This Book

| Numerical & Computer-Based Calculations | Introduction to Python | Vector/Matrix Calculations & Equation Solving | Rate Equations & Data |
| --- | --- | --- | --- |
| [Chapter 1](#ch01.xhtml_c1). Engineering and Scientific Calculations | [Chapter 3](#ch03.xhtml_c3). Python Basics | [Chapter 6](#ch06.xhtml_c6). Array and Matrix Operations | [Chapter 9](#ch09.xhtml_c9). Solving Differential Equations |
| [Chapter 2](#ch02.xhtml_c2). Computer- Based Calculations | [Chapter 4](#ch04.xhtml_c4). Structured Programming with Python | [Chapter 7](#ch07.xhtml_c7). Solving Single Algebraic Equations | [Chapter 10](#ch10.xhtml_c10). Working with Data |
|  | [Chapter 5](#ch05.xhtml_c5). Graphics— Matplotlib | [Chapter 8](#ch08.xhtml_c8). Solving Sets of Algebraic Equations |  |

[Chapters 3](#ch03.xhtml_c3)–[5](#ch05.xhtml_c5) introduce the Python language. The first of these presents the rudiments of the language and the Spyder IDE. Instructors wishing to use another IDE would have to substitute their own orientation here. [Chapter 4](#ch04.xhtml_c4) deals with algorithm structure and completes the coverage of Python required for subsequent chapters. [Chapter 5](#ch05.xhtml_c5) focuses on plotting with the Matplotlib module. Plotting is common in problem-solving applications encountered in later chapters.

The remaining chapters are focused on applications with the Python tools put in place in [Chapter 3](#ch03.xhtml_c3)–5\. [Chapter 6](#ch06.xhtml_c6) introduces arrays and vector/matrix calculations. [Chapter 7](#ch07.xhtml_c7) is all about solving single, nonlinear, algebraic, and transcendental equations with common closed and open methods. Then, there is a natural transition to [Chapter 8](#ch08.xhtml_c8) where systems of linear and nonlinear algebraic equations are studied. [Chapter 9](#ch09.xhtml_c9), which deals with solving rate equations (i.e., differential equations), employs a simple approach using elementary methods of quadrature and integration.

The final [Chapter 10](#ch10.xhtml_c10) is devoted to the study of data and introduces concepts and methods of applied statistics in what could be described as a “statistics light” manner. This last chapter provides students with knowledge and skills that will be relevant to their laboratory courses, both early and later on in their academic careers. We also encourage, and strongly advocate, that all students should obtain more in-depth education in applied statistics via a course later in their academic career or otherwise.

In introducing concepts and methods in [Chapters 6](#ch06.xhtml_c6)–[10](#ch10.xhtml_c10), we first illustrate with basic Python scripts and then invoke built-in capabilities from the NumPy and SciPy modules. Having students see the methods in their own code first helps understanding of the concepts and removes some of the mystery behind the built-in functions. Also, we illustrate that the methods can often be programmed with very few statements.

We have designed the text so that instructors might adapt it to different academic terms and course designs. [Table P2](#ch00_fm07_preface.xhtml_tP2) suggests plans for a 15-week semester, 12-week quarter, and a shorter 6-week Python module that might be part of a computing course that would have other element(s) such as a module on spreadsheets or one on MATLAB. Of course, there would be other schedule requirements, such as more intensive summer courses, and we believe the text can accommodate a variety of these structures.

[**TABLE P2**](#ch00_fm07_preface.xhtml_tP2b)Instructional Plans

| Semester Plan |  | Quarter Plan |  | Python Module |
| --- | --- | --- | --- | --- |
| Week | Chapters |  | Week | Chapters |  | Week | Chapters |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 & 2 |  | 1 | 1 & 2 |  | 1 | 3, 4 & 5 |
| 2 | 2 | 2 |
| 3 | 3, 4 & 5 |  | 3 | 3, 4 & 5 |  | 3 |
| 4 | 4 | 4 | 6 |
| 5 |  | 5 |  | 5 | 7 or 10 |
| 6 | 6 |  | 6 | 6 |  | 6 |
| 7 | 7 |  | 7 | 7 |  |  |  |
| 8 | 8 |
| 9 | 8 |  | 9 | 8, 9, or 10 |  |
| 10 | 10 |
| 11 | 9 |  | 11 |  |
| 12 | 12 | Review |
| 13 | 10 |  |  |
| 14 |
| 15 | Review |  |  |

As this text is employed in instruction and learning, we anticipate there will be valuable impressions, opinions, and recognitions of occasional errors. Although we hope the latter will be minimal, we know that they are inevitable. We encourage instructors, students, and other readers to provide feedback to us (see the email addresses below). We will respond and endeavor to improve the text in its second edition, and your criticisms and ideas will be valuable to us. We have thick skins and small egos, so bring it on!

Although our primary intent is to empower and inspire students, we have the ancillary objective of making this introduction exciting and pleasurable. We believe that motivated students who enjoy coding will ultimately make better professionals. If this book fosters enthusiasm and appreciation for these subjects, we will consider our efforts a success.

MATLAB® is a registered trademark of The MathWorks, Inc. For product information, please contact:

The MathWorks, Inc.

3 Apple Hill Drive

Natick, MA 01760-2098 USA

Tel: 508-647-7000

Fax: 508-647-7001

E-mail: [info@mathworks.com](mailto:info@mathworks.com)

Web: [www.mathworks.com](http://www.mathworks.com)

# Acknowledgments

Both authors, David E. Clough and Steven C. Chapra, have lengthy careers and have benefited from many contributions and influences over the decades. David E. Clough had a high school math teacher, Miss Edith Benjamin, who introduced him to vectors, matrices and sets, and took him, along with two other students, down to Illinois Institute of Technology on Chicago’s South Side, in the evenings, to learn how to program in Fortran. When he arrived at the then Case Institute of Technology in Cleveland, Ohio, in 1964, he was told that Fortran was passé and was taught the language of the future, Algol. Along the way, he learned other “languages of the future” like GE timesharing BASIC, Pascal, and APL. He learned machine and assembly language programming for use with real-time computer systems. Thirty years later, Fortran finally faded, and he learned C/C++, MATLAB^â, Excel’s VBA, and on to Python. It seems that the more computing tools change, the more that fundamentals stay the same. It is worth mentioning that, for Clough, none of this would have been possible without the guidance and facilitation of many individuals, beginning with Miss Benjamin at Arlington High School in Arlington Heights, Illinois.

Steve C. Chapra has never taken a formal course in computer programming. As a freshman at Manhattan College back in the Pleistocene (1966), such courses had yet to be taught. But the college did have a room-sized mainframe computer to manage its scheduling and accounting. He connected with some very bright and generous older physics majors who commandeered a classroom in the evening where they taught Steve and a few other younger students how to code in one of the early versions of IBM Fortran. They also urged him to volunteer to work at the computer center where he swept the floor, replaced vacuum tubes, and learned assembly language. But the coolest part was that he got a key to the computer center so that he and his mates could surreptitiously sneak in late at night to write numerically oriented programs on punch cards. From that point forward, his education and career have been dominated by computing as applied to his research area: environmental modeling. To paraphrase the *Saturday Night Live* character, Chico Escuela: “Computing has been berry, berry good to me!”

Both authors acknowledge the thousands of students they have taught at various institutions and in the professions. Students have kept us on our toes and have exposed any approaches to teaching/learning that are faulty. As we have aged, in many ways, they have and continue to keep our outlooks young.

We sincerely appreciate the willingness of CRC Press, Taylor & Francis Group, to take on this publishing project. Our collaboration with Editor Nicola Sharpe and Editorial Assistant Nishant Bhagat has been supportive and productive and has certainly contributed greatly to the quality of the publication.

# Authors

**David E. Clough** is Professor Emeritus at the University of Colorado. He has experience in a wide array of programming languages and computing tools and has applied his expertise through his teaching, research, and industrial applications. Over his career, Clough has taught hundreds of short courses to practicing professionals on applied computing and problem solving.

**Steven C. Chapra** is the Emeritus Professor and Louis Berger Chair in Civil and Environmental Engineering at Tufts University. Before joining Tufts, he worked for the U.S. Environmental Protection Agency and the National Oceanic and Atmospheric Administration, and taught at Texas A&M University, the University of Colorado, and Imperial College London. He is a Fellow and Distinguished Member of the American Society of Civil Engineering (ASCE) and has received several awards for his scholarly and academic contributions, including the Rudolph Hering Medal (ASCE), and the Meriam-Wiley Distinguished Author Award (American Society for Engineering Education). As a strong proponent of continuing education, he has taught more than 90 workshops around the world for professionals on numerical methods, computer programming, and environmental modeling.

Authors’ email addresses: [david.clough@colorado.edu](mailto:david.clough@colorado.edu) [steven.chapra@tufts.edu](mailto:steven.chapra@tufts.edu)

# 1 Engineering and Scientific Calculations

DOI: [10.1201/9781003256861-1](https://doi.org/10.1201/9781003256861-1)

## Chapter Objectives

*   Review numerical calculations, including significant figures, positional and scientific notation.
*   Understand the typical functions used in engineering and scientific computations, including absolute value, sign, logarithmic, exponential, trigonometric, and hyperbolic relations.
*   Review operations with complex numbers, including rectangular and polar representation.
*   Carry out conversions of units common to engineering and scientific calculations.
*   Develop strategies for engineering and scientific problem solving.

Engineers and scientists carry out numerical calculations as a routine, day-to-day activity. Through years of experience, they have become accustomed to good practices that promote reliability in their results. The objective of this chapter is to review these practices and promote standards that will assist you in becoming functional members of STEM[¹](#ch01.xhtml_n1_1) professions. The rest of society plays fast and loose with numerical quantities and their interpretation. Engineers and scientists do not. Their work is examined closely and will be disregarded if it doesn’t measure up. If numerical issues are not detected, they can sometimes lead to big problems in the products they create.

We will consider here numerical quantities, calculations involving them and the units associated with them. Also, approaches to problem solving will be considered.

## 1.1 Numerical Quantities

We all grow up using decimal, base-10 numbers. As you will see in [Chapter 2](#ch02.xhtml_c2), this is not the number system used internally in computers. In fact, we are so accustomed to decimal numbers that we forget about the basics of their structure. It is also important to review this structure because, when we move internally to computers, that number base is going to change from 10 to 2.

### 1.1.1 Positional and Scientific Notation

*Positional notation* is a good place to start. A number like

1.  1234.56

uses the digits available in the decimal numbering system, 0 1 2 3 4 5 6 7 8 9\. The positions of the digits indicate a contribution to the overall number by powers of the base of the number system, 10\. If we index the positions according to [Figure 1.1](#ch01.xhtml_f1_1), then the contributions of the digits are represented as shown in [Table 1.1](#ch01.xhtml_t1_1).

![](images/Fig01_01.jpg)

**[FIGURE 1.1](#ch01.xhtml_f1_1b)** Positional notation.

[**TABLE 1.1**](#ch01.xhtml_t1_1b) Contribution of Digits

| Index | Digit | Contribution |
| --- | --- | --- |
| 3 | 1 | 1 × 10³ = 1,000 |
| 2 | 2 | 2 × 10² = 200 |
| 1 | 3 | 3 × 10¹ = 30 |
| 0 | 4 | 4 × 10⁰ = 4 |
| -1 | 5 | 5 × 10^(¯1) = 0.5 |
| -2 | 6 | 6 × 10^(¯2) = 0.06 |

Of course, the various contributions sum to the original number. This leads to the way of describing large and small decimal numbers that is common in engineering and science, positional notation, also commonly called *scientific notation*. Our example number 1234.56 expressed in typical positional notation is

1.  1.23456 × 10³

The 1.23456 part is called the *significand* or *mantissa*,[²](#ch01.xhtml_n1_2) and the power 3 is called the *characteristic* or *exponent*. It would have also been possible to express the number as

1.  123456\. × 10^(¯2)

but this is less common. In typical scientific notation, the number is *normalized* with only one digit to the left of the decimal point. Scientific notation gives us the ability to represent very large and small numbers conveniently. For example,

1.  Avogadro’s number: 6.022 × 10^(23)
2.  Planck’s constant: 6.626 × 10^(¯34)

### 1.1.2 Accuracy and Precision

The arithmetical operations of addition, subtraction, multiplication, and division are the basis of all numerical calculations. We carry out these operations daily with or without the use of a calculator or computer, without much thought, and perhaps with the occasional error. It is not our purpose here to reteach you arithmetic; rather we would like to highlight a few features of these operations that raise issues in engineering and scientific calculations.

First, we need to introduce the concepts of *precision*, *significant figures* and *rounding*, since they govern how we report the results of these calculations. It is important to distinguish the terms precision and accuracy. *Accuracy* refers to measurements and their comparison with accepted standards. Ultimately, these standards are traceable to those maintained by national organizations, such as the National Institute of Standards and Technology (NIST) in the U.S. and Association Française de Normalisation (AFNOR) in France. These are members of the International Organization for Standardization (ISO). *Precision* has to do with the resolution with which a number is expressed. For example, if a measured temperature is 24°C, it is precise to 1°; whereas, 24.1°C is precise to 0.1°C. The second temperature is more precise than the first; yet, a common misconception is that it is more accurate than the first. When a measurement is written as 24°C ± 1°C, that usually implies the accuracy of the measurement, that is the true value of the temperature is somewhere between 23°C and 25°C; however, even this type of description must be understood clearly because in other contexts the ± interval may relate to the random error associated with making the measurement. Be careful with the terms accuracy and precision. In fact, precision is so misused to imply accuracy that it is preferable to use *resolution* instead of precision in scientific writing.

Compare the following:

65^∘F         18.3333^∘C

The second temperature is closely equivalent to the first, since it was converted using the formula[³](#ch01.xhtml_n1_3)

${^\circ}\text{C} = \frac{{^\circ}\text{F} - 32}{1.8}$

However, there is a significant difference in the way these two quantities are represented. By writing 65°F, we understand that the temperature is certainly in the 60s, and it is closer to 65°F than to 64 or 66\. By writing 18.3333°C, we imply that the temperature is exact to 18.333 and closer to 18.3333 than to 18.3332 or 18.3334\. Of course, it is impractical to make a temperature measurement to such precision, and the precision implied by the two quantities is entirely different. You can see that we should report the converted temperature as 18°C, implying a similar precision to that of 65°F. As described next, this leads us to the concept of *significant figures*.

### 1.1.3 Significant Figures

Significant figures are almost always expressed as the “number” of significant figures; that is, the total number of digits that satisfy the definitions. Let’s elaborate with several examples.

| 65°F | 2 significant figures by rule (*b*) |
| 18.3333°C | 6 significant figures by rule (*a*) |
| 0.00471 | 3 significant figures by rule (*a*) |
| 43,500 | 3 significant figures by rule (*b*) |
| 43,500. | 5 significant figures by rule (*a*) |

The last two examples raise an important point. What if the number is known exactly for the digits 4 3 5, and it is also known that the next 0 is closer than one digit above or below it? In other words, we have four significant digits, and the rules (*a*) and (*b*) don’t cover that possibility. What to do? As a matter of fact, even the difference between 43,500 and 43,500\. is easy to miss. The answer lies in using scientific notation. There is no ambiguity in the following three numbers:

| 4.35  ×  10⁴ | 3 significant figures |
| 4.350 × 10⁴ | 4 significant figures |
| 4.3500 × 10⁵ | 5 significant figures |

and rule (*a*) applies to all of them. Consequently, we suggest using scientific notation whenever there could be ambiguity in the number of significant figures.

One additional point related to clarity: When expressing a decimal fraction in written work (hand-written or printed), it is important to include a leading zero before the decimal point. That is,

1.  0.471     rather than .471

because the leading decimal point in the latter is so easily missed by the reader.

### 1.1.4 Rounding

The concept of significant figures carries over to numerical calculations and introduces the need to round numbers to a given digit position. With simple addition, forming the sum

```
 12.3
  14.36
  26.66
```

is easy. But note that the sum as expressed implies that the first number is known as 12.30\. Since we don’t know that number to such resolution (to the one-hundredths place), it would be better to round the second number to the precision of the first, 14.4, and carry out the sum as

```
 12.3
  14.4
  26.7
```

or at least round the former result, 26.66, to the 26.7 below. The same goes for subtraction.

The standard rules for rounding are:

Rule (*c*) provides that the 5’s will be rounded up about half the time and down about half the time. Study the examples in [Table 1.2](#ch01.xhtml_t1_2).

[**TABLE 1.2**](#ch01.xhtml_t1_2b) Rounding Examples

| Original Number | Round to Place[^a](#ch01.xhtml_tfn1_2_1) | Result | Rule Applied |
| --- | --- | --- | --- |
| 43,500 | 1,000 | 44,000 | (*c*) |
| 42,500 | 1,000 | 42,000 | (*c*) |
| 18.3333 | 0.1 | 18.3 | (*b*) |
| 0.05493 | 0.01 | 0.05 | (*b*) |
| 7.86 × 10³ | 0.1 | 7.9 × 10³ | (*a*) |

[^a](#ch01.xhtml_tfn1_2_1b) Place in the significand, excluding the exponent.

There may be a temptation in the fourth example to round first to 0.055 and then round again 0.06\. Don’t get caught in this trap—**round only once!**

There are specific rules that govern the management of significant figures in calculations:

1.  For addition and subtraction:

    The positions of the last significant figure of each number should be compared. Of these positions, the one farthest to the left is the position of the last permissible significant figure of the sum or difference.

2.  For multiplication and division:

    The number of significant figures retained in the result should equal the lowest number of significant figures of any of the multiplicands, divisors, or dividends.

When we carry out an addition or subtraction with numbers in scientific notation, it is necessary to change the positional notation of at least one of the numbers so that the exponents are the same. For example, to add

```
 1.046 × 1011
    7.46 × 1010
```

It should be converted to one of the following two forms

```
 0.046 × 1011         10.46  × 1010
  0.764 × 1011           7.64 × 1010
  1.810 × 1011          18.10 × 1010
```

The result of the second form can be normalized to give the same result as the first form.

When two numbers are multiplied, the number of digits required to represent the product can be as many as the sum of the number of digits in each quantity. For example,

```
 12.3×
  14.36
     .738
  3.69
  49.2
   123\.      
   176.628
```

There are six digits in the product, but there could be as many as seven or more. However, by applying the rule of significant figures for multiplication, the least number of significant figures is three (from 12.3); therefore, only three significant figures should be retained in the answer That is, the answer should be expressed as 177.

Rounding for long division deserves a closer look. Note that, if the divisor goes evenly into the dividend, the number of digits in the quotient can be no more than the difference between the number of digits in the dividend minus the number of digits in the divisor. Turning the above example around,

![](images/un01_01.jpg)

And, this quotient should be expressed as 14.4 to reflect the limiting number of significant figures in the divisor, 12.3\. When the division does not come out even, it can be carried out as far as desired but will always have a remainder. The remainder is expressed as a fraction. Modifying the last example slightly,

![](images/un01_02.jpg)

So the quotient for this case would be expressed as 14.3 + 0.71/12.3.

As you can see from this example, it is best to carry out the division at least one place more than the eventual number of significant figures to make sure the correct rounding takes place.

When two numbers expressed in scientific notation are multiplied, the significands can be multiplied and the exponents added. It is convenient to normalize the resulting product, and it should be expressed with the correct number of significant figures, the least of the two multiplicands. For example,

```
 6.022   × 1023
   × 6.63    × 10–34
    39.92586 × 10–11    →    3.99 × 10-10
```

Not only is the product normalized on the right, it is expressed with the same limiting precision of the multiplicands.

In division, the divisor’s significand can be divided into the dividend’s significand, and the divisor’s exponent subtracted from that of the dividend. Here is an example:

$\begin{matrix} {7.65 \times 10^{10}\begin{array}{r} {0.1369 \times 10^{1}} \\ {1.046 \times 10^{11}} \end{array}} & {\text{o}\text{r}} & {1.37 \times 10^{0}} \end{matrix}$

Again, the quotient has been carried out an additional place and rounded down to the appropriate three significant figures.

## 1.2 Mathematical Functions

In carrying out engineering and scientific calculations, it is frequently necessary to use a variety of mathematical functions, commonly including

*   absolute value and sign functions,
*   exponents and logarithms,
*   trigonometric functions and
*   hyperbolic functions.

In this section, we will review certain aspects of calculating these functions that are prone to cause errors in results. It is not our intention to repeat the exhaustive treatment that can be found in good books and videos on college algebra and pre-calculus mathematics. Such books and videos should be consulted if you need a more in-depth review.

### 1.2.1 Absolute Value and Sign Functions

Calculating the absolute value of a number is easy. If the number is negative, change it to positive; otherwise, leave the number alone. The familiar symbol for the absolute value function is to surround the quantity with vertical bars, for example |*x*|. The absolute value function can be used in some creative ways though. For example, let’s say that you wanted to have a method of squaring a quantity yet preserving the quantity’s sign in the result. Applying this rule to -3 would yield -9, and applying it to 3 would yield 9\. Consider the following formula, and you will see that it accomplishes this:

*x*  |*x*|

Another related function is the sign (also called *signum*) function, abbreviated sgn. It can be expressed in terms of the absolute value function by the formula

$\text{s}\text{g}\text{n}(x) = \frac{|x|}{x}$(1.3)

When *x* is positive, sgn(*x*) = 1, and, when *x* is negative, sgn(*x*) = -1\. This formula gets into trouble when *x* = 0, yielding an indeterminate form 0/0; so, for that case, sgn(0) is just defined to be 0.

Note that the prior example, preserving the sign with the square, can be restated in terms of the sgn function,

*x*  |*x*| = sgn(*x*)  *x*²(1.4)

### 1.2.2 Exponents and Logarithms

Exponents and logarithms are dreaded by some students. That’s too bad because they are an essential part of scientific and engineering formulas and calculations. The key relationship that defines the exponent and its inverse function, the logarithm, is

log[*x*](*x*^(*y*)) = *y*(1.5)

The term *x*^(*y*) means *x* raised to the power *y*, which you probably understand. For integer powers, raising to a power can be handled by repeated multiplication, and perhaps division, for example

$\begin{array}{l} \left. 1.5^{4} = 1.5 \times 1.5 \times 1.5 \times 1.5 = 5.0625\Rightarrow 5.1 \right. \\ \left. 1.5^{- 3} = \frac{1}{1.5^{3}} = \frac{1}{1.5 \times 1.5 \times 1.5} = 0.296\ldots\Rightarrow 0.30 \right. \\ \left. \left( {- 1.5} \right)^{3} = \left( {- 1.5} \right) \times \left( {- 1.5} \right) \times \left( {- 1.5} \right) = - 3.375\Rightarrow - 3.4 \right. \end{array}$

Notice how the significant figures rule for multiplication/division is applied above. However, calculating *x*^(*y*) when *y* is a real number with a fractional part is not so straightforward. Consider the following examples:

$\begin{matrix} 1.5^{4.1} & 1.5^{- 0.41} & \begin{matrix} ( - 1.5) \end{matrix}^{1.4} \end{matrix}$

The scheme for computing when the power has a fractional part comes from the use of logarithms. Before doing that, it is useful to consider some specific types of logarithmic functions. The *common* (or base-10) *logarithm* is given by[⁴](#ch01.xhtml_n1_4)

log[10](10^(*y*)) = *y*

So, if log[10](2) = 0.301…, that means that

10^(0.301…) = 2

To explain this in words, the common logarithm of a number is the power to which 10 is raised to give that number.

Likewise, the *natural* (or *Napierian*) *logarithm* has the base *e*, where *e* is defined by the infinite series

$e = 1 + \frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \cdots \cong 2.718281828\ldots$

and

log[*e*](*e*^(*y*)) = ln(*e*^(*y*)) = *y*

Therefore, if ln(2) = 0.693…, then *e*^(0.693…) = 2\. The Napierian base arises frequently in calculus and differential equations, and the natural logarithm can be represented by another infinite series,

$ln(x) = 2 \cdot \left\lbrack {\frac{x - 1}{x + 1} + \frac{1}{3} \cdot \left( \frac{x - 1}{x + 1} \right)^{3} + \frac{1}{5} \cdot \left( \frac{x - 1}{x + 1} \right)^{5} + \cdots} \right\rbrack\quad\text{for}\, x > 0\text{only}$(1.6)

We can compute the natural logarithm to a given resolution by evaluating this series to the number of terms required to give convergence to that resolution. Notice that the logarithm is only defined for positive values of *x*.

Now, how do we use this ability to calculate the natural logarithm? Consider log[*a*](*x*) equal to some *y*. That means *a*^(*y*) = *x*. If we take the natural logarithm of both sides of this equation, ln(*a*^(*y*)) = ln(*x*), or *y*⋅ln(*a*) = ln(*x*), the result is

$\text{l}\text{o}\text{g}_{a}(x) = y = \frac{\text{l}\text{n}(x)}{\text{l}\text{n}(a)}$(1.7)

This useful formula provides a way to and calculate the logarithm for any other base. For example

$\log_{10}(100) = \frac{\text{ln}(100)}{\text{ln}(10)} = \frac{4.60517...}{2.30259...} = 2$

Let’s get back to that *x*^(*y*) where *y* is a real number with a fractional part. Represent the result of the calculation as *z*, so

*z* = *x*^(*y*)

and taking the natural logarithm of both sides of the equation, we get

ln(*z*) = *y*  ln(*x*)

Taking *e* to the power of each side of this equation gives

*e*^(ln(*z*)) = *z* = *e*^(*y*  ln(*x*))

Thus, *x*^(*y*) = *e*^(*y*  ln(*x*)). Since there is also an infinite series for *e*^(*x*),

$e^{x} = 1 + x + \frac{x^{2}}{2!} + \frac{x^{3}}{3!} + \cdots$(1.8)

We now can compute, from first principles, *x*^(*y*), by calculating ln(*x*) approximately using the infinite series for the natural logarithm, then calculating *e*^(*y* ⋅ ln(*x*)) from the infinite series given above. You should notice that this won’t work for *x* less than or equal to zero. The one example cited above

(−1.5)^(1.4)

can’t be done; in fact, it doesn’t make any sense.

You will probably never calculate logarithms and exponents by hand using the series approximations – usually you’ll just press the appropriate buttons on a calculator or use the corresponding built-in functions in a computer software, but it is useful to have some background on how these calculations are made and why certain limitations come into play. Reviewing our examples from above,

$\begin{array}{l} {1.5^{4.1} = e^{4.1\,\,\text{I}\text{n}{(1.5)}} = e^{4.1 \cdot 0.405\ldots} = e^{1.662\ldots} \cong 5.3} \\ {1.5^{- 0.41} = e^{- 0.41\,\,\text{I}\text{n}{(1.5)}} = e^{- 0.166\ldots} \cong 0.85} \\ {\left( {- 1.5} \right)^{1.4}\,\,\,\,\,\text{C}\text{a}\text{n}'\text{t}\,\text{b}\text{e}\,\text{d}\text{o}\text{n}\text{e}\,\text{b}\text{e}\text{c}\text{a}\text{u}\text{s}\text{e}\, - \, 1.5\,\text{i}\text{s}\,\text{l}\text{e}\text{s}\text{s}\,\text{t}\text{h}\text{a}\text{n}\text{0}} \end{array}$

Appropriate significant figures are shown for each of these examples, although more precision is carried through in the intermediate calculations. Like we wrote above, calculating *x*^(*y*), when *y* is a real number with a fractional part, is not that straightforward. This bears repeating.

Reviewing the key relationships from above,

$\begin{array}{l} {\text{l}\text{o}\text{g}_{x}\left( x^{y} \right) = y} \\ {\text{l}\text{o}\text{g}_{a}\left( x^{y} \right) = y\,\,\text{l}\text{o}\text{g}_{a}(x)} \\ {\text{l}\text{o}\text{g}_{a}(x) = \frac{\text{l}\text{n}(x)}{\text{l}\text{n}(a)}} \\ {x^{y} = e^{y\,\,\text{l}\text{n}{(x)}}} \end{array}$(1.9)

Other useful relationships involving exponents and logarithms are

$\begin{array}{l} {\text{l}\text{o}\text{g}_{a}\left( {x\, y} \right) = \text{l}\text{o}\text{g}_{a}(x) + \text{l}\text{o}\text{g}_{a}(y)} \\ {\text{l}\text{o}\text{g}_{a}\left( \frac{x}{y} \right) = \text{l}\text{o}\text{g}_{a}(x) - \text{l}\text{o}\text{g}_{a}(y)} \\ {x^{y + z} = x^{y}\, x^{z}} \\ {a^{x\, y} = \left( a^{x} \right)^{y}} \end{array}$(1.10)

We provided you with specific rules regarding significant figures and the arithmetic operations of addition, subtraction, multiplication, and division. Matters aren’t so easily defined when using logarithms, exponentials, and other nonlinear functions, such as trigonometric and hyperbolic functions. Let’s illustrate this with a prior example:

1.  1.5^(4.1)

There are evidently two significant figures in both quantities, 1.5 and 4.1\. How many significant figures should be represented in the result? Let’s take a numerical approach to this called *sensitivity analysis*. (This can also be approached with calculus and partial derivatives.) We will determine the effect on the result of changing each of the two numbers by one unit in their respective least significant digits. [Table 1.3](#ch01.xhtml_t1_3) gives us the answers to three significant digits.

[**TABLE 1.3**](#ch01.xhtml_t1_3b) Sensitivity Analysis

|  | 4.0 | 4.1 | 4.2 |
| --- | --- | --- | --- |
| 1.4 | 3.84 | 3.97 | 4.11 |
| 1.5 | 5.06 | 5.27 | 5.49 |
| 1.6 | 6.55 | 6.87 | 7.20 |

Observe the dramatic effect of changing the 1.5 quantity by ±0.1! For a given exponent value, the answer changes by about ±1.5\. The effect of changing the exponent 4.1 by ±0.1 is much milder, about ±0.2\. So, if the resolution of the 1.5 value is as stated, we cannot really report the result to any more than one significant figure, that is, 5\. This demonstrates that one must be very careful in reporting values that are results of calculations using nonlinear functions like exponentiation.

### 1.2.3 Trigonometric Functions

The various trigonometric functions occur all the time in scientific and engineering calculations. One problem that students encounter frequently in calculating formulas that include trigonometric functions is that most of these expect the angles to be in radians, not degrees. It seems that many students are accustomed to degrees from their previous math courses, especially those in high school. We will start by reviewing the basis of the three common “trig” functions and use this to understand the difference between degrees and radians.

The trigonometric functions relate the angles in a right triangle to its sides and hypotenuse. They are often conveniently represented on a two-dimensional graph using a unit circle, that is, a circle with a radius of 1\. Compare the definitions in Equation 1.11 to the diagram in [Figure 1.2](#ch01.xhtml_f1_2).

![](images/Fig01_02.jpg)

**[FIGURE 1.2](#ch01.xhtml_f1_2b)** Trigonometric relationships on the unit circle.

$\begin{array}{l} {\text{s}\text{i}\text{n}(\theta) = b} \\ {\text{c}\text{o}\text{s}(\theta) = a} \\ {\text{t}\text{a}\text{n}(\theta) = \frac{b}{a}} \end{array}$(1.11)

The right triangle of reference has sides of length *a* and *b* and a hypotenuse of length 1, given by the radius of the unit circle. Note that the *x*-axis coordinate *a* is the length of the right triangle side adjacent to the angle *θ*, and the *y*-axis coordinate is the side opposite the angle *θ*. This gives rise to the right-triangle-based definitions:

$\begin{array}{l} {\text{s}\text{i}\text{n}(\theta) = \frac{\text{opposite side}}{\text{hypotenuse}}} \\ {\text{c}\text{o}\text{s}(\theta) = \frac{\text{adjacent side}}{\text{hypotenuse}}} \\ {\text{t}\text{a}\text{n}(\theta) = \frac{\text{opposite side}}{\text{adjacent side}}} \end{array}$(1.12)

and their reciprocal functions

$\begin{aligned} {cosecant\text{:}\,\,\,\,\,\, csc(\theta) =} & \frac{1}{sin(\theta)} \\ {secant\text{:}\,\,\,\,\,\,\,\,\,\,\, sec{(\theta) =}} & \frac{1}{cos(\theta)} \\ {cotangent\text{:}\,\,\,\, cot{(\theta) =}} & \frac{1}{tan(\theta)} \end{aligned}$(1.13)

There are two common ways to express the angle *θ*.[⁵](#ch01.xhtml_n1_5) By dividing the circle into 360 angular increments, we get degrees. If we consider an arc of length one on the unit circle, the angle included by that arc is defined as a radian. Since the circumference of the unit circle is 2*π*, and that includes 2*π* radians and 360°, we have the equivalencies

$\begin{array}{l} {2\pi\,\,\, radians\,\,\,\text{=}\,\,\,\text{360}\,\,\,\deg rees} \\ {\text{1}\,\,\,\,\, radian\,\,\,\text{=}\,\,\,\,\frac{180}{\pi}\,\,\,\deg rees\,\,\, \cong \,\,\, 57.3{^\circ}} \\ {\frac{\pi}{180} = \,\,\, 1\,\,\,\deg rees\,\,\, \cong \,\,\,\text{0.0175}\,\,\, radians} \end{array}$

As with the exponential function and natural logarithm, the trigonometric functions are defined in terms of infinite series, and these can be used to approximate numerical results. For example,

$\text{sin}(x) = x - \frac{x^{3}}{3!} + \frac{x^{5}}{5!} - \cdots$(1.14)

This requires that *x* be expressed in radians, not degrees. Often you may use a calculator to compute trigonometric results, and you must be very aware whether the calculator expects the angles to be input in radians or degrees. Many calculators have a default setting for degrees and require a special action to switch them over to radians mode.

Here are some common trigonometric facts that many engineers and scientists have committed to memory:

$\begin{array}{ll} {\sin(30{^\circ}) = \sin\left( \frac{\pi}{6} \right) = 0.5} & {\cos(60{^\circ}) = \cos\left( \frac{\pi}{3} \right) = 0.5} \\ {\cos(30{^\circ}) = \cos\left( \frac{\pi}{6} \right) = \frac{\sqrt{3}}{2} = 0.866...} & {\tan(45{^\circ}) = \tan\left( \frac{\pi}{4} \right) = 1} \\ {\tan(60{^\circ}) = \tan\left( \frac{\pi}{3} \right) = \sqrt{3} = 1.732...} & {\tan(30{^\circ}) = \tan\left( \frac{\pi}{6} \right) = \frac{\sqrt{3}}{3} = 0.577...} \end{array}$

The *inverse* or “arc” *trigonometric functions* are used frequently in scientific formulas. Their mathematical definition is straightforward. For example,

*y* = sin(*x*) ⇒ *s**i**n*^(−1)(*y*) = *x*

Instead of sin^(–1)(*x*), the terminology arcsin(*x*) is sometimes used. Notice that the result of the inverse sine formula is an angle, typically in radians. One way to think of the inverse sine formula above (this implies a method for obtaining it) is: “Given a value of *y*, what angle *x* will yield the sine of *y*?” To do that with a calculator, you might guess an *x*, compute the sine function, compare the result to *y* and guess new *x*’s until your answer is close to *y*. Of course, many modern calculators have the inverse trigonometric functions built in, and, behind the scenes, they use a similar strategy.

There are some tricky aspects to the calculation of inverse trigonometric functions. You should appreciate this with the following example.

Consider the angle described on the unit-circle diagram in [Figure 1.3](#ch01.xhtml_f1_3).

![](images/Fig01_03.jpg)

**[FIGURE 1.3](#ch01.xhtml_f1_3b)** Unit circle diagram with quadrants.

The angle is clearly greater than *π* (180°) and less than 3*π*/2 (270°). Notice that the coordinate values of *a* and *b* are both negative. By our definition,

$\text{t}\text{a}\text{n}(\theta) = \frac{b}{a}$

and, if we chose a value of *θ* and computed the tangent, the result would certainly be equal to the ratio of *b* to *a*. But consider the inverse tangent function for a moment. Say we knew *b* and *a* and wanted to compute *θ* (very common in engineering calculations). By definition again,

$\theta = \text{t}\text{a}\text{n}^{- 1}\left( \frac{b}{a} \right)$

but when we carry out the calculation, taking the ratio of the negative values of *b* and *a* yields a positive result, and the inverse tangent result is an angle between 0 and *π*/2 (90°). You will notice that the quadrants of the unit circle are numbered with Roman numerals in [Figure 1.3](#ch01.xhtml_f1_3). By computing the ratio of *b* to *a* and losing the sense of their negative signs, we have failed to recognize that the answer should be an angle in quadrant III. To get the correct answer, we have to look at the values of *a* and *b*, recognize they are both negative and add *π* (180°) to the calculated result. There are similar considerations in distinguishing calculations in quadrants II and IV.

So, you can see that just punching the buttons of a calculator without understanding the nature of the functions you are using can get you into trouble. Computer software typically provides two inverse tangent functions, one returning angles in quadrants I and IV only, and another that returns the correct angles in all four quadrants.

A useful property involving the inverse trig functions comes from the common fact noted above,

$\text{t}\text{a}\text{n}\left( \frac{\pi}{4} \right) = 1$

By applying the inverse tangent function to both sides of the equation, we get

$\begin{matrix} {\frac{\pi}{4} = tan^{- 1}(1)} & \text{or} & {\pi = 4 \cdot tan^{- 1}(1)} \end{matrix}$

If we have a convenient way of computing the inverse tangent, this last formula gives us a way of getting a value for *π* to as many significant digits carried by your calculator or computer.

There are many practical scenarios where trigonometric functions arise. One of these is in conjunction with quantities that vary periodically, like sine waves. Application areas include:

*   electronic circuits
*   electrical power distribution
*   communications and signal processing
*   mechanical and structural vibrations
*   automation and control systems

Consider the sinusoidal signal shown in [Figure 1.4](#ch01.xhtml_f1_4), which is produced by graphing the function

![](images/Fig01_04.jpg)

**[FIGURE 1.4](#ch01.xhtml_f1_4b)** Example sinusoidal signal.

1.47  sin(0.89 *t* + 0.32)(1.15)

The *amplitude* of the sine wave is 1.47, and you can see in the graph that the peaks are ±1.47\. The *frequency* of the sine wave is 0.89 radians/second, and, by comparing with the graph, you can confirm that the *period* of the sine wave is, as determined below,

$\begin{array}{l} {\text{for}\omega = 0.89\,\,\frac{\text{radians}}{\text{second}}} \\ {\text{and}f = \frac{\omega}{2\pi} \cong 0.14\,\,\frac{\text{cycles}}{\text{second}}\,\, or\,\,\text{Hertz}\left( \text{Hz} \right)} \\ {\text{then}P = \frac{1}{f} \cong 7.1\,\,\,\text{seconds}} \end{array}$

The *phase shift* of the sine wave is 0.32 radians (or 18°). A sine function without phase shift would have a value of zero at time = 0, ±*π*/*ω*, ±2*π*/*ω*, … You can see from the graph that the wave starts early; in fact, at time = −0.32/*π* the value is zero. The sine wave has been advanced in time by the phase shift. Of course, the phase shift could be negative, and the sine wave would be delayed.

By employing the “sum of angles” trigonometric identity,

sin(*α* + *β*) = sin(*α*) cos(*β*) + cos(*α*) sin(*β*)(1.16)

our sine wave formula can be written in the equivalent form

$\begin{aligned} {1.47\,\text{s}\text{i}\text{n}(0.89\, t + 0.32)} & {= 1.47\, cos(0.32)\,\,\text{s}\text{i}\text{n}(0.89\, t) + 1.47\,\text{s}\text{i}\text{n}(0.32)\, cos(0.89\, t)} \\ & {\cong 1.40\,\text{s}\text{i}\text{n}(0.89\, t) + 0.462\, cos(0.89\, t)} \end{aligned}$

You can see then that a sine function with a phase shift (or cosine function with a phase shift) can be written as a sum of sine and cosine functions of the same frequency but differing amplitudes.

### 1.2.4 Hyperbolic Functions

In deriving many engineering formulas, another family of functions arises: the *hyperbolic functions*. These are actually defined in terms of exponential functions; so, knowing how to calculate *e*^(*x*) gives us the capability to calculate the hyperbolics. Many calculators have *e*^(*x*) built in, but not the hyperbolic functions. A variety of software products used by engineers and scientists do have these functions available. Their definitions are

$\begin{array}{l} {\text{hyperbolic sine}:\quad\text{s}\text{i}\text{n}h(x) = \frac{e^{x} - e^{- x}}{2}} \\ {\text{hyperbolic cosine}:\quad cosh(x) = \frac{e^{x} + e^{- x}}{2}} \\ {hyperbolictangent:\quad tanh(x) = \frac{e^{x} - e^{- x}}{e^{x} + e^{- x}}} \end{array}$(1.17)

The hyperbolic functions can be derived from the angles formed between the origin and the coordinates of a *rectangular hyperbola*.[⁶](#ch01.xhtml_n1_6) We won’t get into that here, but you should know how to calculate the hyperbolics should they arise in formulas.

## 1.3 Complex Numbers

Complex numbers arise in many engineering applications, perhaps most frequently in electrical engineering. You are undoubtedly familiar with them through the solution of the quadratic equation, *ax*² + *bx* + *c* = 0, by the quadratic formula

$x = \frac{- b \pm \sqrt{b^{2} - 4\, a\, c}}{2\, a}$(1.20)

In evaluating the quadratic formula, the term *b*²–4*ac* is called the *discriminant* because, depending on its sign, very different solutions arise. When the discriminant is positive, two distinct real roots result. When it is zero, there are two equal real roots. When *b*²–4*ac* < 0, we are faced with the awkward situation of finding the square root of a negative number. This is handled by defining a symbol, *j*, to represent the square root of −1 as

$j \triangleq \sqrt{- 1}$

then

$\sqrt{b^{2} - 4\, a\, c} = \sqrt{\left( {- 1} \right)\,\left( {4\, a\, c - b^{2}} \right)} = j\,\sqrt{4\, a\, c - b^{2}}$

which gives rise to two complex roots, each one having a real part and an imaginary part with coefficient *j*. These are called a complex, *conjugate pair* because the real parts are equal and the imaginary parts are equal but opposite in sign.

$x = - \frac{b}{2\, a} \pm j\,\frac{\sqrt{4\, a\, c - b^{2}}}{2\, a}$(1.21)

A complex number is, in fact, a pair of numbers generally represented in the form

*a* + *j* *b*

where *j* is understood to be $\sqrt{- 1}$, and is called the imaginary unit.[⁸](#ch01.xhtml_n1_8) You can see by its definition that *j*² = -1\. The quantity *a* is called the *real part*, and *b* is called the *imaginary part*. It is convenient to represent a complex number by graphing it in a plane with the horizontal axis used for the real part and the vertical axis for the imaginary part, as shown in [Figure 1.6](#ch01.xhtml_f1_6).

![](images/Fig01_06.jpg)

**[FIGURE 1.6](#ch01.xhtml_f1_6b)** Number on the complex plane.

It is then possible to represent the number by polar coordinates instead of rectangular, Cartesian, coordinates ([Figure 1.7](#ch01.xhtml_f1_7)) where $r = \sqrt{a^{2} + b^{2}}$ and *θ* = tan^(–1)(*b*/*a*).[⁹](#ch01.xhtml_n1_9)

![](images/Fig01_07.jpg)

**[FIGURE 1.7](#ch01.xhtml_f1_7b)** Number on the complex plane using polar coordinates.

From trigonometry, we also have that

*a* = *r* cos(*θ*)  and  *b* = *r* sin(*θ*)

Therefore, the original representation of the complex number, *a* + *jb*, can also be written

*a* + *j* *b* = *r*  (cos(*θ*) + *j* sin(*θ*))(1.22)

Euler proposed the following identity:

*e*^(*j*  *θ*) ≡ cos(*θ*) + *j* sin(*θ*)(1.23)

which leads to

*a* + *j* *b* = *r* *e*^(*j* *θ*)(1.24)

The expression on the right, *r e* ^(*jθ*), is called the polar form on the complex number. This also leads to the following identities for the trigonometric functions:

$\begin{matrix} {\text{s}\text{i}\text{n}(\theta) \equiv \frac{e^{j\,\theta} - e^{- j\,\theta}}{2\, j}} & {cos(\theta) \equiv \frac{e^{j\,\theta} + e^{- j\,\theta}}{2}} \end{matrix}$(1.25)

## 1.4 Engineering Units[^(10)](#ch01.xhtml_n1_10)

One of the more confusing aspects of making engineering and scientific calculations is units of measurement. [Table 1.4](#ch01.xhtml_t1_4) illustrates that for common units of measurement for pressure as related to an SI standard unit, kPa:

[**TABLE 1.4**](#ch01.xhtml_t1_4b) Common Units for Pressure (kPa)

| Atmosphere | 101.325 |  |
| --- | --- | --- |
| in Hg | 3.37685 | kPa |
| in H[2]O | 0.24884 | kPa |
| torr (mm Hg) | 0.133322 | kPa |
| psi | 6.894757 | kPa |
| bar | 100 | kPa |
| kg[f]/cm² | 98.0665 | kPa |

Given this table, suppose you are faced with a pressure measurement in Hg (typical units used for barometric pressure in the U.S.), and you are asked to report the measurement in atmospheres. This shows how to make that conversion using the table:

$29.48\,\text{i}\text{n}\,\text{H}\text{g} \cdot \frac{3.37683\,\,\text{k}\text{P}\text{a}}{1\,\,\text{i}\text{n}\,\text{H}\text{g}} \cdot \frac{1\,\,\text{a}\text{t}\text{m}}{101.325\,\,\text{k}\text{P}\text{a}} \cong 0.9825\,\,\text{a}\text{t}\text{m}$

Of course, you could look for a conversion factor from in Hg to atm directly; however, with so many pressure units in common use, just having the relationship with a standard SI unit, kPa, is a convenient way to create the conversion.

The international standard units of measurement are those defined by the *SI system* (*Système internationale d’unités*), which is a modern form of the metric system. The basic SI units of measurement are given in [Table 1.5](#ch01.xhtml_t1_5).

[**TABLE 1.5**](#ch01.xhtml_t1_5b) Basic Units of the SI System

| Time | Second | s |
| --- | --- | --- |
| Length | Meter | m |
| Mass | Kilogram | kg |
| Current | Ampere | A |
| Temperature | Kelvin | K |
| Amount | Mole | mol |
| Luminous intensity | Candela | cd |

Commonly derived quantities encountered in engineering and scientific calculations are shown in [Table 1.6](#ch01.xhtml_t1_6).

[**TABLE 1.6**](#ch01.xhtml_t1_6b) Derived Quantities and SI Units

| Area | m² |  |
| --- | --- | --- |
| Volume | m³ |  |
| Volumetric flow rate | m³/s |  |
| Density | kg/m³ |  |
| Force | N | kg·m/s² |
| Pressure | Pa | N/m² |
| Energy | J | N·m |
| Power | W | J/s |
| Viscosity | Pa·s | N·s/m2 |

For each of these quantities, you will encounter different units used. For example, civil engineers in the U.S. will encounter cubic feet per second (ft³/s or cfs) used for volumetric flow rate, and U.S. chemical engineers may encounter gallons per minute (gpm).

Scaled units are commonly used in describing quantities. For example, millimeters (mm) or micrometers (μm) may be used to measure dimensions of smaller particles. There are standard prefixes for scaling units, and these are presented in [Table 1.7](#ch01.xhtml_t1_7).

[**TABLE 1.7**](#ch01.xhtml_t1_7b) Scale Prefixes for Units

| Scale Factor | Name | Abbreviation | Scale Factor | Name | Abbreviation |
| --- | --- | --- | --- | --- | --- |
| 10 | deca- | da | 0.1 | deci- | d |
| 100 | hecto- | h | 0.01 | centi- | c |
| 1,000 | kilo- | k | 0.001 | milli- | m |
| 10⁶ | mega- | M | 10^(−6) | micro- | μ |
| 10⁹ | giga- | G | 10^(−9) | nano- | n |
| 10^(12) | tera- | T | 10^(−12) | pico- | p |
| 10^(15) | peta- | P | 10^(−15) | femto- | f |
| 10^(18) | exa- | E | 10^(−18) | atto- | a |

Specialized areas of science and engineering have specific units that are common. For example, in electrical engineering, [Table 1.8](#ch01.xhtml_t1_8) may be useful.

[**TABLE 1.8**](#ch01.xhtml_t1_8b) Common Units for Electrical Measurement.

| Quantity | Unit | Abbreviation | Base Units |
| --- | --- | --- | --- |
| Electrical charge | Coulomb | C | s·A |
| Electrical potential | Volt | V | W/A |
| Capacitance | Farad | F | C/V |
| Resistance | Ohm | Ω | V/A |
| Magnetic flux | Weber | Wb | V·s |
| Inductance | Henry | H | Wb/A |
| Luminous flux | Lumen | lm | cd·sr |

There are common constants used in calculations in chemistry, physics and engineering. One of these is the universal gas constant, *R*. This constant is employed to relate amount, temperature, pressure, and volume of a gas and appears in the ideal gas law as

*P* *V* = *n* *R* *T*(1.26)

where *P* = pressure, *V* = volume of gas, *n* = number of moles of gas, and *T* is the temperature in absolute units. The units required for the gas law constant depend on the units used for these quantities. This is illustrated by solving the ideal gas law for *R* and incorporating the units at hand.

$R = \frac{P\, V}{n\, T} \cong 8.3145\frac{\text{Pa} \cdot \text{m}^{\text{3}}}{\text{mol} \cdot \text{K}}$

There are extensive tables available (e.g. on the Internet) of *R* in various units. In [Table 1.9](#ch01.xhtml_t1_9), we tabulate several of the most common used.

[**TABLE 1.9**](#ch01.xhtml_t1_9b) Common Units for the Gas Constant, *R*.

| 8.3144621… | Pa·m³/(mol·K) |
| 8.3144621… | J/(mol·K) |
| 0.08205746… | atm·L/(mol·K) |
| 1.9858775… | cal/(mol·K) |

When working with mixed units in engineering and scientific calculations, we suggest the following steps:

*   convert all input quantities to SI units,
*   carry out the calculations, producing results in SI units,
*   convert results to the units expected by your audience.

**We strongly recommend that you do not bury unit conversions in formulas, rather keep them separate.**

## 1.5 Organizing and Planning Solutions to Problems

Your career as a scientist or engineer will be filled with problem-solving activities. You will be expected to be a proficient problem-solver, but you may not be that yet. How do you get from here to there?

One way, the long way, is through the “school of hard knocks.” That is, by solving many, many problems, you will eventually get good at it. Of course, getting there will be painful. You should be interested in ways to become a better problem solver faster. The purpose of this section is to help you move along in that direction.

There are many good sources of information on problem solving. Many of these treat problem solving in a much more general setting, and others focus on the mathematical aspects of problems. We cannot equal the scope of books like these here, but we can point out some useful strategies that will pay off later in this text, in other courses in your curriculum, and in professional practice.

We start this section with a nice example to illustrate some features of problem solving. It is useful to deal with something concrete before considering general methods. Then, a general approach to problem solving is presented. As problems become more complicated, and especially when a team of people attacks a problem, a systematic, structured approach is of great value. Ways of categorizing typical problems are described. Much efficiency in problem solving comes from recognizing the pattern or type of a problem, leading directly to a solution strategy. Finally, several alternative examples are presented.

In a general approach to solving a problem, there are three initial planning steps that are essential. The first is to gather and summarize all the basic information and parameter values presented in the problem. The second is to state clearly what results the scenario requires. And the third is to derive and develop the relationships that translate the information in step one into the desired results in step two. This is illustrated in [Figure 1.13](#ch01.xhtml_f1_13).

![](images/Fig01_13.jpg)

**[FIGURE 1.13](#ch01.xhtml_f1_13b)** Problem-solving steps.

Once the solution strategy is designed, one applies the necessary methods to calculate and analyze the results. Along the way, there are important issues to address:

*   Are there sufficient information and basic data to solve the problem? Is there too much information? Is it necessary to research and develop additional information?
*   Are the assumptions associated with the problem description valid? What factors might be missed?
*   Does my strategy yield the requested results? It is a waste of time and effort to produce results that are not needed nor wanted.
*   Are the methods employed to determine the solution valid? How do I validate the results?
*   How are my results sensitive to changes in the input parameters? If the sensitivity is high, the results will be in doubt if the input parameter is uncertain.

We have addressed several of these issues with our simple ladder-hallway example. For example, we didn’t need to solve for *z* and *y*, once we had a value for *x*. Solving for *z* and *y* would be wasted effort. Version B of the problem did not provide sufficient information. To validate our result, we might test it on our scale drawing. We could check the Pythagorean theorem for the big triangle in the diagram with sides 2.5 + *z* and 1.5 + *y* and the hypotenuse at 6 m. Of course, then we would have to solve for *z* and *y*.

As far as assumptions involved in the problem statement being valid, it is stated that the ladder is held horizontally. If you have ever tried to carry ladders in restricted spaces, you know that you would tilt the ladder to gain better access. If we change the problem description to allow this, we would need the height of the hallways and more dimensional information on the ladder (width and thickness). Also then, the problem would become more complicated. We analyzed the ladder as a line on our diagram. Ladders have a thickness dimension. Including this would affect our original problem description, even with horizontal alignment.

Judgment must be exercised in removing assumptions and consequently complicating problem descriptions and solutions. Even if our ladder is 10 cm thick, do we get a sufficiently good result ignoring that information? Such questions can be addressed based on experience, but, without that, it may be necessary to carry out a trial solution of a more complicated scenario and compare it with the simpler one.

Our final comment here is that initial efforts in analyzing the problem and carefully planning the solution strategy always pay off. Jumping right into the solution of a problem (sometimes called *shotgunning*) leads to many difficulties, erroneous results, extended time to obtain a solution and endless frustrations. All this is amplified as the scope of a problem increases. Develop the habits suggested here, and they will pay off for you for a long, long time.

## Problems

1.  **1.1** Express the following numbers in normalized scientific notation.
    1.  0.0001005
    2.  3.14159
    3.  62459100
    4.  602.2 × 10^(21)
2.  **1.2** Carry out the following computations using a calculator or spreadsheet. Express the results to the appropriate number of significant figures.
    1.  `6.001`
    2.  0.1546.001
    3.  $\begin{matrix} {\quad 1.25} & \times & 10^{- 2} \\ {\quad 7.61} & \times & 10^{- 1} \\ \underset{¯}{\begin{matrix} {+ 3.06} \end{matrix}} & \times & \underset{¯}{\begin{matrix} 10^{- 3} \end{matrix}} \end{matrix}$
    4.  `1.017 × 10`^(`5`) `÷ 3.64 × 10`^(`7`)
3.  **1.3** Round the following to the place indicated.
    1.  1047560 to 1000
    2.  1.047 to 0.1
    3.  7450 to 100
    4.  -15.43 to 1
4.  **1.4** Rework problem **1.2(b)** using long division.
5.  **1.5** For the components and sum shown below, calculate the percentage each component is of the total. Express your percentages with appropriate significant figures and ensure they sum to 100%.

    ```
     375
       44
      145
       14
      201
      779
    ```

6.  **1.6** Compute the following functions using a calculator or spreadsheet.
    1.  sin (1.84*π*)
    2.  $\tan\left( {- \frac{\pi}{4}} \right)$
    3.  cos(47.9^∘)
    4.  tan^(−1)(25)
7.  **1.7** Determine the roots of the following quadratic equations.
    1.  *x*² + 0.20 ⋅ *x* + 0.70 = 0
    2.  *x*² − 28.4 ⋅ *x* + 201.64 = 0
    3.  24 ⋅ *x*² − 13 ⋅ *x* = 0
    4.  *x*² + 187 ⋅ *x* − 24.0 = 0
8.  **1.8** Write down an approximate equation for the waveform shown in [Figure P1.8](#ch01.xhtml_fP1_8).![](images/Fig01P_08.jpg)

    **[FIGURE P1.8](#ch01.xhtml_fP1_8b)** Waveform.

9.  **1.9** In the U.S., vehicle fuel economy is typically reported in miles per gallon (mpg). In Europe, the common measure is liters per 100 km (L/100 km). Americans would know a decent fuel economy to be 40 mpg. Help Europeans understand this by converting it to L/100 km.
10.  **1.10** Carry out the following unit conversions.
    1.  150 kph = ?? mph (a moderate speed on the autobahn)
    2.  7 ft–6 inches = ?? m (this is the altitude of Yao Ming – who is he?)
    3.  45°C =?? °F (typical summer temperature in the Middle East)
    4.  12.4 psi =?? Pa (typical atmospheric pressure at 1,800 m altitude)
11.  **1.11** In most countries, other than the U.S., a person’s weight is reported in kilograms. Convert your weight (or a weight you would like to have) from pounds to kilograms (or vice versa). Also, in the U.K., weight is often cited in *stone*. Convert that weight to stone also.
12.  **1.12** A crude oil supertanker typically has a capacity of 100,000 dwt. The shipping unit dwt is called a deadweight ton and corresponds to a metric ton or 1,000 kg of capacity. Crude oil typically has a density of about 835 kg/m³. Determine the amount of liquid fossil fuels consumed in the U.S. or a country of your choice on a monthly basis in terms of crude oil. Determine also what percentage of the crude oil is imported via ship. How many supertankers must unload at ports per month?
13.  **1.13** In most countries of the world, mountain heights are given in meters; whereas, in the U.S., feet are typically used. What are the altitudes, in both feet and meters, of the following well-known peaks in the world? Describe the location of each peak too. Mont Blanc, Denali, Mount Everest, Kilimanjaro, Aconcagua, Mount Fuji.
14.  **1.14** The price of regular, unleaded gasoline varies significantly from location to location. In the U.S., it is given in dollars per gallon. In most other countries, it is in their currency per liter. Pick a location in the U.S. and a European country. Compare current fuel prices using both bases.
15.  **1.15** For a triangle with sides of length *a*, *b*, and *c*, there is an inscribed circle of radius *r* and a circumscribed circle of radius *R*. The inscribed circle is the largest circle that fits inside the triangle and touches all three sides. The circumscribed circle is the smallest circle that contains the triangle and touches all three vertices. For *a* = 10, *b* = 8, and *c* = 5, determine *r* and *R*.
16.  **1.16** A tank is to be constructed that will hold 500 m³ of crude oil when filled. The shape of the tank is to be a right circular cylinder, including base, with a right conical section mounted on top (see [Figure P1.16](#ch01.xhtml_fP1_16)) with height equal to radius for each part. The material and labor costs to construct the cylindrical portion including the base are $300 per m², and the costs for the conical section are $400 per m². Find the cost of this tank.![](images/Fig01P_16.jpg)

    **[FIGURE P1.16](#ch01.xhtml_fP1_16b)** Cylindrical tank with conical top.

17.  **1.17** The sector and segment of a circle are related to various dimensions, shown in [Figure P1.17](#ch01.xhtml_fP1_17).

    ![](images/Fig01P_17.jpg)

    **[FIGURE P1.17](#ch01.xhtml_fP1_17b)** Sector and segment of a circle.

    Given values of *θ* and *R*,

    $\begin{array}{l} {s = R\,\theta} \\ {d = R\,\text{c}\text{o}\text{s}\left( \frac{\theta}{2} \right)} \end{array}$

    *h* = *R* − *d*

    $c = 2R\,\text{s}\text{i}\text{n}\left( \frac{\theta}{2} \right)$

    Formulas for area are

    Sector: $A_{\sec t} = \frac{1}{2}R\, s$ (sector is “pie slice”)

    Segment: $A_{seg} = \frac{1}{2}R^{2}\left\lbrack {\theta - \text{s}\text{i}\text{n}(\theta)} \right\rbrack$ (segment is between c and s curves)

    If *R*  =  3.6 and *s*  =  1.78, determine the two areas.

# 2 Computer-Based Calculations

DOI: [10.1201/9781003256861-2](https://doi.org/10.1201/9781003256861-2)

## Chapter Objectives

*   Understand how numerical quantities are stored and manipulated within computer architecture.
*   Familiarize yourself with the different number bases and systems: decimal, binary, octal, and hexadecimal and how to convert numbers between the bases.
*   Learn how integers are stored in computers including signed numbers and limits on range.
*   Understand how real numbers with fractional parts and exponents are represented in computer architecture, including limits on precision and range.
*   See how other types of information, such as text and True/False Boolean data, are stored and manipulated in computers.

What goes on inside a computer differs from what engineers and scientists do on paper, perhaps with the assistance of a calculator. Out in the real world, we deal with numbers using the *decimal system*, or *base 10*. Internal to computers, the basis for all operations is the *binary or base-2* system (0–1). The objective of this chapter is to build a bridge of understanding between these two worlds and understand any inherent limitations. With such an understanding, computer-literate engineers and scientists can observe computer actions and results without being baffled.

We will start with an example describing positional notation and conversion between decimal and binary numbers.

[**TABLE 2.1**](#ch02.xhtml_t2_1b) Binary, Octal, and Hexadecimal Equivalents

| Decimal | Binary | Octal | Hexadecimal |
| --- | --- | --- | --- |
| 0 | 0000 | 0 | 0 |
| 1 | 0001 | 1 | 1 |
| 2 | 0010 | 2 | 2 |
| 3 | 0110 | 3 | 3 |
| 4 | 0100 | 4 | 4 |
| 5 | 0101 | 5 | 5 |
| 6 | 0110 | 6 | 6 |
| 7 | 0111 | 7 | 7 |
| 8 | 1000 | 10 | 8 |
| 9 | 1001 | 11 | 9 |
| 10 | 1010 | 12 | A |
| 11 | 1011 | 13 | B |
| 12 | 1100 | 14 | C |
| 13 | 1101 | 15 | D |
| 14 | 1110 | 16 | E |
| 15 | 1111 | 17 | F |
| 16 | 10000 | 20 | 10 |
| 17 | 10001 | 21 | 11 |

## 2.1 Numerical Quantities as Stored in the Computer

Quantities internal to the computer are stored as binary digits and organized in groups. The fundamental grouping is called a *word*. In the early days of digital computers, words were groups of 8, 12, or 16 binary digits, or *bits*. A group of 8 bits is commonly called a *byte*.[⁴](#ch02.xhtml_n2_4) As computer architectures became more sophisticated, word lengths of 32 and then 64 bits became common. Words in the computer typically represent either instructions or information, and they are of finite length.

### 2.1.1 Integer Numbers

Integers, “whole numbers” or numbers without fractional parts, are typically stored in one computer word, and possibly multiple words. Consider a simple example, the 8-bit byte. We can represent all the possible binary numbers in a table from 00000000[2] to 11111111[2]:

1.  00000000
2.  00000001
3.  00000010
4.  00000011
5.  •
6.  •
7.  •
8.  11111101
9.  11111110
10.  11111111

Although it should be obvious to you, we will mention that there isn’t any room for additional digits—we are restricted to 8\. Now, we pose a question: What happens when we add 1 to the last number in the table? The result is 00000000[2]. You might wonder about the 1 that was carried out of that addition, but there is no room for that. It has been said that it goes into the proverbial *bit bucket*. So, apparently, we added 1 to 11111111[2] and obtained 00000000[2]. That means, taking signs into account, that 11111111[2] is equivalent to −1, and that opens the door to defining negative integers—that is, they have a 1 in the leading position.

Another convenient way of illustrating this is shown in [Figure 2.1](#ch02.xhtml_f2_1). Numbers on the left side of the circle are considered negative, and those on the right positive. The only awkward consequence of this arrangement is at the bottom of the circle. Since we have an even number of binary arrangements, 2⁸ = 256, taking out 00000000[2], there is one left over, 10000000[2], which is self-negative (i.e. adding it to itself yields zero). By convention, since it has a leading 1, we consider it to be negative. Then, by converting to decimal, we see that our range of integers is from −128 to +127\. This is called the *2*’*s complement* representation of integers.

![](images/Fig02_01.jpg)

**[FIGURE 2.1](#ch02.xhtml_f2_1b)** The number circle for a byte.

To generalize this concept, if the word length is *n*, here 8, then the integer range is −2^(*n*)−¹ to +2^(*n*)−¹−1\. This leads to [Table 2.2](#ch02.xhtml_t2_2), which shows the 2’s complement integer range for different word lengths. For many computing software systems, the 32-bit and 64-bit word lengths, often called *short integer* (or simply *integer*) and *long integer*, respectively, are used and available to the programmer. In deciding between the two, the programmer needs to consider the range required for the application at hand. The long integer has a much wider range, but it requires twice the computer memory. Python is different. It allocates the computer words necessary to represent the integer at hand and, in this sense, has a *dynamic range* for integers of any magnitude. This removes the concern whether a finite range is limiting and is an advantage over languages such as Visual Basic or C/C++ where extra programming must be implemented when dealing with large integers. We will see more of this in [Chapter 3](#ch03.xhtml_c3).

[**TABLE 2.2**](#ch02.xhtml_t2_2b) 2’s Complement Integer Range for Different Word Lengths

| Word | Range |  |
| --- | --- | --- |
| Length | Low | High |  |
| --- | --- | --- | --- |
| 8 | –128 | 127 |  |
| 16 | –32,768 | 32,767 | “short integer” |
| 32 | –2,147,483,648 | 2,147,483,647 | “long integer” |

### 2.1.2 Real Numbers

Representing real numbers internal to the computer presents several challenges:

*   how to deal with exponents and their range
*   representing fractional parts and their precision
*   lack of precise representation of decimal fractions

Let us deal with the last challenge first.

The conversion factor from feet to meters is 0.3048\. To represent this fraction in the computer, we will convert it to binary:

1.  0.3048−2 −²  =  0.0548
2.  0.0548−2 −⁵  =  0.02355
3.  0.02355−2 −⁶  =  0.007925
4.  0.007925−2 −⁷  =  0.0001125
5.  0.0001125−2 −^(14)  =  0.00005146484375
6.  •
7.  •

To this point, the binary fraction is 0.01001110000001…, but, apparently, the conversion would keep going. This illustrates an important point—**it is not possible to represent many (or in fact, most) decimal fractions with a binary fraction with finite digits**. Hence, the precision of the conversion will depend on the number of binary digits used. For example, the exact decimal number, 0.1, cannot be represented precisely in binary. That is, whereas 0.1 can be expressed exactly with a finite number of decimal digits, it cannot be represented exactly with a finite number of binary digits.

Considering scientific notation with decimal numbers, we have integer exponents of 10\. We can then directly consider a range of binary equivalents. So, for example, if we allocate a byte for the exponent of a number, that will allow a range of 10^(−128) to 10^(127), if the binary integers are represented in 2’s complement format. For most engineering and scientific applications, that would be enough. Consequently, a decision must be made regarding how many binary digits to allocate for the exponent of a real number.

The last challenge relates to the precision of the stored number, which depends on the number of binary digits allocated. In the early days of digital computers, several different formats were used to store real numbers. Happily, over time, a common standard now called *IEEE 754 double-precision* is used by most computing systems, both in floating-point circuitry and software programs. A real number is stored in a 64-bit word (8 bytes) according to the layout illustrated in [Figure 2.2](#ch02.xhtml_f2_2).

![](images/Fig02_02.jpg)

**[FIGURE 2.2](#ch02.xhtml_f2_2b)** Layout of IEEE 754 standard for storage of real numbers.

The first bit is used to indicate the sign of the number, 0 for + and 1 for −. The exponent field of 11 bits is not laid out according to 2’s complement but rather as shown in [Table 2.3](#ch02.xhtml_t2_3). This arrangement is called a *biased exponent*. In a way, it is like rotating the number circle in [Figure 2.1](#ch02.xhtml_f2_1). The range of exponents is then

[**TABLE 2.3**](#ch02.xhtml_t2_3b) Biased Exponent Representation

| Binary | Decimal Equivalent |
| --- | --- |
| 11111111110 | 1,023 |
| 11111111101 | 1,022 |
| • | • |
| 10000000000 | 1 |
| 01111111111 | 0 |
| 01111111110 | –1 |
| • | • |
| 00000000010 | –1,021 |
| 00000000001 | –1,022 |

2^(−1022) ≅ 2.23 × 10^(−308) ↔︎ 2^(1023) ≅ 8.99 × 10^(307)

or approximately 10−^(308) to 10^(307). This is a more-than-ample range for most engineering and scientific calculations. [Figure 2.3](#ch02.xhtml_f2_3) illustrates how real numbers are represented on the real number line. Note the two gaps between the smallest positive and negative numbers and zero. In computer science, this is called the *hole at zero*.

![](images/Fig02_03.jpg)

**[FIGURE 2.3](#ch02.xhtml_f2_3b)** IEEE 754 representation of the real number line.

The final part of the real number layout is the actual number or *mantissa*. In binary exponential notation, all numbers can be represented as

±  *m**a**n**t**i**s**s**a*  ⋅ 2^( exp *o**n**e**n**t*)

The mantissa can always be normalized with a leading 1 before the *binary point*. For example, to represent the number (21.375)[10], it would first be converted to binary (10101.011)[2], then it would be normalized to (1.0101011 × 2⁴)[2].

Because the mantissas of all numbers have 1 as their first digit (except 0 of course), the IEEE 754 format does not store that leading 1—it is just understood. The remaining 52 bits are used to represent the fraction to the right of the binary point. The number of unique binary numbers that can be represented is then 1.11…11[2] or 2^(54)−1, which is approximately equal to 1.8 × 10^(16). This implies that a real number can be stored with a precision of approximately one part in 10^(16) or to 16 significant digits. Again, this is more than adequate for most computations.

## 2.2 How the Computer Stores Text

Internal storage of text or *string* information is very important since many computer applications deal with manipulation of such data (e.g. names or identification numbers that are not used in calculations). Although engineers and scientists may be more concerned with numerical data, it is important to know the basics of storing and manipulating strings. Happily, there has been a well-established standard for representing and storing text for decades. It is the ASCII code (“askey,” **A**merican **S**tandard **C**ode for **I**nformation **I**nterchange) and uses one byte to store each character. [Tables 2.4](#ch02.xhtml_t2_4) shows the ASCII codes for each text character.

For example, this is how the string “Yes” would be stored,

| Y | e | s |
| --- | --- | --- |
| 59[h] | 65[h] | 73[h] |

It is important to note that the amount of memory required to store a text string is variable depending on its length. Also, the amount of memory can be substantial, as 8 bits are used to represent a single character.

[**TABLE 2.4**](#ch02.xhtml_t2_4b) ASCII Codes for Standard Text Characters

| ![](images/Fig02_05.jpg) |

## 2.3 Boolean True/False Information

*Boolean* data are directly compatible with computer architecture, since only two states, True and False, need to be represented. The naive approach would be to do this with a single binary digit or bit. However, that does not fit well with computer architecture, which is organized in bytes and words. Consequently, it is common to use a wasteful scheme to represent a Boolean quantity, and that is to use an integer number 0 for False and 1 for True. If this is a “short” integer, requiring 32 bits, that means only the last digit is meaningful, and the other 31 are just set to zero.

Given this scheme, a Boolean quantity can be checked by testing whether it is equal to 1 or 0\. However, it is typical for programming systems to have defined Boolean constants called True and False. In this way, there is no need to understand the equivalency between the words and the numbers.

## 2.4 Computer Storage Evolution and Terminology

Since the early days of digital computers, there has been an amazing evolution of storage technology. Early computer memories were based on the use of tiny magnetic cores, like donuts, through which four thin wires were strung. To store a 1, the core was magnetized, and to store a zero, it was demagnetized. A common size for a memory bank was 2^(12) or 4,096 12-bit words or 49,152 cores. In their era, the cost for such memory was about $1/word or $4,000 for one memory unit. Today, a two terabyte USB “thumb” drive can be purchased for $40, and sizes continue to increase with costs decreasing.

To carry on this comparison, we need to understand some storage terminology. This is summarized in [Table 2.5](#ch02.xhtml_t2_5). The reduction in memory cost is phenomenal, amounting to a reduction by a factor of more than 10^(10)! Do note that the common terminology for computer storage is often (slightly) misunderstood. A megabyte (Mb) is not a million bytes, but about a million, and so forth.

[**TABLE 2.5**](#ch02.xhtml_t2_5b) Computer Storage Terminology and Size

| Term | Size |
| --- | --- |
| Bit | 1 binary digit |
| Byte | 8 bits |
| Kilobyte (kb) | 2^(10) = 1,024 bytes |
| Megabyte (Mb) | 2^(20) = 1,048,576 bytes |
| Gigabyte (Gb) | 2^(30) ≅ 1.074 × 10⁹ bytes |
| Terabyte (Tb) | 2^(40) ≅ 1.1 × 10^(12) bytes |

There is more to it than just these numbers. In the early days, computer memory was so small and expensive that programming techniques often focused on using memory sparingly and carefully. In today’s world, these techniques have largely disappeared since storage is so large and economical. The landscape of computer storage has changed dramatically.

## Problems

1.  **2.1** Express the following base-10 numbers in binary.
    1.  18191
    2.  5389
    3.  66.3125
2.  **2.2** Convert the following binary numbers to decimal.
    1.  01001101
    2.  1110001101
    3.  1000.111
3.  **2.3** Express the following base-10 numbers in base-8, octal.
    1.  87
    2.  29
    3.  53
4.  **2.4** Conversions between binary, octal, and decimal systems.
    1.  Convert the following binary numbers to octal.

        011101000010 110101100001

    2.  Convert the following binary numbers to hexadecimal.

        1001110100001001 1111010110000100

    3.  Convert the following hexadecimal numbers to binary.

        ACDC F2D1

5.  **2.5** Express your age (or another age of your choice over 18) in **(a)** decimal, **(b)** binary, **(c)** octal, and **(d)** hexadecimal.
6.  **2.6** Using binary arithmetic, compute the following additions:
    1.  101 + 011
    2.  0011 + 1001 + 0101
7.  **2.7** Using binary subtraction, compute the following subtractions:
    1.  1010−0101
    2.  11000−00111
8.  **2.8** Repeat Prob. 2.7 but perform the subtractions by adding the 2’s complement of the subtrahend. Use 8-bit integer representation.
9.  **2.9** Using binary arithmetic, compute the following product: 111011  ×  1011
10.  **2.10** Using binary arithmetic, carry out the following long divisions:
    1.  101101101
    2.  11100100
11.  **2.11** Employ 2’s-complement 8-bit integers to compute the negative of
    1.  01011010
    2.  11110000
12.  **2.12** Show the IEEE 745 binary layout for the following decimal quantities.
    1.  6.626196 × 10^(−27) (Planck’s constant)
    2.  6.02252 × 10^(23) (Avogadro’s number)
13.  **2.13** Compute the number of bytes and bits for the hard disk storage of your laptop computer.
14.  **2.14** Early in school, you undoubtedly learned about the primary colors: red, blue, and yellow and that there were three secondary colors, orange, green, and violet that are created by the addition of pairs of the primary colors (orange  =  red  +  yellow). Computers represent colors differently as they deal with the mixture of light. Thus, the three primary colors for computers, televisions, and electronics are red, green, and blue. This is called the *RGB color model,* standing for red, green, and blue. As depicted in [Table P2.14](#ch02.xhtml_tP2_14), the secondary colors are yellow, magenta, and cyan. The RGB model is an additive model, meaning that colors are created through light waves that are added together in particular combinations in order to produce colors.

    [**TABLE P2.14**](#ch02.xhtml_tP2_14b) The RGB Color Model Indicating the Mixtures of the Primary Colors that Yield the Secondary Colors

    |  | R | G | B |
    | --- | --- | --- | --- |
    | R | Red | Yellow | Magenta |
    | G |  | Green | Cyan |
    | B |  |  | Blue |

    As with everything within the computer, colors are represented by a code. The color code for RGB uses a six-digit combination of hexadecimal numbers and letters preceded by a hash mark. Each pair of hexadecimal digits represents the mix of red, green, and blue (RGB) with the magnitude of each pair indicating the intensity of each color. For example, pure blue would be represented by `#0000FF`. Because we are “decimal” animals, the hexadecimal code is often expressed as a decimal RGB code for better human understanding and communication. Because FF[h] corresponds to 255[10], the code for blue could be expressed in base-10 as

    `#0000FF` ↔︎ RGB(0, 0, 255)

    1.  Convert the code for pink `(#FFC0CB`) to the RGB code.
    2.  To convince yourself of the usefulness of hexadecimal, convert the code for pink to the equivalent binary code.

        Convert the following Hex codes to RGB codes and guess what colors they represent:

    3.  `#000000`
    4.  `#FFFFFF`
    5.  `#00FFFF`
    6.  `#A020F0` (hint: Elvis and Prince loved this color)

        If you would like to learn more about the fascinating topic of color mixing, check out [https://en.wikipedia.org/wiki/Color_mixing](https://en.wikipedia.org/). (Last edited date May 18, 2022.)

# 3 Python Basics

DOI: [10.1201/9781003256861-3](https://doi.org/10.1201/9781003256861-3)

## Chapter Objectives

*   Gain familiarity with the features of the Spyder integrated development environment, including the IPython Console, the Spyder Editor, and the Explorer window.
*   Learn how to implement algebraic expressions in Python, including those with logarithmic, exponential, trigonometric, and hyperbolic terms.
*   Create variables and use them in Python computations. Track their properties and stored values in the Variable Explorer.
*   Learn about objects, and their attributes and methods. Also, become familiar with data types, including integers, floating-point, Boolean and strings.
*   Use the arithmetic, relational and logical operators, and understand their precedence in establishing the order of calculations.
*   Learn about the various collections in Python with special attention given to lists, tuples and arrays.
*   Create simple, well-presented plots in Python with the `pylab` module, including scatter and line plots with multiple data sets, legends and titles.
*   Learn ways to input data and display results in Python, including the use of the IPython Console and external files.
*   Practice using the various sources of help for the Spyder IDE, Python and its support modules, including NumPy and SciPy.

Python is a general-purpose programming language developed in the late 1990s by the Dutch programmer, *Guido van Rossum*. It emphasizes many desirable features including *code readability* which facilitates the creation of clear, logical programs. Because of such features as well as its comprehensiveness and sound design, it consistently ranks as one of the most popular programming languages for STEM[¹](#ch03.xhtml_n3_1) applications.

The current version of the Python language, Python 3, is widely available at no cost as an open-source software package. Python has broad capabilities as an object-oriented language and is supplemented by many modular packages that contain well-tested subprograms to assist with computing tasks without “reinventing the wheel.” Python programs can be developed with a simple text editor and executed with elementary “command window” statements. Because that is a very “unfriendly” way to go about programming, several software products, called *integrated development environments* (*IDE*s), have been developed. We have selected one of these, IPython in the Spyder environment, for this text. It is a common choice for engineers and scientists for numerical problem solving and has many features to facilitate program development, debugging, documentation and “help” access to important supplementary modules.

Python, its supporting modules, and the IDEs are subject to periodic revision and improvement. Consequently, with the passage of time, it is likely that you will have access to more recent versions. The changes that occur as new versions arise are generally incremental and backward compatible[²](#ch03.xhtml_n3_2); so, you should be able to adapt easily given the information and examples presented here.

Python has many features and capabilities that are not focused on engineering and scientific computations. It would be possible to expand this chapter and subsequent chapters significantly to encompass a broad coverage of Python. An outcome of such an expansion would be to drown you in details that, although perhaps interesting and necessary to paint a complete picture, are not essential to our purpose here. We do appreciate the interests of students to learn more about Python and suggest they seek out materials and courses in computer science or on the Internet that provide this. For now, let’s get to the task at hand.

## 3.1 The Spyder/IPython Environment[³](#ch03.xhtml_n3_3)

To proceed, you first need to install the Spyder/IPython IDE on your computer. We suggest strongly that you do that before proceeding. This IDE is typically obtained by installing the *Anaconda software package*. Anaconda includes access to other open-source software packages and interfaces, such as RStudio and R for applied statistics. Information on acquiring Anaconda can be obtained via the Internet at the URL, [https://www.anaconda.com/distribution/](https://www.anaconda.com/).

After installing and launching Anaconda, you will see an interface that provides an icon for Spyder. Versions are updated periodically, so it’s likely that the version number you see will be higher than the one shown below.

![](images/SpyderLogo.jpg)

Once Spyder has been launched the first time, it will be available for direct launch, bypassing the Anaconda interface, and a Spyder command icon can be added to your operating system:

![](images/SpyderIcon.jpg)

The Spyder interface can be customized to different layouts, color schemes, etc., but the default presentation with a white background is shown in. [Figure 3.1](#ch03.xhtml_f3_1)

![](images/Fig03_01.jpg)

**[FIGURE 3.1](#ch03.xhtml_f3_1b)** The Spyder interface.

For the purposes of this chapter, we will first be typing commands into the IPython Console window. Further orientation for the IDE can be obtained via the tutorial referenced in the Explorer window. In [Section 3.7](#ch03.xhtml_h3_7), we will enter code into the Editor window and run it from there.

The calculator mode for Python operates in a sequential fashion as you type in commands line by line. For each command, you get a result. Thus, you can think of it as a fancy calculator. For example, if you type in

```
In [1]: 55-16
```

the Console will display the result[⁴](#ch03.xhtml_n3_4)

```
Out[1]: 39
```

Most calculations will involve *arithmetic operators*. These are included in *arithmetic expressions*. The arithmetic operators in Python are shown in [Table 3.1](#ch03.xhtml_t3_1).

[**TABLE 3.1**](#ch03.xhtml_t3_1b) Python’s Arithmetic Operators

| `+` | Addition |
| `−` | Subtraction and negation (unary) |
| `*` | Multiplication |
| `/` | Division (floating point) |
| `//` | Division (integer) |
| `%` | Modulus (remainder) |
| `**` | Exponentiation |

When these are combined in an expression to calculate a result, there is a priority order by which they are evaluated as summarized in [Table 3.2](#ch03.xhtml_t3_2).

[**TABLE 3.2**](#ch03.xhtml_t3_2b) Python’s Arithmetic Operator Priority Order

| Operator | Priority |
| --- | --- |
| `**` | Highest |
| `−` (unary minus) | . |
| `*, /, //, %` | . |
| `+, −` (subtraction) | Lowest |

Expressions are evaluated from left to right, except for repeated exponentiation which is from right to left. Parentheses are used to alter the order. The following examples are instructive.

```
0.5 ** 2 / 3 * 5 + 1.2
```

The calculation steps would be

```
 0.5 ** 2 ⇨ 0.25
0.25 / 3 ⇨ 0.0833…
0.0833… * 5 ⇨ 0.4166…
0.4166… + 1.2 ⇨ 1.6166…
```

You might be tempted to think that the 5 is in the denominator, but following the left-to-right process, you can see that it is not. If we wanted the 5 to be in the denominator, there are two ways to accomplish that:

```
 0.5 ** 2 / (3 * 5) + 1.2 or 0.5 ** 2 / 3 / 5 + 1.2
```

In the first case on the left, the denominator multiplication (`3` * `5`) is highest priority because of the parentheses. In the second case, because of left-to-right order, `0.25` is divided by `3` and then divided again by `5`. Some programmers prefer the first case because it clearly sets off the denominator and relates well to the algebraic version,

$\frac{0.5^{2}}{3 \cdot 5} + 1.2$

but either is valid.

The following example also brings the priorities into focus.

```
-3 ** 2 ⇨ -9
```

Here, since exponentiation (**) has the highest priority, that occurs first. Then, negation is carried out with the unary minus (−). This example is worth illustrating because you may find this priority switched in different software programs. For example, that is the case for the Excel spreadsheet where the unary minus has higher priority than exponentiation.

The third example illustrates the priority order of repeated exponentiation.

```
3 ** 2 ** 1.5 ⇨ ≅ 22.361...
```

The first operation is `2` ** `1.5` ⇨ `≅ 2.828...` since repeated exponentiation is processed right to left. And then `3` ** `2.828`... is carried out. If we consider the algebraic representation,

*   3^(2^(1.5))

we might normally assume that 2^(1.5) would be computed first; so, Python follows this interpretation. However, you must be aware that this order is not common to other software programs. Of course, if you wanted the 3² to be calculated first, you could enforce that with parentheses, as in

```
(3 ** 2) ** 1.5
```

In any case, if you ever have questions or doubts about the priority of operations, you can determine that by trying a few test cases. Then, if you have further doubts, you can avoid these by using parentheses.

There are two arithmetic operators that may be less familiar to you. These are integer divide, //, and modulus, %. Here is an example of *integer division*:

```
12.435 // 2.9 ⇨ 4.0
```

Regular or *floating point division* would yield a value 4.28… Integer division carries out floating-point division and then truncates (or chops off) the fractional part of the result. It is a fine point right now but note the decimal point in the result, which indicates that the result is actually a floating-point number with a zero fractional part.

The *modulus* (also called the *modulo*) *operator* returns the remainder of the integer quotient divided into the dividend. That is, carrying out the division to obtain the quotient, then taking only the integer part of that value, multiplying it by the divisor and subtracting the result from the dividend to obtain the remainder. Following the above example,

```
12.435 % 2.9 ⇨ 0.835
```

Careful with the interpretation here. This is obviously not the remainder of floating-point division: 0.28… It is the result of 2.9*4 subtracted from 12.435, where 4 is the integer part of the quotient. The modulus operator is most often used with integer calculations where the interpretation is simpler. In this case, the result is just the remainder of integer division. For example, if we want to determine whether an integer is odd or even, we can employ modulus 2, and if the result is zero, the number is even—if it is one, the number is odd. For example,

```
1243 % 2 ⇨ 1 and 1244 % 2 ⇨ 0
```

You will note here that, since the two numbers are not entered with a decimal point, the results are integers with no decimal point.

One of the most common constants used in engineering and scientific calculations is `pi` (*π*). Some software packages provide `pi` directly for use. Python does not. To obtain a built-in value of `pi`, one must invoke a supporting module. There are two common modules that provide this value: Math and NumPy. We will introduce NumPy later in this chapter. For now, if you include the `import math` statement in your Console commands, `pi` will be available as follows:

```
import math
math.pi
3.141592653589793
```

With *π* available, here to 16 significant figures, a calculation using it, such as computing the volume of a sphere of radius 5, can be carried out.

```
4/3 * math.pi * 5**3 ⇨ 523.598...
```

As summarized in [Table 3.3](#ch03.xhtml_t3_3), other constants, such as the base of the Napierian logarithm *e* (also known as *Euler’s number*), are available. Although most are not commonly used in mathematical expressions, they are sometimes displayed as the result of a calculation. For example, recalling our discussion of real numbers in [Section 2.1.2](#ch02.xhtml_h2_1_2), the maximum floating-point number for a 64-bit computer is on the order of 1 × 10^(308). Therefore,

[**TABLE 3.3**](#ch03.xhtml_t3_3b) Python’s Built-in Constants

| Name | Symbol | Definition | Value | Python |
| --- | --- | --- | --- | --- |
| Pi | *π* | Ratio of circle’s circumference to its diameter | 3.14159265358979... | math.pi |
| Euler’s number | *e* | Base of the natural logarithm | 2.71828182845905... | math.e |
| Infinity | *∞* | Value that is boundless |  | math.inf |
| Not a number |  | Value that is not numeric |  | math.nan |

```
2 * 1e308 ⇨ inf
```

## 3.2 Mathematical Functions

In [Chapter 1](#ch01.xhtml_c1), we introduced the various math functions that appear regularly in engineering and scientific calculations. It is important for you to know how to invoke those functions in Python. First, there are a few available directly in Python. Two that we use frequently are absolute value, `abs`(`•`), and rounding, `round` (`•`).

The *absolute value function* operates on real numbers as we might suspect.

```
abs(-5) ⇨ 5 and abs(5) ⇨ 5
```

It also operates on a complex number and produces the magnitude, as in

$\left| {a + j\, b} \right| = \sqrt{a^{\text{2}} + b^{\text{2}}}$

An example is

```
abs(-6 + 4j) ⇨ 7.211...
```

Notice how a complex quantity is represented in Python with the `j` symbol following the number for the imaginary part.

Here are examples of the `round`:

```
round(4.5) ⇨ 4 and round(3.5) ⇨ 4
```

Note that this function follows the convention, round 0.5 to even, that we discussed in [Chapter 1](#ch01.xhtml_c1).

There is an optional additional argument for rounding to *n* digits to the right of the decimal point that we illustrate here:

```
round(math.pi, 5) ⇨ 3.14159 and round(1250.33,-2) ⇨ 1300.0
```

Here, you will see that a positive rounding place applies to decimal fractions, a negative value to places to the left of the decimal point, and if *n* is zero, the number is rounded to the nearest integer. Also, in the second example, the round is not to even because the decimal fraction moves the value above 1,250 slightly.

As we move into exponential, logarithmic, trigonometric, and hyperbolic functions, again, we need to import these from a module. We will illustrate the *Math module* here.

```
math.exp(1) ⇨ 2.718… and math.log(math.e) ⇨ 1.0
```

The first example shows that exp (1) equals the Napierian *e*, and the second example illustrates that the `log` (•) function is the natural logarithm. Is there a base-10 logarithm?

```
math.log10(1000) ⇨ 3.0
```

Yes, there is. The `log`(,•) function can also be used to determine the logarithm to an arbitrary base, here for base 2:

```
math.log(8192,2) ⇨ 13.0
```

It is worth mentioning the `math.sqrt`(•) function as it is also used frequently.

[Table 3.4](#ch03.xhtml_t3_4) summarizes the trigonometric and hyperbolic functions available from the Math module.

[**TABLE 3.4**](#ch03.xhtml_t3_4b) Trigonometric and Hyperbolic Functions in the Math Module

| Trigonometric | Hyperbolic |
| --- | --- |
| sin(•) | asin(•) | sinh(•) | asinh(•) |
| cos(•) | acos(•) | cosh(•) | acosh(•) |
| tan(•) | atan(•) | tanh(•) | atanh(•) |

The direct trigonometric functions, e.g. `sin`(•), require radians as the argument, and the inverse trig functions, e.g. `asin`(•), produce results in radians. Although it is fairly simple to convert back and forth between radians and degrees, the Math module does provide two functions for this.

```
math.degrees(1) ⇨ 57.295… and math.radians(60) ⇨ 1.047…
```

In making this calculation with the lengthy expression, it might have occurred to you that it would be more convenient and accurate to include the conversions to radians in our commands, and perhaps we would prefer to break up the calculations in parts to make them more manageable and easier to follow, debug, and verify. The next section addresses these needs.

## 3.3 Variables and Assignment

When we write formulas and equations, we use symbols to represent the various involved quantities. The formula for the Great Circle distance (Equation 3.1) in the last section is an example of this. It is then natural for us to want to use symbols in our programming statements. This is accomplished using variable names. Values are associated with variable names through the process of assignment. Here is the simplest of examples:

```
a  = 5
```

The variable name `a` represents a location in computer memory where, after the assignment statement executes, the value `5` will be stored. A convenient analog for this process is the mailbox shown in [Figure 3.3](#ch03.xhtml_f3_3).

![](images/Fig03_03.jpg)

**[FIGURE 3.3](#ch03.xhtml_f3_3b)** Mailbox analogy for assignment.

The mailbox itself is the variable name (which corresponds to a memory location). The envelope is the value placed in the mailbox by assignment. If we follow the statement above with

```
a  = −4
```

then the `5` envelope will be removed, discarded, and replaced with a `−4` envelope.

Once a variable has been defined and assigned a value, it can be examined in the *Variable Explorer window* above the IPython Console. There, if you select the Variable Explorer tab, you will see

![](images/VariableExplorer1.jpg)

In addition to the variable name and the currently stored value, the type of the value stored, in this case an integer, is noted, and the size (number of items, here 1). As we will see later, it is possible to store collections of data under a variable name. Also, once defined, a variable can then be used in subsequent expressions. For example,

```
math.exp(a) ⇨ 0.01831…
```

What happens if we make the following assignment?

```
A  = 12
```

and check the Variable Explorer:

![](images/VariableExplorer2.jpg)

You can see that `A` and `a` are distinct mailboxes (variables). Python distinguishes between upper- and lower-case letters. In formal terms, the Python language is *case sensitive*. It is also possible to have other characters than letters in variable names, but a variable name must start with a letter. Here are three examples:

```
b12      c_10      Temperature_Value
```

Most special characters will not work in names. If you are ever in doubt, try one, and you will find out. This is especially true for special characters that are operators, like +, −, *, /, and &. The use of the underscore `(_)` as shown above is good style for separating words that are part of a variable name.

It is a best practice to use variable names that have meaning to the problem you are solving. Sometimes, this relates to names on a schematic drawing, such as `h` and `w` for height and width. On other occasions, a longer, more meaningful name makes matters clearer; however, using many long names becomes intrusive.

You need to be especially careful not to use a name that is a *keyword* in Python. Spyder helps you with this because, either in the IPython Console or in the Editor window, as soon as you type a keyword, it is coded blue. A good example is the Greek letter name `lambda`, which you will see later is employed to define a user-defined function in shorthand fashion in Python.

As we will see later, with such multi-step computations, it is more convenient to handle them in the Spyder Editor window.

## 3.4 Objects, Attributes, Methods, and Data Types

Python is an object-oriented programming language. This takes some getting used to. All entities in Python are considered, generally, to be *objects*. This includes numbers and variables. In addition to the operations we carry out with variables and numerical quantities, we may refer to the object’s *attributes* (also called *properties*), and we may invoke *methods* to act upon these objects. You will see many examples of this in this text. The syntax used in relating an object to its attributes or methods is

```
object_name.attribute       object_name.method()
```

The period (**.**) used above is not our typical decimal point—it separates the object name from what follows. The parentheses after the method name are commonly empty, but they may contain certain specifications or *arguments*. Here are two examples that are relevant to the next chapter:

```
 (123456789).bit_length() ⇨ 27

a  = 1234567890
a.bit_length() ⇨ 31
```

The `bit_length`() *method* determines the number of binary digits (bits) that are required to store the given quantity. You will notice that, when a number (also called a *literal*) is the object, it is enclosed in parentheses. That is not required for a variable name.

Another example extracts the parts of a complex quantity using the `imag` and `real` attributes:

```
 (24-0.3j).imag ⇨ -0.3
(24-0.3j).real ⇨ 24.0
```

Here, the parentheses associated with the attribute are not required. Often, we have alternatives between an object-oriented expression, as above, and the use of a built-in function, as shown here:

```
 import numpy as np
np.real(24-0.3j) ⇨ 24.0
```

We import the NumPy numerical support module and give it a shortcut name `np`. You will find that this is a common operation and style for our Python programs. Then, we can use the built-in function `real`(•) to extract the real part of the complex quantity. You will need to become accustomed with both ways of accomplishing such tasks.

As we have moved along, we have seen two numerical data types: integer and float. We have also shown how these can be combined to form the complex number type. In [Chapter 2](#ch02.xhtml_c2), we discussed how these are stored internally in the computer memory. One interesting feature of Python is that it places no limit on the magnitude of integer quantities and will allocate the amount of memory required to represent those. You can see that above with our use of the `bit_length()` method.

### 3.4.1 Boolean Type

There are two other types of information that are frequently used in Python. These are the *logical* (or *Boolean*) type and the *character* (or *string*) type. Python has two literal values for the Boolean type, `True` and `False`. We can assign a variable as follows:

```
switch  = True
```

Although you may not see it here, `True` is formatted in blue to indicate it is a keyword. If we look at the Variable Explorer,

![](images/VariableExplorer3.jpg)

you will see that the type of the variable is `bool` (Boolean), and its current value is `True`. Related to Boolean quantities, we can introduce the relational operators as in

```
math.pi > 22/7 ⇨ False
```

Here, we are posing the True/False question: is *π* greater than its approximation as 22 sevenths? And, the answer is no, or `False`. The various *relational operators* are given in [Table 3.5](#ch03.xhtml_t3_5).

[**TABLE 3.5**](#ch03.xhtml_t3_5b) Python’s Relational Operators

| Example | Operator | Relationship |
| --- | --- | --- |
| `x` == `0` | == | Equal to |
| `y` != `x` | != | Not equal to |
| `a` > `0` | > | Greater than |
| `s` < `t` | < | Less than |
| `3.9` >= `a/3` | >= | Greater than or equal to |
| `r` <= `0` | <= | Less than or equal to |

The last four may make immediate sense to you, but pay attention to the first two. We do not check equality (as a True/False test) with just one = sign, but rather two, ==.[⁶](#ch03.xhtml_n3_6) And we test that the two quantities are not equal with !=. This latter operator varies from one programming language to the next.

In addition to the relational operators, there are *logical operators* that work with one or more Boolean quantity. For example,

```
 switch = True
light  = False
switch and light ⇨ False
```

A *truth table* showing the results of using these operators is displayed in [Table 3.6](#ch03.xhtml_t3_6).

[**TABLE 3.6**](#ch03.xhtml_t3_6b) Truth Table for Logical Operators

|  |  | Highest → Lowest |
| --- | --- | --- |
| `x` | `y` | `not x` | `x and y` | `x or y` |
| T | T | F | T | T |
| T | F | F | F | T |
| F | T | T | F | T |
| F | F | T | F | F |

The `not` *operator* reverses the sense of its argument. The `and` *operator* provides a `True` result only when its two arguments are both `True`. And the `or` *operator*’s result is `True` when either or both of its arguments are `True`. Just as with the arithmetic operators, there is a precedence order when these operators are combined in an expression. This precedence is indicated Highest → Lowest at the top of the table.

It is common for the relational and logical operators to be combined in an expression. Here is an example

```
not 12 < 8 and -3 > -5
```

How does this work? First, the relational expressions are evaluated:

```
not False and True
```

Then, according to the table, the `not` operator is evaluated first,

```
True and True
```

and finally, the `and` operator is evaluated:

```
True
```

Just like arithmetic expressions, the order of these operations can be modified with parentheses. In later chapters, you will see that relational and logical expressions are essential to structured programming.

### 3.4.2 Character Type

*Character* (or *string*) data types store text. A string constant is denoted by enclosing it in either single or double quotation marks (`'` or `"`). Examples would be

```
'Isaac Newton' "Marie Curie" '123.5'
```

The open and closed marks must be the same – you can’t mix them.

One can also assign a string constant to a variable name:

```
switch  = 'on'
```

with the Variable Explorer showing

![](images/VariableExplorer4.jpg)

There are a variety of manipulations, operations, and functions that can be applied to strings. We don’t deal with these in great detail here because our emphasis is numerical problem solving. However, there are a few features worth covering. First is *concatenation*, joining strings into longer strings. Here is an example:

```
'on' + 'off' ⇨ 'onoff'
```

A few useful string-related functions are shown in [Table 3.7](#ch03.xhtml_t3_7).

[**TABLE 3.7**](#ch03.xhtml_t3_7b) String Functions

| Len(s) | Number of characters in the string `s` |
| Str(x) | Convert the number `x` to a string |
| Int(s) | Convert the string `s` to integer number |
| Float(s) | Convert the string `s` to a floating-point number |

What if you wanted to extract the first two characters of a string? Characters in a string can be referenced as follows:

```
 string[start:stop:step]
```

To extract the first two characters, here is an example:

```
'onoff'[0:2] ⇨ 'on'
```

Note that the index of the first character is zero, and the selection is up to but not including the `stop` index, 2\. For the last three characters, we can use

```
'onoff'[-3:] ⇨ 'off'
```

Indices are also used to select one or more characters in the middle of a string. For example,

```
'onoff'[1:3] ⇨ 'no'
```

That’s enough on string data types for now.

## 3.5 Collections of Data

In engineering and scientific problem solving, we are often interested in more than one data item, whether it is a number, Boolean or string. It is natural that we would want to associate a variable name with the entire collection. There are several questions that we need to address as we explore this topic:

*   Does our collection contain different data types?
*   Do we need to be able to manipulate the elements in our collection, add elements, remove them and rearrange them?
*   If our collection contains just numbers, do we need to be able to manipulate the entire collection mathematically, e.g. multiply all members by a number?

Python provides several alternatives for representing collections of data ([Table 3.8](#ch03.xhtml_t3_8)). At first, this is confusing, but, for engineering and scientific calculations, we use mainly one of these. Two others come up occasionally, and two do not.

[**TABLE 3.8**](#ch03.xhtml_t3_8b) Python Representations of Collections of Data

| Type | Description | Example |
| --- | --- | --- |
| List | A collection of various data types; e.g. using brackets |  
```
[2, False, 'oats', 0.618034]
```

 |
| Tuple | An immutable list (cannot be extended, shrunk, have elements removed or reassigned); e.g. using parentheses |  
```
(2, False, 'oats', 0.618034)
```

 |
| Set | An unordered collection of unique objects; e.g. using braces |  
```
{2, False, 'oats', 0.618034}
```

 |
| Dictionary | A collection of objects, each identified by a key, not a numerical index or subscript; e.g. value pairs within braces |  
```
Fourteeners={'Elbert':4401.2,
'Massive':4398.,
'Harvard':4395.6}
```

 |
| Array | A collection of a single data type indexed by integer subscripts for use in numerical methods and statistical calculations, provided by the NumPy module | See examples below |

The simplest type of collection is the *list*. It can contain different data types, and its contents have a distinct order (first element, second element, etc.). In defining a list, as shown in the example, brackets are used. Here is an example where the list in the example is assigned to a variable name:

```
 mylist  = [2, False, 'oats', 0.618034]
```

We can refer to specific members or elements of the list as follows:

```
 mylist[0] ⇨ 2
mylist[3] ⇨ 0.618034
```

There are two important observations here. First, brackets, not parentheses, are used following the variable name to refer to a specific element in the list. Second, the first element in the list is indexed zero, not one. This index is often called a *subscript* since it relates to subscripts in typical mathematical notation. Some confusion arises because it is customary in math notation that the first element is indexed as one, not zero. You will have to deal with this over and over in your Python programming.[⁷](#ch03.xhtml_n3_7) We will introduce more features of subscripting in dealing with arrays.

A *tuple* is a list that is *immutable* (unchangeable). You will note that it is set off with parentheses, not brackets. Once created its elements cannot be changed. Often in Python, a tuple is produced by a function, and, as a result, it wouldn’t naturally be changed, but it is typical to extract elements of a tuple, as shown here:

```
 mytuple = (2, False, 'oats', 0.618034)
mytuple[2] ⇨ 'oats'
```

We won’t spend time on the *set* and *dictionary* collections here. You may find them useful for general Python applications but less so in engineering and scientific problem solving.

The *array* is the central collection type you will see in this book. This is provided by the NumPy module in what is called a *class* named *ndarray*. The array must contain only elements of the same type. It can be created from a list or a tuple using the array function or constructor from NumPy. See these two examples:

```
 import numpy as np
x  = np.array([2.3, -4, 23.45, 5.6, -14.77])
y  = np.array((1, 2, 3, 4, 5))
```

and how the `x` and `y` variables are denoted in the Variable Explorer:

![](images/VariableExplorer5.jpg)

You will notice how we use a convenient abbreviation of `numpy` to `np` with the `import` statement. The statement creating the `x` array converts a list into an array. The second item in the list shows as an integer, but it is converted (or elevated) into a floating-point number in the `x` array, and thus shows as -`4`. in the Variable Explorer. The type of the array is `float64` where the 64 refers to the number of *binary digits* (*bits*) used to store each number (recall [Section 2.1.2](#ch02.xhtml_h2_1_2)). Notice that the size is now given as `(5,)`. The reason for the comma (`,`) is that an array can have two dimensions, often interpreted in matrix terminology as rows and columns. The statement that creates the `y` array converts a tuple into an array. The type is `int32`, meaning integer with each number stored with 32 bits. It is an integer array because all elements in the tuple are integers.

Just as with lists and tuples, we can refer to individual elements in an array with subscripts, as in

```
 x[2] ⇨ 23.45
```

Again, we note the zero-based indexing.

At this point, it is timely to introduce another feature about subscripts. This is the use of the colon (**:**). It is employed to specify a range of subscripts. A first example is

```
y[1:3] ⇨ array([2, 3])
```

Notice that the result appears to be the second and third element of the y array. Also, in the Console, the result is displayed as an array. We could understand the second element, since the first index is 1 (zero-based indexing again!). But what about this third element? Based on our use of `1`:`3`, we might expect the second through the fourth element. Not so. When we use an index range, `i`:`j`, it extracts the `i`th element (again, remember, zero-based) and up to *but not including* the `j`th element. You may think that this makes no sense. Welcome to another idiosyncrasy of Python!

The use of the colon can be extended by leaving out one of the indices:

```
x[1:] ⇨ array([ -4., 23.45, 5.6, -14.77])
y[:3] ⇨ array([1, 2, 3])
```

In the first example, leaving out the second index means “through the end of the array,” so we get the second through the fifth element. In the second example, leaving out the first index indicates “from the beginning of the array,” and we get elements `0`, `1`, and `2`. Remember, it is up to but not including the index `3` element. This indexing takes some getting used to. Be patient as understanding comes with practice.

The final feature that will be illustrated with arrays (i.e. for now—there will be more in subsequent chapters) has to do with numerical calculations. Check these examples out.

```
 2.3*y ⇨ array([ 2.3, 4.6, 6.9, 9.2, 11.5])
x*y ⇨ array([ 2.3, -8., 70.35, 22.4, -73.85])
```

First, you can see that we can multiply arrays by a constant. Of course, we could also divide by a constant. Second, arrays can be multiplied by each other if they contain the same number of elements. This multiplication is called an *array operation* because the multiplications take place item by item. In [Chapter 5](#ch05.xhtml_c5), we will introduce vector-matrix operations like dot and cross products. Those follow different rules but are just as important.

Operations like this *cannot* be performed with lists or tuples. This pair of examples is also instructive:

```
math.sqrt(x)
TypeError: only size-1 arrays can be converted to Python
scalars
np.sqrt(y) ⇨ array([1., 1.41421356, 1.73205081, 2.,
2.23606798])
```

In the first example, we attempt to use the `sqrt` function from the Math module to extract the square roots. We get an error because the functions in the Math module cannot be applied to an array, only to a single, or scalar value. For the second example, we use instead the `sqrt` function from the NumPy module, and it extracts the square roots into a corresponding array. We might expect this because the *ndarray* class is defined within NumPy. Because the functions in the Math module are also available in NumPy, you will find that we use the NumPy functions more frequently in later chapters.

The final feature to be illustrated at this point is the creation of a two-dimensional array from a two-dimensional list. See this example:

```
 X = np.array([ [ 1., 2., 3\. ], [4., 5., 6.], [7., 8., 9.] ])
X ⇨ array([[1., 2., 3.],
             [4., 5., 6.],
             [7., 8., 9.]])
```

We used an upper-case `X` here to indicate a matrix. This is not required, just a typical convention. We can interpret the array in terms of rows and columns, here 3 × 3\. To extract an element from the array, we need two indices, both zero-based,

```
X[1,1] ⇨ 5.0
```

Two-dimensional arrays still support mathematical operations, such as

```
np.log10(X)
with the result
array([[0\.        , 0.30103   , 0.47712125],
       [0.60205999, 0.69897   , 0.77815125],
       [0.84509804, 0.90308999, 0.95424251]])
```

We will feature two-dimensional arrays frequently later in the text.

## 3.6 Creating Plots

Python provides the `pylab` module that allows plots to be created quickly and conveniently. The “parent” module for graphics in Python is *Matplotlib*. We will introduce more features of Matplotlib and its `pyplot` submodule in later chapters. Many plots created in engineering and scientific problem solving are relatively simple, and `pylab` serves well to create these. We can include the capabilities of `pylab` in typical fashion with the statement

```
 import pylab as py
```

Here we are defining the abbreviation `py` to use instead of typing `pylab` each time we use its commands.

Engineering and scientific plots are typically created from data or calculated with analytical functions. When there are measured data points, but not an overwhelming number, it is typical to plot these with symbols, formally called *markers*. Occasionally, we will connect these markers with straight lines to aid in pattern recognition. When there are hundreds of data, it is typical to suppress the markers to eliminate clutter and just connect the data points with straight lines. If we are plotting an analytical function, we use many points, often hundreds, and connect these with straight lines to give the appearance of smooth curves. We recommend against using markers in the plotting of analytical functions.

If more than one series is plotted, we are faced with the decision of how to distinguish the series on the plot. For data, different marker styles are available. For lines, we can use different line styles. It is possible to use colors to distinguish markers or lines, but we must be assured that these colors will be replicated in any documents or presentations where the plot appears. If there are more than one series on the plot, it is usually a requirement to include a legend to distinguish them.

We will start with a simple scatter plot of a few data. This begins with creating arrays for our *x*-axis and *y*-axis variables.

```
import numpy as np
x  = np.array([1.5, 2.6, 4.3, 6.7, 9.9])
y  = np.array([25.7, 12.9, 17.6, -3.4, 7.7])
```

This is the command to create the plot:

```
py.scatter(x, y)
```

The plot is visible in the Explorer window above the Console by selecting the Plots tab. This is shown in [Figure 3.5](#ch03.xhtml_f3_5).

![](images/Fig03_05.jpg)

**[FIGURE 3.5](#ch03.xhtml_f3_5b)** Display in Explorer window with the Plots tab selected.

On the right, eventually there will be a stack of previous plots that you can return to display. The plot in this window can be copied to the clipboard by right-clicking it and then clicking the Copy Image icon or by using the shortcut Ctrl-C. From there, it can be pasted elsewhere in a document or presentation.

We notice some features of the plot above that we would like to modify and others that we would like to add. Here is a list:

*   The markers are blue by default. We would prefer black.
*   Engineers and scientists usually like gridlines to be able to align the data points with the scales.
*   How about axis titles? And a title for the plot too?

There are many, many options that can be specified for plots. We can address the points above with these changes:

```
 py.grid()
py.xlabel('x')
py.ylabel('y')
py.title('my first plot')
```

But first, there is a problem. We cannot enter these commands one-by-one in the IPython Console. That will not work. (Try it!) We must enter all the statements required in the *Spyder Editor* window as a Python script. It should then appear as shown in [Figure 3.6](#ch03.xhtml_f3_6).

![](images/Fig03_06.jpg)

**[FIGURE 3.6](#ch03.xhtml_f3_6b)** Spyder Editor window with Python script.

In the future, we will use the Editor to develop our Python scripts. The Console will be reserved for exploring and testing commands and one-time calculations. The Spyder Editor operates like a simple text processor, like Notepad in the Windows operating system. Although colors are not displayed in [Figure 3.6](#ch03.xhtml_f3_6), you will note in the Editor window that it automatically color codes keywords (blue), data in lists (red), and strings (green).

We’ll deal with more details of the Spyder Editor in the next section of this chapter, but, for now, it is good practice to save the script as a .`py` file before you run it. There are three ways to do that. First, from the File menu, you can select Save. You will note there that you can also save the file with a shortcut, Ctrl-S. Also, on the toolbar below the menu bar, there is a Save File icon, ![](images/SaveIcon.jpg). Here, we have saved the file in a convenient folder with the name `firstplot.py`. Once the file is saved, you should see the Save icon grayed out. Then, to run the script, there are choices too.

First, you can select Run from the Run menu, and you will see an F5 key shortcut there. You can also click the Run button, ![](images/RunButton.jpg). In the Explorer Plots window, you should see the display in [Figure 3.7](#ch03.xhtml_f3_7).

![](images/Fig03_07.jpg)

**[FIGURE 3.7](#ch03.xhtml_f3_7b)** Plot display in Explorer window.

From [Figure 3.6](#ch03.xhtml_f3_6), you can see that the color code for black is `'k'`. [Table 3.9](#ch03.xhtml_t3_9) lists the various color choices.

[**TABLE 3.9**](#ch03.xhtml_t3_9b) Color Codes

| Character | Color |
| --- | --- |
| `k` | Black |
| `b` | Blue |
| `g` | Green |
| `r` | Red |
| `c` | Cyan |
| `m` | Magenta |
| `y` | Yellow |
| `w` | White |

The `py.grid()` command has parentheses because there are options that we are not using here. The default markers are filled circles, but there are options, shown in [Table 3.10](#ch03.xhtml_t3_10).

[**TABLE 3.10**](#ch03.xhtml_t3_10b) Marker Codes

| Character | Symbol | Description |
| --- | --- | --- |
| `.` | • | Point |
| `o` | ○ | Circle |
| `+` | + | Plus sign |
| `x` | × |  |
| `D` | ◊ | Diamond |
| `v` | ∇ | Del |
| `^` | ∆ | Triangle |
| `s` | □ | Square |

As another option, what if we wanted to plot our data with markers and also connect the markers with straight lines? We would replace the `py.scatter` command with the following `py.plot` command:

```
py.plot(x, y, color = 'k', marker = 's')
```

We have also changed the marker style to a square. You will note that the Save icon is no longer grayed out, and there is an asterisk next to the file name in the tab just above the Editor window, ![](images/FirstPlotTab.jpg). These are cues to re-Save the script (a good general practice). The resulting plot is depicted in [Figure 3.8](#ch03.xhtml_f3_8).

![](images/Fig03_08.jpg)

**[FIGURE 3.8](#ch03.xhtml_f3_8b)** Plot with markers and lines.

Next, the script is modified to add another data series with its own marker and line styles and provide a legend to distinguish the curves. The result is in [Figure 3.9](#ch03.xhtml_f3_9).

![](images/Fig03_09.jpg)

**[FIGURE 3.9](#ch03.xhtml_f3_9b)** Plot with two series and a legend.

```
 import numpy as np
import pylab as py
x = np.array([1.5, 2.6, 4.3, 6.7, 9.9])
y1 = np.array([25.7, 12.9, 17.6, -3.4, 7.7])
y2 = np.array([20.2, 15.3, 10.6, 3.4, 15.2])
py.plot(x, y1,color='k', marker='s', label='y1')
py.plot(x, y2,color='k', linestyle='--', marker='d',
label='y2')
py.grid()
py.xlabel('x')
py.ylabel('y')
py.title('my first plot')
py.legend()
```

There are a couple of new elements here. First, there is a second `py.plot` command for the second `y2` series. The `label` argument provides text for the `py.legend()` command. We specify diamond markers and a dashed linestyle. The linestyle choices are shown in [Table 3.11](#ch03.xhtml_t3_11).

[**TABLE 3.11**](#ch03.xhtml_t3_11b) Linestyle Choices and Codes

| Character | Style |
| --- | --- |
| `-` | Solid |
| `--` | Dashed |
| `:` | Dotted |
| `-.` | Dash-dot |

As we create more plots like this, we will find it convenient to use certain abbreviations for the arguments in the `py.scatter` and `py.plot` commands. The two most common are:

| color | c |
| linestyle | ls |

There are many more specifications that can be made on `pylab` plots; however, what has been presented here is sufficient for you to create many functional, attractive engineering and scientific plots. In [Chapter 5](#ch05.xhtml_c5), we will introduce the Matplotlib `pyplot` module that is more comprehensive than `pylab`; but, on the other hand, it’s more complicated to use.

When you run Python scripts in the Spyder IDE, plots appear automatically when their commands are executed. Outside this environment, that may not be the case. You may have to include, at the end of the plot commands, the statement `py.show()`.

## 3.7 The Spyder Editor

In the last section, we introduced the use of the Spyder Editor and mentioned that it operates like a text editor. That is certainly true, but the Editor provides many more features that help your Python program development. The two that are most prominent are *error diagnostics* and *debug tracing*. We will explore these in this section.

Starting with the `firstplot.py` script from the last section,

```
 import numpy as np
import pylab as py
x = np.array([1.5, 2.6, 4.3, 6.7, 9.9])
y1 = np.array([25.7, 12.9, 17.6, -3.4, 7.7])
y2 = np.array([20.2, 15.3, 10.6, 3.4, 15.2])
py.plot(x, y1,color='k', marker='s', label='y1')
py.plot(x, y2,color='k', linestyle='--', marker='d',
label='y2')
py.grid()
py.xlabel('x')
py.ylabel('y')
py.title('my first plot')
py.legend()
```

We will remove a right bracket (]) from the `x` = statement and notice how the Editor reacts.

![](images/ErrorWarning1.jpg)

Immediately a red ![](images/ErrorWarningIcon.jpg) error warning appears. If we hover the mouse pointer on the ![](images/ErrorWarningIcon.jpg), a tooltip also appears:

![](images/ErrorWarning2.jpg)

It alerts us to a *syntax error*,[⁸](#ch03.xhtml_n3_8) and we need to check the statement carefully, and add the right bracket to balance the earlier left bracket. One of the common syntax errors in coding is parentheses or brackets that are out of balance.

There is a second type of notification that the Spyder Editor will provide. Suppose that we type:

![](images/ErrorWarning3.jpg)

Here, we have made a typographical error and entered `z` instead of `x` as the first argument of the `py.plot` command. The Editor immediately flags that with the tooltip

![](images/ErrorWarning4.jpg)

The statement uses a variable name, `z`, that has not been defined yet. That should help us recognize the typo.

Another error-trapping feature of the Editor is that it recognized (what it thinks are …) extraneous statements in the code. For example, if we add the statement

![](images/WarningTriangle1.jpg)

we see a warning triangle, ![](images/WarningTriangleIcon.jpg), with the corresponding tooltip

![](images/WarningTriangle2.jpg)

As soon as we would add a statement utilizing a function from the Math module, this warning would disappear. Some warnings are a bit of a nuisance, but it is still good to keep a watchful eye on them.

Even if our code contains no Editor warnings, there still may be errors that only show up when the script is run. The Spyder Editor provides a good debugging tool to help in discovering the source of such *execution* (or *runtime*) *errors*. The strategy is to *single step* through the code and keep an eye on the values of the variables in the Variable Explorer window. With our current script, choose Debug from the Debug menu of the Editor. Notice the shortcut Ctrl-F5\. You can also click the Debug icon on the tool bar ![](images/DebugIcon.jpg). Upon initiating debugging, an arrow appears adjacent the statement about to be executed, and the execution is stalled there.

![](images/DebugExecution1.jpg)

We single step the code by pressing the Ctrl-F10 combination or clicking the ![](images/SingleStepIcon.jpg) icon on the tool bar. After we pass the `x` = statement, the x variable appears in the Explorer window as

![](images/VariableExplorer6.jpg)

If we pass the point where we recognize our execution error, there are two alternatives. Typically, we just stop the debugging execution, and the simplest way to do this is to click the *stop button*, ![](images/StopButton.jpg), on the toolbar. Alternately, we might want to let the program execute without single stepping through to the end of the script. To do that, click the *continue execution button*, ![](images/ContinueExecutionButton.jpg).

When the Python script is longer, it often would take too many single steps to reach the point of interest in the code. A technique we can use in such cases is to place a *breakpoint* in the code, execute continuously to that point, and then begin single stepping. For example, we might like to stop at the first `py.plot` command. If you move the mouse point up and down slowly just to the right of the line number in the Spyder Editor, you will see red dots appear. Stop at the line where the breakpoint will be set and click the red dot. That places the breakpoint there.

![](images/Breakpoint1.jpg)

If we begin continuous execution with the Debug File button, ![](images/DebugFileButton.jpg), or Ctrl-F5, the code will run until the breakpoint line and stop.

![](images/Breakpoint2.jpg)

There we can examine variables and continue execution, either continuously, ![](images/ContinueExecutionButton.jpg), or single stepping, ![](images/SingleStepIcon.jpg). When there is no more need for the breakpoint, it can be removed by clicking the red dot. More than one breakpoint can be set, and a breakpoint can also be set or removed by selecting the line of code and pressing the F12 key. There is an option on the Debug menu to clear all breakpoints. With practice, you will find these debugging operations natural and very convenient, especially for large scripts.

It is common to be working with more than one Editor window at a time. A new window can be created from the File menu, New File command, using the Ctrl-N shortcut, or clicking the New File icon ![](images/NewFileIcon.jpg) on the left end of the toolbar. The new window will appear with a suggested heading that we can either edit, remove, or possibly replace. One feature that you observe in this heading is text between triple quotations, `"""`. In Python, this is called a *docustring* and is used to provide information about the Python script, possibly including a description of its purpose, author, and date of development. With simple scripts where we are just exploring Python, we typically remove this *header information*. Later, we will use them regularly.

An important feature of Python programming is to include explanatory *comments* within the code. These non-executable labels are essential for making your code readily understandable by others and even for you if you have been away from the script for some time. Comments are preceded by the character # and can be inserted on their own line or added to the end of lines of code. Here are two examples:

![](images/AddingComments.jpg)

The Spyder Editor shows the comments in a light gray italic font.

When the Python script file is no longer needed, you can remove it from the Spyder Editor window by clicking the ![](images/TabX.jpg) on the tab. If the latest version of the file has not been saved, the Editor will remind you to save it before removing it.

There are several additional Spyder features that are worth mentioning. When using the Variable Explorer in conjunction with Editor debugging, as you run the script over and over, variables displayed in the Explorer are not removed—some are just updated. This means that the Explorer window can become cluttered with previous variables that are no longer of interest. A way to handle this is to clear the window, and this is done by clicking the icon in the toolbar at the upper left of the Variable Explorer window.

![](images/RemoveVariables.jpg)

There is a similar icon in the top right corner of the Console that performs the same action.

While we are in the business of *clearing*, if the IPython Console has a long history of commands that are no longer of interest, you can type `clear` as a command, and that history will be removed. You will start over with a blank window.

Spyder provides a *Preferences window* on the Tools menu or by clicking the wrench icon, ![](images/WrenchIcon.jpg). Although we won’t go into that in detail here, this provides many options for customizing Spyder including the overall appearance and layout of the windows, background colors (some prefer a black background with light fonts). It also allows for setting preferences having to do with functional features of Spyder, such as run execution, the Editor, the Variable Explorer, and keyboard shortcuts.

## 3.8 Input and Output

There are numerous ways to get information into a Python script and getting results out. As far as input goes, the two common methods are (1) input directly from the user during the execution of a script and (2) input of large amounts of data from an external file. Output methods are displaying results in the Console and outputting results to an external file. Along with the output methods comes the issue of formatting of results.

### 3.8.1 Console Input and Output

User input is commonly employed for scripts to allow user interaction. Here is a simple example:

```
tempF  = input('enter a temperature in degrees F: ')
```

When this statement is executed, the string within parentheses of the input statement appears as a prompt in the Console, where you can type in a value followed by the Enter key.

```
enter a temperature in degrees F: 72
```

After executing this statement, checking the Variable Explorer, we see

![](images/VariableExplorer7.jpg)

A key observation is that the `tempF` variable is storing a string, not an integer or floating-point number. We intend to use the value of `tempF` as a number in a formula, so we must convert the string into a floating-point number. This is accomplished with the `float` function (recall [Table 3.7](#ch03.xhtml_t3_7)),

```
tempF  = float(input('enter a temperature in degrees F: '))
```

and, after execution, the Variable Explorer now shows

![](images/VariableExplorer8.jpg)

which indicates that `tempF` is now type `float` and ready for calculations. A statement can then be added to convert the temperature to Celsius.

```
tempC  = (tempF-32)/1.8
```

When the script is run, the Variable Explorer now shows

![](images/VariableExplorer9.jpg)

Although we can see the converted value, it would be more convenient to display that value in the Console right after the input query. To do that, we add the statement

```
print('temperature in degree C is', tempC)
```

and the combined display in the Console shows as

```
enter a temperature in degree F: 72
temperature in degree C is 22.22222222222222
```

Of course, the display of so many fractional digits is not satisfying, and we will get back to that later.

### 3.8.2 File Input and Output

An alternate type of input is to read data in from an external file. These are most often *text files*, either `.txt` or `.csv` type. The `.csv` file may be produced by saving data on an Excel spreadsheet and indicates that, if there are multiple data on a line (or record), these are separated by commas (*comma delimited*). Information in a text file may be numerical or strings or a combination. [Table 3.12](#ch03.xhtml_t3_12) presents an example set of data counting the number of Atlantic hurricanes per year from 1851 to 2020.[⁹](#ch03.xhtml_n3_9)

[**TABLE 3.12**](#ch03.xhtml_t3_12b) Number of Atlantic Hurricanes Per Year from 1851 to 2020

| 1851 | 3 | 1871 | 6 | 1891 | 7 | 1911 | 3 | 1931 | 3 | 1951 | 8 | 1971 | 6 | 1991 | 4 | 2011 | 7 |
| 1852 | 5 | 1872 | 4 | 1892 | 5 | 1912 | 4 | 1932 | 6 | 1952 | 6 | 1972 | 3 | 1992 | 4 | 2012 | 10 |
| 1853 | 4 | 1873 | 3 | 1893 | 10 | 1913 | 4 | 1933 | 11 | 1953 | 6 | 1973 | 4 | 1993 | 4 | 2013 | 2 |
| 1854 | 3 | 1874 | 4 | 1894 | 5 | 1914 | 0 | 1934 | 7 | 1954 | 8 | 1974 | 4 | 1994 | 3 | 2014 | 6 |
| 1855 | 4 | 1875 | 5 | 1895 | 2 | 1915 | 5 | 1935 | 5 | 1955 | 9 | 1975 | 6 | 1995 | 11 | 2015 | 4 |
| 1856 | 4 | 1876 | 4 | 1896 | 6 | 1916 | 10 | 1936 | 7 | 1956 | 4 | 1976 | 6 | 1996 | 9 | 2016 | 7 |
| 1857 | 3 | 1877 | 3 | 1897 | 3 | 1917 | 2 | 1937 | 4 | 1957 | 3 | 1977 | 5 | 1997 | 3 | 2017 | 10 |
| 1858 | 6 | 1878 | 10 | 1898 | 5 | 1918 | 4 | 1938 | 4 | 1958 | 7 | 1978 | 5 | 1998 | 10 | 2018 | 8 |
| 1859 | 7 | 1879 | 6 | 1899 | 5 | 1919 | 2 | 1939 | 3 | 1959 | 7 | 1979 | 5 | 1999 | 8 | 2019 | 6 |
| 1860 | 6 | 1880 | 9 | 1900 | 3 | 1920 | 4 | 1940 | 6 | 1960 | 4 | 1980 | 9 | 2000 | 8 | 2020 | 13 |
| 1861 | 6 | 1881 | 4 | 1901 | 6 | 1921 | 5 | 1941 | 4 | 1961 | 8 | 1981 | 7 | 2001 | 9 |  |  |
| 1862 | 3 | 1882 | 4 | 1902 | 3 | 1922 | 3 | 1942 | 4 | 1962 | 3 | 1982 | 2 | 2002 | 4 |  |  |
| 1863 | 5 | 1883 | 3 | 1903 | 7 | 1923 | 4 | 1943 | 5 | 1963 | 7 | 1983 | 3 | 2003 | 7 |  |  |
| 1864 | 3 | 1884 | 4 | 1904 | 4 | 1924 | 5 | 1944 | 8 | 1964 | 6 | 1984 | 5 | 2004 | 9 |  |  |
| 1865 | 3 | 1885 | 6 | 1905 | 1 | 1925 | 1 | 1945 | 5 | 1965 | 4 | 1985 | 7 | 2005 | 15 |  |  |
| 1866 | 6 | 1886 | 10 | 1906 | 6 | 1926 | 8 | 1946 | 3 | 1966 | 7 | 1986 | 4 | 2006 | 5 |  |  |
| 1867 | 7 | 1887 | 11 | 1907 | 0 | 1927 | 4 | 1947 | 5 | 1967 | 6 | 1987 | 3 | 2007 | 6 |  |  |
| 1868 | 3 | 1888 | 6 | 1908 | 6 | 1928 | 4 | 1948 | 6 | 1968 | 4 | 1988 | 5 | 2008 | 8 |  |  |
| 1869 | 7 | 1889 | 6 | 1909 | 6 | 1929 | 3 | 1949 | 7 | 1969 | 12 | 1989 | 7 | 2009 | 3 |  |  |
| 1870 | 10 | 1890 | 2 | 1910 | 3 | 1930 | 2 | 1950 | 11 | 1970 | 5 | 1990 | 8 | 2010 | 12 |  |  |

*Source:* [http://tropical.atmos.colostate.edu/Realtime/index.php?arch&loc=northatlantic](http://tropical.atmos.colostate.edu/)

These data have been stored from a spreadsheet in a text file, `AtlanticHurricaneHistory.csv`, with each year and number on a line separated by a comma. We would like to import the data into a Python script and create a plot of number of hurricanes versus calendar year. You can see that it would not be practical to enter these values into our script one by one. To read these data into our script, we use the `loadtxt` function from the NumPy module:

```
 import numpy as np
year, hurr  = np.loadtxt('AtlanticHurricaneHistory.csv' \
       , unpack = True, delimiter = ', ')
```

When this is executed, the Variable Explorer shows

![](images/VariableExplorer10.jpg)

Notice that, even though the numbers appear as integers in the data file, they are imported as floating-point. The `unpack`=`True` specification asks the `loadtxt` function to separate the items on each record into distinct array variables. The `delimiter` specification is because we have a `.csv` file. Now, we can add the code to produce a plot of the data. Since there are quite a few, we won’t use markers, just straight lines connecting the data points.

```
 import numpy as np
import pylab as py
year, hurr = np.loadtxt('AtlanticHurricaneHistory.csv', \
             unpack=True, delimiter=', ')
py.plot(year, hurr, c='k')
py.grid()
py.xlabel('Year')
py.ylabel('Number of Hurricanes')
py.title('Atlantic Hurricane History')
```

The plot produced is shown in [Figure 3.11](#ch03.xhtml_f3_11)

![](images/Fig03_11.jpg)

**[FIGURE 3.11](#ch03.xhtml_f3_11b)** Plot of Atlantic hurricane data.

There is a companion NumPy function called `savetxt` that allows you to save a data set to a text file. From there, it might be imported by other software, such as an Excel spreadsheet. Another need that may arise is saving data for future access in another Python script. Although that could be managed using `savetxt` and `loadtxt` functions, NumPy provides `save` and `load` functions to export an array in a binary format for subsequent importing into a Python script.

### 3.8.3 Formatting Output

We have used the `print` function earlier in this chapter to display results in the IPython Console. An issue that we pointed out was that the numbers displayed were to full precision with too many digits. The way to manage this is to include format information in the `print` statement. Here is an earlier example:

```
tempF  = float(input('enter a temperature in degrees F: '))
tempC  = (tempF-32)/1.8
print('temperature in degrees C is', tempC)
```

with the Console display

```
 enter a temperature in degrees F: 88
temperature in degrees C is 31.11111111111111
```

Perhaps we would like to display the converted temperature only to the tenths place. A modification to the `print` statement accomplishes this.

```
print('temperature in degrees C is {0:5.1f}'.format(tempC))
```

with the resulting output

```
temperature in degrees C is 31.1
```

What did we do here? There are two changes. First, we included a format specification in the string, `{0:5.1f}`. This governs the display of the `tempC` value. It is fairly cryptic, so it deserves some explanation.

First, notice that it is enclosed in braces, {•}. Next, the leading `0` indicates that this is the first value to be formatted (more than one can be formatted—zero-based indexing rears its head again!). Following a separator colon (:), we see `5.1f`. The `5` specifies the width of the field for the display and the `.1` indicates to one decimal place. Finally, the `f` indicates that this is a floating-point display.

There are other formatting letter characters:

*   b – binary
*   d – decimal (for integers)
*   e – exponent (scientific notation)
*   g – general (floating point, using scientific notation for large or tiny numbers)

and more beyond these.

Here are three illustrative examples:

```
 numdays = 44165
print('number of days since Jan 1, 1900: {0:6d}'.format(numdays))
number of days since Jan 1, 1900: 44165
----------------------------------------------------------------
Planck = 6.62607015e-34 # J*s
print("Planck's constant is {0:15.8e}".format(Planck))

Planck's constant is 6.62607015e-34
----------------------------------------------------------------
mu = 0.000001 # m
print('one micron is {0:3.1g} meters'.format(mu))
mm = 0.001 # m
print('one millimeter is {0:3.1g} meters'.format(mm))
one micron is 1e-06 meters

one millimeter is 0.001 meters
```

Things to notice: The number of days is an integer, so the `d` format is appropriate. Planck’s constant requires scientific notation with the `e` format.[^(10)](#ch03.xhtml_n3_10) The `g` format chooses to display the micron equivalent in scientific notation, but the millimeter equivalent in floating-point format. It turns out that 0.001 is the dividing point for that decision. The upper dividing point depends on the number of decimal places requested and is 10 raised to that number.

You will see many examples of `print` formatting used in this text. We have found that a good practice is to display results first with a simple `print` statement and then add formatting later to make the output look better. It is worth mentioning that formatting is a more general topic. There are many alternatives, and we have chosen one here to limit the complexity.

Information on `print` formatting and functions like `loadtxt` and `savetxt` is available from Python and NumPy documentation. That introduces the next section where we discuss how to find help on Python, its modules like NumPy, and the Spyder IDE.

## 3.9 Obtaining Help

It is a common and very frequent need when programming Python scripts to look for assistance. This occurs at several levels:

*   recalling the arguments or specifications that accompany a built-in function, e.g. `loadtxt` from NumPy,
*   finding information on a feature or function that you think exists or should exist, e.g. a four-quadrant arctangent function in NumPy or elsewhere, and
*   asking a general question, “How do I . . . in Python?”

There is far more detail associated with Python and its various support modules that we can present in this text. You may wish to supplement your library with one or more general texts on Python programming. Good examples are [Deitel and Deitel (2020)](#ch11_ref.xhtml_r4) and [Gaddis (2018)](#ch11_ref.xhtml_r5). In addition, there are a plethora of videos on Python that you can access on the Internet.

The Spyder Editor provides timely assistance as you enter a Python function. An example is shown in [Figure 3.12](#ch03.xhtml_f3_12) for the `print` function used in the previous section.

![](images/Fig03_12.jpg)

**[FIGURE 3.12](#ch03.xhtml_f3_12b)** Example Spyder Editor tooltip for the `print` function.

The floating tooltip shows the arguments or parameters of the function and provides additional information below. This may not occur with all keywords and functions but is commonly provided. One can also hover the mouse pointer on a keyword or function and press Ctrl-I. For example, on the `print` function, this provides help information in the Explorer Window.

![](images/PrintHelp.jpg)

The next level of assistance is provided via the *Spyder Help menu*.

![](images/SpyderHelpMenu.jpg)

There are several, general resources here of interest, including Spyder documentation, tutorial videos, and Spyder tutorial. As for specific help on Python, NumPy, and another frequently used module, SciPy, this is found via the Internet. For the version of Python (3.9) shown here: [https://docs.python.org/3.9/](https://docs.python.org/).

You will find numerous choices there as shown in [Figure 3.13](#ch03.xhtml_f3_13).

![](images/Fig03_13.jpg)

**[FIGURE 3.13](#ch03.xhtml_f3_13b)** Python Help selections.

There is also a Quick search field where we could type `abs`, and it would take us to

![](images/AbsHelp.jpg)

Often, we are searching for information on features of the NumPy or SciPy modules. A good place to start at is [https://docs.scipy.org/doc/](https://docs.scipy.org/).

You will see there the display in [Figure 3.14](#ch03.xhtml_f3_14).

![](images/Fig03_14.jpg)

**[FIGURE 3.14](#ch03.xhtml_f3_14b)** NumPy and SciPy Help selections.

Our typical choices here will be Complete Numpy Manual or SciPy Reference Guide. As an example, choosing the former provides the display in [Figure 3.15](#ch03.xhtml_f3_15).

![](images/Fig03_15.jpg)

**[FIGURE 3.15](#ch03.xhtml_f3_15b)** NumPy Help selections.

We can type `tangent` in the Quick search field and click Search (or press Enter), and the result is shown in [Figure 3.16](#ch03.xhtml_f3_16)..

![](images/Fig03_16.jpg)

**[FIGURE 3.16](#ch03.xhtml_f3_16b)** Search results for tangent.

The `arctan2` entry looks interesting as far as a four-quadrant arctangent, so, selecting that, we get the detail depicted in [Figure 3.17](#ch03.xhtml_f3_17).

![](images/Fig03_17.jpg)

**[FIGURE 3.17](#ch03.xhtml_f3_17b)** Detail information on the `arctan2` function.

Below this, it provides details on all the parameters or arguments to the function.

Finally, we come to the most general “How do I …?” inquiry about Python. The open nature of Python stimulates a lot of information available on the Internet. An example that relates to [Chapter 5](#ch05.xhtml_c5) in this text might be

![](images/DotProductQuestion.jpg)

There are many results. One is displayed in [Figure 3.18](#ch03.xhtml_f3_18).

![](images/Fig03_18.jpg)

**[FIGURE 3.18](#ch03.xhtml_f3_18b)** Internet search results for the dot product.

As you make your way through programming in Python to solve engineering and scientific problems, you will encounter many questions and perhaps frustrations. Although we sympathize, this is the way it goes. And, in fact, it is the nature of problem solving in general. After looking for help online, via the Spyder IDE or the Internet, you should keep in mind consulting with others: instructors, teaching assistants, fellow students, etc. Some worry that, by seeking assistance, they are exposing their lack of knowledge. Don’t fall into that trap.

Also, avoid spending too much time with a “try this, try that” approach, sometimes called *shotgun programming*, hoping for success without really understanding what you’re doing. It’s better to look for help and examples that will shortcut the time to success in solving your problems.

## Problems

1.  **3.1** Implement the following arithmetic expressions in the IPython Console and report the numerical results.
    1.  $\frac{12 - \frac{5}{\text{2}}}{\left| {\frac{\text{22}}{\text{7}} - \pi} \right|}$
    2.  $\pi\, \cdot \text{1}\text{1}^{\text{2}}\,\left( \frac{\text{3} \cdot \text{15} - \text{11}}{\text{3}} \right)$
    3.  $\frac{\text{1}}{\frac{\text{1}}{\text{20}}\text{+}\frac{\text{3}}{\text{11}} - \frac{\text{0.6}}{\text{0.2}}}$
2.  **3.2** Determine the Great Circle distance in kilometers between the following airport locations.
    1.  Reykjavik, Iceland – Keflavik Airport

        Los Angeles – LAX Airport

    2.  Dubai, UAE – International Airport

        Buenos Aires, Argentina – Ministro Pistarini International Airport

    3.  London, England – Gatwick Airport

        Belfast, N. Ireland – George Best City Airport

3.  **3.3** The sum-of-angles trigonometric identity for tangents is given as

    $\text{t}\text{a}\text{n}\left( {\alpha + \beta} \right) = \frac{\text{t}\text{a}\text{n}(\alpha) + \text{t}\text{a}\text{n}\beta}{\text{1} - \text{t}\text{a}\text{n}(\alpha)\,\text{t}\text{a}\text{n}(\beta)}$

    Verify this identity with computations in the IPython Console for *α* = 37° and *β = *107°.

4.  **3.4** As shown in [Figure P3.4](#ch03.xhtml_fP3_4), a *lune* is a three-dimension, pie-like slice of a sphere. The volume of a lune is given by 2*r*²*θ* where *r* is the radius of the sphere, and *θ* is the included angle. Using Python, compute the volume of a lune of the Earth in cubic kilometers from the longitude of Istanbul, Turkey, to that of Madrid, Spain.![](images/Fig03P_04.jpg)

    **[FIGURE P3.4](#ch03.xhtml_fP3_4b)** Depiction of a lune.

5.  **3.5** Find the worldwide annual production of methanol in million metric tons. Obtain the density of methanol at room temperature and compute the corresponding volume of methanol in cubic meters. Determine the volume of a typical tanker truck used for transporting liquid chemicals. Compute the number of tanker trucks required to contain this annual production. Estimate the length of the tanker truck including its tractor. If the computed number of tanker trucks were lined up one after another, how long would the line be? How does that compare to the circumference of the Earth at the Equator?
6.  **3.6** The Colorado River Aqueduct carries about 1.1 million acre-feet of water per year from the Colorado River at the Arizona-California border to the Los Angeles basin. The average daily consumption of water in Los Angeles County is 85 gallons. How many people could be supplied water by the Colorado River Aqueduct?
7.  **3.7** Using Python, complete the following expressions and explain the results.
    1.  `round(np.pi,8)` and `round(np.pi,7)`
    2.  `2`**`3`**`4` and `(2`**`3)`**`4`
    3.  np`.``arctan(1.5)` and `np.``arctan2(−3.,−2.)`
    4.  `4`+`−3`
8.  **3.8** The following data represent the density of water, *ρ* (kg/m³), at sea-level atmospheric pressure for temperatures, *T*, from 0 ° C to 100 ° C. Use Python’s `pylab` module to create a neatly labeled plot of the data and comment on any characteristics you observe.

    | ***T***(°C) | ρ(kg/m³) | ***T***(°C) | ρ(kg/m³) | ***T***(°C) | ρ(kg/m³) | ***T***(°C) | ρ(kg/m³) |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | 0 | 999.87 | 20 | 998.23 | 50 | 988.07 | 80 | 971.83 |
    | 2 | 999.97 | 25 | 997.08 | 55 | 985.73 | 85 | 968.65 |
    | 4 | 1,000 | 30 | 995.68 | 60 | 983.24 | 90 | 965.34 |
    | 6 | 999.97 | 35 | 994.06 | 65 | 980.59 | 95 | 961.92 |
    | 10 | 999.73 | 40 | 992.25 | 70 | 977.81 | 100 | 958.38 |
    | 15 | 999.13 | 45 | 990.25 | 75 | 974.89 |  |  |

9.  **3.9** Download, as a .`csv` file, the history of global average temperature deviation from the 20th Century average from NOAA’s National Centers for Environmental Information (NCEI)- Climate at a Glance website. Write a Python script to import these data and create a neatly labeled plot.
10.  **3.10** Download, as a .`txt` file, the history of atmospheric global CO[2] concentration from [https://gml.noaa.gov/ccgg/trends/data.html](https://gml.noaa.gov/). Write a Python script to import these data and create a neatly labeled plot. If you also solved Problem 3.9, plot the two datasets on the same graph with a legend. To do this, you will have to “trim” the temperature dataset so the years match those of the CO[2] history. Also, scale down the CO[2] data by a factor of 1,000.
11.  **3.11** Write a Python script that computes the volume of liquid in a horizontal, cylindrical tank. See [Figure P3.11](#ch03.xhtml_fP3_11). Specify a tank diameter of 2 m and length of 4 m. Allow the user to input the liquid depth at the centerline of the tank. Produce output in the Console displaying the liquid volume in liters. The formula to be used is

    ![](images/Fig03P_11.jpg)

    **[FIGURE P3.11](#ch03.xhtml_fP3_11b)** Horizontal, cylindrical tank containing a liquid.

    $V = \left( {r^{\text{2}}\,\text{c}\text{o}\text{s}^{- \text{1}}\left( \frac{r - h}{r} \right) - \left( {r - h} \right)\,\sqrt{\text{2}\, r\, h - h^{\text{2}}}} \right)\,\, L$

    where *V* = volume of liquid, *r* = tank radius = diameter/2, *L* = length of the tank, *h* = liquid depth. All dimensions used in the formula must be consistent.

12.  **3.12** Newton’s Universal Law of Gravitation is given by

    $F = \frac{G\, m_{\text{1}}\, m_{\text{2}}}{d^{\text{2}}}$

    where *F* = gravitational force (N), *m*[1] and *m*[2] = the two involved masses (kg), *d* = distance between the centers of the two masses (m) and *G* = the universal gravitation constant (6.673 × 10^(–11 )N·m²/kg²). Determine the gravitational force for the following two cases:

    1.  A person with mass 80 kg standing on the surface of the Earth. The radius of the Earth is 6,371 km, and its mass is estimated as 5.98 × 10^(24 )kg.
    2.  The mass of the planet Jupiter is estimated as 1.898 × 10^(27 )kg. The mass of Jupiter’s moon Europa is 4.8 × 10^(22 )kg. The orbital radius of Europa is 670,900 km.
13.  **3.13** When counting hours on a twelve-hour clock, you count up to 12 and then wrap back to 1\. For example, say you want to determine what time it would be 10 hours after 9:00 a.m. On a twelve-hour clock, you cannot simply add 10 to 9 because you would get 19\. Complete the last two statements of the following code fragment to compute the time for a 24-hour clock (`t24`) and use the modulus operator to compute the 12-hour clock time (`t12`):

    ```
     tinit = 9
      deltat=10
      t24 =
      t12 =
    ```

# 4 Structured Programming with Python

DOI: [10.1201/9781003256861-4](https://doi.org/10.1201/9781003256861-4)

## Chapter Objectives

*   Understand the need for modifications to the sequential structure of Python programs.
*   Learn about selection structures and be able to implement the various `if` statement types to accomplish the required decisions.
*   Know how to use the `for` loop structure to implement count-controlled iteration.
*   Be able to program the `while` loop structure to accomplish pre-test, mid-test, and post-test loops, and combinations of those.
*   Create user-defined functions to “package” calculations.
*   Know how to break down programs into manageable modules, often with user-defined functions.
*   Understand the concept of variable scope as it relates to subprograms.
*   Learn how to store functions as separate Python program files and import those files into Python scripts.

The Python scripts introduced in [Chapter 3](#ch03.xhtml_c3) consisted of a set of statements that were executed in sequence. That arrangement works well for simple calculations but runs into problems when faced with the following scenarios:

*   different calculations are required depending on one or more True/False conditions that are evaluated,
*   code needs to be repeated many times,
*   a calculation needs to be “packaged” so that it may be invoked several times, perhaps from different locations in a script, or
*   a Python script grows to be hundreds (or thousands!) of statements and needs to be broken down into “bite-size” modules to become more manageable.

Of course, these challenges have confronted programmers from the beginning of digital computer technology in the mid-20th century, and all programming languages have provided features to handle these scenarios. The purpose of this chapter is to introduce these features as provided by Python.

## 4.1 An Overview of Program Structure

A big picture view of a programming task is illustrated in [Figure 4.1](#ch04.xhtml_f4_1). The primary concept presented here is that of a linear sequence. The oversimplified flowchart on the left is expanded on the right to illustrate the typical first and final steps with a main segment of computations in between.

![](images/Fig04_01.jpg)

**[FIGURE 4.1](#ch04.xhtml_f4_1b)** Overall program structure.

As we delve into the program computations, situations arise that require deviation from the sequential, step-by-step scheme. The first of these scenarios is when a condition needs to be satisfied before one or more statements are executed. These are *decision structures*, also called *selection*, and are illustrated in the flowcharts in [Figure 4.2](#ch04.xhtml_f4_2).

![](images/Fig04_02.jpg)

**[FIGURE 4.2](#ch04.xhtml_f4_2b)** Decision structure: One-way and Two-way If.

For the *One-way If*, a logical condition is checked, and, if True, a set of program statements is executed. If False, that set is skipped. In either case, the subsequent program segment continues from the same position. The *Two-way If* structure provides a separate set of computations when the logical condition tests False. It is worth mentioning that, within the computations blocks in the figure, there can and will be imbedded structures, including If structures. In the next section, we will see how to implement these structures in Python.

The second scenario is when computations need to be repeated. This is called a *loop structure*, also *repetition*, and there are two implementations. The first of these, called the *general loop*, is presented in [Figure 4.3](#ch04.xhtml_f4_3). The second implementation includes the *list-controlled* and *count-controlled loops*. These are illustrated in [Figure 4.4](#ch04.xhtml_f4_4). The distinction between the two implementations is that, for the general loop, the number of repetitions cannot be determined before the loop is entered; whereas, for the list-controlled and count-controlled loops, the number of repetitions can be calculated prior to loop entry.

![](images/Fig04_03.jpg)

**[FIGURE 4.3](#ch04.xhtml_f4_3b)** Repetition structure: the general loop.

![](images/Fig04_04.jpg)

**[FIGURE 4.4](#ch04.xhtml_f4_4b)** List-driven and count-controlled loop structures.

Referring to [Figure 4.3](#ch04.xhtml_f4_3) for the general loop, the diagram shows a circle, or “bubble,” as the entry point to the loop. In terms of programming, there must be a statement that provides this function.

Also, although there is no bubble shown, there must be a way of signaling the end of the loop at the bottom of the figure. Within the loop, there always has to be a way to exit; otherwise, there would be a so-called *infinite loop*. This is denoted as a single decision block, although there may be more than one. There will be computations either before the loop exit decision or after or in both locations, depending on what the repetition task requires. If the exit decision is just after the loop entry, this is called a *pre-test loop*. Alternately, if the decision as at the bottom, with no post-test computations, it is called a *post-test loop*. For the full structure shown in the figure, it is a *mid-test loop*. Depending on when the end condition is met, there may be 1, 10, 100, or 1,000 repetitions.

The second loop scenarios are illustrated in [Figure 4.4](#ch04.xhtml_f4_4) where the number of loop repetitions is known ahead of the loop being entered. The first is the *list-driven structure*, and this is an important feature of Python[¹](#ch04.xhtml_n4_1). It is based on a list of items where the loop is repeated for each item in the list in sequence.

The second is the *count-controlled loop*, a structure that has been around since the earliest programming languages. This loop is characterized by three parameters: a start value, end value, and step value. After each loop iteration, the step value is added to the loop counter, and, unless the end value is equaled or exceeded, the loop is repeated. In this way, it is possible to calculate ahead of loop entry how many times the loop will be repeated. In fact, once the loop is being executed, modifying the step and stop values will not affect the number of repetitions, since they are precalculated.

In a following section of this chapter, you will learn how to implement the repetition structures in Python. It will be important to reference the figures shown here to keep in mind a good picture of the structures. Also, you will learn some variations and combinations of the structures. This will also be the case for the selection structures.

## 4.2 Implementing Decision Structures with Python

Learning the general programming structures is important because it prepares you to implement these with different programming languages. You can approach a new language, such as Python, with a question, “Since I already know what a Two-way If is, how do I implement a Two-way If in Python?” In other words, once you learn a procedural programming language like Python, you are never starting from scratch.

The first, simplest decision structure is the *One-way If*, as shown in [Figure 4.2](#ch04.xhtml_f4_2). The general syntax for this in Python is quite simple:

```
 if condition:
     statements
```

Notice the use of the colon (:) and the indentation (four spaces) for the program code that executes if the condition is True. An example might be to square a quantity but preserve the sign of the quantity:

```
 Sgnx2 = x**2
if x < 0:
    Sgnx2  = - Sgnx2
```

After the `if` statement and statement that executes if True, the code would continue, but not indented. There is no formal statement to terminate the `if` structure—it is denoted by returning to the indentation of the `if` statement.

When the statements executed if True are brief, typically one statement, a compact version of the One-way If is available:

```
 Sgnx2 = x**2
if x < 0: Sgnx2  = - Sgnx2
```

This style is often called a *One-line If*. It is possible to add statements to the `if` line delimited by semicolons (;), but this is usually not done in favor of the previous style where the indented statements follow the `if` line.

The *Two-way If*’s syntax is that of the One-way If with an “`else`” clause added:

```
 if condition:
   statements1
else:
   statements2
```

Again, the structure is terminated when the following statements return to the indentation of the `if` and `else` statements. In this example, the square of the quantity is included in the Two-way If structure:

```
 if x < 0:
    Sgnx2  = - x**2
else:
    Sgnx2  = x**2
```

Python and many other programming languages include an expanded version called the *Multi-alternative If* structure. This allows for multiple decisions to be cascaded if the prior decision is False. This is illustrated in [Figure 4.5](#ch04.xhtml_f4_5). The general syntax for this structure is

![](images/Fig04_05.jpg)

**[FIGURE 4.5](#ch04.xhtml_f4_5b)** The Multi-alternative If structure.

```
 if condition1:
    statements1
elif condition2:
    statements2
•
•
elif condition_n:
    statements_n
else:
    else statements
```

The `else` clause is optional. A somewhat trivial example of the Multi-alternative If is:

```
 if temperature < 0:
    print('Brrr!')
elif temperature < 10:
    print('Chilly')
elif temperature < 20:
    print('Comfortable')
elif temperature < 30:
    print('Warm')
elif temperature < 40:
    print('Whew! Hot!')
else:
    print('Ssssss! Gimme a break!')
```

It is important to note the `elif` clauses have to follow a particular order. The condition test `temperature `<` 30` implies that the temperature is >= 20 because of the previous test. For this example, the order is obvious, but, in other cases, you must pay close attention to the order of the `elif` clauses.

It is worth mentioning here that some other programming languages, e.g. MATLAB, Excel/VBA, C/C++, have an additional multi-alternative structure that doesn’t require the condition tests to be ordered in the sequence of evaluation; however, generally, the tests have to be mutually exclusive. (Only one test can evaluate True at a time.) These structures may be called *switch* or *select-case* and are typically used for menu selections. Python doesn’t have such a structure, but that doesn’t limit numerical computations to any great extent.

Finally, it is important to consider that one decision structure can be imbedded in another. As an example, for consider adding another Two-way If in place of code block 1 in the figure. The general syntax would then be

```
 if condition1:
    if condition1a:
        statements1a
    else:
       statements1b
elif condition2:
        statements2
•
•
elif condition_n:
       statements_n
else:
     else statements
```

After either `statements1a` or `statements1b `are executed, the overall Multi-alternative If structure is terminated and program flow continues below it.

Notice how indentation emphasizes the imbedding of the `condition1a` Two-way If structure into the `condition1` True branch. And the indentation is mandatory! But beyond being required, indentation makes the resulting code more easily readable and its underlying structure more transparent. We consider this a positive attribute of Python.

## 4.3 Implementing Repetition Structures with Python

We will consider the three loop structures, illustrated in [Figures 4.3](#ch04.xhtml_f4_3) and [4.4](#ch04.xhtml_f4_4) separately, since the implementations in Python are different.

### 4.3.1 The General Loop Structure

Python provides us with a `while` statement that allows implementation of the general loop structure. To do this, we don’t use the statement quite like it was intended. The general syntax for the `while` statement is

```
 while condition:
    loop statements
```

If the logical `condition` tests True, the `loop` `statements` (indented) are executed, and the loop is repeated. If False, the loop is exited.

Referring to [Figure 4.3](#ch04.xhtml_f4_3), the `while` code is similar to the pre-test version of the general loop, but the exit test is inverted, staying in the loop on True, and exiting on False. We need to modify the `while` code to provide the pre-, mid-, and post-test alternatives. This is accomplished with the following general syntax:

```
 while True:
    pre-test statements
    if condition: break
    post-test statements
```

First, since the `while` condition is always `True`, the loop will never exit there. Instead, we provide the opportunity for exit with the One-line If statement. When its `condition` is True, the `break` command exits the `while` loop. In this way, we have the flexibility needed to leave out the pre-test code and have a pre-test loop or leave out the post-test code and have a post-test loop. Also, this allows for the inclusion of more than one `if` statements in the loop for multiple exit opportunities.

### 4.3.2 The List-Driven and Count-Controlled Loop Structures

The need for the *list-driven loop* doesn’t occur that often in engineering and scientific applications, but it is worth learning, and it provides the context for the count-controlled loop. Python provides this capability with the `for` command. Here is the general syntax:

```
 for variable in [list]:
    loop statements
```

Notice the use of the word `in` between the variable and the list. The operation of the `for` loop is simple—it is repeated for each item in the list. Here is a trivial example:

```
 import numpy as np

for x in [30, 45, 75, 125]:
    print('{0:5.2f}'.format(np.cos(np.radians(x))))
```

The value of the cosine is displayed for several angles (in degrees) specified in the list. Here are the results:

```
 0.87
 0.71
 0.26
-0.57
```

We encounter scenarios frequently in our computations where the `for` loop list would include a sequence of values, often integers, with a start value, step interval, and end value. This list might be very long, possibly containing hundreds of values. For this we need a modification of the list-driven `for` structure, and that is provided by the `range` type. It is used to provide a list of integers for the `for` loop. Here are several examples accompanied by explanations:

1.  `range(10) `provides a list of integers from 0 to 9 in steps of 1
2.  `range(n) `assuming n is an integer variable, provides a list from 0 to `n` −1
3.  `range(1,11) `provides a list of integers from 1 to 10
4.  `range(0,11,3) `provides a list of integer values, 0, 3, 6, 9

The general syntax is

```
 range(start,end,step)
```

If `start` and `step` are left out, `start` is 0 and `step` is 1\. If a `step` different than 1 is needed, a `start` value must be included. We generally don’t see the result of the `range` type directly because it is used in the `for` statement, but it can be viewed using the `list` function:

```
 x = range(0,12,3)
print(list(x))

[0, 3, 6, 9]
```

If you are having trouble with a `range` type, you can check it this way.

There are several common scenarios for use of the count-controlled loop:

*   providing a limit on the number of loop iterations,
*   varying the subscript of an array or matrix, and
*   carrying out a set of calculations for a sequence of floating-point values.

We will illustrate all these with examples.

### 4.3.3 The break and Continue Statements with the for Loop

It is worth mentioning two features of the `while` and `for` structures that are useful on occasion. In [Section 4.3.1](#ch04.xhtml_h4_3_1), we employed the `break` statement to exit a `while` loop prematurely. The same `break` statement can be used to exit a `for` loop. Here is a simple example:

```
 import numpy as np

testdata = np.array([])
for i in range(10):
    datain=float(input('enter data item or -9999 to stop: '))
    if datain == -9999: break
    testdata = np.append(testdata,datain)

print(testdata)
```

and an example run:

```
 enter data item or -9999 to stop: -12

enter data item or -9999 to stop: 14

enter data item or -9999 to stop: 9

enter data item or -9999 to stop: 3

enter data item or -9999 to stop: -4

enter data item or -9999 to stop: -9999
[-12\. 14\. 9\. 3\. -4.]
```

This script allows the user to enter a dataset of up to ten values and signal an early end of the entry with an unusual value, here −9999. When that occurs, the `for` loop exits on the `break` statement. The −9999 used to terminate the input sequence is called a *sentinel value*.

A question that arises is how the `break` command behaves when there are nested `for` loops. As with many Python features, an effective way of answering questions is to investigate by developing a test script. Here is such a script that is designed to answer the question:

```
 for i in range(3):
    for j in range(3):
        if j >  0: break
    print('outerloop',i,j)
print('after loops',i,j)
```

Here, there is a `break` from the inner loop. Does that just exit to the outer loop? Or does the `break` exit both loops? Here is the script’s output:

```
 outerloop 0 1
outerloop 1 1
outerloop 2 1
after loops 2 1
```

It is clear that the `break` statement only exits the inner loop and not the outer loop. Well, that raises another question: What if we wanted both loops to be exited? An answer to that is to put the `break` test in both loops, as in

```
 for i in range(3):
    for j in range(3):
        if j > 0: break
    if j > 0: break
    print('outerloop',i,j)
print('after loops',i,j)
```

with the result

```
after loops 0 1
```

In conclusion, the use of the `break` statement with `for` loops is not as common as it is with the `while` loop, but it happens from time to time.

There are occasions where we want part or all of the `for` (or `while`, for that matter) loop code to be skipped, but we want the loop to continue repeating. With Python, this involves the use of the `continue` statement. Here is an example:

```
 import random
import pylab

testdata = []
for i in range(1000):
    rannum = random.normalvariate(0.,1.)
    if rannum < 0.: continue
    testdata.append(rannum)

pylab.hist(testdata,bins=20)
```

The `for` loop generates 1,000 random numbers, emulating the standard normal distribution (mean = 0, standard deviation = 1)[³](#ch04.xhtml_n4_3). The `random` module provides a family of functions related to random numbers. A common use of the module is to generate a sequence of random numbers that appear to have been drawn from a particular distribution. One common distribution is the *uniform distribution* where the probability of drawing numbers between two limits is constant. If the limits are 0 and 1, the probability of drawing a number between 0 and 0.1 is the same as that between 0.7 and 0.8.

The other common distribution is the *normal* or *Gaussian distribution* which is modeled by the classical bell curve. It is more probable to generate values near the center of the distribution, the mean, and that probability drops off as the distance from the mean increases. We use the `random  `module frequently to generate a series of random numbers. They do not follow the specified distribution exactly and so are often referred to as pseudorandom numbers. You can find out more about the `random` module from [https://docs.python.org/3/library/random.html](https://docs.python.org/).

The `if` statement skips the following `append` statement if the current random number is negative. If the number is positive, it is appended to the `testdata` array. After the `for` loop, a histogram of the `testdata` array is generated and illustrated in [Figure 4.8](#ch04.xhtml_f4_8) with a histogram plot. There were 495 data used to form this plot, about one-half of the `for` loop iterations, as expected.

![](images/Fig04_08.jpg)

**[FIGURE 4.8](#ch04.xhtml_f4_8b)** Histogram of positive values generated from the standard normal distribution.

## 4.4 User-Defined Functions in Python

We have seen the use of many built-in functions in Python and its supporting modules, like NumPy and SciPy. An important and essential feature of Python is the ability to create your own function. The concept of such a *user-defined function* is illustrated in [Figure 4.9](#ch04.xhtml_f4_9).

![](images/Fig04_09.jpg)

**[FIGURE 4.9](#ch04.xhtml_f4_9b)** Illustration of the Python user-defined function.

Functions are useful on several counts. First, they allow you to “package” a calculation so it can be invoked at several different locations in a script. Second, by carefully validating a function, the reliability of the calculation is enhanced. Third, functions are portable in that they can be made available to different scripts and programmers.

The general syntax for a Python function is

```
 def function_name(argument list):
    statements
    return results
```

Using our example from [Section 4.2](#ch04.xhtml_h4_2), squaring a value but preserving its sign, we can construct

```
 def sgnsqr(x):
    sgnx2  = x**2
    if x < 0: sgnx2  =  -sgnx2
    return sgnx2
```

Here, the function name is `sgnsqr`, and there is one argument, `x`. The code to attach the sign of `x` to the result variable, `sgnx2`, is like what we have seen before. The result is provided with the `return` statement. To use this function, either in a script or in the IPython Command window, the script must be executed or run first. If that is done, then here are examples of using the function in the Command window:

```
 sgnsqr(-2)
Out[8]: -4

sgnsqr(2)
Out[9]: 4

sgnsqr(0)
Out[10]: 0

y = -12

sgnsqr(y)
Out[12]: -144
```

This illustrates that we can use a numeric value, or a variable, here `y`, that stores a value as the argument.

We can also add a script below the function in the Editor window to prompt the user for input:

```
 def sgnsqr(x):
    sgnx2 = x**2
    if x < 0: sgnx2 = -sgnx2
    return sgnx2

y = float(input('enter a number: '))
print(sgnsqr(y))
```

When we run the script, here is an example output in the Command window:

```
 enter a number: -400
-160000.0
```

Because of the requirement to run the function code before invoking the function, you will see that we place one or more functions at the beginning of longer scripts before the ensuing script code. To enhance portability, it is also possible to save a Python code file of just the function code and then import the function into another script. If the function is saved as sgnsqr_function.py, we can import it as follows:

```
 from sgnsqr_function import sgnsqr

y  = float(input('enter a number: '))
print(sgnsqr(y))
```

and the script will execute properly. A requirement here is that the path in the file system must be such that the file can be found by the `from` command. In a sense, the .py file is our own, user-defined module, and it might contain a family of useful functions.

### 4.4.1 lambda Functions

Python provides a convenient, one-line style for creating simple functions. These are called `lambda`[⁴](#ch04.xhtml_n4_4) *or anonymous functions*. For example, we can create an abbreviated function definition like

```
 def gety(x,a,b):
    return a*x**b
```

that implements a formula *a·x*^(*b*). This can also be written more concisely as

```
gety = lambda x,a,b: a*x**b
```

Alternately, we can define the function without the parameters `a` and `b`,

```
 gety = lambda x: a*x**b
```

but then those parameters must be defined in the main script. Here is example code with accompanying execution:

```
 a = 4
b = -0.32

gety = lambda x: a*x**b

y = []
for x in [0.1,0.5,0.9]:
   y.append(gety(x))

print(y)

[8.357184523416159, 4.9933221956064475, 4.137160678619936]
```

You see that the variables `a` and `b` are first assigned values. Then, they are available to the `gety` `lambda` function. A list-driven `for` loop is used to fill out a list `y` with three evaluations of the `gety` function, and the results being displayed in the Console.

### 4.4.2 Function Arguments

The list of arguments in a function definition can take various forms. First, it is possible that arguments are not required, so the list is empty. Following an example in the previous section, we might want to have a function that provides a random value from the positive half of the standard normal distribution. That function definition, along with a test, would then be

```
 import random

def halfrand():
    while True:
        rannum = random.normalvariate(0.,1.)
        if rannum > 0.: break
    return rannum

print(halfrand())
```

An example result is

```
0.28609469258613235
```

Next, we can have a similar function but with multiple arguments. Here, the function requires specification of the mean and standard deviation of the normal distribution.

```
 def halfrand(mu,sig):
    while True:
        rannum = random.normalvariate(mu,sig)
        if rannum > mu: break
    return rannum

print(halfrand(100.,20.))
```

with the result

```
 95.48642189840088
```

As a third variation on this theme, we might want to allow for specification of the mean and standard deviation, and, if not supplied, assume the values for the standard normal distribution, 0\. and 1., respectively. This is accomplished by using *keyword arguments*.

```
 def halfrand(mu=0.,sig=1.):
    while True:
        rannum  = random.normalvariate(mu,sig)
        if rannum > mu: break
    return rannum
```

In this case, one or both arguments can be supplied. If only the second argument is supplied, it must be accompanied with the associated keyword.

```
 print(halfrand(sig=0.1))

0.18326947282604794
```

If both arguments are provided in the correct order, keyword identifiers are not required, and, if both arguments are left out, the function will use the default values. Here are two example statements with explanations:

1.  `halfrand(20.,5.)` Here, `mu`  =  20 and `sig`  =  5.
2.  `halfrand()` Since no arguments are specified, the default values are used.

In many instances, we would like to have function arguments that are arrays. It would be typical that the arrays supplied to the function would have different numbers of elements, so, within the function, the number of elements would have to be determined. As an example, we might like to create our own function to determine the *percentile value* of an ordered array. Here is a Python function that accomplishes this.

```
 def pctile(x,pct):
    n = len(x)
    mp = pct/100*(n-1)
    mp1 = int(mp)
    xp = (mp-mp1)*x[mp1]+(1-(mp-mp1))*x[mp1+1]
    return xp
```

The two arguments are an array (or list or tuple) of numerical values sorted in ascending order, and the percentile value desired (in %). The function first determines the number of elements in `x`. Then the fractional percentile location, `mp`, is calculated, where `n-1` is used because of the zero-based indexing of `x`. The integer part of the percentile location is determined using the built-in `int` function. Then, the percentile value is computed proportionately between the `mp` location `x` value and the `mp`+`1` location `x` value. This value is returned. Here is an example of the use of the `pctile` function:

```
 x = [0.1, 0.5, 0.8, 1.2, 1.7, 2.3, 3.1, 4.7, 5.1, 6.7]
print(pctile(x,25.))

1.0999999999999999
```

We can consider enhancements to the `pctile` function to make it more versatile. The requirement that the input array be sorted is restrictive. Therefore, we can add code to the function to sort the `x` array into another `y` array, and then determine the percentile using `y`. There are many ways to do this. To keep it simple here, we take advantage of the `sort` function from the NumPy module.

```
 import numpy as np

def pctile(x,pct):
    y = np.sort(x)
    n = len(y)
    mp = pct/100*(n-1)
    mp1 = int(mp)
    xp = (mp-mp1)*y[mp1]+(1-(mp-mp1))*y[mp1+1]
    return xp

x = [0.1, 0.5, 0.8, 1.2, 6.7, 2.3, 3.1, 4.7, 5.1, 1.7]
print(pctile(x,25))
```

which produces the same result, but now the `x` array does not have to be presorted in ascending order.

You can see in this last example that we invoked a function, `sort`, within another function, `pctile`. We can certainly do this with our user-defined functions too. Consider we would like to compute the *interquartile range* (`iqr`), which is the difference between the 75th and 25th percentile values—containing the centrally located 50th percentile value of our data. Given our `pctile` function, this becomes easy.

```
 def iqr(x):
    pct25 = pctile(x,25)
    pct75 = pctile(x,75)
    return pct75 - pct25
```

And testing it with our `x` array yields

```
 x = [0.1, 0.5, 0.8, 1.2, 6.7, 2.3, 3.1, 4.7, 5.1, 1.7]
print('iqr = {0:5.2f}'.format(iqr(x)))

iqr = 2.40
```

An important feature of function arguments is that, apart from variables, they can be the names of other functions. These have been called *function functions*. Let’s illustrate this with a simple example, a function to compute the average of a set of values computed from a formula supplied by a second function.

```
 import numpy as np

def funavg(func,x):
    n = len(x)
    y = np.zeros(n)
    for i in range(n):
        y[i] = func(x[i])
    return np.mean(y)
```

The first argument of the `funavg` function is the name of a function, `func`, not a variable. The second argument, `x`, is an array variable to contain a set of values. In the function code, an array `y` is created the same size as `x`, and, with a `for` loop, the `y` array is filled with the values of the `func` function evaluated with the values in the `x` array. Finally, the average of the `y` array values is returned using the `mean` function from the NumPy module.

The `funavg` function can be tested as follows:

```
 f = lambda x: x**3 - 0.28*x**2 + 0.43*x - 17.4

x = np.linspace(-10,10)
favg = funavg(f,x)
print(favg)
```

with the result

```
 -27.11428571428567
```

Notice here that we use the alternate `lambda` form for the function definition. The function `f` used here could be changed to another function and generate a corresponding different result. You can then see the flexibility of this arrangement. The concept of having a function name as an argument to another function is implemented easily and directly in Python. That is not the case in other programming languages and software packages where the implementation is more complicated or perhaps not even feasible.

This brings us to the last topic regarding function arguments. In our example above, rather than having the function `f` defined as shown there, we might want more flexibility by adding variables to define the coefficients of the polynomial expression, as in

```
 f = lambda x,a,b,c,d: a*x**3 + b*x**2 + c*x +d
```

Our `funavg` function must now “pass” the values of `a`, `b`, `c`, and `d` on through to the `func` call. But we can’t do that explicitly because then `funavg` would lose its generic character. This is accomplished by using a generic argument *`args` as shown below.

```
 def funavg(func,x,*args):
    n = len(x)
    y = np.zeros(n)
    for i in range(n):
        y[i] = func(x[i],*args)
    return np.mean(y)
```

Then, the script can be modified and tested with the same polynomial as follows:

```
 f = lambda x,a,b,c,d: a*x**3 + b*x**2 + c*x +d

x = np.linspace(-10,10)
a = 1\. ; b = -0.28 ; c = 0.43 ; d = - 17.4
favg = funavg(f,x,a,b,c,d)
print(favg)
```

The same result is produced.

As a variation on this method, we consider the situation where one or more of the arguments to our function `f` are keyword arguments, typically representing default values. We can illustrate this with a modification of the script computing a set of values from the positive half of the normal distribution, but now using a function `genrand`.

```
 import random
import pylab

def genrand(mu=0.,sig=1.):
    testdata = []
    for i in range(1000):
        rannum = random.normalvariate(mu,sig)
        if rannum < 0.: continue
        testdata.append(rannum)
    return testdata

testdata = genrand(sig=4.)

pylab.hist(testdata,bins=20)
```

You will note that when the `genrand` function is invoked (or “called”), only the `sig` variable is specified. This means that the default value of the `mu` variable will be used. The resulting histogram plot is shown in [Figure 4.10](#ch04.xhtml_f4_10).

![](images/Fig04_10.jpg)

**[FIGURE 4.10](#ch04.xhtml_f4_10b)** Histogram of data generated with the genrand function for a `sig` value of 4.0.

Now, let’s suggest that we modify our `funavg` function to accommodate a simpler `genrand` function that produces a single, positive value from the normal distribution, and we do so preserving the use of keyword arguments. Here is the code that results

```
 import random
import numpy as np

def funavg(func,x,**kwargs):
    n = len(x)
    y = np.zeros(n)
    for i in range(n):
        y[i] = func(x[i],**kwargs)
    return np.mean(y)

def genrand(x,mu=0.,sig=1.):
    while True:
        rannum = random.normalvariate(mu,sig)
        if rannum > 0.: break
    return rannum

n = 1000
x = np.arange(1,n+1)

normavg = funavg(genrand,x,sig=4.)
print(normavg)
```

First, notice that we have replaced the *`args` generic keyword argument with **`kwargs` (two asterisks!). Since the `random.normalvariate` function doesn’t really have an “x” argument, a “dummy” `x` array of numbers from 1 to 1,000 is set up using the `np.arange` function. With the `funavg` call, the `genrand` function name is supplied, the dummy x array and only one of the keyword arguments. (The other, `mu`, will employ the default value of 0.) The use of the `while` loop in the `genrand` function repeats the random number generation until a positive value is produced. The `genrand` function only returns a single value. The result is

```
 3.0213502792531117
```

Generally, the order of argument values supplied to a function has to agree with those in the function definition. If there are extra *`args` or **`kwargs`, these must follow the other arguments. Any *`args` must agree in order with their function definition and be supplied completely. Keyword arguments can be supplied partially or in different order, but they must follow other arguments, and it is common practice for them to follow required *`args` arguments. This may seem a bit confusing, but, in time, you will get used to it. Also, you will see many examples in later chapters.

### 4.4.3 Variable Scope

A simple way of defining variable scope is that it describes where a variable and its value(s) can be “seen” from different locations in a script. A good way to understand scope is to explore it with a few simple examples and then generalize our observations. Here is a first example:

```
 def func(x):
    a = 4.
    b = -0.32
    return a*x**b

print(func(12.3))
print(a,b)
```

When this code it entered in the Spyder Editor, an error is immediately noted beside the last `print` statement. This is because the values of `a` and `b` are not available in the main script – they are “local” to the function definition. If we modify the code to

```
 def func(x):
    a = 4.
    b = -0.32
    print(a,b)
    return a*x**b

print(func(12.3))
```

there are no errors noted, and the code executes to produce

```
 4.0 -0.32
1.7918033972156524
```

As we would expect, there is no problem with the `print` command inside the function because the `a` and `b` values are available there.

Now let’s turn the tables on this example.

```
 def func(x):
    print(a,b)
    return a*x**b
a  =  4.
b = -0.32

print(func(12.3))
```

This code produces the same results as above. It is evident that the variables (and their values) `a` and `b` are available in the function definition even though they are defined in the main script.

So, our first and important observation is that variables defined within functions cannot be seen outside the function; whereas, variables outside functions in the main script can be seen inside functions. The former are said to have local scope and the latter global scope. This observation excludes function arguments which reference variables outside the function and return results.

This observation raises a question: Is there any way to force a variable inside a function to be seen everywhere else in the script? The answer is yes, and this script illustrates how:

```
 def func(x):
    global a
    a = 4.
    b = -0.32
    return a*x**b

print(a)
print(func(12.3))
```

with the output display

```
 1.7918033972156524
4.0
```

The use of the `global` declaration expands the scope of a variable so that it can be seen everywhere – it then has global scope.

## Problems

1.  **4.1** Write a Python script for the flowchart depicted in [Figure P4.1](#ch04.xhtml_fP4_1).![](images/Fig04P_01.jpg)

    **[FIGURE P4.1](#ch04.xhtml_fP4_1b)** Flowchart.

2.  **4.2** Consider a vertical, cylindrical bin with conical base partially filled with grain. Refer to [Figure P4.2](#ch04.xhtml_fP4_2). Develop and test a Python function named `binvol` that has arguments of the bin cylindrical radius, `r`, the heights of the cylindrical, `hcyl`, and conical, `hcon`, sections, and the overall depth of the grain in the bin, `h`. The function should return the volume of grain, `gvol`. It should also check that the grain depth is feasible—not greater than the sum of the conical and cylindrical heights.![](images/Fig04P_02.jpg)

    **[FIGURE P4.2](#ch04.xhtml_fP4_2b)** Grain bin.

3.  **4.3** Approximate models for the variation of temperature and pressure versus altitude in the Earth’s atmosphere are available.[⁵](#ch04.xhtml_n4_5) They provide formulas for three atmospheric layers: the troposphere, lower stratosphere, and upper stratosphere.

    troposphere (*h* <  11,000):

    $\begin{matrix} {T = 15.04 - 0.00649h} & {P = 101.29\left( \frac{T + 273.15}{288.08} \right)^{5.256}} \end{matrix}$

    lower stratosphere (11,000 <  *h* <  25,000):

    $\begin{matrix} {T = - 56.46} & {P = 22.65e^{1.73 - 0.000157h}} \end{matrix}$

    upper stratosphere (25,000 <  *h*):

    $\begin{matrix} {T = - 131.21 + 0.00299h} & {P = 2.488} \end{matrix}\left( \frac{T + 273.15}{216.6} \right)^{- 11.388}$

    In the formulas above, the specific units required are

    *h*: meters (m) *T*: °C *P*: kilopascals (kPa)

    and the density of air is related to temperature and pressure by

    $\begin{matrix} {\rho = \frac{P}{0.2869(T + 273.15)}} & \rho \end{matrix}:\text{kg/m}^{3}$

    1.  Develop a Python function, `atm`, that has a single argument, `h`, and returns the temperature, `T`, pressure, `P`, and density, `rho`. Test this function for different `h` values.
    2.  Use your function from to produce a plot of density versus altitude from 0 to 25,000 m. Altitude should be the vertical axis.
4.  **4.4** Scientists and engineers frequently must extract numerical information from tables of data. For example, it is well known that the density of water, *ρ* (kg/m³), changes with temperature, *T* ( °C). This relationship can be represented by the data in [Table P4.4](#ch04.xhtml_tP4_4). Develop and test a Python function, `H2Oden`, with a single argument of temperature, `T`, that returns an estimate of the density, `rho`, using the method of *linear interpolation*. For this method, the function finds the pair of table entries that bracket the input temperature, denoted 1 and 2, and then uses a straight line to estimate the corresponding density, as in

    [**TABLE P4.4**](#ch04.xhtml_tP4_4b) Density of Water versus Temperature

    | ***T*** | *ρ* | ***T*** | *ρ* | ***T*** | *ρ* | ***T*** | *ρ* |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | (°C) | (kg/m³) | (°C) | (kg/m³) | (°C) | (kg/m³) | (°C) | (kg/m³) |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | 0 | 999.87 | 20 | 998.23 | 50 | 988.07 | 80 | 971.83 |
    | 2 | 999.97 | 25 | 997.08 | 55 | 985.73 | 85 | 968.65 |
    | 4 | 1,000.00 | 30 | 995.68 | 60 | 983.24 | 90 | 965.34 |
    | 6 | 999.97 | 35 | 994.06 | 65 | 980.59 | 95 | 961.92 |
    | 10 | 999.73 | 40 | 992.25 | 70 | 977.81 | 100 | 958.38 |
    | 15 | 999.13 | 45 | 990.25 | 75 | 974.89 |  |  |

    $\rho = \frac{T - T_{1}}{T_{2} - T_{1}}\left( \rho_{2} - \rho_{1} \right) + \rho_{1}$

5.  **4.5** What is wrong with the following Python code segment? Propose a corrected version.

    ```
     if x <= 0.:
        fval = -x
    else:
        if x < 1:
            fval = x**2
        else:
            fval = 1
    ```

6.  **4.6** The graph shown in [Figure P4.6](#ch04.xhtml_fP4_6) describes a functional relationship between an input variable, *x*, and an output variable, *y*. Electrical engineers might call this a linear function with saturation. Develop and test a Python function, `sat`, which accepts an input argument, `x`, and returns the `y` value.![](images/Fig04P_06.jpg)

    **[FIGURE P4.6](#ch04.xhtml_fP4_6b)** Saturation function.

7.  **4.7** An environmental scientist is developing a computer program to determine whether it is safe to introduce a weed herbicide into a lake. According to scientific studies, the chemical should only be applied when the water temperature is less than 30 °C, the dissolved oxygen concentration is above 6 mg/L, and the pH is between 6.8 and 8\. Develop a Python function, `weedtest`, with arguments temperature, `T`, dissolved oxygen concentration, `DO`, and `pH`, and returns a string, either `‘safe’` or `‘unsafe’`. Test your function for various input values.
8.  **4.8** Write and test a Python function, `findrx`, that has one argument, `x`, and returns `rx`. The value of `x` is required to be positive or zero, so the function should check for this and return an error message is `x` is negative. If the value of `x` is zero, the function simply returns a value of zero. For positive `x` values, the function implements the flowchart shown in [Figure P4.8](#ch04.xhtml_fP4_8). Test your function with various values of x. What calculation does your function perform?![](images/Fig04P_08.jpg)

    **[FIGURE P4.8](#ch04.xhtml_fP4_8b)** Flowchart with loop.

9.  **4.9** The famous *Fibonacci series* starts with the sequence 0 and 1\. Each subsequent number in the series is the sum of the two previous numbers. Applying that to the first two numbers, the series evolves with the numbers 0, 1, 1, 2, 3, 5, … Develop a Python function, `fibo`, that has an integer input argument, `n`. The function computes `n` terms of the Fibonacci series (n must be greater than 2) and returns the ratio of the second last term to the last term. Experiment with the function to see whether the ratio converges for larger values of `n`. Compare the ratio to the *Golden Ratio*, given by

    $\frac{\sqrt{5} - 1}{2}$

    As a supplement, do some reading on the Fibonacci series, its evidence in nature and its relationship to the Golden Ratio.

10.  **4.10** Develop a Python function, `sumn`, that has an integer input argument, `n`, and returns the sum of the integers from 1 to `n`. Test your function and compare the result to the shortcut formula

    $\frac{n(n + 1)}{2}$

11.  **4.11** The American Association of State Highway and Transportation Officials provides the criteria in [Table P4.11](#ch04.xhtml_tP4_11) for classifying soils in accordance with their suitability for use in highway subgrades and embankment construction. Develop a Python function, `soilclass`, that has average grain size, `gsize`, as an input argument and returns the classification.

    [**TABLE P4.11**](#ch04.xhtml_tP4_11b) Soil Classification

    | Grain Size mm | Classification |
    | --- | --- |
    | Size > 75 | Boulders |
    | 2 < size ≤75 | Gravel |
    | 0.05 < size ≤2 | Sand |
    | 0.002 < size ≤0.05 | Silt |
    | Size ≤ 0.002 | Clay |

12.  **4.12** Write a Python code segment to implement the flowchart shown in [Figure P4.12](#ch04.xhtml_fP4_12).![](images/Fig04P_12.jpg)

    **[FIGURE P4.12](#ch04.xhtml_fP4_12b)** Flowchart with embedded structure.

13.  **4.13** The ideal gas law is widely used to predict the pressure, temperature, or volume of a gas at conditions that are not extreme, especially not inordinately high pressure. It can be expressed as

    $P\overset{\hat{}}{V} = RT$

    where *P*: pressure, $\overset{\hat{}}{V}$: specific volume, *R*: the gas law constant and *T*: the absolute temperature. For typical SI units, *P* [ =] kPa, $\overset{\hat{}}{V}$ [=] m³/kmol, *T* [=] K, and the value of *R* is approximately 8.3145 kPa·m³/[kmol·K]Develop a user-defined Python function called `idealgas` that has input arguments of *P*, $\overset{\hat{}}{V}$ and *T*. Use keyword arguments. When invoked, only two of the three arguments are provided, and the function returns the third. Test your function for various scenarios.

14.  **4.14** As temperature increases, solid materials expand. This expansion can be quantified by a coefficient with the formula

    *Δ**L* = *α**Δ**T**L*

    where Δ*L* is the change in length, *α* is the linear expansion coefficient, Δ*T* is the change in temperature and *L* is the length of the material at the base temperature, *T*.

    The table below lists the expansion coefficients for several common materials.

    | Material | Expansion Coefficient × 10⁶ m/[m·°C] |
    | --- | --- |
    | Copper | 16 |
    | Aluminium | 22.5 |
    | Glass | 5.9 |
    | Steel | 11.5 |
    | Polyethylene | 125 |

    Create a Python function called `linexp` that has input arguments of material type (text string), temperature change, and base length. The function should return the expanded length. Test your function with various examples.

15.  **4.15** In the U.S., vehicle fuel economy is typically reported in units of miles per gallon (mpg); whereas, in Europe, the quantity used is L/100 km traveled (L/100 km). Create a `lambda` function that converts mpg to L/100 km. If a good value for fuel economy in the U.S. is 40 mpg, use your function to compute the value in L/100 km.
16.  **4.16** At some point, you may have the adventure of purchasing a new or used vehicle (perhaps you have experienced this treat already). It is usually necessary to finance part of the purchase with a loan. Key parameters associated with the loan are its amount or principal, *P*, the interest rate, *i*, the term of length of the loan (*n*  =  number of monthly payments), and the constant monthly payment, *A*. These are related by the formula

    $A = P\frac{{i(1 + i)}^{n}}{(1 + i)^{n} - 1}$

    If the interest rate is given in annual terms, and the payments are monthly, the interest rate divided by 12 must be used in the formula.

    Develop a Python function called `loanpmt` with the arguments of loan amount, annual interest rate, and number of years of the loan period. The function should return the monthly payment.

    Imagine that you can afford a monthly payment of $400, and you can obtain a loan term of 6 years at 4.8% annual interest rate. If a 20% down payment is required to qualify for the loan, experiment with your function to determine the maximum purchase price you can afford.

17.  **4.17** Ohm’s Law describes the relationship of electrical current, *I*, and voltage, *V*, for a resistance, *R*. Standard units are amperes (*A*), volts (*V*) and ohms ( Ω), and the Ohm’s Law formula is

    *V* = *I* ⋅ *R*

    Develop a Python function called `ohmslaw` with three keyword arguments, `I`, `V`, and `R`. When the function is invoked, two of these three are supplied and the function computes and returns the third. Test your function with several examples.

# 5 Graphics—Matplotlib

DOI: [10.1201/9781003256861-5](https://doi.org/10.1201/9781003256861-5)

## Chapter Objectives

*   Learn about the Matplotlib module and its `pyplot` submodule.
*   Be able to create scatter and line plots using `pyplot`.
*   Customize plot axes including the addition of a right-side axis.
*   Learn how to create subplots for multiple plots in a figure object.
*   Create and customize bar graphs with more flexibility than with `pylab`.
*   Explore creating other plots, such as polar plots, stem plots, and pie charts.
*   Learn how to create plots with logarithmic axis scales.
*   Be able to create contour and surface plots to depict two-dimensional data and functions.

In [Chapter 3](#ch03.xhtml_c3), you learned how to use the `pylab` module to create various plots. That module provides a convenient interface for many graphics applications but lacks the flexibility and capabilities provided by the more comprehensive Matplotlib module. The purpose of this chapter is to expand your ability to create plots that are common and useful in engineering and science.

## 5.1 Introduction to Matplotlib

The *Matplotlib module* provides extensive graphics capabilities for use with Python. A comprehensive coverage of Matplotlib is not feasible in this chapter. The Matplotlib User’s Guide will help you expand your knowledge.[¹](#ch05.xhtml_n5_1) Here, we focus on Matplotlib’s `pyplot` submodule and its features most useful for engineering and science.

The typical command line we use to access `pyplot` is

```
 import matplotlib.pyplot as plt
```

using the `plt` abbreviation to save keystrokes later in the script. This is just like using `np` for the NumPy module. Many of the simpler plots are generated in a similar fashion to `pylab`. We will illustrate this with some examples.

Plotting an analytical function is a common task. Consider generating a plot of the curve of the function

*f*(*x*) = cos (*x*)cosh (*x*) − 10 ≤ *x* ≤ 5(5.1)

Here is the Python code to produce the plot shown in [Figure 5.1](#ch05.xhtml_f5_1).

![](images/Fig05_01.jpg)

**[FIGURE 5.1](#ch05.xhtml_f5_1b)** A simple line plot of an analytical function.

```
 import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,5)
f = lambda x: np.cos(x)*np.cosh(x)-1
plt.plot(x, f(x))
plt.show()
```

The code for [Figure 5.1](#ch05.xhtml_f5_1) makes use of the `plot` function in `pyplot`. Also, the NumPy module is included to utilize the `linspace`, `cos`, and `cosh` functions. Since our function is simple, we use a `lambda` definition. Although not visible to you, the curve on the figure is blue. The `linspace` function provides 50 points by default, and these are enough to depict most continuous curves well. We already see opportunities to improve the plot and will get to them later.

Next, we see how to create simple plots of discrete data sets. Individual data are typically plotted as markers, unless there are a large number which would clutter the plot unnecessarily. In the latter case, the data are often connected with straight lines and without markers. We will illustrate both cases here.

To this point, we have generated three typical plots with the Matplotlib’s `pyplot` module. There are many combinations and enhancements that now must be considered. The next section addresses these needs.

## 5.2 Customizing Line and Scatter Plots

There are numerous features we would like to add to simple plots to improve their appearance, readability, and complexity. Here is list:

*   adding gridlines, axis titles, and a plot title,
*   customizing the properties of lines and markers, including colors,
*   combining markers and lines in plotting a data set,
*   plotting more than one series and adding a legend,
*   adjusting axis limits, and
*   adding an axis on the right of a plot with an appropriate legend.

Later we will consider creating multiple plots on a single figure object and other types of plots used by engineers and scientists.

Let’s return to the simple plot illustrated in [Figure 5.1](#ch05.xhtml_f5_1) and add code to provide grid lines, and axis and plot titles. The result is shown in [Figure 5.4](#ch05.xhtml_f5_4).

![](images/Fig05_04.jpg)

**[FIGURE 5.4](#ch05.xhtml_f5_4b)** Line plot with grid and titles.

```
 import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,5)
f = lambda x: np.cos(x)*np.cosh(x)-1
plt.plot(x, f(x))
plt.grid()
plt.xlabel('x')
plt.ylabel('f(x)')
plt.title('Plot of cos(x)*cosh(x) -1')
plt.show()
```

These additions are identical to the statements we used in [Chapter 3](#ch03.xhtml_c3) with the simpler `pylab` module. Most engineers and scientists like to have grids on their plots because they help reading the plot and avoiding *parallax errors*. Of course, good axis titles and a plot title help provide an accurate description of the plot.

Employing color and different styles of lines are useful for making your plots more attractive and readable. For plots that will be rendered in black-and-white documents, we might change the color of the line from the default blue to black. This involves specifying a color choice as part of the plot command. The color choices, shown here in [Table 5.2](#ch05.xhtml_t5_2), are the same as those presented in [Chapter 3](#ch03.xhtml_c3) as [Table 3.7](#ch03.xhtml_t3_7).

[**TABLE 5.2**](#ch05.xhtml_t5_2b) Color Codes

| Character | Color |
| --- | --- |
|  
```
k
```

 | Black |
|  
```
b
```

 | Blue |
|  
```
g
```

 | Green |
|  
```
r
```

 | Red |
|  
```
c
```

 | Cyan |
|  
```
m
```

 | Magenta |
|  
```
y
```

 | Yellow |
|  
```
w
```

 | White |

```
 plt.plot(x, f(x), color = 'k')
```

*Note*: You can use the shorthand notation `c` for `color`. We do not show the result here as it is the same as [Figure 5.4](#ch05.xhtml_f5_4), just with the line color now black.

In certain situations, we may want to employ a different style of line, such as a dashed line. This occurs most often used to distinguish one plotted curve from another. We can achieve this by adding a `linestyle` specification to the `plot` command. [Table 5.3](#ch05.xhtml_t5_3) presents the choices for `linestyle`.

[**TABLE 5.3**](#ch05.xhtml_t5_3b) Linestyle Choices and Codes

| Character | Style |
| --- | --- |
| - | Solid |
| -- | Dashed |
| : | Dotted |
| -. | Dash-dot |

For example, we can change the solid line to a dashed line with

```
 plt.plot(x, f(x), color='k', linestyle='--')
```

[Figure 5.5](#ch05.xhtml_f5_5) shows this version of the plot. *Note*: You can use the shorthand notation `ls` for `linestyle`.

![](images/Fig05_05.jpg)

**[FIGURE 5.5](#ch05.xhtml_f5_5b)** Plot with black curve and dashed line.

Before we move on to customizing markers, we can consider how to change the width or “weight” of the line. We do this by adding the `linewidth` (or `lw`) specification to the plot command. For example,

```
 plt.plot(x, f(x), color='k', linestyle='--', linewidth=2.5)
```

and you will get used to a shortened version of this statement:

```
 plt.plot(x, f(x), c='k', ls='--', lw=2.5)
```

The default linewidth is 1.5, and you can experiment with different values to find the one that works for your plot.

Now, on to marker options. We can specify *marker color* in the same way we did for lines, using the `color` (or `c`) specification in the `scatter` command. We may be interested in changing the marker style, and these are presented in [Table 5.4](#ch05.xhtml_t5_4).

[**TABLE 5.4**](#ch05.xhtml_t5_4b) Marker Codes

| Character | Symbol | Description |
| --- | --- | --- |
| . | • | Point |
| o | ○ | Circle |
| `+` | + | Plus sign |
| `x` | × |  |
| `D` | ◊ | Diamond |
| `v` | ∇ | Del |
| `^` | ∆ | Triangle |
| `s` | □ | Square |

In our glycol freezing point plot (), we might want to change the markers to black ×’s. Along the way, we can also add a grid and titles. Here is the modified Python code to implement these modifications. The resulting plot is shown in [Figure 5.6](#ch05.xhtml_f5_6).

![](images/Fig05_06.jpg)

**[FIGURE 5.6](#ch05.xhtml_f5_6b)** Freezing point plot with black “×” markers, grid, and titles.

```
 import matplotlib.pyplot as plt

PG = [0., 10., 20., 30., 40., 50., 60., 80., 90., 100.]
FP = [0., -3.4, -7.9, -13.7, -23.5, -36.8, -52.8, -46.,
-30., -12.8]

plt.scatter(PG, FP, marker='x', c='k')
plt.grid()
plt.xlabel('Glycol - % by volume')
plt.ylabel('Freezing Point - degC')
plt.title('Freezing Point of Glycol Aqueous Solutions')
plt.show()
```

For the marker styles that have edges, e.g. circle, diamond, square, it is possible to customize the edges and the interior of the marker. This is accomplished by using the `edgecolors` specification and the `color` specification for the interior. Here is an example:

```
 plt.scatter(PG, FP, marker='s', c='w', edgecolors='k')
```

[Figure 5.7](#ch05.xhtml_f5_7) shows the result.

![](images/Fig05_07.jpg)

**[FIGURE 5.7](#ch05.xhtml_f5_7b)** Freezing point plot with square markers, black edges, and white interiors.

The last enhancement we will consider for a scatter plot is to connect adjacent markers with lines. This is accomplished by adding marker specification(s) to the `plot` command, not by using the `scatter` command. We add lines to [Figure 5.7](#ch05.xhtml_f5_7) by replacing the `scatter` command with

```
 plt.plot(PG, FP, c='k', marker='s', markeredgecolor='k' \
, markerfacecolor='w')
```

with the result shown in [Figure 5.8](#ch05.xhtml_f5_8). Notice that we used the `markeredgecolor` (or `mec`) and `markerfacecolor` (or `mfc`) here to distinguish them from the `color` (or c) specification for the line.

![](images/Fig05_08.jpg)

**[FIGURE 5.8](#ch05.xhtml_f5_8b)** Freezing point plot with lines connecting markers.

We often use lines connecting markers to reveal patterns in the data. This only becomes limiting when we have hundreds of data points, and the markers clutter the plot too much. Next, we move to depicting more than one data series on the same plot.

Beyond what we’ve shown so far, there are many, many other specifications available for the `plot` command. It is useful to reference these in the *Matplotlib documentation* available from [https://matplotlib.org/stable/users/index.html](https://matplotlib.org/).

The plotted weather data presented in [Figure 5.14](#ch05.xhtml_f5_14) may not be satisfactory to some viewers because of the overlay of the two curves. This might be addressed by using different colors for the curves if color is acceptable as a feature. Another approach is to use separate plots stacked vertically. We will consider that in the next section.

## 5.3 Using Figure Window Objects

The use of figure objects provides additional flexibility in the creation of plots using Matplotlib and `pyplot`. We can create multiple plot objects within a script, and we can include multiple plots in a single figure.

One scenario where multiple plots are desired is where we want a plot of two functions versus an independent variable, and then we also need a *phase plot* where the two function values are plotted against each other with the independent variable as a running parameter. This is accomplished with the repeated use of `figure` command, as shown in the script below.

```
 import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,np.pi, 100)
fun1 = lambda x: np.sin(x)
fun2 = lambda x: np.cos(x)

plt.figure()
plt.plot(x, fun1(x), c='k', label='sin(x)')
plt.plot(x, fun2(x), c='k', ls='--', label='cos(x)')
plt.grid()
plt.xlabel('x')
plt.ylabel('sin(x) and cos(x)')
plt.title('trig functions')
plt.legend()
plt.show()

plt.figure()
plt.plot(fun1(x), fun2(x), c='k')
plt.grid()
plt.xlabel('sin(x)')
plt.ylabel('cos(x)')
plt.title('cos(x) vs sin(x) for x = 0 to pi')
```

The two figures created are shown side-by-side in [Figure 5.15](#ch05.xhtml_f5_15). These are independent plot figures and can be arranged in documentation as preferred. You can see that creating multiple plots is simple—just use the `figure` command prior to each.

![](images/Fig05_15.jpg)

**[FIGURE 5.15](#ch05.xhtml_f5_15b)** Two figures to plot sin(*x*) and cos(*x*).

If we would like to create an array of plots within a single figure, this requires the use of axes objects and the specification of the array—how many plots in each row and how many rows. Let’s first apply this method to the previous two trigonometric function plots. In the script below, we create a `figure` object, `fig`, and then add axes objects, `ax1` and `ax2`, using the `add_subplot` method. The specified arrangement, `121` or `122`, is 1 row and 2 columns with the last digit indicating which subplot in the figure, counting across rows. Then, instead of using `plt` for the plot and other commands, we use the axes objects. Also, note that previous commands, like `xlabel`, are now `set_xlabel`. The plot arrangement is shown in [Figure 5.16](#ch05.xhtml_f5_16).

![](images/Fig05_16.jpg)

**[FIGURE 5.16](#ch05.xhtml_f5_16b)** Side-by-side plots of trigonometric functions in a single figure.

```
 import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,np.pi, 100)
fun1 = lambda x: np.sin(x)
fun2 = lambda x: np.cos(x)

fig = plt.figure()
ax1 = fig.add_subplot(121)
ax1.plot(x, fun1(x), c='k', label='sin(x)')
ax1.plot(x, fun2(x), c='k', ls='--', label='cos(x)')
ax1.grid()
ax1.set_xlabel('x')
ax1.set_ylabel('sin(x) and cos(x)')
ax1.set_title('trig functions')

ax1.legend()

ax2 = fig.add_subplot(122)
ax2.plot(fun1(x), fun2(x), c='k')
ax2.grid()
ax2.set_xlabel('sin(x)')
ax2.set_ylabel('cos(x)')
ax2.set_title('cos(x) vs sin(x) for x = 0 to pi')

plt.show()
```

A “cosmetic” problem is immediately apparent in [Figure 5.16](#ch05.xhtml_f5_16). The two plots crowd and overlap each other. There are two remedies available for this common phenomenon. The first is to add space between the plots with the `wspace` specification. The neater arrangement is shown in [Figure 5.17](#ch05.xhtml_f5_17).

![](images/Fig05_17.jpg)

**[FIGURE 5.17](#ch05.xhtml_f5_17b)** Side-by-side plots with space added between.

```
 fig.subplots_adjust(wspace=0.5)
plt.show()
```

Perhaps, we don’t like that the two plots in [Figure 5.17](#ch05.xhtml_f5_17) are compressed somewhat horizontally. This can be addressed by changing the aspect ratio (width, height) of the figure window by modifying the `figure` statement as

```
 fig = plt.figure(figsize=(8,3))
```

The result is more pleasing and is shown in [Figure 5.18](#ch05.xhtml_f5_18). The same `wspace` specification is used here. *Note*: To adjust spacing between rows of plots, you can use the `hspace` specification.

![](images/Fig05_18.jpg)

**[FIGURE 5.18](#ch05.xhtml_f5_18b)** Side-by-side plots with aspect ratio changed.

## 5.4 Creating Bar Plots Including Histograms

Engineers and scientists encounter the need to display information in bar charts frequently. Matplotlib `pyplot` provides a flexible capability to produce these, more so that its `pylab` submodule. One of the common applications is the histogram, so we will consider that first, then generalize to other uses.

*Histogram charts* are used to describe the variability in measurements of the same quantity. For example, we could consider repeated dimensional measurements on many samples of the same manufactured part. [Table 5.6](#ch05.xhtml_t5_6) presents inside diameter measurements for engine piston rings (Montgomery, 2013).

[**TABLE 5.6**](#ch05.xhtml_t5_6b) Engine Piston Ring Inside Diameter Measurements, mm

| 74.030 | 73.995 | 73.988 | 74.002 | 73.992 | 74.009 | 73.995 | 73.985 | 74.008 | 73.998 |
| 73.994 | 74.004 | 73.983 | 74.006 | 73.984 | 74.000 | 73.994 | 74.006 | 73.984 | 74.000 |
| 73.982 | 74.004 | 74.010 | 74.015 | 73.982 | 74.012 | 73.995 | 73.987 | 74.008 | 74.003 |
| 73.994 | 74.008 | 74.001 | 74.015 | 74.030 | 74.001 | 74.015 | 74.035 | 74.017 | 74.010 |

The basis of the histogram is to devise a set of measurement intervals and count the number of measurements in each interval. For the 40 measurements in the table, four-to-six intervals would be recommended. Here are some sample statistics for the data:

| Number | 40 |
| Average | 74.002 |
| Minimum | 73.982 |
| Maximum | 74.035 |

We propose intervals based on approximately one-sixth of the range (maximum – minimum). Here are the “edges” of the intervals chosen.

| 73.980 |
| 73.990 |
| 74.000 |
| 74.010 |
| 74.020 |
| 74.030 |
| 74.040 |

The NumPy module has a `histogram` function that provides the count data. The Python script below illustrates this.

```
 import numpy as np

diam = np.loadtxt('PistonData.txt')
hist, bin_edges = np.histogram(diam,
bins=6,range=[73.98,74.04])
print(bin_edges)
print(hist)
```

with the results displayed in the Console as[³](#ch05.xhtml_n5_3)

```
 [73.98 73.99 74\. 74.01 74.02 74.03 74.04]
[ 8 8 14 7 0 3]
```

Next, we add the code to create a bar chart using the count data computed by `hist`. The chart is presented in [Figure 5.19](#ch05.xhtml_f5_19). The first set of statements creates an array of the center points of the bars to be displayed. In the `bar` command, the `hist` values provide the heights of the bars, and there are additional specifications for the width of the bars (equal to the bin widths, so the bars are touching), the interior color, and edge color of the bars.

![](images/Fig05_19.jpg)

**[FIGURE 5.19](#ch05.xhtml_f5_19b)** Histogram chart of piston data.

```
 bin_width = bin_edges[1]-bin_edges[0]
n = len(hist)
bin_centers = np.zeros((n))
for i in range(n):
    bin_centers[i] = (bin_edges[i]+bin_edges[i+1])/2

import matplotlib.pyplot as plt
plt.bar(bin_centers, hist, width=bin_width, color='w', \
    edgecolor='k')
plt.xlabel('Piston Inside Diameter - mm')
plt.ylabel('Frequency')
plt.title('Histogram Chart of Piston Data')
```

The chart shows the most frequent measurements in the interval 74.00–74.01\. The rest of the measurements are not distributed symmetrically about that interval, and there appear to be just two parts with unusually high measurements.

We can customize the plot by changing the color scheme. We could narrow the bars by replacing `width`=`bin_width` with `width`=`0.7`*`bin_width`. There are other options to be found in the Matplotlib manual on the Spyder help menu.

A more general bar plot is the *categorical chart*. Here is an example to illustrate this chart.

## 5.5 Creating Other Plots of Interest

A *polar plot* is based on using *polar coordinates* where the axes are angle and magnitude. When we have a function based on trigonometric functions, it may be more convenient to plot on polar coordinates. Here is an example, using the function and angle range:

*f*(*θ*) = sin (*θ*) ⋅ cos (*θ*)0 ≤ *θ* ≤ *π*(5.2)

The following Python code creates the polar plot displayed in [Figure 5.21](#ch05.xhtml_f5_21). You will note the use of the `pad` specification in the `title` command. This provides more space between the plot and the title; otherwise, they overlap. You will also note that the scale on the radial distance includes negative values. These are just values that the function produces when the sign of the cosine function is negative between *π*/2 and *π*. You can see in the plot that the values are negative in this range.

![](images/Fig05_21.jpg)

**[FIGURE 5.21](#ch05.xhtml_f5_21b)** Polar plot of sin(*x*)⋅cos(*x*).

```
 import numpy as np
import matplotlib.pyplot as plt

theta = np.linspace(0., np.pi, 100)

f = lambda th: np.sin(th)*np.cos(th)
plt.polar(theta, f(theta), c='k')
plt.title('Polar Plot of sin(x)*cos(x)', pad=15)
plt.show()
```

A style of plot that some prefer to use in certain situations is the *stem plot*. It uses markers and connects a vertical line or “stem” from the abscissa to each marker. Here is an example based on a function we used at the beginning of this chapter, Equation 5.1\. The plot is shown in [Figure 5.22](#ch05.xhtml_f5_22).

![](images/Fig05_22.jpg)

**[FIGURE 5.22](#ch05.xhtml_f5_22b)** Stem plot of cos(*x*)⋅cosh(*x*) − 1.

```
 import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,5,20)
f = lambda x: np.cos(x)*np.cosh(x)-1
plt.stem(x, f(x), linefmt='k-', markerfmt='ks', basefmt='k-' \
, use_line_collection=True)

plt.grid()
plt.xlabel('x')
plt.ylabel('cos(x)*cosh(x)-1')
plt.title('Example Stem Plot')
plt.show()
```

In the `stem` command, the specifications are vertical lines as solid black (`k`-) and the markers as black squares (`ks`). The baseline is also solid black. To follow the latest version of Matplotlib, we set the `use_line_collection` specification to `True`.

There are occasions where we want to use logarithmic axes, either *x* or *y* or both. This usually arises when the range of values covers several decades of magnitude, and the behavior of the plot in each decade is of interest.

If the situation calls for it, a logarithmic scale can be employed for the *x* axis using the `semilogx` command, and, on other occasions, log scales are needed for both axes and you will use the `loglog` command.

Another type of plot that is used frequently in presentations is the pie chart. Matplotlib `pyplot` provides a `pie` function to create *pie charts*. We illustrate that here with an example.

## 5.6 Contour and Surface Plots

We are all familiar with looking at and reading maps. Essentially, we extract information that is superimposed on two dimensions. Less frequently, continuous information is present on a map. The best example is the *topographic map*, an example shown in [Figure 5.26](#ch05.xhtml_f5_26). The contours on the map, called *isobars* for constant pressure curves, represent elevations. Hikers know well how to interpret these maps in terms of slopes and directions.

![](images/Fig05_26.jpg)

**[FIGURE 5.26](#ch05.xhtml_f5_26b)** Example topographic map. (With permission from [https://blog-assets.thedyrt.com/uploads/2019/06/shutterstock_75803032-1.jpg](https://blog-assets.thedyrt.com).)

In science and engineering, we encounter situations where there is a quantity we need to study that is described in terms of more than one variable. When it is two variables, a *contour plot* is a possibility. We can also consider a three-dimensional representation that is created on a two-dimensional surface. There are two types of these contour and surface plots that are of interest. The first is based on an array of discrete data, often measurements, and the second is taken from a mathematical function. We will use the latter here to illustrate how to create contour and surface plots with Python and Matplotlib.

Consider the following function of two independent variables, *x* and *y*,

*f*(*x*, *y*) = 89 + 0.04*x* − 0.16*y* − 8.09*x*² − 5.78*y*² − 5.89*x**y*(5.6)

over the domain −2 ≤ *x* ≤ 2  ,   − 2 ≤ *y* ≤ 2. The following Python script creates the contour plot illustrated in [Figure 5.27](#ch05.xhtml_f5_27).

![](images/Fig05_27.jpg)

**[FIGURE 5.27](#ch05.xhtml_f5_27b)** Simple contour plot.

```
 import numpy as np
import matplotlib.pyplot as plt

def f(x, y):
    return 89.+0.04*x-0.16*y-8.09*x**2-5.78*y**2-5.89*x*y

x = np.linspace(-2., 2.)
y = np.linspace(-2., 2.)
X, Y = np.meshgrid(x, y)
Z = f(X, Y)
plt.figure()
contplt = plt.contour(X, Y, Z, [80., 85., 88., 92., 95.],
colors='k')
plt.grid()
plt.clabel(contplt)
plt.xlabel('x')
plt.ylabel('y')
```

The first feature to notice in the code is the use of the `meshgrid` function. This function takes two arrays of *x* and *y* values respectively and creates two-dimensional arrays, `X` and `Y`, that are essentially a map of locations; that is, coordinates of the grid. The figure below illustrates this with a 4-by-4 array. The first digit in each pair represents the `X` array and the second the `Y` array.

![](images/unTab05_01.jpg)

A two-dimensional `Z` array is computed using the `f` function with the `X` and `Y` arrays as arguments. This is an *array operation* where the function is applied to each pair of `x` and `y` values. The `contour` function from Matplotlib is used, assigning the result to the `contplt` object variable. This is done so that the contour label function, `clabel`, can be applied to that object.

The plot in [Figure 5.26](#ch05.xhtml_f5_26) is useful because values of the function can be interpolated and read given the labeled contours. Another way to use a contour plot is with colored, filled contours which provide a “feel” for the function but do not allow reading of values easily. The following modified portion of the script accomplishes this, and the contour plot is shown in [Figure 5.28](#ch05.xhtml_f5_28). The `contourf` function fills the contours with the specified colors (although the different colors may not be visible here), and the labeling of the contours is removed.

![](images/Fig05_28.jpg)

**[FIGURE 5.28](#ch05.xhtml_f5_28b)** Filled contour plot.

```
 plt.figure()
plt.contourf(X, Y, Z, [80., 85., 88., 92., 95.] \
              , colors=['b', 'g', 'c', 'm'])
plt.grid()
plt.xlabel('x')
plt.ylabel('y')
```

The relationship of a quantity to two independent variables can also be depicted by rendering a three-dimensional surface on a two-dimensional space. Just as with a filled-color contour plot, a surface plot provides a feel for the dependency of the quantity on the input variables. There are two styles of surface plots provided by Matplotlib: mesh plots and solid, shaded surface plots. We will illustrate these with the analytical function used with contour plots earlier.

The Python script below is used to produce the *mesh plot* shown in [Figure 5.30](#ch05.xhtml_f5_30). First, you will notice that we have imported the `Axes3D` module. You may notice that the Spyder Editor provides a warning that this module is imported but not utilized. This warning is incorrect, so you can ignore it. Next, you see that we have created the plot as a subplot of an axes object, `ax1`, in a figure object, `fig`. The `plot_wireframe` function is used to generate the plot, and the “stride” specifications define the number of mesh contours. Following that and the `grid` statement, the tick intervals on the three axes are set, and plot labels are provided.

![](images/Fig05_30.jpg)

**[FIGURE 5.30](#ch05.xhtml_f5_30b)** Mesh plot of an analytical function, *f*(*x*, *y*).

```
 import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

def f(x, y):
return 89.+0.04*x-0.16*y-8.09*x**2-5.78*y**2-5.89*x*y

x = np.linspace(-2., 2.)
y = np.linspace(-2., 2.)
X, Y = np.meshgrid(x, y)
Z = f(X, Y)

fig = plt.figure()
ax1 = fig.add_subplot(111,projection='3d')
ax1.plot_wireframe(X, Y, Z, color='k', rstride=5,cstride=5)
ax1.grid()
ax1.set_xticks([-2., -1., 0., 1., 2.])
ax1.set_yticks([-2., -1., 0., 1., 2.])
ax1.set_zlim(0., 100.)
ax1.set_zticks(np.arange(0., 120., 20.))
plt.xlabel('x')
plt.ylabel('y')
plt.zlabel('f(x, y)')
```

There are additional commands that allow rotation of the viewpoint of the surface. For example,

```
 ax1.view_init(35)
```

rotates the viewpoint upward by 35°. More information is available from the Matplotlib User’s Guide ([https://matplotlib.org/stable/users/index.html](https://matplotlib.org/)).

An alternate presentation is to use a shaded surface instead of a mesh. The modifications to the Python script are to add the import of the `cm` module from Matplotlib and replace the `plot_wireframe` command with `plot_surface` as shown below.

```
 from matplotlib import cm
ax1.plot_surface(X, Y, Z, cmap=cm.gray)
```

[Figure 5.31](#ch05.xhtml_f5_31) shows the shaded surface plot. Of course, it is possible to use colors for the surface if that suits the mode of presentation of the plot.

![](images/Fig05_31.jpg)

**[FIGURE 5.31](#ch05.xhtml_f5_31b)** Surface plot of an analytical function, *f*(*x*, *y*).

We have barely opened the door when it comes to surface and mesh plots provided by Matplotlib. There are many examples available in the Matplotlib manual. We encourage you to experiment with these to develop the most effective presentations of multidimensional functions and data.

One question that arises is what to do when there are more than two independent variables that describe a quantity of interest. A typical approach is to pick a pair of independent variables and study them for specific values of the others. This is akin to providing pictures of “slices” of the multidimensional space to get a picture of paired relationships.

In this chapter, we have provided you with many examples of the typical plots that engineers and scientists use frequently in their Python programming and work. These are meant to give you a good start and basis for moving forward with your work. The problems that follow provide you with the opportunity to practice using most of these plot types.

## Problems

1.  **5.1** Develop a Python script using the Matplotlib `pyplot` module to produce a well-labeled line plot of the function

    *f*(*x*) = *x*²|sin (*x*)| − 4

    over the domain 0 ≤ *x* ≤ 4.

2.  **5.2** [Table P5.2](#ch05.xhtml_tP5_2) presents greenhouse gas emissions by the U.S. over the years 1990–2019\. Write Python scripts using Matplotlib `pyplot` to generate the following well-labeled plots:

    [**TABLE P5.2**](#ch05.xhtml_tP5_2b) Greenhouse Gas Emissions by the U.S. from 1990 to 2019 (MMT CO[2] Equivalent)

    |  | 1990 | 1991 | 1992 | 1993 | 1994 | 1995 | 1996 | 1997 | 1998 | 1999 |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | Carbon dioxide | 5113.5 | 5057.9 | 5167.5 | 5267.3 | 5358.8 | 5421.5 | 5610.6 | 5686.5 | 5731.0 | 5804.7 |
    | Methane | 776.9 | 781.8 | 780.5 | 770.7 | 777.0 | 767.7 | 760.8 | 746.8 | 731.7 | 713.4 |
    | Nitrous oxide | 452.7 | 443.2 | 443.1 | 471.3 | 457.0 | 468.8 | 480.8 | 466.8 | 467.7 | 457.5 |
    | Fluorinated gases | 99.7 | 90.7 | 95.3 | 95.0 | 99.0 | 117.9 | 129.0 | 136.4 | 152.9 | 149.9 |
    | Total | 6442.7 | 6373.6 | 6486.3 | 6604.3 | 6691.8 | 6775.9 | 6981.2 | 7036.5 | 7083.3 | 7125.4 |
    |  | **2000** | **2001** | **2002** | **2003** | **2004** | **2005** | **2006** | **2007** | **2008** | **2009** |
    | Carbon dioxide | 6010.5 | 5904.9 | 5946.8 | 6011.8 | 6114.0 | 6134.5 | 6051.7 | 6131.0 | 5914.1 | 5478.2 |
    | Methane | 707.6 | 699.8 | 692.8 | 692.7 | 687.0 | 686.1 | 690.8 | 693.9 | 700.8 | 689.7 |
    | Nitrous oxide | 444.7 | 460.4 | 458.8 | 459.8 | 469.9 | 455.8 | 452.5 | 463.5 | 446.9 | 445.6 |
    | Fluorinated gases | 150.9 | 137.9 | 145.9 | 137.0 | 144.6 | 146.6 | 149.5 | 161.2 | 162.8 | 158.5 |
    | Total | 7313.6 | 7203.0 | 7244.3 | 7301.4 | 7415.5 | 7423.0 | 7344.5 | 7449.6 | 7224.6 | 6772.0 |
    |  | **2010** | **2011** | **2012** | **2013** | **2014** | **2015** | **2016** | **2017** | **2018** | **2019** |
    | Carbon dioxide | 5675.8 | 5540.2 | 5338.7 | 5474.3 | 5522.8 | 5371.8 | 5248.0 | 5207.8 | 5375.5 | 5255.8 |
    | Methane | 692.1 | 666.2 | 658.2 | 654.4 | 651.0 | 651.5 | 642.4 | 648.4 | 655.9 | 659.7 |
    | Nitrous oxide | 455.0 | 445.6 | 416.8 | 463.9 | 474.0 | 468.2 | 450.8 | 446.3 | 459.2 | 457.1 |
    | Fluorinated gases | 168.2 | 175.5 | 172.3 | 172.1 | 177.1 | 179.6 | 179.1 | 180.9 | 180.8 | 185.7 |
    | Total | 6991.1 | 6827.4 | 6585.9 | 6764.7 | 6825.0 | 6671.1 | 6520.3 | 6483.3 | 6671.4 | 6558.3 |

    1.  a scatter plot of total emissions versus year, and
    2.  a line plot of carbon dioxide, methane and nitrous oxide emissions by year using twin axes. Employ different linestyles and a legend.

        [https://cfpub.epa.gov/ghgdata/inventoryexplorer/#allsectors/allsectors/allgas/gas/all](https://cfpub.epa.gov/)

3.  **5.3** In the production of sugar (sucrose, C[12]H[22]O[11]), the concentration of sucrose solutions is typically measured by refractive index (using an instrument called a *refractometer*). The data in [Table P5.3](#ch05.xhtml_tP5_3) present relevant measurements. A relationship between refractive index, *n*, and sucrose concentration, *pctS*, has been proposed as

    [**TABLE P5.3**](#ch05.xhtml_tP5_3b) Refractive Index of Sucrose Solutions

    | Per cent Sucrose | Refractive Index | Per cent Sucrose | Refractive Index | Per cent Sucrose | Refractive Index |
    | --- | --- | --- | --- | --- | --- |
    | 0 | 1.3330 | 30 | 1.3811 | 60 | 1.4418 |
    | 5 | 1.3403 | 35 | 1.3902 | 65 | 1.4532 |
    | 10 | 1.3479 | 40 | 1.3997 | 70 | 1.4651 |
    | 15 | 1.3557 | 45 | 1.4096 | 75 | 1.4774 |
    | 20 | 1.3639 | 50 | 1.4200 | 80 | 1.4901 |
    | 25 | 1.3723 | 55 | 1.4307 | 85 | 1.5033 |

    *n* = 1.32495 + 1.99515 × 10^(−3)*p**c**t**S*

    Create a Python script using the Matplotlib `pyplot` module that produces a plot of the sucrose concentration data using only markers and adds the model to the plot using lines. Label the plot and add a legend.

4.  **5.4** Create a two-by-two array of line plots in a `pyplot figure` window for the following hyperbolic functions over the domain -1 ≤ *x* ≤ 1.![](images/unTab05_02.jpg)
5.  **5.5** [Table P5.5](#ch05.xhtml_tP5_5) below presents the escape velocities from planets in the solar system. Employ the Matplotlib `pyplot` module in a Python script to create an ordered (Pareto style) horizontal bar chart to display these data.

    [**TABLE P5.5**](#ch05.xhtml_tP5_5b) Escape Velocity (km/h) for Planets in the Solar System

    |  | Escape Velocity (km/h) |
    | --- | --- |
    | Mercury | 1.302E+04 |
    | Venus | 3.747E+04 |
    | Earth | 4.027E+04 |
    | Mars | 1.831E+04 |
    | Jupiter | 2.145E+05 |
    | Saturn | 1.278E+05 |
    | Uranus | 7.666E+04 |
    | Neptune | 8.525E+04 |

6.  **5.6** [Example 5.5](#ch05.xhtml_exa5_5) presents data and illustrates a bar chart for wind power capacity by country. Create a similar plot based on data of solar capacity by country.
7.  **5.7** An analytical function that we used in this chapter for examples of line and stem plots is

    *f*(*x*) = sin (*x*)cosh (*x*) − 10 ≤ *x* ≤ 4

    Create a polar plot of this function over the given domain (radians) using a Python script and the Matplotlib `pyplot` module. Label the plot.

8.  **5.8** The data in [Table P5.8](#ch05.xhtml_tP5_8) were collected from a set of experiments involving a chemical reaction at different temperatures and catalyst concentrations. Using the `stem` function from Matplotlib `pyplot`, create a three-dimensional `stem` plot of these data. Access the Matplotlib Users Guide, if necessary.

    [**TABLE P5.8**](#ch05.xhtml_tP5_8b) Product Yield at Different Temperatures and Catalyst Concentrations

    | Catalyst Concentration (g/L) | Temperature (°C) | Product Yield (%) |
    | --- | --- | --- |
    | 0.54 | 110 | 83 |
    | 0.63 | 117 | 87 |
    | 0.71 | 113 | 84 |
    | 0.48 | 107 | 82 |
    | 0.57 | 118 | 92 |
    | 0.63 | 117 | 89 |
    | 0.59 | 102 | 78 |
    | 0.60 | 118 | 91 |

9.  **5.9** A rectangular wave is depicted in [Figure P5.9](#ch05.xhtml_fP5_9). This waveform can be broken down into an infinite series of sinusoidal components called a *Fourier series*.

    ![](images/Fig05P_09.jpg)

    **[FIGURE P5.9](#ch05.xhtml_fP5_9b)** Rectangular wave.

    $f(x) = \frac{4}{\pi}\cos(x) - \frac{4}{3\pi}\cos\left( {3x} \right) + \frac{4}{5\pi}\cos\left( {5x} \right) - \frac{4}{7\pi}\cos\left( {7x} \right) + \cdots$

    Write a Python script that produces a line plot for −*π* ≤ *x* ≤ *π* including curves of the first term above, the first two terms, the first three terms, and so on to the first five terms. Use colored curves and provide a legend on the plot.

10.  **5.10** A study has been conducted on the effect of water temperature and time in solution on the amount of dye absorbed by a type of fabric yarn. A standard amount of dye (200 mg) was added to a fixed amount of water. The three temperatures used in the experiments were 105°C, 120°C, and 135°C. The fabric was left in the water 15, 30, or 60 minutes. For each of these temperature-time combinations, the amount of dye absorbed by the yarn was measured. The experiments yielded the results shown in [Table P5.10](#ch05.xhtml_tP5_10).

    [**TABLE P5.10**](#ch05.xhtml_tP5_10b) Dye Absorption for Different Solution Times and Temperatures

    | Dye in Yarn (mg) | Time in Solution (min) | Temperature (°C) |
    | --- | --- | --- |
    | 120.4 | 15 | 105 |
    | 143.0 | 30 | 105 |
    | 190.6 | 60 | 105 |
    | 111.2 | 15 | 120 |
    | 134.8 | 30 | 120 |
    | 182.6 | 60 | 120 |
    | 98.4 | 15 | 135 |
    | 123.9 | 30 | 135 |
    | 173.2 | 60 | 135 |

    Create a meshplot of the dye absorbed versus time in solution and temperature.

11.  **5.11** Develop mesh and surface plots for the following model developed from experimental data of a response, *y*, for different values of two independent variables, *x*[1] and *x*[2].

    *y* = 60.64 − 3.672*x*[1] + 11.661*x*[2] − 3.514*x*[1]² − 0.924*x*[2]² + 2.220*x*[1]*x*[2]

    Determine a meaningful range for each of the independent variables to illustrate the function near its minimum and display this case as your final plot.

12.  **5.12** For the salt density data presented in [Table 5.9](#ch05.xhtml_t5_9), use the Matplotlib `pyplot` module to produce two line plots:
    1.  Salt density versus concentration with separate lines for temperatures 0°C, 25°C, 60°C, and 100°C.
    2.  Salt density versus temperature with separate lines for concentrations 1, 8, 16, and 26 wt%.

        For each plot, label the axes and include a title. Also, use different linestyles, black color, and provide a legend.

13.  **5.13** The Pareto chart from [Example 5.5](#ch05.xhtml_exa5_5) is often accompanied by a plot of the cumulative percentages of the total number of occurrences. Expand the Python code from [Example 5.5](#ch05.xhtml_exa5_5) to compute the cumulative % of total wind power capacity and develop a line plot of cumulative capacity versus country.

# 6 Array and Matrix Operations

DOI: [10.1201/9781003256861-6](https://doi.org/10.1201/9781003256861-6)

## Chapter Objectives

*   Be able to create arrays from numerical lists and tuples using the `ndarray` class with the NumPy module.
*   Learn how to create arrays of more than one dimension to represent matrices.
*   Be able to create special arrays, such as those filled with zeros, and combine and split arrays.
*   Learn how to implement subscripts as array indices, including the use of the colon (**:**) to reference ranges of indices.
*   Understand vectorization and learn how calculations can be vectorized using NumPy arrays.
*   Be able to write Python code to carry out matrix math operations, including addition, subtraction, scalar and matrix multiplication, and transpose.
*   Understand the meaning of the inverse of a square matrix and how this matrix can be used to solve a set of linear algebraic equations.
*   Become familiar with the NumPy `linalg` module and its `inv` function.

Computations made by engineers and scientists often involve individual numerical quantities and their variables. These have been the focus of previous chapters. Now, we consider collections of numbers. Although we can use the Python’s lists and tuples for storing such collections, we find that these are not useful structures when it comes to numerical calculations. This is where arrays created within the `ndarray` class of the NumPy module come into play. These arrays are the focus of this chapter.

What are typical computational tasks that involve arrays? Here are several examples:

*   storing and accessing tables of data, such as those that describe physical or chemical properties of substances, alloys, composites, or mixtures,
*   collections of measurements from experiments, manufacturing processes, or environmental phenomena,
*   discrete approximations of continuous quantities, such as temperatures throughout a solid object like a cooling fin,
*   case studies where input parameters are varied over a range of interest, and output results are computed and displayed in plots, and
*   physical or chemical variables that occur in staged processes, such as those used to separate desired products from waste or materials to be recycled.

To proceed, we need to know how to create arrays, either in one or two dimensions. Next, we must know how to include arrays in numerical calculations, often called array operations. Then, we move on to vector/matrix calculations including multiplication and transpose. Finally, we introduce the `linalg` module which contains many useful functions for array and matrix calculations.

A caution to the student. This chapter introduces many concepts and methods that are likely to be new to you. To make the presentation complete, we introduce alternate methods to accomplish certain computations. You will have the opportunity to select methods with which you are most comfortable, and your instructor may have preferences. Also, after the introduction provided in this chapter, you will see the methods repeated in subsequent chapters, and, in that way, you will be able to become better oriented to them. We have two suggestions as you study this chapter. First, work through everything carefully, replicating all the example code, and trying variations. Second, be patient and do not get too discouraged if you encounter difficulties.

## 6.1 Creating Arrays in Python

Python provides the list and tuple collection types for storing multiple items. The items can include numbers and text. It turns out that lists and tuples have limitations when it comes to numerical calculations that engineers and scientists frequently carry out. To meet these needs, the NumPy module provides the `ndarray` class that allows us to create numerical arrays.

First, let’s illustrate why the array collection is needed. What happens if we create a numeric list in Python and multiply that list by a constant value? Here is an example:

```
 list1 = [1.5, 3.2, -6.4, 0.9]
list2 = 2*list1
print(list2)

[1.5, 3.2, -6.4, 0.9, 1.5, 3.2, -6.4, 0.9]
```

You can see that multiplying the list by two just extended it by duplication. In numerical calculations, we would expect rather that each element of the list would be doubled, and the length of the list would be preserved.

If we try

```
 list3 = [0., 1., 4., -2.]
list4 = list1*list3
```

the result in the Console is

```
 TypeError: can't multiply sequence by non-int of type 'list'
```

In other words, you cannot do that. We might have expected the corresponding items in the two lists to be multiplied to yield a list of the same length. Not so.

So, the short answer to this dilemma is to convert the lists into arrays. This requires the NumPy module, and the code might look like

```
 a = np.array(list1)
b = 2*a
print(b)

c = np.array(list3)
d = a*c
print(d)
```

with the resulting output:

```
 [  3\.    6.4 -12.8   1.8]
[  0\.    3.2 -25.6  -1.8]
```

We see that the operations take place as we hoped. Multiplying the array `a` by two gives an array `b` with the values in `a` doubled. Multiplying the arrays `a` and `c` carries out item-by-item multiplication. These are called *array operations*.

The Variable Explorer provides information about the types of variables and their values ([Figure 6.1](#ch06.xhtml_f6_1)). You will notice that arrays are created for floating-point numbers, and their size is displayed with a comma. The arrays created are one-dimensional, sometimes called *vectors* or *vector arrays*.

![](images/Fig06_01.jpg)

**[FIGURE 6.1](#ch06.xhtml_f6_1b)** The Variable Explorer indicates the variable values and their types.

It is also common to have multidimensional arrays, usually two-dimensional, sometimes called *matrices*. Here is example code to create a two-dimensional array:

```
import numpy as np

A = np.array([[2., -3.], [6., 1.]])
print(A)

[[ 2\. -3.]
[ 6\. 1.]]
```

The resulting matrix has two rows and two columns. The rows are contained in the extra sets of brackets, [•]. Notice how each one-dimensional array is presented as a single row. If, instead, we use

```
b = np.array([[1], [2], [3], [4]])
print(b)

[[1]
 [2]
 [3]
 [4]]
```

The array `b` is displayed as a *column vector*.

We will mention here that Python and NumPy allow a special type of array, defined as a `matrix`. This type allows the creation of vectors and matrices with a style similar to the MATLAB^® software. We do not emphasize that in this text because we can accomplish the calculations using just the `array` type.

### 6.1.1 Creating Special Arrays

Python and NumPy provide functions to create special arrays and to combine or split up arrays. Here are examples of three functions that we use frequently.

The `zeros` function is the most common. It allows us to create a one- or two-dimensional array, filled will zeros. For example,

```
A = np.zeros((3,2))
print(A)

[[0\. 0.]
 [0\. 0.]
 [0\. 0.]]
```

We use this in Python code to create an array of a given size, filled initially with zeros, that we will modify later with other numbers.

The `ones` function is similar except filling the arrays with ones instead of zeros. Because the following example creates a two-dimensional array, notice that two sets of parentheses, ((•)) are used

```
B = np.ones((2,3))
print(B)

[[1\. 1\. 1.]
[1\. 1\. 1.]]
```

If we create a one-dimensional array of zeros or ones, only one set of parentheses is required, as in

```
d = np.zeros(5)
print(d)

[0\. 0\. 0\. 0\. 0.]
```

The `eye` function creates a square *identity* or “I” array. The single specification gives the number of rows and columns, both equal. For example,

```
C = np.eye(4)
print(C)

[[1\. 0\. 0\. 0.]
 [0\. 1\. 0\. 0.]
 [0\. 0\. 1\. 0.]
 [0\. 0\. 0\. 1.]]
```

### 6.1.2 Combining, Stacking, and Splitting Arrays

There are times that we want to combine arrays, either side-by-side or by stacking them, or split arrays into subarrays. Here are illustrations of the functions that accomplish this.

First, we define two 2 × 2 arrays.

```
import numpy as np

A = np.array([[3.6, 2.1], [-1.4, 0.7]])
B = np.array([[-12., 7.7], [2.1, -1.9]])
```

Next, we create a new 4 × 2 array by stacking A on top of B using the `vstack` function.

```
C = np.vstack((A, B))
print(C)

[[ 3.6 2.1]
[ -1.4 0.7]
[-12\. 7.7]
[ 2.1-1.9]]
```

Alternately, B can be placed to the right of A using the `hstack` function.

```
D = np.hstack((A, B))
print(D)

[[ 3.6 2.1–12\. 7.7]
[ -1.4 0.7        2.1-1.9]]
```

Going in the opposite direction, we can split an array into subarrays. Here are examples. First, the `vsplit` function with the argument 2 splits `C` vertically into two equal-size arrays.

```
 A1,B1 = np.vsplit(C, 2)
print(A1)
print('\n', B1)

[[ 3.6  2.1]
 [-1.4  0.7]]

 [[-12\.    7.7]
 [  2.1  -1.9]]
```

By using the `hsplit` function, we can separate the `D` array into two equal-size arrays.

```
 A3,B3 = np.hsplit(D, 2)
print(A3)
print('\n', B3)

[[ 3.6  2.1]
 [-1.4  0.7]]

 [[-12\.    7.7]
 [  2.1  -1.9]]
```

### 6.1.3 Reshaping Arrays

Although it doesn’t arise frequently in engineering calculations, it is possible to reshape arrays into different row/column formats. One of the simplest methods is to *flatten* a multidimensional array into one dimension.[¹](#ch06.xhtml_n6_1) For example, we can flatten our `A` array from above with the command

```
 a = A.flatten()
print(a)
[ 3.6  2.1-1.4   0.7]
```

You will note that the method flattens the array by rows. This method doesn’t change the dimensions of `A`, but recasts `A` into a one-dimensional array that is assigned to `a`.

Although it may be a bit confusing to you at this point, there is an alternate method, `ravel`, that provides another *view* of the same array, and any modifications of the array affect both the new view and the original array. This is illustrated by

```
 print('\n')
b = A.ravel()
print(b)
b[2] = 99.
print(b)
print(A)

[ 3.6  2.1 -1.4  0.7]
[ 3.6  2.1 99\.   0.7]
[[ 3.6  2.1]
 [99\.   0.7]]
```

You see here that, first, the `ravel` method flattens `A` into `b`. Then, the third element of `b` is modified to 99 as in the second display of `a`. And finally, by displaying `A` again, we see that the corresponding element was changed to 99 there too. So, `b` and `A` reference the same memory locations but do so with a different view.

Alternately, we can reshape an array into a different arrangement of rows and columns. Here is an example.

```
 B = np.array([[1., 3., 5.], [2., 4., 6.]])
D = B.reshape(3,2)
print D

[[1\. 3.]
 [5\. 2.]
 [4\. 6.]]
```

The original `B` array is two rows by three columns. The array is then reshaped into three rows and two columns. There is an alternate `resize` method that, like the `ravel` method, provides a different view of an array, but does not change the array’s structure.

Arrays can also be created using the NumPy `loadtxt` function, retrieving data from external text files. You have seen example of this in earlier chapters.

## 6.2 Indexing: Array Subscripts

It is very common to refer to individual elements or sets of elements in arrays. This is accomplished through *indexing*, also called *subscripting*. This raises an important point and source of confusion when relating mathematical descriptions and Python arrays. This is illustrated in [Figure 6.2](#ch06.xhtml_f6_2). The observation we make is that typical mathematical subscripting has an origin of 1, and Python’s subscripting has an origin of 0.[²](#ch06.xhtml_n6_2)

![](images/Fig06_02.jpg)

**[FIGURE 6.2](#ch06.xhtml_f6_2b)** Mathematical and Python array indexing.

First, let’s consider a simple, one-dimensional array,

```
 import numpy as np

a = np.array([1.2, 3.5, 7.9, 8.4, 9.9])
print(a[2])

7.9
```

You can see that we use the index 2, and that selects the third element of the array.

Next, we illustrate this further with a two-dimensional array. Notice that brackets, [•], are employed for subscripts.

```
 B = np.array([[1., 3., 5.], [2., 4., 6.]])
print(B[1,2])

6.0
```

The `[1,2]` indices select the element of `B` in the second row and third column. This may take some getting used to, but be patient. With practice, it will become second nature.

Next, we introduce the use of the colon, **:**, in indexing. When used alone, the colon indicates “all.” Here is an example using the `B` array from above.

```
 print(B[:, 1])

[3\. 4.]
```

The second column (index 1, all rows) is extracted and displayed in the Console.

We can also use the colon to select ranges of subscripts. When we do this, there is a further point of confusion possible. This example illustrates it.

```
 print(a[1:3])

[3.5 7.9]
```

The second and third element of the `a` array are selected. With zero-based indexing, we might have expected the second through the fourth element, but that didn’t happen. Just like the `arange` function and the `range` type, specifying `[1:3]` provides elements up to but not including the final index, `3`. Extending this technique, suppose we want to select the second and third rows and columns of the following array:

$\begin{bmatrix} 3 & {- 2} & 7 & 1 \\ 4 & {- 1} & 6 & 5 \\ 9 & {- 8} & 4 & 2 \\ {- 5} & 8 & {- 7} & {- 3} \end{bmatrix}$

That would then be

```
 import numpy as np

Z = np.array([[ 3, -2, 7, 1],
              [ 4, -1, 6, 5],
              [ 9, -8, 4, 2],
              [-5, 8, -7, -3]])
print(Z[1:3,1:3])

[[-1 6]
 [-8 4]]
```

Commonly, subscripts are used as indices in `for` loops. For example, this script sums the squares of the elements of `a`.

```
 sumsqa = 0
for i in range(5):
    sumsqa = sumsqa + a[i]**2
print(sumsqa)

244.67000000000002
```

You will recall from [Chapter 4](#ch04.xhtml_c4) that the `range` type generates a sequence from 0 to 4, and these align well with the zero-based indexing of the `a` array. The squares of the five elements are accumulated in the `sumsqa` variable and then displayed. It is of note here, with Python, that the `sumsqa` variable must be initialized first by assigning zero to it; otherwise, there will be an error in the statement that uses `sumsqa` on the right of the equal sign. This is not necessarily the case with other programming systems where the variable is created automatically with a zero value.

Similarly, we can accumulate the square roots of the `B` array with nested `for` loops as follows.

```
sumsqrtB = 0
for i in range(2):
    for j in range(3):
        sumsqrtB = sumsqrtB + np.sqrt(B[i,j])
print(sumsqrtB)

10.83182209022494
```

Here, the `i` index is for rows 0 and 1, and the `j` index is for columns 0, 1, and 2.

When working with arrays and subscripting, you always must keep in mind the zero-based subscripting and the way the colon is used with ranges of subscripts. At times, it’s best to make sketches by hand to make sure you have it right, and then, of course, check results carefully.

## 6.3 Array Operations

There are two types of mathematical operations that are applied to arrays. One is item-by-item or array operations, and the other is vector/matrix operations. For certain operations, the calculations are the same, such as addition, subtraction, and multiplication/division by a constant. However, in other cases, such as multiplication and division, there are differences. In the example below, we illustrate division of an array `a` by a constant, 3\. The result is as we would expect, each element of `a` is divided by 3 giving a new array of the same dimension or shape as `a`. This is called an array operation and has the characteristic item-by-item.

```
 a = np.array([1.2, 3.5, 7.9, 8.4, 9.9])
b = a/3
print(b)

[0.4        1.16666667 2.63333333 2.8        3.3      ]
```

When addition and subtraction are carried out, a restriction comes into play. The arrays must have the same shape (or dimensions). We illustrate that here with two examples, one that is successful and another that is erroneous.

```
 import numpy as np

a = np.array([1.,3.,5.])
b = np.array([2.,4.,6.])

print(a+b)

d = np.array([7.,9.])
print(a+d)

[ 3\.  7\. 11.]

ValueError: operands could not be broadcast together with
shapes (3,) (2,)
```

We see that the `a` and `b` arrays have the same number of elements, and their addition produces the expected item-by-item sum. However, when an addition of `a` and `d` is attempted, there is an error because they do not have the same shape.

Now, we move on to multiplication and division. In the last example, what happens if we attempt to multiply a times `b`?

```
 print(a*b)

[ 2\. 12\. 30.]
```

Like addition and subtraction, we see that the multiplication takes place item-by-item. The same would be true for division. As we will see in the next section, there are differences when we wish to carry out an operation like a vector dot product.

The basics of array operations extend to more complicated expressions. We can evaluate a polynomial as shown in the code below. This provides an array of three results with the calculation carried out item-by-item.

```
 import numpy as np

x = np.array ([0.1,0.2,0.3])
print(x**3-2*x**2 + 0.4*x + 3)

[3.021 3.008 2.967]
```

An important distinction arises when we consider using built-in functions. For example, if we want to evaluate the sine of the `x` array, we might try the following.

```
 import math
import numpy as np

x = np.array([0.1, 0.2, 0.3])

print(math.sin(x))

TypeError: only size-1 arrays can be converted to Python
scalars
```

Evidently, we are unable to use the `sin` function from the `math` module for array operations. On the other hand, see the code below.

```
 print(np.sin(x))

[0.09983342 0.19866933 0.29552021]
```

So, we see that using the similar `sin` function from the NumPy module does support array operations.

[Figure 6.3](#ch06.xhtml_f6_3) illustrates the contrast between item-by-item and *vectorized* calculations. For item-by-item calculation, a `for` loop is used to cycle through all the items in an array making individual calculations of the hyperbolic cosine (`cosh`) function. The vectorized calculation simplifies this significantly by placing the entire `x` array as an argument to the `np.cosh` function and a corresponding `y` array is created. Also, notice that, with the item-by-item approach, we need to create the `y` array first before populating its values in the `for` loop. Alternately, we could have created an empty `y` array and populated it using the `append` method.

![](images/Fig06_03.jpg)

**[FIGURE 6.3](#ch06.xhtml_f6_3b)** Contrast of item-by-item and vectorized computational strategies.

As you write Python code and construct expressions, you need to consider whether it is important to support arrays and array operations. If so, care is needed in implementing nonlinear functions, both built-in functions from the NumPy module and user-defined functions.

## 6.4 Vector/Matrix Operations

Multidimensional computations occur frequently in engineering and science. Representing quantities as vectors and matrices often represents a compact, efficient way to accomplish computational tasks. Take, for example, a set of linear algebraic equations.

$\begin{array}{l} {- 2x_{1} + 5x_{2} = 43} \\ {7x_{1} + 0.5x_{2} = - 9} \end{array}$(6.2)

We find it convenient to represent these in vector/matrix form:

$\begin{bmatrix} {- 2} & 5 \\ 7 & 0.5 \end{bmatrix} \cdot \begin{bmatrix} x_{1} \\ x_{2} \end{bmatrix} = \begin{bmatrix} 43 \\ {- 9} \end{bmatrix}$(6.3)

and with the definitions shown below, we can describe the equations in a compact, general form.

$\left. \mathbf{A} = \begin{bmatrix} {- 2} & 5 \\ 7 & 0.5 \end{bmatrix},\,\,\,\,\,\,\mathbf{x} = \begin{bmatrix} x_{1} \\ x_{2} \end{bmatrix},\,\,\,\,\,\,\mathbf{b} = \begin{bmatrix} 43 \\ {- 9} \end{bmatrix}\,\,\,\,\,\,\,\Rightarrow\,\,\,\,\,\,\,\mathbf{Ax} = \mathbf{b} \right.$(6.4)

Seeing the arrangement above introduces the concept of matrix/vector multiplication.

### 6.4.1 Matrix/Vector Multiplication

[Figure 6.9](#ch06.xhtml_f6_9) depicts matrix/vector multiplication. One way to describe this is that we “pour” the first row of the matrix down the vector then multiply paired elements and add them. This process is repeated for the second row. These are then matched with the elements of the **b** vector to form the linear equations.

![](images/Fig06_09.jpg)

**[FIGURE 6.9](#ch06.xhtml_f6_9b)** Illustration of matrix/vector multiplication.

The linear equation example leads us to consider how we multiply a row vector times a column vector to compute a single, scalar result. This is illustrated in [Figure 6.10](#ch06.xhtml_f6_10). This is also called an *inner product* or *dot product*. The requirement that is evident is that the number of elements of each array must be the same.

![](images/Fig06_10.jpg)

**[FIGURE 6.10](#ch06.xhtml_f6_10b)** Row vector × column vector to obtain scalar result.

How do we accomplish an inner or dot product of two arrays in Python? The code below illustrates this using the `dot` method.

```
 import numpy as np

a = np.array([0.5, 1.7, -6.2, 4.3])
b = np.array([-0.7, 3.3, 5.1, -7.2])
```

```
 c = a.dot(b)
print(c)

-57.32
```

Next, we consider how to carry out *matrix multiplication*. [Figure 6.11](#ch06.xhtml_f6_11) illustrates this process.

![](images/Fig06_11.jpg)

**[FIGURE 6.11](#ch06.xhtml_f6_11b)** Example illustration of matrix multiplication.

You will notice that each row of the first matrix and each column of the second matrix perform a dot product. The third row of the first matrix and the second column of the second matrix produce the corresponding result in the product matrix. Here, we see that a 3 × 2 matrix multiplies a 2 × 3 matrix to yield a 3 × 3 matrix. The general scheme and requirement for matrix multiplication for the product **C** = **A**·**B** is shown in [Figure 6.12](#ch06.xhtml_f6_12) which illustrates in detail the dot product that produces element *c*[ij]. The figure also illustrates that the inner dimensions of the matrices **A** and **B**, *n*, must match (it illustrates them “canceling out” and leaving the outer dimensions), and the outer dimensions, *m* and *p*, form the dimensions of the product matrix **C**.

![](images/Fig06_12.jpg)

**[FIGURE 6.12](#ch06.xhtml_f6_12b)** General illustration of matrix multiplication and the dimensional requirements.

Given this scheme, we can construct a Python function to implement matrix multiplication; however, we must account for zero-based indexing.

```
 import numpy as np

def  matmult (A,B):
     (m,nA)  = A.shape
     (nB,p)  = B.shape
     if nA != nB:
         return "matrix inner dimensions are not equal"
     n = nA
     C = np.zeros((m,p))
     for i in range(m):
        for j in range(p):
            C[i,j] = 0
            for k in range(n):
                C[i,j] = C[i,j] + A[i,k]*B[k,j]
     return C
```

In the `matmult` function, the numbers of rows and columns of the `A` and `B` arguments are determined using the `shape` attribute for each. Then, the inner dimensions are checked for equality with an error message returned if they are not. A product array `C` is created, filled with zeros. The matrix multiplication is accomplished with three nested `for` loops. The outer `for` loop iterates the `i` index from `0` to `n-1` for the number of rows in the product. The next inner `for` loop iterates the `j` index from `0` to `m-1` for the number of columns in `C`. The innermost loop computes the dot product of row `i` of `A` with column `j` of `B` to yield the `i`, `j` element of `C`. Here is a test of the `matmult` function corresponding to the example in [Figure 6.11](#ch06.xhtml_f6_11).

```
 A = np.array([[-2, 5],[7, 0.5],[-4, 3.4]])
B = np.array([[0.2, -0.4, 1.2],[4.2, 12, -6]])
C = matmult(A,B)
print(C)

[[ 20.6   60.8  -32.4 ]
 [  3.5    3.2    5.4 ]
 [ 13.48  42.4  -25.2 ]]
```

Alternately, we can attempt to use the `dot` method for the matrix multiplication.

```
 D = A.dot(B)
print(D)

[[ 20.6   60.8  -32.4 ]
 [  3.5    3.2    5.4 ]
 [ 13.48  42.4  -25.2 ]]
```

It is evident that the `dot` method accomplishes this in a more concise fashion, and our longer, home-grown `matmult` function is not required. However, the `matmult` function does illustrate how this operation takes place.

### 6.4.2 Transpose

Another common vector/matrix operation is the *transpose*. When an array is transposed, its rows become columns and vice versa as illustrated below,

$\begin{bmatrix} {- 2} & 5 \\ 7 & 0.5 \\ {- 4} & 3.4 \end{bmatrix}^{\, T} = \begin{bmatrix} {- 2} & 7 & {- 4} \\ 5 & 0.5 & 3.4 \end{bmatrix}$(6.5)

where the transpose operation is denoted with a superscript T. Python has a `transpose` method to implement the operation. Here is an example of its use.

```
 import numpy as np

A = np.array([[-2, 5],[7, 0.5],[-4, 3.4]])
B = A.transpose()
print(A)
print(B)

[[-2\.    5\. ]
 [ 7\.    0.5]
 [-4\.    3.4]]
[[-2\.    7\.  -4\. ]
 [ 5\.    0.5  3.4]]
```

### 6.4.3 Matrix Inversion

The final matrix operation we consider in this chapter is the *matrix inverse*. It is applied to square matrices (same number of rows as columns). We are all familiar with the concept of the inverse in scalar calculations. Here are examples.

$a \cdot \frac{1}{a} = 1\,\,\,\,\,\,\,\,\,\,\sin(\theta) \cdot \sin^{- 1}(\theta) = 1\,\,\,\,\,\,\,\,\,\,\,\,\,\text{ln}\left( {\exp(b)} \right) = 1$

The result of applying the inverse to a quantity, whether via division or a function, is unity, 1\. When we consider the inverse of a matrix, multiplication by the inverse cannot yield unity but rather results in a matrix of 1’s on the diagonal, also known as an *identity matrix*.

**A** ⋅ **A**^(−1) = **I**(6.6)

An example of this would be

$\begin{bmatrix} {- 2} & 5 \\ 7 & 0.5 \end{bmatrix} \cdot \begin{bmatrix} {ai_{11}} & {ai_{12}} \\ {ai_{21}} & {ai_{22}} \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$(6.7)

where the values of *ai*[ij] represent the elements of the inverse matrix. These can be found here by multiplying out to yield four linear equations which can be solved in pairs with the results shown.

$\begin{matrix} \begin{matrix} \begin{array}{l} {- 2ai_{11} + 5ai_{21} = 1} \\ {- 2ai_{12} + 5ai_{22} = 0} \\ {7a_{11} + 0.5ai_{21} = 0} \\ {7ai_{12} + 0.5ai_{22} = 1} \end{array} & {\begin{bmatrix} {- 2} & 5 \\ 7 & 0.5 \end{bmatrix}^{\, - 1} = \begin{bmatrix} {- \frac{1}{72}} & \frac{5}{36} \\ \frac{7}{36} & \frac{1}{18} \end{bmatrix}} \end{matrix} \end{matrix}$(6.8)

We can test our inverse matrix using matrix multiplication in a Python script.

```
 import numpy as np

A = np.array([[-2, 5], [7, 0.5]])
AI = np.array([[-1/72, 5/36], [7/36, 1/18]])

print(A.dot(AI))

[[1.00000000e+00 0.00000000e+00]
 [1.38777878e-17 1.00000000e+00]]
```

The result is an identity matrix with a tiny roundoff error in the lower left element.

Although this example and method are illustrative, this is not the way that the inverse is computed with numerical methods. We consider that in [Chapter 8](#ch08.xhtml_c8). In the meantime, we can illustrate how to obtain the inverse using the `inv` function from NumPy’s `linalg` submodule.

```
 from numpy import linalg

Ainv = linalg.inv(A)
print(Ainv)
print(Ainv.dot(A))

[[-0.01388889  0.13888889]
 [ 0.19444444  0.05555556]]

[[1.00000000e+00 1.38777878e-17]
 [0.00000000e+00 1.00000000e+00]]
```

The inverse matrix, `Ainv`, is displayed followed by the matrix product `Ainv·A` to confirm that it is a valid inverse. You will also note, from our two last examples, that **A-**^(**1**)**·A** gives the same result as **A·A-**^(**1**). In other words, the order of multiplication of a matrix and its inverse is *commutative*. That is not generally the case for matrix multiplication which is not commutative; that is, **A·B** ≠ **B·A**. Except for square matrices, one of these products is not feasible because of the requirements for matrix multiplication.

Although we have illustrated the vector dot product and matrix multiplication of arrays with the `dot` method, it is worthwhile to point out that the NumPy `linalg` module also has functions that accomplish these and many other linear algebra operations. For example, there are `matmul` and `vdot` functions available. More information is available in the NumPy manual ([https://numpy.org/doc/stable/](https://numpy.org/)).[³](#ch06.xhtml_n6_3)

## Problems

1.  **6.1** Write a Python script to create the two-dimensional array shown below, and then add statements to extract the subset array indicated. Hint: Use the colon in array indexing. Use `print` statements to document your results.![](images/un06_01.jpg)
2.  **6.2** Write a Python script using a `for` loop to create a one-dimensional array with odd numbers from 1 to 9\. Use `print` statements to document your results.
3.  **6.3** Employ the stack commands to add the following to the array in Problem 6.1.
    1.  Add this row to the bottom of the array: $\begin{matrix} {- 1} & {- 2} & {- 3} & {- 4} & {- 5} \end{matrix}$
    2.  Add this column to the right side of the array: $\begin{matrix} 6 \\ 7 \\ 8 \\ 9 \end{matrix}$

        Provide your Python code and document your results.

4.  **6.4** Write Python code to create an array of one hundred *x* values from 0 to 5, and then use this array to create a well-formatted plot of the following function:

    *e*^(−*x*/4)(2 − *x*) − 1

5.  **6.5** Write a compact set of Python statements to create a 7  ×  7 array filled with sevens. Use a `print` statement to display the array.
6.  **6.6** Develop Python code that changes this row array

    $\begin{matrix} {- 1} & {- 2} & {- 3} & {- 4} & {- 5} \end{matrix}$

    into a column array. Do so with both the `reshape` function and the `transpose` method and compare the results.

7.  **6.7** Create a Python function called `fnorm` that computes the square root of the sum of squares of an array. The function should perform with one- or two-dimensional arrays. Test it for both. Compare your result to that from using the `norm` function from the NumPy `linalg` module. This is called the *Frobenius norm*.
8.  **6.8** The *vector product*, **x**^T **x**, is equivalent to the dot product of **x** with itself. A more general form is the *quadratic form*,

    **x**^(*T*) ⋅ **Q** ⋅ **x**

    where **Q** is a symmetric, square matrix. The form of the **Q** matrix is such that its transpose is the same matrix. The elements on opposite sides of the diagonal are equal.

    $\begin{bmatrix} q_{11} & q_{21} & \cdots & q_{n1} \\ q_{21} & q_{22} & \cdots & q_{n2} \\ \vdots & \vdots & \ddots & \vdots \\ q_{n1} & q_{n2} & \cdots & q_{nn} \end{bmatrix}$

    Develop a Python function, called `quadform`, that takes arguments of `x` and `Q` and computes the quadratic product as shown above. The function should check that the dimension of `x` matches the number of rows and columns of `Q`. It should also check that `Q` is a square matrix and a symmetric matrix. Test and document your results.

9.  **6.9** Write a Python script to determine the inverse of the following matrix.

    $\begin{bmatrix} 1.13 & 3.83 & 1.16 & 3.40 \\ 0.53 & 1.79 & 2.53 & 1.54 \\ 3.41 & 4.93 & 8.76 & 1.31 \\ 1.24 & 4.99 & 10.67 & 0.02 \end{bmatrix}$

    Include in your script a test of the inverse by multiplying it by the original matrix with the result of an approximate identity matrix.

10.  **6.10** Solve the following set of linear equations via a Python script using the `inv` function from the NumPy `linalg` module and the `dot` method. Test your solution using the equations.

    $\begin{matrix} {8x_{1} + 2x_{2} + 3x_{3} = 30} \\ {x_{1} - 9x_{2} + 2x_{3} = 1} \\ {2x_{1} + 3x_{2} + 6x_{3} = 31} \end{matrix}$

11.  **6.11** Develop and test a Python function, called `trace`, which has a square array as an argument and returns the sum of the diagonal elements of the array. The function should check that the input argument is a square matrix.
12.  **6.12** Develop and test a Python function, called `absnorm`, which is an alternate to the Frobenius norm. This norm sums the absolute values of the array elements.

# 7 Solving Single Algebraic Equations

DOI: [10.1201/9781003256861-7](https://doi.org/10.1201/9781003256861-7)

## Chapter Objectives

*   Learn bracketing methods for solving single equations, both bisection and false position.
*   Implement the bracketing methods by developing Python functions.
*   Understand the background behind open methods for solving single equations, including the Newton-Raphson method and the secant method.
*   Develop Python functions to implement the open methods.
*   Learn about a hybrid, bracketing/open method, Brent’s method, and how to use the built-in `brentq` function from the SciPy `optimize` module.
*   See how some equations occur naturally in a successive substitution or circular format, *x* = *g*(*x*), and understand the characteristics that govern convergence of fixed-point iteration.
*   Program Python to apply fixed-point iteration to the solution of circular, *x* = *g*(*x*), equations.
*   Learn the Wegstein method as an enhancement of fixed-point iteration and how it can be implemented with a Python function.

In solving numerical problems, engineers and scientists frequently must compute a series of formulas implemented as Python expressions in assignment statements. There are many occasions, however, when sequential calculations are not the complete story. Numerical solution of equations is a routine activity for engineers and scientists, and they need to be well equipped to solve such equations with Python.

There are several, well-recognized categories of equations needing solution. In this chapter, we consider single, nonlinear algebraic, and transcendental equations. An *algebraic equation* consists of constants, variables, and the basic algebraic operations of addition, subtraction, multiplication, division, and raising to a power. Examples include simple polynomials such as

*f*(*x*) = 6*x*⁵ − 3*x*³ + 5*x* + 7(7.1)

A *transcendental equation* is one which “transcends” algebra by including terms such as the exponential and trigonometric functions. For example,

*f*(*x*) = *e*^(−0.5*x*)sin (3*x* − 1)(7.2)

In subsequent chapters, you will learn how to use Python to solve systems of linear and nonlinear algebraic equations and equations that describe rates of change—differential equations. This and the following two chapters open the door to the study of numerical methods. You may well take one or more courses in numerical methods later in your academic career, but here our purpose is to introduce you to methods that you can apply to advantage now and in your upcoming studies.

## 7.1 The Nature of Single, Nonlinear Equations in One Unknown

In a typical application, we will have an equation that has terms on both sides of the equal sign. Here is an example:

sin (*x* + 2)cosh (*x*) = −2(7.3)

To solve the equation, we need to find a value of *x* so that the left-hand side of the equation evaluates to −2\. By convention, when we are solving equations like this, we move all terms to one side of the equation. Here, that would then be

sin (*x* + 2)cosh (*x*) + 2 = 0(7.4)

Thus, the *root* is the value of *x* that makes the function on the left-hand side equal to zero. More generally, the root satisfies

*f*(*x*) = 0(7.5)

As in [Figure 7.1](#ch07.xhtml_f7_1), an effective way to visualize the scenario is the plot the left-hand side, *f*(*x*), versus *x* for a range of *x* values and examine the behavior. By reading the graph, we can see that *f*(*x*) = 0 at about *x* = 1.8\. Although this is a good first approximation, we may need a more precise answer for the solution or root of the equation, and we return to that.

![](images/Fig07_01.jpg)

**[FIGURE 7.1](#ch07.xhtml_f7_1b)** Example plot of *f*(*x*).

Next, instead of plotting the curve for *x* from 0 to 3, [Figure 7.2](#ch07.xhtml_f7_2) displays the curve from −3 to 3.

![](images/Fig07_02.jpg)

**[FIGURE 7.2](#ch07.xhtml_f7_2b)** Plot of Equation 7.1 with an expanded *x* range.

Imagine we plot a different function and produce [Figure 7.3](#ch07.xhtml_f7_3). Examining this plot, we reach the conclusion that this function has no roots; or more accurately, no real roots. The equation plotted here is

![](images/Fig07_03.jpg)

**[FIGURE 7.3](#ch07.xhtml_f7_3b)** Plot of a function with no real roots.

*x*² − 6*x* + 13 = 0(7.6)

and its roots, by the quadratic formula, are a complex conjugate pair, 3 ± 2j. The message to be drawn from these plots is that it is worthwhile to study graphically the behavior of the equation you are going to solve so that you understand better the situation you are facing.

Now, going back to Equation 7.1 and [Figure 7.1](#ch07.xhtml_f7_1), one way to determine a more precise root is by trial-and-error. [Table 7.1](#ch07.xhtml_t7_1) shows a sequence of values for *x* and corresponding *f*(*x*) results where we are trying to home in on a solution.

[**TABLE 7.1**](#ch07.xhtml_t7_1b) Sequence of Trial-and-Error Values

| *x* | *f*(*x*) |
| --- | --- |
| 1.8 | 0.09867 |
| 1.82 | 0.01257 |
| 1.84 | −0.07539 |
| 1.825 | −0.00924 |
| 1.823 | −0.00050 |

With the four additional estimates from the initial *x* = 1.8 from our plot, we have a good estimate of the solution, *x* = 1.823, to four significant figures.

If we only had to solve an equation once and be on our way, the plot and trial-and-error method may be all we need. It is a simple approach, and it is not necessary to involve more complicated techniques for a one time solution. However, maybe we need to solve this equation thousands of times as part of a bigger computational scheme, or perhaps we need a very, very precise solution. Then, we need to look at numerical methods to be programmed in Python, and that is where we are headed in the next section.

## 7.2 Bracketing Methods—Bisection

The numerical methods that use a bracketing technique require two initial estimates, *x*[1] and *x*[2] (sometimes called guesses, but usually “educated guesses”) for the root that are on either side of the true root; that is, which “bracket” the root. Referencing [Figure 7.1](#ch07.xhtml_f7_1), we could choose as our initial estimates 0 and 3 or, more narrowly 1.5 and 2.

How do we tell whether our initial estimates do bracket a root? Typically, the signs of *f*(*x*[1]) and *f*(*x*[2]) are opposite, but we must be careful. Referring to [Figure 7.2](#ch07.xhtml_f7_2), if we chose −3 and 3 as initial estimates, both would produce negative signs for *f*(*x*), and you can see that this is because we have two roots between those estimates. So, when we apply bracketing methods, we need to check that there is only one root in our bracket and that *f*(*x*) is a smooth function over that range with no weird characteristics like discontinuities. Most of the real problems that engineers and scientists solve will be like this, but there are exceptions.

We introduce the simplest of the bracketing methods with the illustration in [Figure 7.4](#ch07.xhtml_f7_4). By choosing the initial estimates *x* = 0\. and 3., we note on the figure that *f*(*x*[1]) > 0 and *f*(*x*[2]) < 0, which establishes that the product *f*(*x*[1]) ⋅ *f*(*x*[2]) < 0.

![](images/Fig07_04.jpg)

**[FIGURE 7.4](#ch07.xhtml_f7_4b)** Illustration of the first iteration of bisection.

The *bisection method*, as its name implies, chooses the midpoint between *x*[1] and *x*[2], called *x*[mid] on the diagram, as the next estimate for the solution. The next step of the method is to determine which half of the bisected interval contains the solution. That’s easy to tell from the plot, but how do we do so analytically? Since we are still looking for a sign change in *f*(*x*), we can compare the signs of *f*(*x*[1]) and *f*(*x*[2]) with that of *f*(*x*[mid]). Where there is a match, *x*[mid] replaces either *x*[1] or *x*[2] as the bracket for the next round of the method. In our case above, *x*[mid] replaces *x*[1] and the next round or iteration looks like the updated plot in [Figure 7.5](#ch07.xhtml_f7_5).

![](images/Fig07_05.jpg)

**[FIGURE 7.5](#ch07.xhtml_f7_5b)** Second iteration of the bisection method.

We can see that the next midpoint is at *x* = 2.25, and the root is located between *x*[1] and *x*[mid]. Consequently, *x*[mid] will become *x*[2] for the third iteration of the method.

Notice that the original interval has width 3; the second’s interval is 1.5, and the third interval will be 0.75\. The interval containing the solution is cut in half each iteration. If the method is conducted for *n* iterations, the final interval of uncertainty containing the solution will be given by

$\frac{\text{orginal~interval}}{\text{2}^{n}}$

Two examples: For ten iterations, the final interval will be the original divided by 1,024\. For 20 iterations, it will be divided by 2^(20) = 1,048,576 or about a million. Practically, knowing the solution to one part in a million of the original interval is generally good enough, and the best part is that it is guaranteed!

The next step is to code the bisection method as a function in Python. That code is presented in [Figure 7.6](#ch07.xhtml_f7_6).

![](images/Fig07_06.jpg)

**[FIGURE 7.6](#ch07.xhtml_f7_6b)** Python bisection function.

The `bisect` function is designed to be general purpose. Its first argument is the name of the Python function that provides the value of *f*(*x*) given a value of *x*. The second and third arguments are the bracket values of *x*, and the final keyword argument, `maxit`, is the maximum number of iterations with a default value of 20 if it is not specified. The `bisect` code first checks to make sure that the signs of *f*(*x*[1]) and *f*(*x*[2]) are opposite. If not, an error message is returned. Following that, the function uses a `for` loop to iterate the bisection method `maxit` times. For each iteration, the function computes the `f(xmid)` value and checks if it is the same sign as `f(x1)`. Note that this is accomplished by taking the product of the two and testing to see if that is positive. If it is, `xmid` becomes the next `x1`. If not, `xmid` becomes the next `x2`. Finally, the last value of `xmid` is returned as the solution estimate.

Notice that the `bisect` function only has nine executable statements. It is compact and easy to understand. Simplicity and brevity are good features of Python code. We can apply this `bisect` function to solve for the root of the equation from the previous section with the Python script:

```
 import numpy as np

def f(x):
    return np.sin(x+2)*np.cosh(x)+2.

x1 = 0\. ; x2 = 3.
xsoln = bisect(f,x1,x2)
print('solution is {0:6.4f}'.format(xsoln))
```

and the display in the Console is

```
 solution is 1.8229
```

You can see that this is close to our trial-and-error solution of 1.823, but it is precise to one part in a million of the original interval, 3., or a precision of 3/2^(20) ≅ 3 × 10^(−6).

## 7.3 Bracketing Methods—False Position

As elementary numerical methods, like bisection, are introduced, it is worthwhile to consider modified or enhanced versions; that is, taking one step beyond the base method. That will be a theme in this chapter (as well as numerical methods in general), and we start with an enhancement of the bisection method called *false position*. This method is illustrated in the diagram in [Figure 7.8](#ch07.xhtml_f7_8).

![](images/Fig07_08.jpg)

**[FIGURE 7.8](#ch07.xhtml_f7_8b)** False position method.

Instead of using the midpoint between the initial estimates, the false position (also called *regula falsi*[²](#ch07.xhtml_n7_2) in some references) method projects a straight line between the estimates and obtains the next estimate, *x*[new], where the line crosses *f*(*x*) = 0\. With the *x*[new] value in hand, the same logic used in bisection applies in determining whether *x*[new] becomes the new *x*[1] or *x*[2] for the next iteration of the method. In the illustration in the diagram, evidently *x*[new] will become the next *x*[1].

What we need then is a formula that allows us to calculate *x*[new]. We can obtain this by equating the ratios of sides of two similar triangles as follows:

$\frac{f\left( x_{\text{1}} \right) - f\left( x_{\text{2}} \right)}{x_{\text{2}} - x_{\text{1}}} = \frac{f\left( x_{\text{1}} \right) - \text{0}}{x_{\text{new}} - x_{\text{1}}}$(7.10)

and then solve this analytically for *x*[new]:

$x_{\text{new}} = \frac{x_{\text{1}}\, f\left( x_{\text{2}} \right) - x_{\text{2}}\, f\left( x_{\text{1}} \right)}{f\left( x_{\text{2}} \right) - f\left( x_{\text{1}} \right)}$(7.11)

You will note in the diagram above that the first *x*[new] value is farther away from the solution than the first *x*[mid]. This will not always be the case. You can imagine if the *f*(*x*) curve were more linear (that is, less curved), the false position method would get very close to the solution in the first iteration.

Modifying our `bisect` function to accommodate the false position method is easy. See the result in the `falpos` function in [Figure 7.9](#ch07.xhtml_f7_9). The midpoint formula from `bisect` has been replaced by the false position formula (Equation 7.5) and all the `xmid` notations have been changed to `xnew  `to be consistent with our terminology. We can evaluate the `falpos` function by solving Equation 7.1,

![](images/Fig07_09.jpg)

**[FIGURE 7.9](#ch07.xhtml_f7_9b)** Python false position function.

sin(*x* + 2)cosh(*x*) + 2 = 0(7.12)

with initial estimates *x*[1] = 0 and *x*[2] = 3\. Here is the script and the results:

```
 import numpy as np

def f(x):
    return np.sin(x+2)*np.cosh(x)+2.

x1 = 0.
x2 = 3.

xsoln = falpos(f,x1,x2)
print('x = {0:6.4f}'.format(xsoln))

x = 1.8229
```

Although the false position method appears to find the root just as well as the bisection method, there is a lingering doubt. One of the advantages of bisection is that, knowing the number of iterations taken (20 as default), the precision of the solution is guaranteed (one part in 2^(20) of the original interval). That is not the case with false position. This raises the possibility of determining precision, or at least convergence, in another way. This is accomplished by examining the current `xnew` value in comparison with its value from the previous iteration. When there is negligible change in these two successive values, we can conclude that the method has converged to a sufficient extent to provide a solution. In comparing these two values, we usually want to measure the change as a fraction or percentage of the values themselves. This leads to a definition of percent relative error as follows:

$\varepsilon_{a} = \left| \frac{\text{current}\text{x}_{\text{new}} - \text{previous x}_{\text{new}}}{\text{current x}_{\text{new}}} \right|\, \times \, 100\%$(7.13)

When the percent relative error, *ε*[a], falls below a specific tolerance, *ε*[s], the method is considered converged, the solution is terminated, and the current root estimate is returned. Note that the subscript “a” designates that *ε*[a] is an “approximate” error whereas the subscript “*s*” designates that *ε*[s] is a “stopping” error.

Using an error tolerance/convergence scheme raises another issue. We usually want this convergence to occur within a maximum number of iterations. If the maximum is reached, the method should signal that the maximum has been reached along with returning the current estimate. Here, we introduce two different algorithm structures that accomplish this. The first uses a `for` loop that will execute the maximum number of iterations. Within the loop, it tests for convergence and exits (or returns) if the tolerance is met. The second uses a `while` loop with two exits, one if convergence is achieved, and another if the maximum iterations is met.

For the first algorithm structure, we modify the `falpos` function to `falpos1` as shown in [Figure 7.10](#ch07.xhtml_f7_10). You will notice that the fractional (not percentage here) error tolerance, `Ea`, has been added to the function arguments with a default value of 1 × 10^(–7), and the maximum iterations, `maxit`, now has a default value of 30\. Of course, we hope that the method converges before the maximum iterations is reached. Next, the function returns two values, usually the solution estimate and number of iterations taken (since `i` starts at zero, the number of iterations taken is `i`+1). If the initial estimates do not bracket a solution (*f*(*x*[1]) and *f*(*x*[2]) are not the same sign), an error message and zero iterations are returned.

![](images/Fig07_10.jpg)

**[FIGURE 7.10](#ch07.xhtml_f7_10b)** Python false position function `falspos1` with relative error convergence using a `for` loop structure.

To get the calculation of relative error off the ground, an initial value of `xnew` is required, called `xnewprev` and set equal to the midpoint between `x1` and `x2`. What’s new in the `for` loop is that the relative error is calculated, and, if it is less than the error tolerance, there is a return with the solution estimate and the number of iterations taken—a good return! Otherwise, the same logic is used as before in determining whether `xnew` becomes the new `x1` or `x2`. What is added after that is that the `xnew` value is saved in `xnewprev` for the next iteration. If the `for` loop is completed, having reached the maximum iteration limit, the current value of `xnew` and the number of iterations is returned. By checking the iterations returned against the maximum, it can be determined whether the iteration limit has been reached.

If we apply this new false position function, `falpos1`, to the solution of the previous equation, here is a script and the results.

```
 import numpy as np

def f(x):
    return np.sin(x+2)*np.cosh(x)+2.

x1 = 0.
x2 = 3.

xsoln,iter = falpos1(f,x1,x2)
print('x = {0:6.4f}'.format(xsoln))
print('number of iterations taken = {0:3d}'.format(iter))

x = 1.8229
number of iterations taken = 17
```

We obtain the same solution to five significant figures and note that 17 iterations were required.

To implement the second algorithm structure, we modify the `falspos1` function to a new `falspos2` function, replacing the `for` loop with a `while` loop. This is shown in [Figure 7.11](#ch07.xhtml_f7_11). To save space, we have omitted the initial docstring comments. You will note that there is a `while True`: statement that creates a general iterative loop. As we discussed in [Chapter 4](#ch04.xhtml_c4), this loop will not exit on the `while` statement, but rather depends on exit or termination based on `if` tests within the loop. There are two such `if` tests, one for convergence and another for exceeding the iteration limit. Rather than exiting the `while` loop with a `break` statement, we use a `return` statement to terminate the function.

![](images/Fig07_11.jpg)

**[FIGURE 7.11](#ch07.xhtml_f7_11b)** Python false position function `falspos2` with relative error convergence using a `while` loop structure.

If we test the `falspos2` function, it produces the same solution as the `falspos1` function. Also, we can evaluate it with a lower limit on iterations that will be met.

```
 xsoln, iter = falpos2(f, x1,x2,maxit=10)
print(xsoln)
print(iter)
```

with the results

```
 maximum iterations reached
11
```

As we encounter iterative methods that test for convergence and have an iteration limit, you can implement these with either the `for` or `while` loop structures. We will illustrate both in later chapters.

Two bracketing methods, bisection and false position, have been introduced, which raises the question, which is the best to use? That is not that easy to answer. If we are solving a nonlinear, algebraic equation only once, bisection can get us the answer to a desired precision, even though the method might require more iterations than false position. We do encounter applications where solving the equation is embedded in a larger calculation which may require the equation to be solved thousands of times. If that is the case, the efficiency of the method becomes relevant. This will be discussed in the next section.

## 7.4 Open Methods—Newton-Raphson

The bracketing methods introduced in the previous two sections have an advantage and possibly a disadvantage. If the initial estimates encompass a single root of the equation, generally the methods, bisection or false position, will find the root. That’s good. However, with the way that the methods proceed, they typically plod along and would not be considered efficient. With some analysis, we can demonstrate that the bracketing methods reduce the relative error each iteration in a linear fashion. Consequently, there is interest in finding and using methods which converge more quickly. Also, the bracketing methods require two initial estimates. In order that they always encompass the root of the equation, we may have to set their interval wide. That also slows the process down when we are repeating the solution many times.

*Open methods* provide an alternative. These methods also involve systematic trial-and-error iterations but require only a single starting value or two starting values that do not necessarily bracket the root. As such, they sometimes diverge or move away from the true root as the computation progresses ([Figure 7.12c](#ch07.xhtml_f7_12)). However, when the open methods converge ([Figure 7.12b](#ch07.xhtml_f7_12)), they usually do so much more quickly than the bracketing methods.

![](images/Fig07_12.jpg)

**[FIGURE 7.12](#ch07.xhtml_f7_12b)** Graphical depiction of the fundamental difference between (a) bracketing and (b) and (c) open methods for root location (modified from Chapra & Clough 2022). In (a), which is bisection, the root is constrained within the interval prescribed by *x*[l] and *x*[u]. In contrast, for the open method depicted in (b) and (c), which is Newton-Raphson, a formula is used to project from x[i] to x[i+1] in an iterative fashion. Thus, the method can either (b) converge rapidly or (c) diverge, depending on the shape of the function and the value of the initial guess.

Among the most popular and powerful (when it works) of these open methods is the *Newton-Raphson*[³](#ch07.xhtml_n7_3) *method*. This approach requires only one initial estimate, and it would be best if that value were in the vicinity of the solution. That can be a good fit for the multiple solution scenario where the solution changes a bit from one time to the next. The reason for that is that we can use the solution from the last time as the initial estimate for the next time. Also, we will appreciate if the convergence is better than linear; for example, instead of reducing the error linearly with the number of iterations, reduction by the square of the number of iterations would be advantageous.

The concept behind the Newton-Raphson method is illustrated in [Figure 7.13](#ch07.xhtml_f7_13). An initial estimate, *x*[1], is used to evaluate *f*(*x*[1]). From the point {*x*[1], *f*(*x*[1])}, a tangent line is projected to the intersection with the *f*(*x*) = 0 line, which determines the next estimate for the solution, *x*[2]. Then, the method is repeated. The process is stopped when the relative error of *x*[1] to *x*[2] meets a convergence criterion, just as in the `falpos1` function ([Figure 7.10](#ch07.xhtml_f7_10)) of the previous section.

![](images/Fig07_13.jpg)

**[FIGURE 7.13](#ch07.xhtml_f7_13b)** The Newton-Raphson method.

Using the properties of the tangent line, we can write

$\frac{0 - f\left( x_{\text{1}} \right)}{x_{\text{2}} - x_{\text{1}}} = f'\left( x_{\text{1}} \right)$(7.14)

and then solve this analytically for *x*[2],

$x_{\text{2}} = x_{\text{1}} - \frac{f\left( x_{\text{1}} \right)}{f'\left( x_{\text{1}} \right)}$(7.15a)

or in general iterative form

$x_{i + 1} = x_{i} - \frac{f(x_{i})}{f'(x_{i})}$(7.15b)

This is the *Newton-Raphson formula*, which is the key relationship of the method. You can see that, to carry out the method, we need the derivative of *f*(*x*). This may be difficult or impossible to derive analytically, but we will deal with that in the next section. Based on the `falpos1` function of [Figure 7.10](#ch07.xhtml_f7_10), we provide a Python function for the Newton-Raphson method in [Figure 7.14](#ch07.xhtml_f7_14). You will notice that there is only one `if` test in the `for` loop, that being for convergence. The maximum iteration condition is created `if` the `for` loop exceeds `maxit` and exits normally. Because of this, we have to assess the iteration value returned to see if maximum iterations were reached.

![](images/Fig07_14.jpg)

**[FIGURE 7.14](#ch07.xhtml_f7_14b)** Python Newton-Raphson function.

Notice how brief the code is—eight executable statements within the function. We can test the function with our previous example, Equation 7.1,

*f*(*x*) = sin(*x* + 2)cosh (*x*) + 2 = 0(7.16)

but now we have the burden of deriving *f*΄(*x*) and supplying a separate function that evaluates it. For this case, that’s not too difficult with the result obtained through knowledge of calculus

*f*^′(*x*) = cos (*x* + 2)cosh (*x*) + sin (*x* + 2)sin (*x*)(7.17)

In the script below, we program the solution with an initial estimate of *x*[1] = 2.5\. The results are also displayed.

```
 import numpy as np

def f(x):

    return np.sin(x+2)*np.cosh(x)+2.

def fp(x):

    return np.cosh(x)*np.cos(x+2)+np.sinh(x)*np.sin(x+2)

x1 = 2.5

xsoln,iter = newtraph(f,fp,x1)
print('x = {0:6.4f}'.format(xsoln))
print('number of iterations taken = {0:3d}'.format(iter))

x = 1.8229
number of iterations taken = 5
```

The same solution, to five significant figures, is determined as before, but you notice that only five iterations were required. You may recall that false position required 17 iterations.

Below, we attempt the solution for a different initial estimate, *x*[1] = 0.5, and the results are

```
 x = 4.2246
number of iterations taken = 7
```

The Newton-Raphson method has found another solution, evidently outside the range of *x* we have been exploring. An expanded plot of the function is shown in [Figure 7.15](#ch07.xhtml_f7_15).

![](images/Fig07_15.jpg)

**[FIGURE 7.15](#ch07.xhtml_f7_15b)** Expanded plot of function subject to the Newton-Raphson method.

Ah, ha! We note immediately that our function has another solution at *x* = 4.2246, and that this is the one that the Newton-Raphson method found. Not only that, but our initial estimate was to the left of the solution at 1.8, and the method skipped right over that one and located the root to the far right.

Recalling that a graphical analysis can sometimes help us figure out what happened, we have replotted the function showing how the Newton-Raphson iterations evolved. Note that at our initial guess, the slope is very flat. That is, *f*′(0.5) has a very small value of

*f*^′(0.5) = cos(0.5 + 2)cosh (0.5) + sin (0.5 + 2)sin (0.5) = −0.59153(7.18)

Thus, the first iteration shoots the solution far to the right of the initial guess before it intercepts the abscissa at about *x* = 5\. Thereafter, Newton-Raphson rapidly converges on the root at *x* = 4.2246.

For this particular example, the tendency to move away from the area of interest is because a near-zero slope was encountered. But beyond that, the example reveals a more general problem with the Newton-Raphson method, and with open methods in general. There is no guarantee that the method will converge upon the acceptable solution of the equation. In our example above, another solution has been found. In fact, the method may diverge and not find a solution at all. This is the reason why our Python code ([Figure 7.14](#ch07.xhtml_f7_14)) specifies a maximum number of iterations. Further, although it does not necessarily ensure that the method will work, it would certainly be advantageous for our initial estimate to be in close proximity of the desired solution.

## 7.5 Open Methods—Modified Secant

In introducing the Newton-Raphson method in the previous section, we pointed out that there could be difficulty in obtaining an analytical expression for the derivative, *f*΄(*x*), of the equation being solved. There are many examples of this, but a general circumstance that would cause the problem is that *f* (*x*) may be a more involved calculation than one single formula. It might involve the solution of other equations or reading data from tables. Also, to be truthful, many would prefer to avoid a detailed analytical derivation of a derivative, although that challenge can be overcome frequently by using symbolic mathematics software, such as *Wolfram Alpha*.[⁴](#ch07.xhtml_n7_4) In any case, such software is useful in checking your own derivation of the derivative. The purpose of this section is to provide an alternative method to use when do you do not want to derive *f*΄(*x*) or when an analytical derivative is not feasible.

The simple answer is to provide an approximation to *f*΄(*x*) using a local finite difference,

$f'(x) \cong \frac{f\left( {x_{\text{1}}\left( {1 + \delta} \right)} \right) - f\left( x_{\text{1}} \right)}{\delta \cdot x_{\text{1}}}$(7.21)

Here, we provide a small deviation in *x*[1], given by a fraction, *δ*, and compute the change in *f*(*x*) divided by that deviation. The fraction is typically small, for example, 10^(−6). If we substitute this into the Newton-Raphson formula, we get

$x_{\text{2}} = x_{\text{1}} - \frac{f\left( x_{\text{1}} \right)\delta\, x_{\text{1}}}{f\left( {x_{\text{1}}\left( {1 + \delta} \right)} \right) - f\left( x_{\text{1}} \right)} = x_{\text{1}} \cdot \left( {\text{1} - \frac{f\left( x_{\text{1}} \right)\delta}{f\left( {x_{\text{1}}\left( {1 + \delta} \right)} \right) - f\left( x_{\text{1}} \right)}} \right)$(7.22a)

or in general iterative form

$x_{i + 1} = x_{i} \cdot \left( {\text{1} - \frac{f\left( x_{i} \right)\delta}{f\left( {x_{i}\left( {1 + \delta} \right)} \right) - f\left( x_{i} \right)}} \right)$(7.22b)

This is called the *modified secant method*. There is a secant method that uses two previous solution estimates to approximate the derivative. That derivative estimate is not as accurate as the small deviation or perturbation method shown above. We concentrate on the modified secant method here.

To implement this method, we can modify the `newtraph` function of [Figure 7.14](#ch07.xhtml_f7_14). This is shown in [Figure 7.18](#ch07.xhtml_f7_18). The `fp` argument has been removed, and the `delta` argument added with a default value of `1.e-6`. Apart from that, and renaming the function `modsec`, the only other change is the formula calculating the new solution estimate, *x*[2]. We can test this with this script:

![](images/Fig07_18.jpg)

**[FIGURE 7.18](#ch07.xhtml_f7_18b)** Python function for the modified secant method.

```
 import numpy as np

def f(x):
    return np.sin(x+2)*np.cosh(x)+2.

x1 = 2.5

xsoln,iter = modsec(f,x1)
print('x = {0:6.4f}'.format(xsoln))
print('number of iterations taken = {0:3d}'.format(iter))
```

with the results

```
 x = 1.8229
number of iterations taken = 5
```

These are the same results we obtained using the `newtraph` function.

We have shown here that the modified secant method appears to perform well, even almost as well as the Newton-Raphson method for our simple example problem. So, why not use it all the time? Good question. We did replace the need to derive *f*΄(*x*) with the use of the `delta` factor. The latter could be considered a “tuning” parameter. If we choose a value that is too small, Python’s calculations may not yield a measurable change in *f*(*x*), and the modified secant method will fail. If we choose `delta` too large, the approximation to the derivative may be too crude, and the method may be unstable and not converge. So, in using the modified secant method, we may have to find a `delta` value that works well. Although the default value in our function, `1.e-6`, works well for most cases, it may need to be adjusted for some problems.

## 7.6 Circular Methods—Fixed-Point Iteration

As engineers and scientists confront problems that require numerical solutions, their analysis results in one or more equations that need to be solved. Generally, it is sound practice to deal with these equations in their natural format, that is, in the way that they arise via derivation. This is as opposed to carrying out analytical manipulations of the equations into different formats.

Consider this example. From your background, you are aware of the ideal gas law,

$P = \frac{R\, T}{\hat{V}}$(7.23)

where *P* = pressure, *V̂* = specific volume, *R* = the gas law constant, and *T* = the absolute temperature. Typical units might be

P[=]kilopascals(kPa)       *V̂*[ = ]liters/mole of gas (L/mol)       T [=]kelvins(K)

for which *R* ≅ 8.3145 L⋅kPa/(mol⋅K).

*Note:* You should always take care to use the correct value of *R* for the units being used in the problem you are solving. Values for different unit sets are conveniently available on the Internet; for example, Wikipedia under “gas constant.”

When the conditions are extreme, particularly at high pressures, the ideal gas law becomes inaccurate, and modifications are required. One of the classic modified gas laws is the *van der Waals equation*,

$P = \frac{R\, T}{\hat{V} - b} - \frac{a}{{\hat{V}}^{\text{2}}}$(7.24)

where *a* and *b* are parameters whose values depend on the gas under study.

We now wish to solve a problem where *P* and *T* are specified for a particular gas, and we need to solve for *V̂*. Rearranging the equation of state, we obtain

$\hat{V} = \frac{R\, T}{P + \frac{a}{{\hat{V}}^{\text{2}}}} + b$(7.25)

and immediately an issue appears. To calculate a value for *V̂*, we need the same value on the right-hand side of the equation. One approach would be, rather than rearranging the van der Waals equation as first stated, to move all terms to one side of the equal sign and express the problem in the form

$f\left( \hat{V} \right) = P - \frac{R\, T}{\hat{V} - b} + \frac{a}{{\hat{V}}^{\text{2}}} = \text{0}$(7.26)

and apply one of the methods from the previous sections to solve for *V̂*.

An alternate approach, suggested by [Figure 7.19](#ch07.xhtml_f7_19), is to use the second form of the equation (Equation 7.25), and carry out a *successive substitution* method as follows:

1.  Provide an initial estimate for *V̂*.
2.  Compute a new value for *V̂*, using the formula.
3.  Check whether the new value is equal to, or very close to, the initial estimate.
4.  If not, let the new value replace the initial estimate and return to Step 2.
5.  If so, accept the new value as a valid solution estimate.

![](images/Fig07_19.jpg)

**[FIGURE 7.19](#ch07.xhtml_f7_19b)** Circular calculation scheme.

Such schemes are called *circular* because of the loop depicted by the dashed lines in [Figure 7.19](#ch07.xhtml_f7_19) where *V̂* is recalculated as a function of *V̂* with the rearranged version of the original equation.

Let’s try this scheme in Python with a set of parameter values: *P* = 950 kPa, *T* = 300 K, *a* = 365.4 L²·kPa/mol², *b* = 0.04280 L/mol. Here, the values for *a* and *b* are for carbon dioxide, CO[2].

*P* = 950kPa, *T* = 300K, *a* = 365.4L²·kPa/mol², b = 0.04280L/mol

```
 R = 8.3145 # kPa*L/(mol*K)

a = 365.4 # L2*kPa/mol2
b = 0.04280 # L/mol

P = 950 # kPa
T = 300 # K

V1 = 2.0 # L/mol

V2 = R*T/(P+a/V1**2)+b

print(V1,V2)
```

and the display in the Console is

```
 2 2.438104172468431
```

If we repeat the circular scheme by assigning 2.4381 to `V1`, the result is

```
 2.4381 2.5088634490981945
```

Continuing this scheme yields the following table:

| 2.0000 | 2.4381 |
| 2.4381 | 2.5089 |
| 2.5089 | 2.5172 |
| 2.5172 | 2.5182 |
| 2.5182 | 2.5183 |

It is clear that the process is converging. At the point when `V2` is virtually equal to `V1`, the equation is satisfied, and we have a valid solution estimate.

Another way of illustrating this is with a plot of `V2` versus `V1`, shown in [Figure 7.20](#ch07.xhtml_f7_20). The solid line shows the progression of the values from left to right, and the dashed line is the line where `V2` = `V1`, the 45°-line. You can see that the method converges directly to the solution at the dashed line.

![](images/Fig07_20.jpg)

**[FIGURE 7.20](#ch07.xhtml_f7_20b)** Approach to the solution by successive substitution.

To show the speed of convergence, we can plot the absolute change in solution estimate from one iteration to the next. This is depicted in [Figure 7.21](#ch07.xhtml_f7_21) and uses a logarithmic y-axis scale. The linear nature of the curve suggests an exponential convergence.

![](images/Fig07_21.jpg)

**[FIGURE 7.21](#ch07.xhtml_f7_21b)** Convergence of successive substitution scheme.

Now that we have introduced the technique through an example, it is useful to discuss a few general concepts. The method is formally called *fixed-point iteration* or *successive substitution*. The scenario presents itself when the equation you are trying to solve is expressed as *x* = *g*(*x*); that is, you need the solution for *x* to compute the right-hand side of the equation. Evidently, the method worked with our example. Are there cases where it doesn’t work?

To investigate that, we’re going to manipulate van der Waals equation to solve analytically for the *V̂* that is located in the squared term,

$\hat{V} = \sqrt{\frac{a}{\frac{R\, T}{\hat{V} - b} - P}}$(7.27)

and we will repeat the procedure, starting with `V1 = 2.0`.

| 2.0000 | 1.0612 |
| 1.0612 | 0.4937 |
| 0.4937 | 0.2824 |
| 0.2824 | 0.1965 |
| 0.1965 | 0.1546 |

Clearly, this process is taking us away from the valid solution we determined earlier. Apparently, the method is not working in this case.

This reveals a major disadvantage of the fixed-point iteration method. We are not assured that it will be stable and convergent. By plotting the right-hand sides versus *V̂* along with the progress of our solutions, we can see the problem. This is shown in [Figure 7.22](#ch07.xhtml_f7_22). The root is located at the intersection of the solid and the dashed line. The top plot, which corresponds to Equation 7.25, is convergent, whereas the bottom plot, which corresponds to Equation 7.27, is divergent. These plots are often called “cobweb” plots. See Chapra and Clough (2022) for more detail.

![](images/Fig07_22.jpg)

**[FIGURE 7.22](#ch07.xhtml_f7_22b)** Comparison of cobweb plots for two formulas for fixed-point iteration. Top plot is convergent, whereas the bottom plot diverges.

What we find in the top graph is that, with a starting estimate of 2.0, successive estimates move directly toward the solution at the intersection with the dashed line. In the lower graph, again starting at 2.0, the successive estimates move to the left and will approach a value less than b, yielding a negative square root and failure of the method.

You may have noticed already the difference in the two graphs. For the stable solution, the slope of *g*(*x*) in the vicinity of the solution is less than one (the slope of the dashed line is one), and the opposite is true for the non-convergent case on the right. The condition for a stable solution can be expressed, in general, as ([Chapra and Canale 2019](#ch11_ref.xhtml_r2))

|*g*^′(*x*[*s**o**l**n*])| < 1(7.28)

In practice, if we are confronted with such a non-convergent scheme, a way around this is to solve for another *x* and formulate a new *x* = *g*(*x*) equation. One will usually work.

In [Figure 7.23](#ch07.xhtml_f7_23), a Python fixed-point iteration solving function, `fixpt`, is presented. This is similar to previous functions; however, the new estimate is simply the function `g` evaluated for the current estimate. Convergence is attained when the relative error meets the `Ea` criterion with a default value of `1.e-7`.

![](images/Fig07_23.jpg)

**[FIGURE 7.23](#ch07.xhtml_f7_23b)** Python function for fixed-point iteration.

If we apply this function to the van der Waals problem with the first, stable formulation, the Python script is

```
 def V2(V1):
    return R*T/(P+a/V1**2)+b

R = 8.3145 # kPa*L/(mol*K)

a = 365.4 # L2*kPa/mol2
b = 0.04280 # L/mol

P = 950 # kPa
T = 300 # K

V1 = 2.0 # L/mol

Vsoln,iter = fixpt(V2,V1)

print('V = {0:6.4f}'.format(Vsoln))
print('number of iterations taken = {0:3d}'.format(iter))
```

and the displayed results are

```
 V = 2.5183
number of iterations taken = 8
```

## 7.7 Circular Methods—The Wegstein Method

After studying the bisection method in [Section 7.1](#ch07.xhtml_h7_1), we considered an enhanced method based on a linear interpolation in [Section 7.2](#ch07.xhtml_h7_2), the false position method. Now, we’re going to extend the fixed-point iteration method in a similar way.

[Figure 7.24](#ch07.xhtml_f7_24) illustrates the concept. Instead of one initial estimate, the *Wegstein method* requires two, but, unlike the bisection and false position methods, the two estimates, *x*[1] and *x*[2], do not have to bracket the solution.

![](images/Fig07_24.jpg)

**[FIGURE 7.24](#ch07.xhtml_f7_24b)** Wegstein method concept.

As we have noted in the previous section, for an *x* = *g*(*x*) formulation, the solution is where the *g*(*x*) curve crosses the 45° line. The Wegstein method projects a straight line through the points {*x*[1], *g*(*x*[1])} and {*x*[2], *g*(*x*[2])} to the 45° diagonal to establish the next estimate, *x*[3]. At this point, *x*[2] becomes the new *x*[1], and *x*[3] becomes the new *x*[2]. The method is then repeated until *x*[3] and *x*[2] are sufficiently close, as measured against a relative error criterion.

To derive the update formula for *x*[3], we write the straight-line relationship as illustrated in the figure:

$\frac{g\left( x_{\text{2}} \right) - g\left( x_{\text{1}} \right)}{x_{\text{2}} - x_{\text{1}}} = \frac{x_{\text{3}} - g\left( x_{\text{2}} \right)}{x_{\text{3}} - x_{\text{2}}}$(7.29)

This equation is then rearranged to solve for *x*[3]:

$x_{3} = \frac{x_{\text{1}} \cdot g\left( x_{\text{2}} \right) - x_{\text{2}} \cdot g\left( x_{\text{1}} \right)}{x_{\text{1}} - x_{\text{2}} + g\left( x_{\text{2}} \right) - g\left( x_{\text{1}} \right)}$(7.30)

The Python `fixpt` function ([Figure 7.23](#ch07.xhtml_f7_23)) is then modified to the `wegstein` function as shown in [Figure 7.25](#ch07.xhtml_f7_25).

![](images/Fig07_25.jpg)

**[FIGURE 7.25](#ch07.xhtml_f7_25b)** Python function to implement the Wegstein method.

First, we can test the `wegstein` function with the stable, convergent form of the van der Waals equation (Equation 7.25). Here is the Python script and the results:

```
 def g(V):
    return R*T/(P+a/V**2)+b

R = 8.3145 # kPa*L/(mol*K)

a = 365.4 # L2*kPa/mol2
b = 0.04280 # L/mol

P = 950 # kPa
T = 300 # K

V1 = 2.0 # L/mol
V2 = 2.5

Vsoln,iter = wegstein(g,V1,V2)
print('V = {0:6.4f}'.format(Vsoln))
print('number of iterations taken = {0:3d}'.format(iter))

V = 2.5183
number of iterations taken = 4
```

Notice that the function converges to the solution quickly. To be fair, we should then test the method for the version of the van der Waals equation that was divergent under fixed-point iteration (Equation 7.27). Here is the modified script and results for that case:

```
 import numpy as np

def g(V):
    return np.sqrt(a/(R*T/(V-b)-P))

R = 8.3145 # kPa*L/(mol*K)

a = 365.4 # L2*kPa/mol2
b = 0.04280 # L/mol

P = 950 # kPa
T = 300 # K

V1 = 2.0 # L/mol
V2 = 2.5

Vsoln,iter = wegstein(g,V1,V2)
print('V = {0:6.4f}'.format(Vsoln))
print('number of iterations taken = {0:3d}'.format(iter))

V = 2.5183
number of iterations taken = 7
```

What is interesting here is that the Wegstein method has produced a stable solution for a version of our *x* = *g*(*x*) equation that failed using fixed-point iteration. The disadvantage, perhaps not significant, is that two initial estimates are required. This suggests that for many, perhaps most, applications, the Wegstein method should be chosen over fixed-point iteration.

Can the Wegstein method ever get into trouble? The answer is yes. For our last example, if initial estimates of 1.0 and 2.0 are used, this is the output from the script:

```
 V = nan
number of iterations taken = 30
  C:\Users\cloughd\Documents\IntroPythonText\Chapter7\
wegstein2.py:27: RuntimeWarning: invalid value encountered
in sqrt
  return np.sqrt(a/(R*T/(V-b)-P))
```

Evidently, the function encountered a value for `V` that caused the argument in the square root function to be negative. So, we still must proceed with caution, and, as a lesson, it would always be preferable to use a convergent form of *x* = *g*(*x*).

## 7.8 A Hybrid Approach—Brent’s Method

Reviewing the methods presented so far in this chapter for solving single nonlinear equations, we have seen advantages and disadvantages for each technique. A hybrid method, introduced by Richard Brent,[⁵](#ch07.xhtml_n7_5) attempts to capitalize on the advantages and mitigate the disadvantages. The strategy developed is to use open methods, like Newton-Raphson or modified secant, when possible for fast (quadratic) convergence to the root, and, if these methods wander outside a bracketing set of values, resort to a less efficient bracketing technique, like bisection, until it is possible to switch back to the open method and continue with accelerated convergence.

We will not take the time and space here to derive and code a function for Brent’s method (see Chapra and Clough 2022 for this.) Rather, we will take advantage of a built-in `brentq` function in the SciPy `optimize` module. The syntax for using the `brentq` function is simple,

```
 xsoln = brentq(func, x1,x2)
```

where `func` is the name of the function that evaluates *f*(*x*), and x1, x2 are initial estimates which must bracket the solution. There are additional, optional arguments available:

1.  `maxiter`: maximum number of iterations allowed, otherwise error message
2.  `xtol`: absolute error tolerance limit, default = `2.e-12`
3.  `rtol`: relative error tolerance limit, default = `8.8e-16`
4.  `args`: additional arguments required by `func`, specified as `args`=`(tuple)`
5.  full_output: if `True`, returns both `xsoln` and additional details on the solution,
6.  default `False` returns just `xsoln`

If we apply the `brentq` function to solve for the root of our earlier example,

*f*(*x*) = sin(*x* + 2)cosh(*x*) + 2 = 0(7.4)

with initial estimates `x1` = 1.0 and `x2` = 3.0, here is the Python script followed by the display in the IPython Console:

```
 import numpy as np
from scipy.optimize import brentq

def f(x):
    return np.sin(x+2)*np.cosh(x)+2.

x1 = 1.0
x2 = 3.0

xsoln = brentq(f,x1,x2)

print('solution is {0:6.4f}'.format(xsoln))

solution is 1.8229
```

If we include `full_output`=`True`, the code becomes

```
 import numpy as np
from scipy.optimize import brentq

def f(x):
    return np.sin(x+2)*np.cosh(x)+2.

x1 = 1.0
x2 = 3.0

xsoln,results = brentq(f,x1,x2,full_output=True)

print('solution is {0:6.4f}'.format(xsoln))
print(results)

solution is 1.8229
      converged: True
           flag: 'converged'

function_calls: 10
    iterations: 9
          root: 1.8228849971054475
```

and we get more information about the performance of the algorithm. Often, we use this option at the start, and, once we are convinced that the `brentq` function is performing well, we remove the `full_output` specification.

We fully expect that you will want to employ the `brentq` function in your work; however, there are times when you would prefer one of the simpler methods/functions we have presented in this chapter. The advantage of the latter is that they are not “black boxes” like the `brentq` function where you cannot see inside to understand exactly how they work. Also, for problems that naturally present themselves in *x* = *g*(*x*) format, you may want to consider using fixed-point iteration or the Wegstein method.

## 7.9 Solving for the Roots of Polynomials

In [Example 7.1](#ch07.xhtml_exa7_1), we analyzed the relationship between liquid volume and depth in a spherical tank and determined the relationship

$f(h) = h^{\text{3}} - \text{3}R\, h^{\text{2}} + \frac{\text{3}\, V}{\pi} = \text{0}$(7.9)

Given values for *R* and *V*, this is a cubic polynomial in *h*, and we briefly illustrated solving this polynomial for its three roots with the Python script

```
 import numpy as np
V = 200 # m3
R = 5 # m
coef = np.array([1., -3.*R, 0., 3.*V/np.pi])
r = np.roots(coef)
print(r)
```

and results

```
 [14.02970369 4.20648373 -3.23618742]
```

Since polynomials occur frequently in problem solving in engineering and science, it is worthwhile to spend some time addressing them and their solution. A general form for an *n*th-order polynomial equation is

*a*[*n*] ⋅ *x*^(*n*) + *a*[*n* − 1] ⋅ *x*^(*n* − 1) + ⋯ + *a*[1] ⋅ *x* + *a*[0] = 0(7.32)

This equation will have *n* roots. They will either be real numbers or complex numbers. If there are complex roots, they must appear as complex conjugate pairs, that is,

*α* + *β**j*   *a**n**d*  *α* − *β**j*

The reason for this is that we are assuming that the coefficients of the polynomial, *a*[i], are real quantities. Since the polynomial can be represented as a product of its factors, i.e.

(*x* − *r*[1]) ⋅ (*x* − *r*[2])⋯(*x* − *r*[*n*]) = 0(7.33)

where *r*[i] are the roots, when multiplying out the factors, real coefficients must result. Note that the product of the conjugate pair is

(*x* − (*α* + *β**j*))(*x* − (*α* − *β**j*)) = *x*² − 2 *α* *x* + (*α*² + *β*²)(7.34)

so that pair contributes real coefficients as the factors are multiplied out. Any complex root that does not have a conjugate root would result in complex coefficients.

We have introduced methods in the earlier sections of this chapter that provide for finding a root of a nonlinear, algebraic equation, *f*(*x*) = 0, and these could certainly be applied to a polynomial, but they would determine only one root. How could we go about finding the rest of the roots?

Let’s explore this with an example:

*x*⁴ − 8 *x*³ − 3 *x*² + 62 *x* + 56 = 0(7.35)

We will apply the modified secant method with initial estimate `x1` = 1 to determine a root.

```
 def f(x):
    return x**4 - 8*x**3 - 3*x**2 + 62*x + 56

x1 = 1.

xsoln,iter = modsec(f,x1)
print('x = {0:6.4f}'.format(xsoln))
print('number of iterations taken = {0:3d}'.format(iter))
```

Here are the results:

```
 x = -2.0000
number of iterations taken = 3
```

So, now we know one root. The next step will be to divide the factor associated with that root, (*x* + 2), into the original polynomial. We show long division in [Figure 7.26](#ch07.xhtml_f7_26), but, if we were going to develop a program for this, we would have to translate this into an algorithm.

![](images/Fig07_26.jpg)

**[FIGURE 7.26](#ch07.xhtml_f7_26b)** Long division to determine quotient polynomial.

Since we divided by a root factor, we expect the remainder to be zero. We can now proceed to find a root of the quotient polynomial (the original polynomial with the first root removed).

```
 def f(x):
    return x**3 - 10*x**2 + 17*x + 28

x1 = 5.

xsoln,iter = modsec(f,x1)
print('x = {0:6.4f}'.format(xsoln))
print('number of iterations taken = {0:3d}'.format(iter))

x = 4.0000
number of iterations taken = 5
```

We have the next root and its factor, (*x*−4), and we can proceed with the next long division, which yields

*x*² − 6 *x* − 7(7.36)

This second-order polynomial can be solved for its roots using the quadratic formula to determine the remaining roots, *x* = 7 and *x* = −1.

Although this looks (and feels!) laborious, it is possible to code this method efficiently. It is also possible to determine complex roots. The process of factoring out a root and finding a root in the remaining polynomial is called *deflation*. It is the basis for a classic method for determining the roots of polynomials, *Muller’s method* (Chapra and Canale 2019).

There is another popular method for determining polynomial roots based on linear algebra and the determination of factors called eigenvalues of a matrix containing the polynomial coefficients. We choose not to discuss the details of this method here because it is beyond the scope of preparation we expect from students. It is notable that this is the current method of choice because it is more efficient than Muller’s method.

Python’s NumPy module provides several functions that are useful in computations with polynomials. You have already had a peek at one of them, `roots`, which uses the aforementioned eigenvalue method. Here, we apply it to our example polynomial.

```
 import numpy as np

coeff = [1., -8., -3., 62., 56.]
r = np.roots(coeff)
print('roots are\n',r)

roots are
 [ 7\. 4\. -2\. -1.]
```

You will note here that the coefficients are provided in a list in order of highest power of *x* to lowest last, the constant. The coefficients can also be defined as a tuple or a NumPy array.

There are two companion functions in the NumPy module that complement the `roots` function. The first, `poly`, is essentially the inverse of `roots`. It composes the polynomial from its roots and provides the polynomial coefficients. Here, it is applied to our example.

```
 coeff1 = np.poly([7., 4., -2., -1.])
print('coefficients are\n',coeff1)

coefficients are
 [ 1\. -8\. -3\. 62\. 56.]
```

The second is `polyval`, which evaluates a polynomial, given its coefficients, for a specific value of *x*. Here, we use this function to generate a plot of our polynomial from *x* = −5 to *x* = 10.

```
 import pylab
xplot = np.linspace(-3., 8.)
yplot = np.polyval(coeff, xplot)
pylab.plot(xplot, yplot, c='k')
pylab.grid()
pylab.xlabel('x')
pylab.ylabel('f(x)')
```

The resulting plot is shown in [Figure 7.27](#ch07.xhtml_f7_27), where we can see the four real roots.

![](images/Fig07_27.jpg)

**[FIGURE 7.27](#ch07.xhtml_f7_27b)** Polynomial plot showing roots at zero crossovers.

## 7.10 Case Study: Trajectories of Projectiles in Air

The study of the trajectory of a projectile is wide ranging, from sports to missiles to weapons ordnance. The horizontal distance of the trajectory is usually one important objective along with the horizontal, side-to-side position or windage. A typical trajectory is illustrated in [Figure 7.28](#ch07.xhtml_f7_28), not considering the horizontal position. If air resistance is neglected, such a trajectory can be described based on physics by the following equation:

![](images/Fig07_28.jpg)

**[FIGURE 7.28](#ch07.xhtml_f7_28b)** Projectile trajectory with no air resistance.

$y = \text{tan}(\theta)x - \frac{g}{\text{2}\, v_{\text{0}}^{\text{2}}\,\text{cos}^{\text{2}}(\theta)}x^{\text{2}} + y_{\text{0}}$(7.25)

where *y* = elevation, *x* = horizontal displacement or range, *θ* = launch angle, *g* = gravitational acceleration, *v*[0] = launch velocity, and *y*[0] = initial elevation. Of course, air resistance and other factors like wind are important, but they complicate the mathematical description beyond the scope of this chapter. We will return to those in a later chapter.

The objective of this study is to determine, for given values of *v*[0] and *y*[0], what is the launch angle, *θ*, for a desired range (value of *x* when *y* = 0). To obtain this objective, we need to solve

$f(\theta) = \text{tan}(\theta)x - \frac{g}{\text{2}\, v_{\text{0}}^{\text{2}}\,\text{cos}^{\text{2}}(\theta)}x^{\text{2}} + y_{\text{0}} = \text{0}$(7.36)

This is a meaningful scenario because, given a desired range, a launch velocity which is set due to physical limits, and geography that establishes elevation differences, the launch angle is the remaining adjustable parameter. As [Figure 7.28](#ch07.xhtml_f7_28) shows, the initial elevation is measured in reference to the final elevation at zero.

In designing a Python script to solve this problem, it would be desirable to have a function that returns the launch angle for input values of range, `r`, launch velocity, `v0`, and launch elevation, `y0`:

```
 def launch_angle(r, v0,y0):
·
·
return theta
```

Of course, consistent units must be used for these quantities. Since *g* is given as 9.807 m/s², the velocity’s time units must be seconds. After that, the distance units must be the same, e.g. meters, kilometers, and miles.

Within this function, we will want to invoke one of our solving methods. As we know, these will require either one or two initial estimates for the angle. For the bisection, false position, and Brent’s methods, the pair of initial estimates must bracket the solution. As we look at the figure, it would seem that bracketing estimates of 0° and 90° would always contain the solution, but given the equation being solved, there is a problem. The tangent function, as *θ* → 90°, approaches infinity. To address this, we would have to assume a reasonable maximum value for the launch angle that is less than 90°, perhaps 80°. For the Newton-Raphson method or the modified secant method, only one initial estimate is required. A mid-range value like 45° or perhaps a value typical of the situation being studied, e.g. 15°, might be used. In the bracketing or single initial estimate cases, testing should be carried out to determine their reliability.

Here is a test script using the `modsec` function from [Figure 7.18](#ch07.xhtml_f7_18):

```
 import numpy as np

def y(th0):
    return np.tan(th0)*x - g/2/v0**2/np.cos(th0)**2*x**2 + y0

g = 9.807 # m/s2
th0d = 45\. # degrees
th0 = np.radians(th0d)

y0 = 10\. # m
v0 = 50\. # m/s
x = 160.

theta,iter = modsec(y,th0)
thetad = np.degrees(theta)
print('launch angle = {0:5.1f} degrees'.format(thetad))
print('iterations required =',iter)
```

with the results displayed in the Console:

```
 launch angle = 15.4 degrees
iterations required = 5
```

This launch angle seems reasonable. If the launch angles for our application are typically below 20°, an initial estimate of 10° might be appropriate.

Alternately, we might try a bracketing method like the `brentq` function from the SciPy `optimize` module. This would then be the script:

```
 import numpy as np
from scipy.optimize import brentq

def y(th0):
    return np.tan(th0)*x - g/2/v0**2/np.cos(th0)**2*x**2 + y0

g = 9.807 # m/s2
th1d = 0\. # degrees
th1 = np.radians(th1d)
th2d = 25\. # degrees
th2 = np.radians(th2d)

y0 = 10\. # m
v0 = 50\. # m/s
x = 160.

theta = brentq(y,th1,th2)
thetad = np.degrees(theta)
print('launch angle = {0:5.1f} degrees'.format(thetad))
```

and the successful result is displayed:

```
 launch angle = 15.4 degrees
```

You will note that the bracketing initial estimates are 0° and 25°.

There is a choice to be made as to the method to solve for the launch angle. Arbitrarily, we will choose the `brentq` function to continue. Now, we embed the launch angle solving script into the `launch _ angle` function and test it below. You will note that we have passed the `launch _ angle` arguments through to the `y` function by using the `args`=`(r,v0,y0)` argument in the call to `brentq`.

```
 import numpy as np
from scipy.optimize import brentq

def y(th0,r,v0,y0):
    return np.tan(th0)*r - g/2/v0**2/np.cos(th0)**2*r**2 + y0

def launch_angle(r,v0,y0):
    th1d = 0\. # degrees
    th1 = np.radians(th1d)
    th2d = 25\. # degrees
    th2 = np.radians(th2d)
    return brentq(y,th1,th2,args=(r,v0,y0))

g = 9.807 # m/s2

y0 = 10\. # m
v0 = 50\. # m/s
r = 160.

theta = launch_angle(r,v0,y0)
thetad = np.degrees(theta)
print('launch angle = {0:5.1f} degrees'.format(thetad))
```

and it is successful:

```
 launch angle = 15.4 degrees
```

A case study of range versus required launch angle can now be carried out. The script is shown in [Figure 7.29](#ch07.xhtml_f7_29).

![](images/Fig07_29.jpg)

**[FIGURE 7.29](#ch07.xhtml_f7_29b)** Python script for case study of launch angle versus range.

The plot created is shown in [Figure 7.30](#ch07.xhtml_f7_30). A first observation is that the relationship is not quite linear, but approximately linear. Of course, this is for specific values of launch velocity and initial elevation. We could certainly carry out additional case studies where we varied one of these parameters and explored how it affects launch angle.

![](images/Fig07_30.jpg)

**[FIGURE 7.30](#ch07.xhtml_f7_30b)** Plot of required launch angle to achieve a desired range.

This case study illustrates how functions can be developed and tested as building blocks for a larger project. We have seen how it is convenient to pass arguments through functions to subordinate functions using the `args` technique. It was also necessary to consider, and perhaps test, different solving methods before making a choice to proceed. The judicious selection of initial estimates is required. It is not difficult to get our solving techniques into trouble by picking arbitrary values. They need to be tailored to the situation being studied. A general piece of advice is the more complicated the subject under study, the more care in planning and building the solution step-by-step is required for success.

## Problems

1.  **7.1** Use the bisection method to find a root of the following equation between *x* = 0 and *x* = 2.

    $f(x) = e^{- \frac{x}{\text{4}}}\left( {\text{2} - x} \right) - \text{1} = \text{0}$

2.  **7.2** For the equation from Problem 1, devise and carry out a fixed-point iteration scheme to solve for *x*.
3.  **7.3** Determine

    $\sqrt[\text{3}]{\text{5}}$

    using a root-solving method. Hint: If $x = \sqrt[\text{3}]{\text{5}}$, cube both sides and proceed.

4.  **7.4** Create a plot of

    *f*(*x*) = *x*²|sin (*x*)| − 4

    over the range 0 ≤ *x* ≤ 4, and then use the false position method to determine a root that you observe in the plot.

5.  **7.5** Create a plot of

    *f*(*x*) = *x*³ − 12.42 *x*² + 50.444 *x* − 66.552

    over the range 2 ≤ *x* ≤ 6.

    1.  Apply the Newton-Raphson method three times with well-chosen initial estimates for *x* to determine all three roots of the polynomial.
    2.  Use the NumPy `roots` function to determine all the roots of the polynomial and compare these with your results from part **(a)**.
6.  **7.6** Determine the root of

    *f*(*x*) = tan (*x*) − 2 *x* = 0

    between *x* = 0 and *x* = π/2 using the Newton-Raphson method.

7.  **7.7** A common shape for an underground tank to store liquids in a horizontal cylinder with hemispherical ends. This is illustrated in [Figure P7.7](#ch07.xhtml_fP7_7). The volume of liquid, *V*, is related to the liquid depth, *h*, by considering two parts. Conceptually, the hemispherical ends can be put together to form a sphere of radius *R*. The volume in that part is then

    ![](images/Fig07P_07.jpg)

    **[FIGURE P7.7](#ch07.xhtml_fP7_7b)** Horizontal tank with hemispherical ends.

    $V_{\text{sph}} = \pi\, h^{\text{2}}\left( \frac{\text{3}R - h}{\text{3}} \right)$

    The volume in the cylindrical part is given by a more complicated formula:

    $V_{cyl} = \left( {R^{\text{2}}\,\text{cos}^{- \text{1}}\left( \frac{R - h}{R} \right) - \left( {R - h} \right)\sqrt{\text{2}\, R\, h - h^{\text{2}}}} \right)L$

    Then, the total volume of liquid is

    *V* = *V*[sph] + *V*[cyl]

    For a tank with the dimensions, *L* = 5 m and *R* = 0.75 m, write a Python script that finds the depth, *h*, for a given volume, *V*. Then, extend the script to provide a calibration table in even increments of volume in liters giving the corresponding depth for each volume value. Finally, produce a plot of depth in meters versus volume in liters.

8.  **7.8** From [Example 3.1](#ch03.xhtml_exa3_1), we have the formula for computing the Great Circle distance between two points on the Earth as

    $d = \text{2}\,\text{sin}^{- \text{1}}\left( \sqrt{\left( {\text{sin}\left( \frac{lt_{\text{1}} - lt_{\text{2}}}{\text{2}} \right)} \right)^{\text{2}} + \text{cos}\left( {lt_{\text{1}}} \right)\,\,\text{cos}\left( {lt_{\text{2}}} \right)\,\,\left( {\text{sin}\left( \frac{\ln_{\text{1}} - \ln_{\text{2}}}{\text{2}} \right)} \right)^{\text{2}}} \right)\,\, r$

    where {*l**t*[1], ln[1]} is the location of the first point by latitude and longitude. If we pick the Meridian at the Equator the location is {0,0}. For a longitude of 105°W, determine the latitude S that is 10,000 km from the Meridian/Equator. Describe approximately where on the globe this is located.

9.  **7.9** An alternate, and more recent equation of state than the van der Waals equation, which accounts for behavior of gases at nonideal conditions, is that due to *Soave, Redlich, and Kwong* (*SRK*). The SRK equation is

    $P = \frac{R\, T}{\hat{V} - b} - \frac{\alpha\, a}{\hat{V}\,\left( {\hat{V} + b} \right)}$

    where, including example units, *P* = pressure in kPa, *R* = gas law constant, 8.3145 L·kPa/(mol·K), *T* = temperature in K, *V̂* = specific volume in L/mol. The additional parameters, *b* in L/mol, *a* in (L/mol)², and *α* (dimensionless), are dependent on the gas under consideration. For propane, C[3]H[8], their values are

    *a* = 9.3775(L/mol)², *b* = 0.06262L/mol, and *α* = 0.903

    For a temperature of 423 K and a pressure of 7,000 kPa, determine the specific volume using the SRK equation of state. Set this up as a circular calculation and use the Wegstein method. Compare the result to the specific volume determined by the ideal gas law,

    $P = \frac{R\, T}{\hat{V}}$

10.  **7.10** An important property in working with thermal calculations with gases is the heat capacity. In general, it provides the energy required to raise the temperature of the gas by one degree. The heat capacity varies by temperature and can be modeled accurately by a polynomial. An example is the heat capacity of water vapor:

    *C*[*P*] = 33.46 + 0.006880 *T* + 0.7604 × 10^(−5) *T*² − 3.593 × 10^(−9) *T*³

    where *C*[P] is the heat capacity in J/(mol·°C) and *T* is the temperature in °C. This formula is valid for a wide range of temperatures, 0–1,500°C.

    1.  Create a plot of heat capacity versus temperature for the entire valid range of temperatures.
    2.  Create a Python script using the Newton-Raphson method to compute and display the temperature at which the heat capacity is 40 J/(mol·°C).
11.  **7.11** The upward velocity of a rocket can be computed with the following formula:

    $v = u\,\, ln\left( \frac{m_{0}}{m_{0} - q\, t} \right) - g\, t$

    where *v* is the upward velocity, *u* = the downward exit velocity of fuel relative to the rocket, *m*[0] = mass of the rocket at *t* = 0, *q* = the fuel consumption rate, *g* = gravitational acceleration, 9.81 m/s². If *u* = 1,800 m/s, *m*[0] = 160,000 kg, *q* = 2,600 kg/s, compute the time at which *v* = 750 m/s. Use the `brentq` function to solve this problem.

12.  **7.12** You plan to buy a Tesla Model S vehicle for $79,990 by paying 10% down and financing the balance over a 7-year term. You have budgeted a monthly payment of $1,000\. So, now you need to shop for a loan at the required interest rate (or lower, if you can find it!). The formula that governs this is

    $A = P\,\,\frac{i\,\,\left( {1 + i} \right)^{n}}{\left( {1 + i} \right)^{n} - 1}$

    where *A*= the monthly payment, *P*= the loan amount, *i*= the monthly interest rate expressed as a fraction, not a percentage.

    *Note*: Loan interest rates are typically quoted on an annual basis as “APR.” To obtain the monthly interest rate, *i*, you divide the APR by 12\. The actual annual interest rate you pay is greater than the quoted APR. It is (1 + *i*)^(12) − 1 (× 100 for %). As an example, for an APR of 6%, with monthly payments, the actual annual interest rate is 6.17%.

    Determine the APR you will need to obtain to meet your goal.

13.  **7.13** As depicted schematically in [Figure P7.13](#ch07.xhtml_fP7_13), for any two massive bodies there are five points where the net force on a third smaller-mass body is zero. That is, the gravitational forces of the massive bodies and the centrifugal force are in balance. This feature makes them excellent locations for satellites, as minimal orbit corrections are needed to maintain a desired orbit. For our solar system, this is the case for the Sun and any planet, or for a planet and one of its moons. These points are commonly referred to as the *Lagrange points*.[⁶](#ch07.xhtml_n7_6) Noteworthy spacecraft designed to operate near the Earth–Sun *L*[2] are the *Gaia Space Observatory* and the *James Webb Space Telescope*. The force balance equation for *L*[2] can be written as

    ![](images/Fig07P_13.jpg)

    **[FIGURE P7.13](#ch07.xhtml_fP7_13b)** The Lagrange points for two massive bodies.

    $\frac{M_{1}}{{(R + r)}^{2}} + \frac{M_{2}}{r^{2}} = \left( {\frac{M_{1}R}{M_{1} + M_{2}} + r} \right)\frac{M_{1} + M_{2}}{R^{3}}$

    where *r* is the distance of the *L*[2] point from the smaller of the two massive objects, *M*[1] and *M*[2] are the masses of the larger and smaller massive objects, respectively, and *R* is the distance between them. A summary of the parameters for the Sun, Earth, and our Moon are listed in the table below. Determine *r* for an *L*[2] satellite orbiting around **(a)** the Earth and **(b)** the moon.

    | System | Sun-Earth | Earth-Moon | Units |
    | --- | --- | --- | --- |
    | *M*[1] | 1.991 × 10^(30) | 5.98 × 10^(24) | kg |
    | *M*[2] | 5.98 × 10^(24) | 7.35 × 10^(22) | kg |
    | *R* | 149,600,000 | 384,401 | km |

    If the mass of the smaller object is much smaller than the mass of the larger object, a good initial estimate of *r* can be computed with

    $r \approx R\sqrt[3]{\frac{M_{2}}{3M_{1}}}$

14.  **7.14** A four-bar linkage is illustrated in [Figure P7.14](#ch07.xhtml_fP7_14). Such linkages are designed by mechanical engineers to transmit mechanical movement in various ways.

    ![](images/Fig07P_14.jpg)

    **[FIGURE P7.14](#ch07.xhtml_fP7_14b)** Four-bar linkage.

    Member AD is anchored to a supporting base and does not move. Member AB rotates about point A, resulting in a reciprocating movement of members BC and CD. All motion is in the plane of the page. Therefore, angle *θ*[2] changes in response to a change in angle *θ*[1]. This motion is constrained by the equation

    $\overline{AD} = \overline{AB}\cos\theta_{1} - \overline{CD}\cos\theta_{2} + \sqrt{{\overline{BC}}^{2} - \left( {\overline{CD}\sin\theta_{2} - \overline{AB}\sin\theta_{1}} \right)^{2}}$

    Suppose $\overline{AB} = 1.5\, m$, $\overline{BC} = 6\, m$, $\overline{CD} = 3.5\, m$, and $\overline{AD} = 5\, m$.

    Determine angle *θ*[2], given a value of angle *θ*[1], for example, 45°. Use the false position technique.Create a data table of *θ*[2] values for a range of *θ*[1] values. Present a plot of this relationship.

15.  **7.15** When water is flowing down a sloped, open channel, a phenomenon called a hydraulic jump can occur where the water with a depth, *h*[1], and a flowing velocity, *v*[1], suddenly jumps up to a depth, *h*[2], with a slower velocity, *v*[2]. This is depicted in [Figure P7.15](#ch07.xhtml_fP7_15).

    ![](images/Fig07P_15.jpg)

    **[FIGURE P7.15](#ch07.xhtml_fP7_15b)** Hydraulic jump.

    An equation that describes a hydraulic jump is

    $h_{2} = \frac{h_{1}}{2}\left\lbrack {\sqrt{1 + \frac{8v_{1}^{2}}{gh_{1}}} - 1} \right\rbrack$

    and such a jump is possible only if

    $v_{1} > \sqrt{gh_{1}}$

    If values of *v*[1] and *h*[2] are known, create a Python script to determine *h*[1] and whether the jump is possible. Typical velocities (*v*[1]) would be 1-to-2 m/s and after-jump depths would be 2-to-3 cm.

# 8 Solving Sets of Algebraic Equations

DOI: [10.1201/9781003256861-8](https://doi.org/10.1201/9781003256861-8)

## Chapter Objectives

*   Review the scenario for sets of *n* linear equations in *n* unknowns.
*   Know how to solve a 2 × 2 system of linear algebraic equations graphically and understand how this provides insight into singular and ill-conditioned systems.
*   Understand the determinant of a square matrix and how it can be used to detect singular and ill-conditioned systems.
*   Know how Cramer’s Rule uses determinants to solve a set of linear equations.
*   Learn how to implement the Gaussian elimination method, and, from a vector/matrix perspective, how it achieves the solution of a set of linear algebraic equations.
*   Understand the limitations of Gaussian elimination and how they can be overcome by partial pivoting.
*   Be able to solve sets of linear equations with the NumPy `linalg` module.
*   Learn how to solve small sets of nonlinear equations with an extension of the successive substitution method.
*   For sets of nonlinear algebraic equations, see how the Newton-Raphson method can be extended, including the introduction of the Jacobian matrix of partial derivatives.
*   Be able to solve sets of nonlinear algebraic equations with the `root` function from the SciPy `optimize` module.

Systems of linear algebraic equations occur repeatedly in problems across all disciplines of engineering and science. Common examples include structures in civil engineering, circuits in electrical engineering, material balances in chemical engineering, thermal balances in mechanical engineering, and analytical measurements in chemistry. Consequently, it is important to understand the nature of linear algebraic equations and their solution. In this chapter, we focus on a classical method for solution of linear equations, Gaussian elimination, which persists today as the most widely used technique.

Beyond linear systems, systems of nonlinear algebraic equations also arise frequently when modeling physical, chemical, and biological phenomena. Solution of these equations is significantly more challenging than for linear equations. Here, we introduce an extension of the Newton-Raphson method from single to multiple nonlinear algebraic equations.

Finally, it is important to know how to use the tools available in Python’s NumPy `linalg` module and SciPy `optimize` module to solve systems of algebraic equations, both linear and nonlinear.

## 8.1 Systems of Linear Algebraic Equations

In [Chapter 6](#ch06.xhtml_c6), we introduced the vector/matrix description of a set of linear algebraic equations. A general representation is illustrated in [Figure 8.1](#ch08.xhtml_f8_1). Here, we use subscripts typical to mathematical descriptions with origin of one. We must pay attention to this as we transition the scenario to Python with its array origin of zero.

![](images/Fig08_01.jpg)

**[FIGURE 8.1](#ch08.xhtml_f8_1b)** Vector-matrix description of linear algebraic equations.

Before describing methods for solving systems of equations, it’s useful to understand why they so commonly occur in engineering and science problem solving.

## 8.2 Solving Small Numbers of Linear Algebraic Equations

Before proceeding to the computer methods, we will describe several methods that are appropriate for solving small (*n* ≤ 3) sets of simultaneous equations and that do not require a computer. These are the graphical method, Cramer’s rule, and the elimination of unknowns. In describing Cramer’s rule, we also introduce the determinant, which provides a metric for detecting problematic linear systems.

### 8.2.1 Graphical Method

A graphical solution is obtainable for two equations by plotting them on Cartesian coordinates with one axis corresponding to *x*[1] and the other to *x*[2] ([Figure 8.3](#ch08.xhtml_f8_3)). Because we are dealing with linear algebraic equations, each equation plots as a straight line. This can be easily illustrated for the following set of equations,

![](images/Fig08_03.jpg)

**[FIGURE 8.3](#ch08.xhtml_f8_3b)** Graphical solution of a set of two simultaneous linear algebraic equations. The intersection of the lines represents the solution.

$\begin{matrix} {1.5x_{1} + 2x_{2} = 6} \\ {- 0.5x_{1} + 2x_{2} = 2} \end{matrix}$(8.6)

which can each be solved for *x*[2]:

$\begin{array}{l} {x_{2} = 3 - 0.75x_{1}} \\ {x_{2} = 1 + 0.25x_{1}} \end{array}$(8.7)

As plotted on [Figure 8.3](#ch08.xhtml_f8_3), these are two straight lines that intersect at the solution, *x*[1] = 2 and *x*[2] = 1.5\. These values can be checked by substituting them into the original equations,

$\begin{matrix} {1.5(2) + 2(1.5) = 6} \\ {- 0.5(2) + 2(1.5) = 2} \end{matrix}$(8.8)

For three simultaneous equations, each equation would be represented by a plane in a three-dimensional coordinate system. The point where the three planes intersect would be the solution. Beyond three equations, graphical methods break down and, consequently, have little practical value for solving simultaneous equations. However, they are useful for visualizing properties of the solutions for two or three equations.

For example, [Figure 8.4](#ch08.xhtml_f8_4) depicts three cases that can pose problems when solving sets of linear equations. [Figure 8.4a](#ch08.xhtml_f8_4) shows the case where the two equations represent parallel lines. For such situations, there is no solution because the lines never cross. [Figure 8.4b](#ch08.xhtml_f8_4) depicts the case where the two lines are coincident. For such situations, there is an infinite number of solutions. Both types of systems are said to be *singular*. In addition, systems that are very close to being singular ([Figure 8.4c](#ch08.xhtml_f8_4)) can also cause problems. These systems are said to be *ill-conditioned*. Graphically, this corresponds to the fact that it is difficult to identify the exact point at which the lines intersect. Ill-conditioned systems will also pose problems when they are encountered during the numerical solution of linear equations. This is because they will be extremely sensitive to round-off error.

![](images/Fig08_04.jpg)

**[FIGURE 8.4](#ch08.xhtml_f8_4b)** Graphical depiction of singular and ill-conditioned systems: (a) no solution, (b) infinite solutions, and (c) an ill-conditioned system where the slopes are so close that the point of intersection is difficult to detect visually.

The takeaway from this section is that not all sets of linear equations have a unique solution. The equations must be *independent*. That means that any equation cannot be duplicated by another equation (probably obvious to you!), and any equation cannot by obtained by a linear combination of other equations in the set (maybe not that obvious).

### 8.2.2 Determinants and Cramer’s Rule

In your previous mathematics courses, you may have encountered Cramer’s Rule to solve a set of linear equations. This method involves the calculation of the *determinant* of a square matrix. The method is usually illustrated with small equation sets (*n* ≤ 3) because calculating the determinant manually becomes unwieldy for larger sets.

#### 8.2.2.1 Determinants

The determinant is usually introduced for a 2 × 2 matrix:

$\begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix}$

The *determinant*, *D*, of this system is computed from the coefficients as

$D = \left| \begin{matrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{matrix} \right| = a_{11}a_{22} - a_{12}a_{21}$(8.9)

Although the determinant *D* and the coefficient matrix **A** are composed of the same elements, they are completely different mathematical concepts. That is why they are distinguished visually by using brackets to enclose the interior of the matrix and straight lines to enclose the determinant. Additionally, whereas the matrix is a structured collection of numbers, the determinant is a single number.

For a 3 × 3 matrix,

$D = \left| \begin{matrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{matrix} \right|$(8.10)

the determinant can be computed as

$D = a_{11}\left| \begin{matrix} a_{22} & a_{23} \\ a_{32} & a_{33} \end{matrix} \right| - a_{12}\left| \begin{matrix} a_{21} & a_{23} \\ a_{31} & a_{33} \end{matrix} \right| + a_{13}\left| \begin{matrix} a_{21} & a_{22} \\ a_{31} & a_{32} \end{matrix} \right|$(8.11)

where the 2 × 2 determinants are called *minors*. There is a heuristic (in common parlance, “a rule of thumb”) that many have learned that provides a shortcut for computing the determinants of these smaller matrices. This is shown in [Figure 8.5](#ch08.xhtml_f8_5). Note the patterns in the figure. Solid arrows indicate positive contributions and dashed arrows negative.

![](images/Fig08_05.jpg)

**[FIGURE 8.5](#ch08.xhtml_f8_5b)** Shortcut patterns for determinants of small systems of linear algebraic equations.

Observe that each minor is the submatrix left if you remove the row and column of the multiplying factor. For the first minor, the coefficient is *a*[11] and the minor has row and column 1 of the 3 × 3 matrix removed. What about that minus sign on the second minor term? Well, the rule is that, if the sum of the indices on the coefficient is odd, the sign is negative. One could describe that mathematically for coefficient *a*[ij] as

(−1)^(*i* + *j*)

It should be noted that the selection of the three factors, *a*[11], *a*[12], and *a*[13], is arbitrary. The method of minors can be applied with the selection of any three matrix elements. Also, the method of minors applies to the 2 × 2 matrix, except the minors are now individual elements.

The takeaway from this example is that just as the graphical approach provided a visual indication, the determinant offers a means to detect whether a system of linear equations is singular (*D* = 0) or ill-conditioned (*D* near zero). But, in comparison with the graphical approach, it has the advantages that it (1) consists of a single number and (2) is not limited to 2 × 2 systems. Thus, as described later in this chapter, it will prove useful in detecting singular and near-singular (or ill-conditioned) linear systems.

#### 8.2.2.2 Cramer’s Rule

*Cramer’s rule* states that each unknown in a system of linear algebraic equations may be expressed as a fraction of two determinants with denominator *D* and with the numerator obtained as the determinant of the matrix formed by replacing the column of coefficients of the unknown in question by the constants *b*[1], *b*[2], . . . , *b*[n]. For example, *x*[1] would be computed as

$x_{1} = \frac{\left| \begin{matrix} b_{1} & a_{12} & a_{13} \\ b_{2} & a_{22} & a_{23} \\ b_{3} & a_{32} & a_{33} \end{matrix} \right|}{D}$(8.12)

### 8.2.3 Elimination of Unknowns

The *elimination of unknowns*, which is probably familiar to you from your early algebra courses, can be illustrated for a set of two equations with two unknowns:

$\begin{array}{l} {a_{11}x_{1} + a_{12}x_{2} = b_{1}} \\ {a_{21}x_{1} + a_{22}x_{2} = b_{2}} \end{array}$(8.14)

One solution strategy is to multiply the equations by a constant so that one of the unknowns will be eliminated when the two equations are combined. The result is a single equation that can be solved for the remaining unknown. This value can then be substituted into either of the original equations to compute the other variable.

For example, the first equation can be multiplied by *a*[21] and the second by *a*[11] to give

$\begin{array}{l} {a_{21}a_{11}x_{1} + a_{21}a_{12}x_{2} = a_{21}b_{1}} \\ {a_{11}a_{21}x_{1} + a_{11}a_{22}x_{2} = a_{11}b_{2}} \end{array}$(8.15)

Subtracting the two equations will, therefore, eliminate the *x*[1] term from the equations to yield

*a*[11]*a*[22]*x*[2] − *a*[12]*a*[21]*x*[2] = *a*[11]*b*[2] − *a*[21]*b*[1](8.16)

which can be solved for

$x_{2} = \frac{a_{11}b_{2} - a_{21}b_{1}}{a_{11}a_{22} - a_{12}a_{21}}$(8.17)

This equation can then be substituted into either of the equations and the result solved for

$x_{1} = \frac{a_{22}b_{1} - a_{12}b_{2}}{a_{11}a_{22} - a_{12}a_{21}}$(8.18)

Observe that the solutions follow directly from Cramer’s rule, which states

$x_{1} = \frac{\left| \begin{matrix} b_{1} & a_{12} \\ b_{2} & a_{22} \end{matrix} \right|}{\left| \begin{matrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{matrix} \right|} = \frac{a_{22}b_{1} - a_{12}b_{2}}{a_{11}a_{22} - a_{12}a_{21}}$(8.19)

$x_{2} = \frac{\left| \begin{matrix} a_{11} & b_{1} \\ a_{21} & b_{2} \end{matrix} \right|}{\left| \begin{matrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{matrix} \right|} = \frac{a_{11}b_{2} - a_{21}b_{1}}{a_{11}a_{22} - a_{12}a_{21}}$(8.20)

Now, you might be asking yourself: Why did we implement the elimination of unknowns with two different strategies in the preceding text and example? We did it to make the point that even for the simplest two equation system there would be alternative ways that different individuals would employ to generate a solution.

For two or three equations, that would not be a big deal. But what about when the elimination of unknowns is implemented on a computer for large systems of equations? For such applications the question arises: What is the **best** general-purpose elimination algorithm for solving large systems of simultaneous linear algebraic equations? As described in the next section, such a technique can be formalized and readily programmed with a language like Python.

## 8.3 Gaussian Elimination[¹](#ch08.xhtml_n8_1)

*Gaussian elimination* is the standard computer method for solving a system of linear algebraic equations,

**A****x** = **b**(8.27)

In its simplest form, it is implemented as a two-step process consisting of forward elimination and back substitution ([Figure 8.6](#ch08.xhtml_f8_6)).

![](images/Fig08_06.jpg)

**[FIGURE 8.6](#ch08.xhtml_f8_6b)** Depiction of Gaussian elimination consisting of forward elimination and back substitution steps. The primes that appear after the elimination pass indicate that the elements have been changed from their original values.

To maintain the identity of a set of linear equations so that they have the same, valid solution, any manipulations have to satisfy the requirements of *elementary row operations*. These include

*   shuffling or swapping the equations (or rows),
*   multiplying any equation (or row) by a constant and
*   replacing any equation (or row) by a linear combination of equations.

In the forward elimination step, the second and third of these are employed to transform the matrix of coefficients into *upper triangular* form. We will use the first of the three in an enhancement to Gaussian elimination later. To maintain the identity of the original system so that it has the same valid solution, all these operations are applied to both the **A** matrix and the **b** vector.

After the forward elimination step has been implemented, the last equation will have a single unknown and the solution can be obtained by *back substitution*. The algorithm is a relatively simple, elegant method that can be coded in Python in only a few statements.

We will first illustrate it in a step-by-step fashion. Subsequently, a more compact version will be developed. Finally, we will consider including the method of partial pivoting to avoid pitfalls that the original method can encounter. The implications of dealing with singular and almost singular coefficient matrices will also be addressed.

### 8.3.1 Naive Gaussian Elimination

This section includes the systematic techniques for forward elimination and back substitution that comprise Gaussian elimination. We first implement the method in a step-by-step fashion for a simple 3 × 3 system. We then generalize the method to *n* equations with *n* unknowns.

Although these techniques are ideally suited for computer implementation, some modifications will be required to obtain a reliable algorithm. In particular, the computer program must avoid divisions by zero. Because it does not avoid this problem, the method described in the following example is called *naive Gaussian elimination*. A subsequent section will add features like pivoting and determinant evaluation that are required for a reliable and effective computer program.

Of course, when solving such a well-conditioned system in Python on a 64-bit computer, we would obtain results with about 15-digits of precision. In the following section we show how this is done.

### 8.3.2 Gaussian Elimination Computer Algorithm

Now that we have seen how the method works with a step-by-step example, we will translate this into a computer algorithm that can be applied to a general *n* × *n* system of equations. We will do this in two steps. First, we’ll replicate the method shown above. Then, we will see how to combine operations to make the method more efficient.

#### 8.3.2.1 Naive Gaussian Elimination Algorithm

Here is a general description of the algorithm that precedes coding it in Python:

1.  Forward pass:
    1.  1.1 Step down through pivot elements (1, 1) through (*n*, *n*)
        1.  1.1.1 Normalize the row of the current pivot element including the constant by dividing by its value.
        2.  1.2.1 Step down through the rows below the current pivot element.
            1.  1.2.1.1 Reduce below the pivot element by multiplying the pivot row by the element in the row below and subtracting from that row. Skip this for the last pivot element (*n*, *n*) since there are no elements below it.
2.  Back-substitution pass
    1.  2.1 Step back up from pivot elements (*n*−1, *n*−1) through pivot (2,2).
        1.  2.1.1 Reduce above the pivot element by multiplying the pivot row by the elements in the row above and subtracting from those.

A Python function that implements this version of Gaussian elimination is shown in [Figure 8.7](#ch08.xhtml_f8_7). The coding is tricky because we must deal with the zero-based indexing of arrays. The first `for` loop uses `range(n)` which creates a list of integers from `0` to `n-1`. This provides the correct range of zero-based subscripts for the pivot elements as the forward pass proceeds. At each pivot level, the next `for` loop, with a `j` index from `i`+`1` to `n-1`, ranges across these columns to normalize row `i` by dividing by the pivot element. Note that it doesn’t divide `A[i, i]` by itself to produce a 1 because that is a trivial calculation, and the pivot element of `A` is never used again. After normalizing the `i`th row of `A`, the `i`th element of `b` is divided by `A[i, i]` so the linear equation relationship is preserved.

![](images/Fig08_07.jpg)

**[FIGURE 8.7](#ch08.xhtml_f8_7b)** Python function `gausselim` that implements naive Gaussian elimination.

After normalizing the pivot row `i` and the corresponding element of `b`, there is a `for` loop with an index `k` that takes on values from `i`+`1` to `n-1`, representing the rows below the pivot row. If the pivot row is already `n-1`, this `for` loop is skipped automatically since its start index is greater than `n-1`. This loop reduces each element below the pivot element to zero from row `i`+`1` to `n-1`. The indented `for` loop ranging `j` from column `i`+`1` to `n-1` subtracts the element in the reduction row times the corresponding `j `column element in the pivot row from the element in the reduction row. It does not carry out the subtraction to create the zero (starts in column `i`+`1`) because we no longer use that element in the algorithm. It then makes the appropriate subtraction for the `b` vector element to maintain the integrity of the linear equation. This completes the forward pass of the algorithm.

The back-substitution pass of the algorithm is then implemented. Here, there is a `for` loop with index i that ranges the pivot index in descending order from row `n-1` to `1`. For each pivot `i`, there is a `for` loop with index `j` that carries out the back-substitution calculation which would create a zero above the pivot and make the corresponding `b` vector calculation. It doesn’t actually calculate the zero because that is trivial and not needed later. When this pass of the algorithm is complete, the `b` vector holds the solution of the set of equations.

You will note that the `gausselim` function is very compact, only 12 executable statements. If we add code to test it with our previous example, this is the result, replicating our manual solution,

```
 import numpy as np

A = np.array([[3., -2., 7.],[-2., 4., -3.],[-1., 9., 4.]])
b = np.array([15., 12., 27.])

x = gausselim(A,b)
print(x)

    [100.33333333 28.66666667 -32.66666667] 
```

After completing and testing a prototype algorithm such as the `gausselim` function, it is good practice to see how it might be made more efficient. By examining the code in [Figure 8.7](#ch08.xhtml_f8_7), we recognize that, in the forward pass, we first divide the pivot row `i` by its pivot value, `A[i,i]`, and then, for the row `k` reduction step, we multiply the pivot row by the element in row `k` below the pivot, `A[k,i]`, and then subtract it from row `k`. If we combine those two factors into one, `A[k,i]/A[i,i]`, we can carry out the reduction step without the need for the normalization step. This reduces the number of computations. Then, during the back-substitution pass, we must recall that the pivot rows were not normalized. We must incorporate the updated `A[i,i]` values then.

#### 8.3.2.2 Adding Determinant Evaluation

In this section, we introduce the matter of the *determinant* of a square matrix and its relationship to Gaussian elimination. If we refer to an earlier example of linear equations,

$\begin{bmatrix} 3 & {- 2} & 7 \\ {- 2} & 4 & {- 3} \\ {- 1} & 9 & 4 \end{bmatrix} \cdot \begin{bmatrix} x_{1} \\ x_{2} \\ x_{3} \end{bmatrix} = \begin{bmatrix} 15 \\ 12 \\ 27 \end{bmatrix}$

we can use the scheme presented in [Figure 8.5](#ch08.xhtml_f8_5) to calculate the determinant of the coefficient matrix.

$\begin{array}{ccl} {\det\left( \mathbf{A} \right)} & = & {\left| \begin{matrix} 3 & {- 2} & 7 \\ {- 2} & 4 & {- 3} \\ {- 1} & 9 & 4 \end{matrix} \right| = 3 \cdot 4 \cdot 4 + \left( {- 2} \right) \cdot \left( {- 3} \right) \cdot \left( {- 1} \right) + \left( {- 2} \right) \cdot 9 \cdot 7} \\ & & {- \left( {7 \cdot 4 \cdot \left( {- 1} \right) + \left( {- 2} \right) \cdot \left( {- 2} \right) \cdot 4 + \left( {- 3} \right) \cdot 9 \cdot 3} \right) = - 84 - \left( {- 93} \right) = 9} \end{array}$

![](images/Fig08_08.jpg)

**[FIGURE 8.8](#ch08.xhtml_f8_8b)** Gaussian elimination function gausselim1 with improvements.

If we go back to our manual application of Gaussian elimination and tabulate the pivot values that were used to normalize the three rows, these were 3, 8/3, and 9/8\. Then, if we calculate the product of these three values, the result is 9, which matches the determinant. By example, this points out that we can compute the determinant of a square matrix via the forward pass of the Gaussian elimination algorithm by accumulating the normalizing factors and computing their product. We incorporate this scheme in our Python functions below.

[Figure 8.8](#ch08.xhtml_f8_8) provides a modified `gausselim1` function that includes these changes.

Testing this function, the script and results are

```
 import numpy as np

A = np.array([[3., -2., 7.], [-2., 4., -3.], [-1., 9., 4.]])
b = np.array([15., 12., 27.])

x, D = gausselim1(A, b)
print(x)
print(D)

[100.33333333 28.66666667-32.66666667]
9.000000000000014 
```

#### 8.3.2.3 Partial Pivoting

As mentioned previously in this chapter, the `gausselim1` function implements *naive Gaussian elimination*. The method has an important flaw. It will fail to solve the following system of equations.

$\begin{bmatrix} 0 & {- 2} & 7 \\ {- 2} & 4 & {- 3} \\ {- 1} & 9 & 4 \end{bmatrix} \cdot \begin{bmatrix} x_{1} \\ x_{2} \\ x_{3} \end{bmatrix} = \begin{bmatrix} 15 \\ 12 \\ 27 \end{bmatrix}$(8.31)

The first step of the method will be to compute the `factor` ratio. This will cause an immediate “divide by zero” error. But the equations do have a solution, so we need a way around this. Practically, we could see that just swapping the first two rows would avoid the zero pivot element. Yes, that would work, and it introduces an important enhancement to our method which is called *pivoting*. The strategy is, at each pivot level, swap the pivot row with the row below it that has the largest absolute value below in that column. If the pivot element is already the largest, no swap occurs.

The pivot strategy can be implemented in modular fashion by creating its own function with arguments of the current `A` and `b` arrays and the current pivot index. That function returns the `A` and `b` arrays with appropriate swapping of rows. The Python code for the modified `gausselimpivot` function and the `pivotswap` function is provided in [Figure 8.9](#ch08.xhtml_f8_9). This modification to the naive `gausselim1` function is simple; just before the normalization, the `pivotswap` function is invoked to rearrange the `A` and `b` arrays, if necessary.

![](images/Fig08_09.jpg)

**[FIGURE 8.9](#ch08.xhtml_f8_9b)** Gaussian elimination function with `pivotswap` function added.

The `pivotswap` function first sets a maximum value as the absolute value of the current pivot element, `Amax`, and a locator index, `imax`, as the current pivot index. Then, through a `for` loop that ranges from the row below the current pivot row, `ipivot`+`1` to `n-1`, the maximum absolute value and location, `imax`, are updated if warranted. Finally, with the `imax` locator in hand, a swap of the `ipivot` and `imax` rows of `A` and `b` is carried out with a `for` loop. If the maximum value is the current pivot location, no swap is implemented.

We can test the `gausselimpivot` function with the previous set of equations with a zero value in the first pivot location.

```
 import numpy as np

A = np.array([[0., -2., 7.], [-2., 4., -3.], [-1., 9., 4.]])
b = np.array([15., 12., 27.])

x, D = gausselimpivot(A, b)
print('Solution is\n', x)
print('Determinant = ', D)

Solution is
 [-7.525 1.075 2.45 ]
Determinant = -120.0 
```

The improved strategy solves the modified system of equations successfully.

#### 8.3.2.4 Detecting Singular and Ill-Conditioned Systems

Adding the pivot swapping strategy to the naive Gaussian elimination algorithm protects against division by zero when a normalization of the pivot row is carried out. However, there is one lingering problem. What will happen if the set of linear equations has no solution? That is, the *n* × *n* **A** matrix is singular indicating that there are not *n* independent linear equations. If this is the situation, the algorithm will get to a point where the pivot element is zero and any elements below it are also zero. It is then unable to normalize the pivot row, and the method fails.

We need to protect against this by providing for an error exit from the `gausselimpivot` function. Also, it is possible that, rather than encountering a zero pivot that can’t be swapped, there is an `Amax` value that is so tiny that the set of equations is “almost” singular, or singular, except for numerical roundoff error. This is called an *ill-conditioning*. We can protect against this by testing the absolute value of the pivot element value, after the pivot swap takes place, against a small value, e.g. 10^(−15), instead of testing if it is identically zero. This code is added to the `gausselimpivot` function in [Figure 8.10](#ch08.xhtml_f8_10).

![](images/Fig08_10.jpg)

**[FIGURE 8.10](#ch08.xhtml_f8_10b)** Gaussian elimination with pivot strategy and protection against singular and ill-conditioned sets of equations.

If the `gausselimpivot1` function is evaluated with a singular system of equations,

$\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix} \cdot \begin{bmatrix} x_{1} \\ x_{2} \\ x_{3} \end{bmatrix} = \begin{bmatrix} 15 \\ 12 \\ 27 \end{bmatrix}$(8.32)

this is the code and the result.

```
 import numpy as np

A = np.array([[1., 2., 3.], [4., 5., 6.], [7., 8., 9.]])
b = np.array([15., 12., 27.])

result = gausselimpivot1(A, b)
if type(result) == str:
    print(result)
else:
    (x, D) = result
    print('Solution is\n', x)
    print('Determinant = ', D) 
```

The result is

```
 system of equations singular or ill-conditioned 
```

Since the return from the `gausselimpivot1` function can be either an error message or two variables, the script evaluates the result to see whether it is a string or not using Python’s `type` function and `str` constant and prints out the corresponding information.

The coefficient array **A** for this example is called a *circular matrix*. Notice the pattern of the elements. Even though it may not be apparent from its elements, a circular matrix of any dimension *n*×*n* is singular.

## 8.4 Solving Sets of Linear Equations with the NumPy linalg Module

Now that we have learned the basics of solving sets of linear equations with Gaussian elimination, we can proceed to employ built-in functions in the NumPy `linalg` module to accomplish the same. Even though we often use built-in functions for numerical tasks, it is always important to underlay these with fundamental knowledge, here provided by our introduction of Gaussian elimination.

In [Chapter 6](#ch06.xhtml_c6), the solution of a set of linear algebraic equations was expressed as

**x** = **A**^(−1) ⋅ **b**(8.35)

Since the `linalg  `module has a function `inv` that computes the inverse of a square matrix, we can use this along with the `dot` method or the `matmul` function to compute the solution. Here is a Python code script that accomplishes this. You can observe that the two methods yield the same result.

```
 import numpy as np

A = np.array([[3., -2., 7.], [-2., 4., -3.], [-1., 9., 4.]])
b = np.array([15., 12., 27.])

Ainv = np.linalg.inv(A)
x = Ainv.dot(b)
print(x)
x = np.matmul(Ainv, b)
print(x) 
```

The result is

```
 [100.33333333 28.66666667-32.66666667]
[100.33333333 28.66666667-32.66666667] 
```

If the number of individual calculations required to solve a set of equations using the matrix inverse is tabulated, it is much greater than for methods like Gaussian elimination. The `linalg` module provides a `solve` function that implements a more sophisticated, efficient algorithm adapted from a software package called LAPACK,[³](#ch08.xhtml_n8_3) where the routines are written in the Fortran 90 programming language. Here is the solution of our example set using the `solve` function.

```
 x = np.linalg.solve(A, b)
print(x)

[100.33333333 28.66666667-32.66666667] 
```

There is a family of functions in the `linalg  `module, most of which are beyond the scope of this text. One that we will illustrate is the `det` function that computes the determinant of a square matrix.

```
 import numpy as np

A = np.array([[3., -2., 7.], [-2., 4., -3.], [-1., 9., 4.]])
DA = np.linalg.det(A)
print(A)

9.000000000000005 
```

We note there is a tiny roundoff error associated with the determinant computation.

## 8.5 Solving Sets of Nonlinear Algebraic Equations

In [Sections 8.3](#ch08.xhtml_h8_3) and [8.4](#ch08.xhtml_h8_4), methods to solve sets of linear algebraic equations were introduced. A characteristic of their solution is that it is a once-through calculation. Given modern computer technology, the solution is rapid. If the equation set is *well-conditioned* (not singular or nearly so, described as ill-conditioned in [Section 8.3](#ch08.xhtml_h8_3)), the methods can solve hundreds of simultaneous equations with relative ease. As we now consider sets of nonlinear algebraic equations, the scenario changes dramatically. First, iterative methods are necessary which require an initial estimate of the solution. Second, a solution may be difficult-to-impossible for sets of more than just a few equations. The first is a characteristic we encountered in [Chapter 7](#ch07.xhtml_c7) for single equations, and the second compounds the difficulty of the task.

Let’s start with a simple example of two nonlinear equations with two unknowns. Later we will generalize it to *n* equations in *n* unknowns.

$\begin{matrix} {x_{1}^{2} + x_{2}^{2} - 4 = 0} \\ {x_{1}x_{2} - 1 = 0} \end{matrix}$(8.36)

For this example, we have the luxury of being able to plot the two equation curves on the *x*[2]–*x*[1] phase plane. This is shown in [Figure 8.11](#ch08.xhtml_f8_11). It is immediately evident that there are four possible solutions to the equations indicated where the lines cross. So, we have a first characteristic of nonlinear equation sets: multiple solutions. If our equations model a physical or chemical phenomenon, it may be possible to restrict the domains of the unknowns so that only one practical solution is found. But our example raises an important question. Which of the four solutions will be obtained for a given set of initial guesses for *x*[1] and *x*[2]? For this example, we will focus on the two solutions in the upper-right quadrant, assuming that negative solutions make no practical sense.

![](images/Fig08_11.jpg)

**[FIGURE 8.11](#ch08.xhtml_f8_11b)** Plot of two nonlinear functions on the *x*[1]–*x*[2] plane.

There are many approaches to the solution of nonlinear algebraic equation sets, and many of those are more complex and sophisticated than we want to introduce here. We will begin by introducing an extension of successive substitution (or fixed-point iteration).

### 8.5.1 Solution of Nonlinear Algebraic Equations by Successive Substitution

Recall the successive substitution method introduced in [Chapter 7](#ch07.xhtml_c7) for the solution of one nonlinear algebraic equation, *x* = *g*(*x*). This is illustrated in [Figure 8.12](#ch08.xhtml_f8_12).

![](images/Fig08_12.jpg)

**[FIGURE 8.12](#ch08.xhtml_f8_12b)** Successive substitution method for the solution of a single nonlinear equation.

Using the two equations introduced above, we can solve the first equation analytically for *x*[1] and the second equation for *x*[2].

$\begin{array}{l} {x_{1} = \pm \sqrt{4 - x_{2}^{2}} = g_{1}\left( x_{2} \right)} \\ {x_{2} = {1/x_{1}} = g_{2}\left( x_{1} \right)} \end{array}$(8.37)

In this form, we can start with an estimated value for *x*[2] and compute the formulas in sequence with new values for *x*[1] and *x*[2] as a result. Then, we can repeat the calculation with the new *x*[2] and, hopefully, after numerous iterations, the process will converge to a solution.

This scheme is illustrated in [Table 8.1](#ch08.xhtml_t8_1) where the + sign in the first formula is used. The solution to five significant figures is obtained in five iterations.

[**TABLE 8.1**](#ch08.xhtml_t8_1b) Successive Substitution Process

| Iteration | *x*[2] | *x*[1] = *g*[1](*x*[2]) | *x*[2] = *g*[2](*x*[1]) |
| --- | --- | --- | --- |
| 1 | 0.5 | 1.93649 | 0.51640 |
| 2 | 0.51640 | 1.93218 | 0.51755 |
| 3 | 0.51755 | 1.93188 | 0.51763 |
| 4 | 0.51763 | 1.93185 | 0.51764 |
| 5 | 0.51764 | 1.93185 | 0.51764 |

Although this scheme converged, just as with successive substitution for a single equation, it is possible that this process will diverge. One way to investigate this is to plot the new *x*[2] = *g*[2](*x*[1]) versus the previous *x*[2] for a range of acceptable *x*[2] values. This is shown in [Figure 8.13](#ch08.xhtml_f8_13). The solution is where that line crosses the dashed 45° line. You can see that the solid curve is very flat compared to the 45° line. As we learned in [Chapter 7](#ch07.xhtml_c7), this is why the convergence is so rapid.

![](images/Fig08_13.jpg)

**[FIGURE 8.13](#ch08.xhtml_f8_13b)** Plot of the new *x*[2] = *g*[2](*x*[1]) versus *x*[2].

It is possible for this scheme, however, to encounter problems. If we choose an initial *x*[2] greater than 2, the square root will be of a negative number yielding a complex result. Even if we choose an initial *x*[2] equal to 2, this will cause a divide by zero in the second formula. Also, we know from [Figure 8.11](#ch08.xhtml_f8_11) that there are four solutions to the equations. Our substitution scheme has only “discovered” one of those solutions. By reversing the formulation of the *g*(*x*) equations to

$\begin{array}{l} {x_{2} = \pm \sqrt{4 - x_{1}^{2}} = g_{1}\left( x_{1} \right)} \\ {x_{1} = {1/x_{2}} = g_{2}\left( x_{2} \right)} \end{array}$(8.38)

the solution flips to equivalent but opposite values for *x*[1] and *x*[2]. If we use the minus sign with the square root, and with appropriate initial estimates, we can determine the solutions in the other quadrant in [Figure 8.11](#ch08.xhtml_f8_11).

The implementation of the successive substitution method in Python is to use our `fixpt` function from [Chapter 7](#ch07.xhtml_c7) directly and formulate the `g` function argument as *g*[2](*g*[1](*x*[2])). The code is shown in [Figure 8.14](#ch08.xhtml_f8_14), and the results displayed in the Console are

```
 x1 = 1.9319
x2 = 0.5176
number of iterations taken = 6 
```

![](images/Fig08_14.jpg)

**[FIGURE 8.14](#ch08.xhtml_f8_14b)** Adaptation of the `fixpt` function to solve two nonlinear equations.

These confirm the solution from [Table 8.1](#ch08.xhtml_t8_1).

It is possible to employ the *Wegstein method* (recall [Section 7.6](#ch07.xhtml_h7_6)) instead of the fixed-point iteration method, especially for scenarios that are naturally divergent. As we encounter larger sets of nonlinear equations, the successive substitution methods become cumbersome, and we look for other methods. A common alternative is an extension of the Newton-Raphson method from [Chapter 7](#ch07.xhtml_c7).

### 8.5.2 The Newton-Raphson Method for Nonlinear Systems of Equations

You should recall from [Section 7.3](#ch07.xhtml_h7_3) that the *Newton-Raphson* iterative formula for a single equation, *f* (*x*) = 0, is

$x^{i + \text{1}} = x^{i} - \frac{f\left( x^{i} \right)}{f'\left( x^{i} \right)}$(8.39)

where *f*′(*x*) is the derivative of *f*(*x*) with respect to *x*, and the formula describes how the (*i*+1)th estimate of *x* is obtained from the *i*th estimate.

To see how we can extend this method to the solution of multiple equations, let’s start with our example from [Figure 8.11](#ch08.xhtml_f8_11):

$\begin{matrix} {x_{1}^{2} + x_{2}^{2} - 4 = 0} \\ {x_{1}x_{2} - 1 = 0} \end{matrix}$(8.40)

We can express these equations in more general form as

$\begin{array}{l} {f_{1}\left( {x_{1},x_{2}} \right) = 0} \\ {f_{2}\left( {x_{1},x_{2}} \right) = 0} \end{array}$(8.41)

By defining the vector quantities,

$\begin{bmatrix} x_{1} \\ x_{2} \end{bmatrix} = \mathbf{x}\begin{bmatrix} f_{1} \\ f_{2} \end{bmatrix} = \mathbf{f}\quad\quad\text{where the latter represent the two equations,}$

we can express the nonlinear equations in the form

**f**(**x**) = **0**(8.42)

So, we would be tempted to rewrite the Newton-Raphson formula as

$\mathbf{x}^{i + \text{1}} = \mathbf{x}^{i} - \frac{\mathbf{f}\left( \mathbf{x}^{i} \right)}{\mathbf{f'}\left( \mathbf{x}^{i} \right)}$(8.43)

but there are two problems with the **f**΄(**x**^(*i*)) term in the formula. First, what is the meaning of the derivative of a vector function, **f**, with respect to a vector variable, **x**? And then, how do we go about dividing that into the vector function, **f**? This just doesn’t work; so we must reinterpret it.

First, since we have in our example two functions and two variables, which indicates we have four possible derivatives:

$\begin{array}{ccl} \begin{bmatrix} \frac{\partial f_{1}}{\partial x_{1}} & \frac{\partial f_{1}}{\partial x_{2}} \\ \frac{\partial f_{2}}{\partial x_{1}} & \frac{\partial f_{2}}{\partial x_{2}} \end{bmatrix} & = & \begin{bmatrix} {\frac{\partial}{\partial x_{1}}\left( x_{1}^{2} + x_{2}^{2} - 4 \right)} & {\frac{\partial}{\partial x_{2}}\left( x_{1}^{2} + x_{2}^{2} - 4 \right)} \\ {\frac{\partial}{\partial x_{1}}\left( x_{1}x_{2} - 1 \right)} & {\frac{\partial}{\partial x_{2}}\left( x_{1}x_{2} - 1 \right)} \end{bmatrix} \\ & = & \begin{bmatrix} {2x_{1}} & {2x_{2}} \\ x_{2} & x_{1} \end{bmatrix} \end{array}$(8.44)

You will note that we have arranged these in matrix form with the first row being the two derivatives of the first function with respect to the two variables and the second row being the two similar derivatives, but of the second function.

In the case that you are not that familiar with *partial derivatives*, we point out that

$\frac{\partial}{\partial x_{1}}( \bullet )$

is the derivative with respect to *x*[1] with *x*[2] treated like a constant, and vice versa for

$\frac{\partial}{\partial x_{2}}( \bullet ).$

Using this scheme, we have shown above how those partial derivatives are derived for our two example equations. This matrix of partial derivatives is called the *Jacobian matrix*, **J**.[⁴](#ch08.xhtml_n8_4)

So now we have a representation of **f**′(**x**) in the form of a matrix, but the second issue, dividing by a matrix, still doesn’t make any sense. The answer here is instead to multiply by the inverse of the matrix, **J**^(−1). This gives us the formula for the Newton-Raphson method for multiple nonlinear equations:

**x**^(*i* + 1) = **x**^(*i*) − **J**^(−1)(**x**^(*i*)) ⋅ **f**(**x**^(*i*))(8.45)

If we write this out in detail for our example equations, we get

$\begin{bmatrix} x_{1}^{i + 1} \\ x_{2}^{i + 1} \end{bmatrix} = \begin{bmatrix} x_{1}^{i} \\ x_{2}^{i} \end{bmatrix} - \begin{bmatrix} {2x_{1}^{i}} & {2x_{2}^{i}} \\ x_{2}^{i} & x_{1}^{i} \end{bmatrix}^{- 1} \cdot \begin{bmatrix} {x_{1}^{2}{}^{i} + x_{2}^{2i} - 4} \\ {x_{1}^{i}x_{2}^{1} - 1} \end{bmatrix}$(8.46)

and you can see that to move from iteration *i* to *i* + 1, we have to compute the inverse of the Jacobian matrix evaluated for the *x* values at iteration *i*.

This formula can be illustrated with our example system of equations, with starting estimates of {0.5, 1.4}. This is shown in [Figure 8.15](#ch08.xhtml_f8_15). After four iterations, the method converges to the solution {0.5176, 1.9319}, and you will recognize this as the intersection in the upper right on [Figure 8.10](#ch08.xhtml_f8_10). If we start with initial estimates reversed, {1.4, 0.5}, the method converges to the solution {1.9319, 0.5176}, the intersection below and to the right of the previous solution. By selecting initial estimates with some forethought, the method will also converge to the solutions in quadrant III in the lower left.

![](images/Fig08_15.jpg)

**[FIGURE 8.15](#ch08.xhtml_f8_15b)** Two iterations of the Newton-Raphson method.

Now that we have seen how to extend the Newton-Raphson method to two nonlinear equations, we can consider the more general case of a set of *n* equations in *n* unknowns. These can be described as follows.

$\begin{matrix} {\begin{matrix} {f_{1}\left( x_{1},x_{2},\ldots,x_{n} \right) = 0} \\ {f_{2}\left( x_{1},x_{2},\ldots,x_{n} \right) = 0} \\ \vdots \\ {f_{n}\left( x_{1},x_{2},\ldots,x_{n} \right) = 0} \end{matrix}} & \left. \Rightarrow\mathbf{f}\left( \mathbf{x} \right) = \mathbf{0} \right. \end{matrix}$(8.47)

As before, you can see that it is convenient to represent the *n* functions as a vector of functions, **f**, in a vector of *n* unknowns, **x**. We can generalize our description of the Jacobian matrix to

$\begin{bmatrix} \frac{\partial f_{1}}{\partial x_{1}} & \frac{\partial f_{1}}{\partial x_{2}} & \cdots & \frac{\partial f_{1}}{\partial x_{n}} \\ \frac{\partial f_{2}}{\partial x_{1}} & \frac{\partial f_{2}}{\partial x_{2}} & \cdots & \frac{\partial f_{2}}{\partial x_{n}} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial f_{n}}{\partial x_{1}} & \frac{\partial f_{n}}{\partial x_{1}} & \cdots & \frac{\partial f_{n}}{\partial x_{n}} \end{bmatrix} = \mathbf{J}\left( \mathbf{x} \right)$(8.48)

The same general formula can then be utilized to attempt to find a solution.

This raises a couple of important points. First, just as in the single-equation Newton-Raphson method, the solution obtained is sensitive to the initial estimates. Second, it is often the case that the method doesn’t converge.

There are two variations of the Newton-Raphson method that merit our consideration. First, when the method diverges and is unsuccessful, a modification of the method’s formula may remedy the situation. This problem may occur because the adjustment made by the term

**J**^(−1)(**x**^(*i*)) ⋅ **f**(**x**^(*i*))

is too ambitious and causes instability and divergence. The modification is to include a “decelerator” factor,[⁵](#ch08.xhtml_n8_5) *d*, a constant between zero and one, in the formula as follows:

**x**^(*i* + 1) = **x**^(*i*) − *d* ⋅ **J**^(−1)(**x**^(*i*)) ⋅ **f**(**x**^(*i*))(8.49)

The value of *d* usually has to be adjusted by trial-and-error. This modification often obtains success where the original formula is unstable and fails.

Next, there are occasions where the partial derivatives in the Jacobian matrix are difficult, or even impossible, to derive analytically. The strategy here is like the modified secant method described in [Section 7.4](#ch07.xhtml_h7_4). In this case, we replace the elements of the Jacobian matrix with numerical approximations. For each element of the Jacobian matrix, we introduce an approximation based on a small variation in the differentiating variable. For example, with our two-equation set, the approximation of the first element of the Jacobian matrix would be

$\frac{\partial f_{1}}{\partial x_{1}} \cong \frac{f_{1}\left( {x_{1} \cdot \left( {1 + \delta} \right),x_{2}} \right) - f_{1}\left( {x_{1},x_{2}} \right)}{x_{1} \cdot \delta} = \frac{\left( {\left( {x_{1} \cdot \left( {1 + \delta} \right)} \right)^{2} + x_{2}^{2} - 4} \right) - \left( {x_{1}^{2} + x_{2}^{2} - 4} \right)}{x_{1} \cdot \delta}$(8.50)

where *δ* is a small number, e.g., 1 × 10^(–6). If we apply this approximation using our initial estimates from above, {0.5, 1.4}, the result is

$\frac{\partial f_{1}}{\partial x_{1}} \cong \frac{\left( {\left( {0.5 \cdot \left( {1 + 10^{- 6}} \right)} \right)^{2} + 1.4^{2} - 4} \right) - \left( {0.5^{2} + 1.4^{2} - 4} \right)}{0.5 \cdot 10^{- 6}} \cong 1.0000005$

Note that our approximation is very close to the true value of the partial derivative: 2*x*[1] = 2·0.5 = 1.0\. We can use similar approximations for the other elements of the Jacobian matrix. Of course, it’s not necessary to use the approximation in this case because the derivatives are readily derived.

A Python function, `multinewt`, that implements the multivariable Newton-Raphson method is presented in [Figure 8.16](#ch08.xhtml_f8_16). The following Python script solves our example equation set using this function.

```
 import numpy as np

def f(x):
    fn = np.zeros(2)
    fn[0] = x[0]**2 + x[1]**2 - 4
    fn[1] = x[0]*x[1] -1
    return fn

def J(x):
    Jac = np.zeros((2,2))
    Jac[0,0] = 2*x[0]
    Jac[0,1] = 2*x[1]
    Jac[1,0] = x[1]
    Jac[1,1] = x[0]
    return Jac

x0 = np.array([0.5, 1.4])
xsoln,niter = multinewt(f,J,x0)
print(xsoln)
print(niter) 
```

![](images/Fig08_16.jpg)

**[FIGURE 8.16](#ch08.xhtml_f8_16b)** Python function `multinewt` to solve sets of nonlinear algebraic equations.

and the results displayed in the Console are

```
 [0.51763809 1.93185165]
4 
```

Observe that the code for the `multinewt` function is compact, only 12 statements. It relies on the user supplying two functions, `f` and `J`, that compute and return the equation residuals, the `f`’s, and the Jacobian matrix, `J`, for a given set of `x`’s. The function has an `x0` argument for the initial estimates and then keyword arguments for the relative error, `ea`, the maximum iterations allowed, `maxiter`, and the deceleration factor, `decel`. The latter is assigned a default value of one – meaning no deceleration.

The error criterion is compared to the sum of the squares of the differences between the *x*’s this iteration and those from the previous iteration. This is computed as the `dot` product of the `xdev` array with itself. The keyword arguments can be respecified when the function is invoked; otherwise, the default values are used. The function returns the latest solution estimates and the number of iterations taken. If the latter is equal to `maxiter`, that means the method did not converge.

## 8.6 Use of the root Function from the SciPy optimize Module to Solve Nonlinear Equations

There is a built-in function in the SciPy `optimize` submodule, `root`, which provides a more sophisticated approach to solving sets of nonlinear equations. The user can select from seven different methods with a `method` argument. The default is a modified Powell hybrid method adapted from a library of routines called MINPACK ([Moré, Garbow, and Hillstrom, 1980](#ch11_ref.xhtml_r10)). We do not go into the details of this method here. The simplest syntax for using the `root` function is

```
 xsoln = root(f, x0) 
```

where `f` is a function that computes the equation functions for a given set of `x` values, and `x0` is a set of initial estimates for the `x`’s.

It is also possible to pass additional arguments through to the `f` function using an `args(...)` argument. The `root` function doesn’t require us to supply a function for the Jacobian, although it is possible to do so.

The Python script below uses the `root` function to solve the example system illustrated in [Figure 8.11](#ch08.xhtml_f8_11).

```
 import numpy as np
from scipy.optimize import root

def f(x):
    fn = np.zeros(2)
    fn[0] = x[0]**2 + x[1]**2 - 4
    fn[1] = x[0]*x[1] -1
    return fn

x0 = np.array([0.5, 1.4])
result = root(f,x0)
print(result)
print('\nSolution is: \n',result.x) 
```

The `root` function returns a `result` object with various attributes. One is `x`, which provides the solution. In the code above, both the complete object `result` and the solution only as `result.x` are displayed separately in the Console.

```
 fjac: array([[-0.47905266, -0.87778616],
       [ 0.87778616, -0.47905266]])
     fun: array([4.85922413e-12, 1.98183692e-11])
 message: 'The solution converged.'
    nfev: 11
     qtf: array([2.56353178e-09, 6.57163450e-10])
       r: array([-2.12867493, -1.97061865, 3.23224566])
  status: 1
 success: True
       x: array([0.51763809, 1.93185165]) 
```

The solution is:

```
 [0.51763809 1.93185165] 
```

In the output above, you will note an `fjac` array displayed. This is the numerical approximation to the Jacobian that the `root` function produced at the solution. It also displays the final function evaluations as `fun`, very close to zero. The number of iterations (or `f` evaluations), `nfev`, is 11\. The output indicates that the method was successful. The solution matches that which we obtained with our `multinewt` function but requires 11 iterations instead of 4. To be fair, the error tolerance for `root` is tighter than that for `multinewt`, and we provided the Jacobian matrix for the latter.

Although the `root` function is convenient to use, it is very much a “black box” when it comes to its internal operations. Since Python is an open-source language, you can obtain the source code for `root`, but that is over 600 lines and likely would require too much time to fathom for most typical Python users. The `multinewt  `function works well for many applications and has the advantage of simplicity. Also, its method is out in the open and can by well understood by the user. You will often have to make a choice between a home-grown function and one that is built-in with Python. You can even use both to confirm your results. It is a choice that engineers and scientists must make frequently in problem solving.

## Problems

1.  **8.1** Given the system of equations

    $\begin{array}{r} {- 3x_{2} + 7x_{3} = 4} \\ {x_{1} + 2x_{2} - x_{3} = 0} \\ {5x_{1} - 2x_{2} = 3} \end{array}$

    Compute the following manually. For parts **(b)** and **(c)**, check your solutions in the equations.

    1.  Compute the determinant of the coefficient matrix.
    2.  Solve the system of equations using Cramer’s rule.
    3.  Solve the system of equations using Gaussian elimination with pivoting.
2.  **8.2** Solve the following system of equations by hand using naive Gaussian elimination. Check that your answers satisfy the equations.

    $\begin{matrix} {8x_{1} + 2x_{2} + 3x_{3}} & = & 30 \\ {x_{1} - 9x_{2} + 2x_{3}} & = & 1 \\ {2x_{1} + 3x_{2} + 6x_{3}} & = & 31 \end{matrix}$

3.  **8.3** Solve the following system of equations, shown in vector/matrix form, by hand using Gaussian elimination with pivoting. Check your answers by substituting them in the equations. Using information from your solution steps, compute the determinant.

    $\begin{bmatrix} 4 & 3 & {- 1} \\ 7 & {- 2} & 3 \\ 5 & {- 18} & 13 \end{bmatrix}\mathbf{x} = \begin{bmatrix} 6 \\ 9 \\ 3 \end{bmatrix}$

4.  **8.4** Use the `gausselimpivot1` function to solve the following system of equations. Report your solutions to four significant figures. Write Python code to test your solutions in the equations and comment on any roundoff errors.

    $\begin{array}{r} {- 0.083x_{1} - 0.875x_{2} + 0.645x_{3} + 0.675x_{4} = 62.1} \\ {- 0.258x_{1} - 0.730x_{2} + 0.898x_{3} - 0.797x_{4} = 91.8} \\ {0.262x_{1} - 0.467x_{2} + 0.251x_{3} - 0.127x_{4} = 74.9} \\ {0.582x_{1} + 0.025x_{2} - 0.907x_{3} + 0.362x_{4} = 130.9} \end{array}$

5.  **8.5** A special matrix called the *Hilbert matrix* is famous for being ill-conditioned. Its form used in the following four equations in four unknowns is

    $\begin{bmatrix} 1 & {1/2} & {1/3} & {1/4} \\ {1/2} & {1/3} & {1/4} & {1/5} \\ {1/3} & {1/4} & {1/5} & {1/6} \\ {1/4} & {1/5} & {1/6} & {1/7} \end{bmatrix}\mathbf{x} = \begin{bmatrix} 2 \\ {9/7} \\ 1 \\ {3/4} \end{bmatrix}$

    1.  Write Python code to compute the determinant of the coefficient matrix. What do you observe?
    2.  Write Python code to solve the system of equations using the `inv` function from the NumPy `linalg` module.
    3.  Write Python code to solve the system of equations using the `solve` function from the NumPy `linalg` module and compare your results to those from part **(b)**. What do you conclude are the true solutions to these equations?
6.  **8.6** A production process for three different electronic components uses three materials: copper, polystyrene, and neoprene. The amounts of these materials required to produce each component are presented in the table below.

    | Component | Amount Required per Component |
    | --- | --- |
    | Copper (g) | Polystyrene (g) | Neoprene (g) |
    | --- | --- | --- |
    | A | 15 | 3 | 1.2 |
    | B | 17 | 4 | 1.5 |
    | C | 19 | 5.5 | 1.9 |

    If 98.5 kg of copper, 23.6 kg of polystyrene, and 8.77 kg of neoprene are available, how many of each component can be produced? Solve this problem using a Python script. Round your results down to the nearest integer since we are dealing with discrete components.

7.  **8.7** [Figure P8.7](#ch08.xhtml_fP8_7) described a bridge support or truss structure. The equations that determine the truss are horizontal and vertical force balances at the seven nodes. For example, at node 2,

    ![](images/Fig08P_07.jpg)

    **[FIGURE P8.7](#ch08.xhtml_fP8_7b)** Bridge support truss structure.

    $\begin{matrix} {h_{2} + f_{4} + \overline{s}f_{3} - \overline{s}f_{1} = 0} \\ {v_{2} + \overline{c}f_{1} + \overline{c}f_{3} = 0} \end{matrix}$

    where *h*[i]: horizontal load applied at node *i*, positive to the right*v*[i]: vertical load applied at node *i*, positive downward*f*[j]: force in member *j*, negative for compression, positive for tension$\overline{s}$: sin 30°

    $\overline{c}$: cos 30°

    The unknowns in the above equations are the member forces and the knowns are the loads. Write a Python script that determines the member forces in this truss.

8.  **8.8** The diagram presented in [Figure P8.8](#ch08.xhtml_fP8_8) describes an electrical circuit comprised of resistors. You are to develop a Python script that solves for the voltages at nodes 2, 3, 6, and 7, and solves for the currents in all branches of the circuit. The values of the resistances in ohms are given in the table below:

![](images/Fig08P_08.jpg)

**[FIGURE P8.8](#ch08.xhtml_fP8_8b)** Electrical circuit comprised of resistors.

| *R*[12] | 60 | *R*[13] | 60 | *R*[15] | 10 |
| *R*[56] | 50 | *R*[57] | 50 | *R*[67] | 10 |
| *R*[23] | 10 | *R*[24] | 50 | *R*[34] | 50 |
| *R*[36] | 75 | *R*[68] | 60 | *R*[78] | 60 |
| *R*[48] | 20 |  |  |  |  |

There are two electrical laws that give rise to the equations necessary to solve this circuit.

(1) *Ohm’s Law* states that the current through a resistive branch is proportional to the voltage across the branch and inversely proportional to the resistance of the branch. For the diagram below,

| ![](images/un08_01.jpg) | and | *i*[*A*] = *i*[*B*] + *i*[*C*] |

(2) *Kirchhoff’s Law* states that the sum of currents at a node must be equal to zero. For the diagram below,

| ![](images/un08_02.jpg) | and | $i_{AB} = \frac{V_{A} - V_{B}}{R_{AB}}$ |

By writing node equations (Kirchhoff’s law) for nodes 2, 3, 6, and 7, and substituting Ohm’s Law relationships for the currents in the equations, one can develop a set of four linear equations in four unknowns, the voltages at the nodes. These equations are solved; then, with the voltages known, Ohm’s Law can be used to compute currents for all 16 branches in the circuit.

1.  **8.9** For the following system of nonlinear equations,

    $\begin{matrix} {x_{1}^{2} + 3x_{2}^{2} - 5 = 0} \\ {x_{1}^{2} - x_{2} - 1 = 0} \end{matrix}$

    1.  Employ successive substitution to obtain a solution. Use initial estimates *x*[1] = *x*[2] = 1.5.
    2.  Solve the equations using the multivariable Newton-Raphson method with the same initial estimates.

        Use Python scripts to solve this problem.

2.  **8.10** Solve the following set of nonlinear equations,

    $\begin{matrix} {x_{1}^{2} - x_{1} + x_{2} - 0.75 = 0} \\ {x_{1}^{2} - 5x_{1}x_{2} - x_{2} = 0} \end{matrix}$

    1.  using the multivariable Newton-Raphson method, and
    2.  using the `root` function from the SciPy `optimize` submodule. Use a phase plot (*x*[2] vs. *x*[1]) of the two equations to determine suitable initial estimates.
3.  **8.11** Solve the following set of nonlinear equations to determine positive roots.

    $\begin{matrix} {x_{1}^{2} - x_{2} + 1 = 0} \\ {2\cos\left( x_{1} \right) - x_{2} = 0} \end{matrix}$

    1.  using successive substitution,
    2.  using the multivariable Newton-Raphson method and
    3.  using the `root` function from Python’s SciPy `optimize` submodule. Use a phase plot (*x*[2] vs. *x*[1]) of the two equations to determine suitable initial estimates.
4.  **8.12** The following chemical reactions take place in equilibrium at a fixed temperature and pressure.

    $\begin{matrix} \left. 2A\text{+}B\,\,\,\rightleftarrows\,\,\, C \right. \\ \left. A\text{+}D\,\,\,\rightleftarrows\,\,\, C \right. \end{matrix}$

    The equilibrium of each reaction is described in terms of concentrations of the reactants and two equilibrium constants, *K*[1] and *K*[2].

    $K_{1} = \frac{c_{c}}{c_{a}^{2}c_{b}}K_{2} = \frac{c_{c}}{c_{a}c_{d}}$

    If *x*[1] and *x*[2] represent the number of moles of C that are produced by the first and second reactions, respectively, reformulate the equilibrium relationships based on the initial concentrations of the constituents before equilibrium is established. For example,

    1.  *c*[c] = *c*[c,0] + *x*[1] and *c*[a] = *c*[a,0] – 2*x*[1] – *x*[2]

    Solve the resulting nonlinear algebraic equations for the following parameter values:

    1.  *K*[1] = 4 × 10^(–4), *K*[2] = 3.7 × 10^(–2), *c*[a,0] = 50, *c*[b,0] = 5, *c*[c,0] = 0, and *c*[d,0] = 10.
    1.  Use the multivariable Newton-Raphson method to solve for *x*[1] and *x*[2].
    2.  Use the `root` function from the Python SciPy `optimize` submodule to solve the equations and compare to your results from **(a)**.

# 9 Solving Differential Equations

DOI: [10.1201/9781003256861-9](https://doi.org/10.1201/9781003256861-9)

## Chapter Objectives

*   Become familiar with the different forms of differential equations encountered by engineers and scientists.
*   Be able to recognize differential equations that can be solved numerically by the methods of quadrature (finding the area under the curve).
*   Introduce the trapezoidal rule method for solving quadrature problems and the `quad` function from the SciPy `integ``rate` module.
*   Understand how to solve a differential equation with the Euler method.
*   Appreciate the limitations of the Euler method when it comes to the accuracy of the solution.
*   See how the Heun method is an improvement in accuracy over the Euler method.
*   Understand how to extend the methods to the solution of multiple differential equations.
*   Be able to transform a second-order differential equation into two first-order equations and solve the resulting system.
*   See how to use the `solve _ ivp` function from the SciPy `integrate` module to solve one or several differential equations.

The ability of scientists and engineers to model rates of change is critically important. Equations that describe rates of change are also called differential equations because they involve derivatives. Most engineering and science students take a course in differential equations, typically in their second year, and this course emphasizes analytical solution of these equations. Whereas this is important, many, and perhaps most, differential equations that arise from modeling physical and chemical phenomena cannot be solved by analytical methods, and a numerical approach is required.

As you will learn in this chapter, it is possible to employ elementary numerical methods to solve equations that describe rates of change prior to understanding the analytical aspect of these equations. Eventually, it will be important to learn and appreciate the latter, but that doesn’t prevent us from moving forward now.

First, we need to recognize the different forms that differential equations take and how the form will dictate the method we use to solve them. Next, the methods that compute the “area under the curve,” called quadrature, will be introduced. We will also see how to solve these problems using the `quad` function from the SciPy `integrate` module. When the rate of change of a variable depends on the variable itself, another class of methods is required, and we will introduce the most elementary of these, the Euler method. By studying the limitations of this method, we will see that improvements are possible and introduce an enhancement, called Heun’s method.

The numerical methods we study first are designed for a single differential equation with one first-order derivative. We will extend these methods to systems of multiple differential equations. Also, equations arise in modeling physical and chemical phenomena that have second-order and even higher-order derivatives. Decomposing these equations into a system of first-order equations will be illustrated with a second-order differential equation as the example. Finally, we will demonstrate how to use a built-in Python function, `solve _ ivp`, to solve single or multiple differential equations.

## 9.1 Describing Differential Equations

Differential equations model rates of change; in fact, in some circles they have been called *rate equations*. A simple form of a differential equation is

$\frac{dy}{dt} = f\left( {y,t} \right)y(0) = y_{0}$(9.1)

Here, *y* is a dependent variable, such as position, temperature, pressure, and *t* is an independent variable, such as time, *t*, here, or location, *x*. In the case of time, an initial value of *y* is required at *t* = 0\. In this case, we want to develop a solution in the form of *y* versus *t* up to a final *t* = *t*[f].

When the rate of change of *y* only depends on time, a simpler version of the above equation is

$\frac{dy}{dt} = f(t)y(0) = y_{0}$(9.2)

where *y*[0] = is the initial value of *y*. We are interested in the result of the integral form

∫[*y*[0]]^(*y*)*d**y* = *y* − *y*[0] = ∫[0]^(*t*[*f*])*f*(*t*)*d**t*(9.3)

The integral result corresponds to finding the area under the *f*(*t*) curve, a procedure called *quadrature*. A variation of this scenario is given by

$\frac{dy}{dt} = y\, f(t)y(0) = y_{0}$(9.4)

This equation, called *separable*, can be reformulated as

${\int_{y_{0}}^{y}\frac{dy}{y}} = \ln\left( \frac{y}{y_{0}} \right) = {\int_{0}^{t_{f}}{f(t)dt}}\,$(9.5)

The right side of this equation still conforms to finding the area under the *f*(*t*) curve from 0 to *t*[f].

Another common scenario is where the rate of change is influenced by another variable, called an input or *forcing variable*, *w*. This would be described as

$\frac{dy}{dt} = f\left( {y,w,t} \right)y(0) = y_{0}w = g(t)$(9.6)

The two differential equation forms in Equations 9.1 and 9.6 can be pictured in *block diagrams*. See [Figure 9.1](#ch09.xhtml_f9_1). The diagrams introduce the concept of solving the differential equations using an integration method. Since the solution requires *y*[0] to “get off the ground,” these scenarios are called *initial value problems* (IVPs). We will see in this chapter how the solver takes the derivative at a given time, *t*, and computes an approximate value of *y* at *t* + Δ*t*. This process is repeated until a desired final time, *t*[f].

![](images/Fig09_01.jpg)

**[FIGURE 9.1](#ch09.xhtml_f9_1b)** Initial value differential equations without and with an input variable.[¹](#ch09.xhtml_n9_1)

Through developing mathematical models of many physical and chemical systems, we also encounter *second derivatives*. A common example is Newton’s Second Law: *F* = *ma*, which describes the acceleration, *a*, of an object of mass, *m*, when subjected to a force, *F*. For one dimensional motion, acceleration can be represented as the second derivative of position (*a* = *d*²*x*/*dt*²). Therefore, the Second Law can be expressed as a differential equation:

$m\frac{d^{2}x}{dt^{2}} = F$(9.7)

This relationship can be combined with models for spring force (Hooke’s Law) and friction to produce the differential equation for the shock absorber system shown in [Figure 9.2](#ch09.xhtml_f9_2). The motion of the mass, *m*, is governed by its own inertia, the second derivative term, a frictional force proportional to the velocity (*v* = *dx*/*dt*) described by the coefficient, *b*, and the forces provided by the two springs proportional to their displacement from their rest positions (*Hooke’s Law*).

![](images/Fig09_02.jpg)

**[FIGURE 9.2](#ch09.xhtml_f9_2b)** Shock absorber system with second-order differential equation model.

A block diagram for this system ([Figure 9.3](#ch09.xhtml_f9_3)) illustrates that it is necessary to integrate twice, once to get the velocity from the acceleration, and a second time to obtain the position from the velocity. It also shows that two initial conditions are required and denotes the constant parameter values that must be supplied. This is called an *information flow diagram*, and it is helpful in organizing and visualizing differential equation models, especially those that are more complex.

![](images/Fig09_03.jpg)

**[FIGURE 9.3](#ch09.xhtml_f9_3b)** Block diagram of differential equation model for a shock absorber.

A common misconception that arises from studying the diagram is that the velocity and position are required to obtain the acceleration, but the acceleration is required to obtain the velocity and then the position. However, this is *not* the case here. This is because the nature of solving the differential equation is to approximate the solution at time *t* + Δ*t* from values of *x* and *dx*/*dt* at time *t*. Described in a different way, the system is not implicit as long as the information flow passes through an integrator.

You will also note that, in effect, we have broken down the second-order differential equation into two first-order integrations with an intermediate variable, the velocity (*dx*/*dt*). We will discuss this further in [Section 9.3.3](#ch09.xhtml_h9_3_3). Also, because our original equation includes a second derivative, we require two initial conditions.

Many problem contexts evolve mathematical models with more than one differential equation. An example would be the following two equations:

$\begin{matrix} \begin{array}{l} {\frac{dx_{1}}{dt} = - 2x_{1}^{2} + 2x_{1} + x_{2} - 1x_{1}(0) = 2} \\ {\frac{dx_{2}}{dt} = - x_{1} - 3x_{2}^{2} + 2x_{2} + 2x_{2}(0) = 0\quad\quad 0 \leq t \leq 2} \end{array} \end{matrix}$(9.8)

As before, these equations can be depicted in a block diagram. See [Figure 9.4](#ch09.xhtml_f9_4). It is easy to see that the two equations are interdependent. In other words, they are coupled − we must solve them simultaneously.

![](images/Fig09_04.jpg)

**[FIGURE 9.4](#ch09.xhtml_f9_4b)** Information flow diagram for two coupled differential equations.

Equations that involve only one independent variable are called *ordinary differential equations* (ODEs). Although we do not consider them here, it is worth mentioning differential equations that involve more than one independent variable, which are called *partial differential equations* (PDEs). You will likely encounter these later in your engineering or science education, and should you take a course in numerical methods, their solution will be a topic covered. In the coming sections of this chapter, we will consider numerical solutions of the ordinary differential equations discussed to this point.

## 9.2 Quadrature – Finding the Area under the Curve

There are two common scenarios that present the situation described by Equations 9.2 and 9.3\. The first is when *f*(*t*) is an analytical expression. In this case, values of *f*(*t*) are available at any value of *t*. The second is where *f*(*t*) is represented by experimental data taken at *n* discrete values of *t*; that is, {*f*(*t*[i]), *i* = 1, . . ., *n*}. [Figure 9.5](#ch09.xhtml_f9_5) illustrates examples of these two scenarios. When experimental data are involved, they may contain random error, which is evident in the (*b*) plot. The fact that the experimental data are only available at given values of the independent variable makes the quadrature task more difficult. We will consider both in this section.

![](images/Fig09_05.jpg)

**[FIGURE 9.5](#ch09.xhtml_f9_5b)** Examples of the two scenarios for quadrature: (a) a continuous function and (b) experimental data.

### 9.2.1 Pre-computer Methods

Historically, before the advent of computer methods, calculating the areas under curves or within closed boundaries was a common activity. There were several curious methods used.

1.  *Counting the squares method*. Here, we count the squares that are completely below the curve ([Figure 9.5a](#ch09.xhtml_f9_5)). Then, we count the squares that are below and at least partially above the curve. Finally, we take the average of the two and apply the dimensions of the squares to produce an estimate of the area. For [Figure 9.5a](#ch09.xhtml_f9_5), the result is (21  +  34)/2  ×  (0.2 × 0.1)  =  0.55.
2.  *Weighing the curve method*. In this method, with the curve plotted on paper, we carefully cut out the area under the curve in [Figure 9.5a](#ch09.xhtml_f9_5). Then, we cut out a known rectangular area. Both are weighed on an analytical balance, and, using the rectangle’s weight as a calibration standard, the area under the curve is computed.2[²](#ch09.xhtml_n9_2)
3.  *Cartographer’s planimeter method*. This curious device is shown in [Figure 9.6](#ch09.xhtml_f9_6). One traces carefully around a closed curve in a clockwise direction, and the dial on the planimeter arm shows the area. Then, the procedure is repeated but in the counterclockwise direction. The two results are then averaged. Since the planimeter returns the result as a dimensional area (e.g. cm²), a calibration rectangle is required here too. The planimeter has been in use since 1854 and is still employed today. Its common application is finding irregular areas on maps (also becoming obsolete because of geographical information systems and supporting software), but it can be used to find areas under curves as well.![](images/Fig09_06.jpg)

    **[FIGURE 9.6](#ch09.xhtml_f9_6b)** Polar planimeter.[³](#ch09.xhtml_n9_3) (From Polar planimeter 01—Planimeter. [https://en.wikipedia.org/wiki/Planimeter](https://en.wikipedia.org). (Last edited date June 18, 2022).)

The first computer-based method we introduce is akin to the “counting the squares” method above. [Figure 9.7](#ch09.xhtml_f9_7) illustrates two versions of this method. For the continuous, *f*(*t*), scenario, it is based on discretizing the function. This is usually done by choosing a single Δ*t* value for the entire *t* domain; however, it is possible to choose different Δ*t*’s based on the extent of the curvature. This method is called *rectangular integration* or rectangular quadrature.

![](images/Fig09_07.jpg)

**[FIGURE 9.7](#ch09.xhtml_f9_7b)** Rectangular quadrature using (a) the initial value or (b) the final value of the interval.

As the figure illustrates, the two methods either underestimate or overestimate the area depending on whether the curve is ascending or descending. Hence, the two estimates could be implemented and averaged to obtain a superior estimate.

You can also see that, as we decrease Δ*t*, the error of the area estimate will decrease. Since we have an analytical function, it is feasible to adjust the interval in this fashion. With experimental data ([Figure 9.5b](#ch09.xhtml_f9_5)), we do not have that luxury. A logical step would be to take the average of the two area estimates shown in [Figure 9.7](#ch09.xhtml_f9_7). That leads us to the most common, elementary quadrature method, *trapezoidal rule*.

### 9.2.2 Quadrature for Continuous Functions

Rather than choosing the initial or final value of the interval and computing the area of the rectangle below that point, computing the area of a trapezoid with vertices at the initial and final values will provide a more accurate estimate. This is shown in [Figure 9.8](#ch09.xhtml_f9_8). As you can see from the formula, this is equivalent to computing the area of a rectangle where the height is the average of the initial and final values. In fact, it is equivalent to averaging the results of the initial and final value methods of rectangular quadrature! So, it is a more efficient version of averaging the two results shown in [Figure 9.7](#ch09.xhtml_f9_7). The formula in [Figure 9.8](#ch09.xhtml_f9_8) is commonly referred to as the *trapezoidal rule*.

![](images/Fig09_08.jpg)

**[FIGURE 9.8](#ch09.xhtml_f9_8b)** Computing the trapezoidal area for two points on the curve.

Given the scheme and formula in [Figure 9.8](#ch09.xhtml_f9_8), we can develop a simple Python function, `trap1`, to implement the method across a domain, *a* ≤ *t* ≤ *b*, divided into *n* equal intervals. This function is shown in [Figure 9.9](#ch09.xhtml_f9_9). We can apply this function to compute the integral

![](images/Fig09_09.jpg)

**[FIGURE 9.9](#ch09.xhtml_f9_9b)** Python function `trap1` for trapezoidal rule quadrature.

*y* = ∫[0]^(*π*/2)*t* cos (*t*)*d**t*(9.9)

This is the area under the curve shown in [Figure 9.5a](#ch09.xhtml_f9_5). Here is the outcome of applying `trap1` to this equation,

import numpy as np

```
 import numpy as np
def f(t):
return t*np.cos(t)
y = trap1(f, 0., np.pi/2)
print(y)
0.5705516230802059
```

In one sense, this isn’t a particularly good example because the integral can be derived analytically using integration by parts to be

∫[*a*]^(*b*)*t* cos (*t*)=cos (*b*) + *b* sin (*b*) − cos (*a*) − *a* sin (*a*)(9.10)

For *a* = 0 and *b* = *π*/2, this evaluates to 0.5707963267948966\. An advantage here is that we can use the analytically based result to verify and evaluate the trapezoidal rule result. The percentage error is 0.04%. If we used a higher value for *n*, the error would be less; however, we cannot do that without a limitation on how small we can make the size of *h* as the precision of calculations and round-off error would intervene. We will explore this thought in the end-of-chapter Problem 9.14.

The `trap1` function is very compact, only nine statements. However, it is not the most efficient way to code trapezoidal rule. If we consider the repeated use of the formula in [Figure 9.8](#ch09.xhtml_f9_8), this can be represented as

$\begin{array}{l} {\frac{f(a) + f\left( {a + h} \right)}{2}\, h + \frac{f\left( {a + h} \right) + f\left( {a + 2h} \right)}{2}\, h + \cdots} \\ {\quad + \frac{f\left( {b - 2h} \right) + f\left( {b - h} \right)}{2}\, h + \frac{f\left( {b - h} \right) + f(b)}{2}\, h} \end{array}$9.11

where *h* is the interval width.

There are two features of Equation 9.11 that bear mention. First, each term is multiplied by *h* and divided by 2, and we can factor these out and apply them only once. Second, all the *f* terms enter twice, except the first and last term. This allows us to simplify the repeated application of trapezoidal rule to the formula

$\left( {f(a) + 2f\left( {a + \Delta t} \right) + 2f\left( {a + 2\Delta t} \right) + \cdots + 2f\left( {b - 2\Delta t} \right) + 2f\left( {b - \Delta t} \right) + f(b)} \right)\frac{h}{2}$(9.12)

perhaps a better representation consistent with the code would be:

$\left( {f(a) + 2f\left( {a + \Delta t} \right) + 2f\left( {a + 2\Delta t} \right) + \cdots + 2f\left( {a + (n - 1)\Delta t} \right) + f(b)} \right)\frac{h}{2}$

and we can modify our `trap1` function to make it more efficient. See the new `trap` function in [Figure 9.10](#ch09.xhtml_f9_10).

![](images/Fig09_10.jpg)

**[FIGURE 9.10](#ch09.xhtml_f9_10b)** Modified trapezoidal rule function `trap`.

If we evaluate this new function with similar code to that for the `trap1` test, the result is

```
 0.5707434665276926
```

and the error when compared to the analytical result is 0.009%, somewhat better than the previous result.

There is an important general lesson here. We often develop Python scripts and functions to accomplish given numerical tasks. The first time through, we should consider these as prototypes, and later, seek ways to improve them in their efficiency, compactness, and clarity.

It is worth mention that there are other methods available for quadrature. Instead of using two points and the enclosed trapezoid, one could use three points and an area under a quadratic equation that passes through those points. That method is called Simpson’s 1/3 Rule. We do not take the time here to introduce that method or others. If you take a course in numerical methods, you will encounter these. However, it is important to note that the simple trapezoidal rule method with appropriate intervals is adequate for many applications.

### 9.2.3 The quad Function from SciPy’s integrate Module

Before we consider quadrature of experimental data, Python’s SciPy module has an `integrate` submodule with functions that perform quadrature. The `quad` function accommodates the integration of analytical functions. Here is the Python script and result for the integral shown in Equation 9.9.

```
 import numpy as np
from scipy.integrate import quad
f = lambda t: t
a = 0
b = np.pi/2
y, ey = quad(f, a, b)
print(y)
0.5707963267948966
```

The result here is indistinguishable from the analytical solution result. An advanced method is used by the `quad` function. You can read more about the function in the SciPy User Guide ([https://docs.scipy.org/doc/scipy/tutorial/index.html](https://docs.scipy.org/)) as well as numerical methods texts such as Chapra and Clough (2022).

### 9.2.4 Quadrature for Discrete Data

The second scenario for quadrature is when, rather than an analytical function, *f*(*t*), we have a set of experimental data, {*y*[i], *x*[i], *i* = 1, *n*}, as illustrated in [Figure 9.5b](#ch09.xhtml_f9_5). As in the figure, it is common that the data are not measured at a constant interval. This requires a modification of the formula in [Figure 9.8](#ch09.xhtml_f9_8):

$Area = \frac{f\left( t_{i + 1} \right) + f\left( t_{i} \right)}{2}\,\left( {t_{i + 1} - t_{i}} \right)$(9.16)

Following this change, we can modify the `trap` function to create a `trapdata` function as shown in [Figure 9.12](#ch09.xhtml_f9_12). We can write a Python script to estimate the quadrature of the data that produced [Figure 9.5b](#ch09.xhtml_f9_5).

![](images/Fig09_12.jpg)

**[FIGURE 9.12](#ch09.xhtml_f9_12b)** Function for trapezoidal rule method with experimental data.

```
 import numpy as np
t = np.array([0.09,0.32,0.69,1.51,2.29,3.06,3.39,3.63,3.77])
y = np.array([15.1,57.3,103.3,174.6,191.5,193.2,178.7,172.3,167.5])
A = trapdata(t, y)
print(A)
570.134
```

There is also a function, `trapz`, in the SciPy `integrate` submodule that performs the same task as our `trapdata` function. Here is a Python script to duplicate the above calculations and result.

```
 import numpy as np
from scipy.integrate import trapz
t = np.array([0.09,0.32,0.69,1.51,2.29,3.06,3.39,3.63,3.77])
y = np.array([15.1,57.3,103.3,174.6,191.5,193.2,178.7,172.3,167.5])
A = trapz(y, t)
print(A)
570.134
```

You can see that the result is the same.

An alternate approach for quadrature of data is to estimate or “fit” an analytical model to the data. Although we won’t go into the process for doing that in this chapter, assume that the following model has been proposed to fit the data above.

*y* = 4.351 *t*³ − 53.88 *t*² + 185.6 *t* + 0.559

If we add this curve to the plot from [Figure 9.5b](#ch09.xhtml_f9_5), the result is shown in [Figure 9.13](#ch09.xhtml_f9_13).

![](images/Fig09_13.jpg)

**[FIGURE 9.13](#ch09.xhtml_f9_13b)** Experimental data with model curve.

Given the model and observing that it fits the data well, we can use our `trap` function to implement the quadrature. Here is the Python script and the result.

import numpy as np

```
 A = trap(f, 0.09,3.77)
print(A)
def f(t):
return 4.351*t**3-53.88*t**2 + 185.6*t + 0.559
577.640263867974
```

The result is close to the previous one, differing by 1.3%.

We will now leave the topic of quadrature and proceed to differential equations that are not separable.

## 9.3 Solving Differential Equations with Initial Conditions

The general form of the differential equation, as represented in Equation 9.1, repeated here, is

$\frac{dy}{dt} = f\left( {y,t} \right)y(0) = y_{0}$(9.1)

This formulation includes terms in the dependent variable, *y*, on the right side of the equation in *f*(*y*, *t*). The quadrature methods of the previous section no longer apply. This opens the door to a wide variety of methods that have been developed. Although many are sophisticated, simpler methods can suffice for a considerable number of problems in engineering and science. We will focus on two of those methods here.

### 9.3.1 Euler’s Method[⁴](#ch09.xhtml_n9_4)

Equation 9.1 describes an initial value problem. We know the conditions at an initial value of the independent variable, here denoted as zero. We would like to develop the solution for the dependent variable, *y*, out to a given independent variable value, *t*[f].

To motivate our first method, we consider what we know at *t* = 0\. This is depicted in [Figure 9.14](#ch09.xhtml_f9_14). We see that we can locate the solution at *t* = 0, and, by applying the differential equation, we know the initial direction of the solution given by *f*(0, *y*[0]). We would assume that, as the solution departs from the initial condition, the derivative value (and slope of the solution) is likely to change. However, if that departure is a small interval, Δ*t*, the projection of the straight line from *t* = 0 to Δ*t* will be close to the true solution. This is the basis for the *Euler method*. That first solution step is represented as

$y\left( {t_{0} + \Delta t} \right) \cong y\left( t_{0} \right) + \frac{dy}{dt}\left( {t_{0},y_{0}} \right)\,\Delta t$(9.17)

![](images/Fig09_14.jpg)

**[FIGURE 9.14](#ch09.xhtml_f9_14b)** Information on solution at *t* = 0.

After the first step to approximate the solution, it is natural to consider extending the method with a second step and beyond. This is illustrated in [Figure 9.15](#ch09.xhtml_f9_15). What we notice is that the approximate solution departs from the true solution after the first step, and this departure continues after the second step. Imagine taking smaller steps; say, 10 steps for each single step shown in the figure. You can recognize that the true solution would be computed more accurately. That is the essence of the Euler method. On the other hand, if the step size taken is too small, the computation will take much longer and round-off errors could come into play.

![](images/Fig09_15.jpg)

**[FIGURE 9.15](#ch09.xhtml_f9_15b)** First two steps of the Euler method.

To develop a Python function for the Euler method, we will need to supply the function *f*(*t*, *y*), the initial condition, *y*[0], the initial value of the independent variable value, *t*[0] (often zero), the final independent variable value, *t*[f], and the step size, Δ*t*, called *h* in the Python code. One detail is that the final step to take us to *t*[f] may not be *h*, in which case, the final step would have to be adjusted. This function, `euler`, is shown in [Figure 9.16](#ch09.xhtml_f9_16).

![](images/Fig09_16.jpg)

**[FIGURE 9.16](#ch09.xhtml_f9_16b)** Function `euler` to implement the Euler method for one differential equation.

In this implementation of the Euler method, instead of creating arrays for the {*t*, *y*} solutions, empty arrays are created and then expanded using the `append` method as the solution evolves.[⁵](#ch09.xhtml_n9_5) Also, instead of using a `for` loop with a given number of iterations, a `while` loop is used and exited when the computation is complete.

To evaluate the `euler` function, we will use a differential equation that has an analytical solution, as we did previously with the trapezoidal rule method. This is the equation:

$\frac{dy}{dt} = - 0.05y + 2y(0) = 0$9.18

and the analytical solution is

*y* = 40(1 − *e*^(−0.05  *t*))(9.19)

For parameter values, *t*[f] = 80 and *h* = 10, the Python script below computes the approximate solution using the `euler` function and compares it to the analytical solution. A plot is generated and presented in [Figure 9.17](#ch09.xhtml_f9_17) that shows both results.

![](images/Fig09_17.jpg)

**[FIGURE 9.17](#ch09.xhtml_f9_17b)** Euler method solution of differential equation compared to analytical solution for *h* = 10.

```
 import numpy as np
import numpy as np
import matplotlib.pyplot as plt
def f(t, y):
dy = -0.05 * y + 2.
return dy
t0 = 0
tf = 80.
y0 = 0.
h = 10.
t, y = euler(f, y0,t0,tf, h)
def fa(t):
return 40*(1-np.exp(-0.05*t))
ta = np.linspace(t0,tf)
plt.scatter(t, y, c='k', marker='o', label='Euler Method')
plt.plot(ta, fa(ta), c='k', ls='--', label='True Solution')
plt.grid()
plt.xlabel('t')
plt.ylabel('y')
plt.legend()
```

It is clear that the Euler method approximate solution overshoots the true solution. If we change the *h* value to 0.1, the result is shown in [Figure 9.18](#ch09.xhtml_f9_18). As far as we can detect on the plot, the Euler method solution and the analytical solution are identical (at least visually).

![](images/Fig09_18.jpg)

**[FIGURE 9.18](#ch09.xhtml_f9_18b)** Euler method with *h* = 0.1 provides an accurate solution.

A question that arises is, when we have a differential equation that has no analytical solution, how do we determine a step size, *h* value, which provides an accurate solution. A common technique is to solve the equation several times with reducing values of *h* until the solution doesn’t change significantly. And as will be discussed in [Section 9.4](#ch09.xhtml_h9_4), advanced differential equation solvers employ clever adaptive techniques to determine step size.

### 9.3.2 Heun’s Method

As you might suspect, improvements to the Euler method address the error of the method, noting that the error tends to increase as the solution proceeds. We will introduce one of these improved methods, called the *Heun method*, here. You will likely encounter additional methods later in your studies, such as the Runge-Kutta methods.

The Heun method is based on the insight that a fundamental source of error in Euler’s method is that the derivative at the beginning of the interval is assumed to apply across the entire interval. The Heun method addresses this shortcoming as illustrated in [Figure 9.19](#ch09.xhtml_f9_19). The standard Euler method is used to predict to estimate the solution at the end of the first step, *y*[1]¹. Then, the derivative (or slope) at *t*[1] is computed as *f*(*t*[1],*y*[1]¹). The derivative for the original step is then corrected by averaging the two slopes, *f*(0,*y*[0]) and *f*(*t*[1],*y*[1]¹). This average slope is then used to predict *y*[1]². The second step can be iterated until the prediction converges. This type of approach is generally called a *predictor-corrector method*.

The first step is represented by the following formulas:

$\begin{array}{l} {\text{prediction step:}y_{1}^{1} = y_{0} + f\left( {t_{0},y_{0}} \right)\,\Delta t} \\ {{\overline{f}}^{1} = \frac{f\left( {t_{0},y_{0}} \right) + f\left( {t_{1},y_{1}^{1}} \right)}{2}} \\ {\text{corrector step:}y_{1}^{2} = y_{0} + {\overline{f}}^{1}\,\Delta t} \end{array}$(9.20)

![](images/Fig09_19.jpg)

**[FIGURE 9.19](#ch09.xhtml_f9_19b)** Basis for the Heun method. The solid black curve is the analytical solution to provide context for assessing the accuracy of the Heun method. (a) Predictor step. (b) Iterative corrector step

Steps repeated until $\left| \frac{y_{1}^{i} - y_{1}^{i - 1}}{y_{1}^{i}} \right| < \varepsilon_{a}$

After convergence, the method moves on to the next step, from *t*[1] to *t*[2].

We can modify the `euler` function to incorporate the Heun method. The Python code for the `heun` function is shown in [Figure 9.20](#ch09.xhtml_f9_20). In this case, we incorporate a `while` loop to provide convergence of the scheme shown in Equations 9.20.

We can evaluate the Heun method with the same example as shown in [Figure 9.17](#ch09.xhtml_f9_17). The results are surprising and are illustrated in [Figure 9.21](#ch09.xhtml_f9_21). The numerical Heun solution for a step size, *h* = 10, follows the analytical solution closely and performs much better than the Euler method. In fact, the Heun method performs similarly to the Euler method with a step size 100 times smaller.

![](images/Fig09_20.jpg)

**[FIGURE 9.20](#ch09.xhtml_f9_20b)** Python code for the Heun method, function `heun`.

![](images/Fig09_21.jpg)

**[FIGURE 9.21](#ch09.xhtml_f9_21b)** Heun method solution of differential equation compared to analytical solution for *h* = 10.

### 9.3.3 Systems of Differential Equations

Next, we consider the related scenario where there are multiple differential equations that must be solved simultaneously. Equations 9.8 with [Figure 9.4](#ch09.xhtml_f9_4), introduced earlier, provide an example.

$\begin{array}{l} {\frac{dx_{1}}{dt} = - 2x_{1}^{2} + 2x_{1} + x_{2} - 1x_{1}(0) = 2} \\ {\frac{dx_{2}}{dt} = - x_{1} - 3x_{2}^{2} + 2x_{2} + 2x_{2}(0) = 0} \end{array}$(9.8)

We can extend the previous Euler and Heun methods, as Python functions `euler` and `heun`, to accommodate multiple equations. The function `eulerm` `def` statement for the Euler method would be

```
 def eulerm(f,y0,t0,tf,h):
```

This appears to be the same as for the `euler` function, but the difference is that the `f` function argument now returns an array of more than one derivative, and the `y0` initial condition is also an array of initial values for the `y` dependent variables. The modified function is shown in [Figure 9.22](#ch09.xhtml_f9_22). The solution arrays, `t` and `y`, are created with the `zeros` function, and the initial values, `y0`, are assigned to the first row of the `y` array. The `for` loop carries out the solution in the same way as the `euler` function. Note the use of the `:` index to include the dependent variable values, `y`, of all the equations.

![](images/Fig09_22.jpg)

**[FIGURE 9.22](#ch09.xhtml_f9_22b)** Euler method for multiple equations: `eulerm`

The following Python script solves the differential equations (Equation 9.8) with `tf` = 2 and creates the plot depicted in [Figure 9.23](#ch09.xhtml_f9_23). You will note that the step size, `h` = 0.01, is fairly small, yielding 200 intervals to obtain a smooth, accurate solution. The accuracy of the result could be checked by solving the equations with a smaller `h` and comparing the solutions.

```
 import numpy as np
import matplotlib.pyplot as plt
def f(t, y):
dy = np.zeros(2)
dy[0] = -2*y[0]**2 + 2*y[0] + y[1] -1
dy[1] = -y[0] -3*y[1]**2 +2*y[1] + 2
return dy
t0 = 0
tf = 2.
y0 = np.array([2., 0.])
h = 0.01
t, y = eulerm(f, y0,t0,tf, h)
plt.plot(t, y[:, 0], c='k', label='x1')
plt.plot(t, y[:, 1], c='k', ls='--', label='x2')
plt.grid()
plt.xlabel('t')
plt.ylabel('x1 and x2')
plt.legend()
```

![](images/Fig09_23.jpg)

**[FIGURE 9.23](#ch09.xhtml_f9_23b)** Solution of two coupled differential equations.

Similar modifications could be made to the `heun` function. In general, it would be advantageous to have functions for any other, more advanced methods be designed to manage multiple differential equations.

Consider now the shock absorber model described in [Figure 9.2](#ch09.xhtml_f9_2). Here, we have a single differential equation, called second order because it includes a second derivative. The information flow diagram suggests how we might solve this equation with two “integrators,” or, if you prefer, as two first-order equations:

$\begin{array}{l} {\frac{dv}{dt} = \frac{1}{m}\left\lbrack {- b\frac{dx}{dt} - k_{1}\left( {x - x_{1eq}} \right) - k_{2}\left( {x - x_{2eq}} \right)} \right\rbrack v(0) = v_{0}} \\ {\frac{dx}{dt} = vx(0) = x_{0}} \end{array}$(9.9)

In general, we can always decompose an equation with derivatives up to *n*th order into *n* first-order differential equations. Now that we have two first-order equations, we can solve these with an extension of the Euler or Heun methods, such as our `eulerm` function. A Python script to accomplish this is shown below. The equilibrium values, `x1eq` and `x2eq`, are set to zero, indicating that the two springs would be relaxed at *x* = 0\. The initial value of *x* is set equal to 1, indicating that the mass is pushed one meter to the right at *t* = 0.

```
 = 9.801 # m/s2
m = 10\. # kg
b = 5\. # N/[m s] or kg/s
k1 = 1\. # N/m or kg/s2
k2 = 1.
x1eq = 0.
x2eq = 0.
v0 = 0\. # m/s
x0 = 1\. # m
def f(t, y):
v = y[0]
x = y[1]
dy = np.zeros(2)
dy[0] = 1/m * (-b*v - k1*(x-x1eq)) - k2*(x-x2eq)
dy[1] = v
return dy
t0 = 0
tf = 20\. # seconds
y0 = np.array([v0, x0])
h = 0.01 # seconds
t, y = eulerm(f, y0,t0,tf, h)
plt.plot(t, y[:, 1], c='k', label='displacement - m')
plt.plot(t, y[:, 0], c='k', ls='--', label='velocity - m/s')
plt.grid()
plt.xlabel('time - s')
plt.ylabel('displacement & velocity')
plt.legend()
```

The plot produced by the script is shown in [Figure 9.24](#ch09.xhtml_f9_24). You can see that the shock absorber system oscillates, the oscillations dampen out in 20 seconds. By paying attention to more realistic parameter values, we could evaluate and make design changes to a given shock absorber to obtain the desired performance. We would also want the model to include an external force that causes the shock absorber to deflect, and this force might change with time, such as one would find driving a vehicle over an uneven surface, like a dirt road with washboard ripples.

![](images/Fig09_24.jpg)

**[FIGURE 9.24](#ch09.xhtml_f9_24b)** Simulation of shock absorber.

## 9.4 Solving Differential Equations with the solve _ivp Function from SciPy’s integrate Module

Just as with quadrature, Python provides functions to solve differential equations via its SciPy `integrate` submodule. One that is frequently the function of choice is `solve _ ivp`. The syntax for this function is

```
 from scipy.integrate import solve_ivp
result = solve_ivp(f,t_span,y0,t_eval=[•])
```

The `f` argument is the same as for our `eulerm` function, a function that evaluates the derivatives for given values of `t` and `y`. The `t _ span` argument is an array of the initial and final values of `t.` The `y0` argument is an array specifying the initial values of the dependent variables. If there is only one dependent variable, it is a single variable or value; whereas for two or more dependent variables, it is an array. The `t _ eval` argument contains an array of `t` values at which the solution is desired. If it is left out, the `solve _ ivp` function will determine the output intervals.

The return from `solve _ ivp`, `result`, is an object that contains various attributes. Most important to us are

```
 result.t
result.y
```

that contain the independent and dependent variable values at the `t` values specified in the `t _ eval` array or, in the case that only `t0` and `tf` are specified in `t _ span`, the `t` values will be chosen by the `solve _ ivp` function.

The `solve _ ivp` provides six different methods of integration. The details of these are beyond the scope of this text. The default is RK45, a *Runge-Kutta method* with automatic step-size adjustment. An alternate method commonly used when the RK45 method encounters difficulty is the *LSODA method*. You can read more about these in SciPy help. The method is specified as a named argument, e.g. `method` = `'RK45'` or = `'LSODA'`.

We will illustrate the use of `solve _ ivp` with two examples. The first is that described in Equation 9.8 and [Figure 9.23](#ch09.xhtml_f9_23). Here is the Python script we will use:

```
 import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt
def f(t,y):
    dy = np.zeros(2)
    dy[0] = -2*y[0]**2 + 2*y[0] + y[1] -1
    dy[1] = -y[0] -3*y[1]**2 +2*y[1] + 2
    return dy
tf = 2.
tspan = [0., tf]
teval = np.linspace(0., tf)
y0 = np.array([2., 0.])
result = solve_ivp(f,tspan,y0,t_eval=teval)
tm = result.t
x1 = result.y[0,:]
x2 = result.y[1,:]

plt.plot(tm,x1,c='k',label='x1')
plt.plot(tm,x2,c='k',ls='--',label='x2')
plt.grid()
plt.xlabel('t')
plt.ylabel('x1 and x2')
plt.legend()
```

The function `f` is identical to what we used with `eulerm`. The `tspan` variable is set with initial value 0 and final value `tf`. With the `linspace` function, we request 50 evenly spaced values across the domain of the solution. The `y0` argument is as before.

The result from the `solve _ ivp` function is unpacked into independent and dependent variable arrays, `tm`, `x1`, and `x2`, and then a plot is generated. The plot is shown in [Figure 9.27](#ch09.xhtml_f9_27), and it looks identical to that in [Figure 9.23](#ch09.xhtml_f9_23).

![](images/Fig09_27.jpg)

**[FIGURE 9.27](#ch09.xhtml_f9_27b)** Solution of two, coupled differential equations with solve_ivp.

For the second example, we will solve a notorious, single differential equation ([Hornbeck, 1975](#ch11_ref.xhtml_r7)):

$\frac{dy}{dt} = 5\left( {y - t^{2}} \right)y(0) = 0.080 \leq t \leq 5$(9.12)

We can compare our numerical solution to the analytical solution available here:

*y* = *t*² + 0.4 *t* + 0.08(9.13)

Note that at *t* = 5, *y* = 27.08.

This Python script attempts the numerical solution using `solve _ ivp` and compares it with the analytical solution in a plot. The plot is shown in [Figure 9.28](#ch09.xhtml_f9_28). There is obviously a problem with the numerical solution.

```
 import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

def f(t,y):
    return 5.*(y-t**2)

tf = 5.
tspan = [0., tf]
teval = np.linspace(0., tf)
y0 = [0.08]
result = solve_ivp(f,tspan,y0,t_eval=teval)
tm = result.t
ym = result.y[0,:]

ya = tm**2 + 0.4*tm + 0.08

plt.plot(tm,ym,c='k',label='solve_ivp')
plt.plot(tm,ya,c='k',ls='--',label='true solution')
plt.grid()
plt.xlabel('t')
plt.ylabel('y')
plt.legend()
```

![](images/Fig09_28.jpg)

**[FIGURE 9.28](#ch09.xhtml_f9_28b)** Comparison of numerical and analytical solutions with numerical solution blowing up.

What is going on here? The general analytical solution to this equation is

*y* = *t*² + 0.4 *t* + 0.08 + *c* *e*^(5 *t*)(9.14)

where the constant *c* is determined with the initial condition. Since *y*[0] is chosen as 0.08, *c* = 0, and the exploding exponential term drops out analytically. But, if the numerical solution ever deviates measurably from the analytical solution (e.g. due to roundoff error), that exponential term rears its ugly head and causes the numerical solution to blow up. This is called a *parasitic solution*.

There are different approaches to remedying the numerical problem. One is to experiment with different solver methods. Another is to require the `solve _ ivp` to meet more stringent error criteria. The two criteria, with their default values, are

1.  absolute error tolerance, `atol` = `1.e-6`
2.  relative error tolerance, `rtol` = `1.e-3`

If we make these much more stringent via a modification of the `solve _ ivp` statement,

```
 result = solve_ivp(f,tspan,y0,t_eval=teval \
                    , atol = 1.e-12, rtol = 1.e-12)
```

the plot that is produced is shown in [Figure 9.29](#ch09.xhtml_f9_29). The two solutions are indistinguishable.

![](images/Fig09_29.jpg)

**[FIGURE 9.29](#ch09.xhtml_f9_29b)** Comparison of `solve _ ivp` and analytical solutions with tight error tolerances.

The lesson here is that solving differential equations numerically can present challenges that require different approaches to be successful. Also, eventually for you, it will be important to study differential equations, their theory and structure, and their application in the modeling of different phenomena in engineering and science. The purpose of this chapter has been to give you a start in this important endeavor.

## Problems

1.  **9.1** Indicate which solution strategy would be appropriate for the following differential equations.
    1.  $\frac{dy}{dt} = \frac{e^{t}}{1 + e^{t}}y(0) = 0.5\quad\quad\quad\quad\quad\quad\quad 0 \leq t \leq 1$
    2.  $\frac{dy}{dx} = x\, y\, e^{- x^{2}}y(0) = 0\,\quad\quad\quad\quad\quad\quad\quad\,\, 0 \leq x \leq 1$
    3.  $\frac{d^{2}y}{dt^{2}} = - 9yy(0) = 1\,\,\,\frac{dy}{dt}(0) = 0\quad\quad\quad\,\, 0 \leq t \leq 4$
    4.  $\frac{d^{2}y}{dx^{2}} + 2x\,\frac{dy}{dx} = 0y(0) = 1\,\,\,\quad\quad\quad\quad\quad\quad\quad y(10) = 0.1$
2.  **9.2** Draw information flow diagrams for the equations in parts **(c)** and **(d)** in Problem 9.1.
3.  **9.3** Hand draw a plot on graph paper of the function

    *f*(*t*) = ln (5 − 4cos (*x*))

    over the domain 0 ≤ *x* ≤ *π*. Using an interval of Δ*x* = 0.2, employ the counting the squares method to produce low and high estimates of

    ∫[0]^(*π*)*f*(*x*)*d**x*

    and then average the two results to obtain your final estimate.

4.  **9.4** Employ trapezoidal rule to compute the integral in Problem 9.3\. Use Python to compare the results from this chapter’s `trap` function and Python’s built-in `quad` function.
5.  **9.5** Many vessels (tanks) that store liquids have a circular cross-section, but the radius (or diameter) and cross-sectional area vary with height. This is illustrated in [Figure P9.5](#ch09.xhtml_fP9_5). A practical way to calculate the volume of the vessel is to know the radius, *r*, as a function of height, *h*, and then use the integral and associated formula for area, *A*.

    *V* = ∫[0]^(*H*)*A*(*h*)*d**h**A*(*h*) = *π**r*²(*h*)

    The relationship, *r*(*h*), might be obtained from measurements or an analytical formula used to design the vessel. Consider a vessel with

    *r*(*h*) = 8 + 0.34 *h* − 0.002 *h*² cm  and  *H* = 50cm

    Use Python and the method of your choice to compute the volume of this vessel.

    ![](images/Fig09P_05.jpg)

    **[FIGURE P9.5](#ch09.xhtml_fP9_5b)** Vessel with circular cross-section.

6.  **9.6** An important task in public utilities and industry is the totalization of flow of materials, whether gases, liquids, or solids. Measurements are often made of the flow rate of a material, but monetary charges are calculated for the total volume of material that flows over a given time interval. The relationship is given by an integral,

    *V* = ∫[*t*[0]]^(*t*[*f*])*q*(*t*) *d**t*

    where *q*(*t*) is the flow rate, for a liquid in units like liters/min or m³/s, and *V* is the volume that flowed over the interval from *t*[0] to *t*[f].Flow rate data are typically samples collected at equal intervals of time. The data in the table below were collected for a liquid chemical that is transferred from one company to another through a pipeline. Use the built-in Python function `trapz` to totalize the flow for these data.

    | Time (min) | Flow Rate (L/min) | Time (min) | Flow Rate (L/min) | Time (min) | Flow Rate (L/min) |
    | --- | --- | --- | --- | --- | --- |
    | 0 | 17.0 | 55 | 17.4 | 105 | 17.4 |
    | 5 | 16.6 | 60 | 17.2 | 110 | 17.4 |
    | 10 | 16.3 | 65 | 17.4 | 115 | 17.5 |
    | 15 | 16.1 | 70 | 17.4 | 120 | 17.4 |
    | 20 | 17.1 | 75 | 17.0 | 125 | 17.6 |
    | 25 | 16.9 | 80 | 17.3 | 130 | 17.4 |
    | 30 | 16.8 | 85 | 17.2 | 135 | 17.3 |
    | 35 | 17.4 | 90 | 17.4 | 140 | 17.0 |
    | 40 | 17.1 | 95 | 16.8 | 145 | 17.8 |
    | 45 | 17.0 | 100 | 17.1 | 150 | 17.5 |
    | 50 | 16.7 |  |  |  |  |

7.  **9.7** For the differential equation,

    $\frac{dy}{dt} = - 0.2y^{2}y(0) = 3$

    1.  Compute by hand one step of the Euler method for Δ*t* = 1.
    2.  Compute by hand one step of the Heun method for Δ*t*  =  1, including five iterations of the predictor-corrector procedure. Does the method appear to be converging?
8.  **9.8** A famous second-order differential equation, called the *van der Pol* equation, is

    $\frac{d^{2}y}{dt^{2}} = (1 - y^{2})\frac{dy}{dt} - y$

    For the initial conditions, *y*(0) = 1 and *dy*/*dt*(0)  =  0, use the Euler method to solve the equation over the domain 0 ≤ *t* ≤ 10\. Find a step size, Δ*t*, which yields an accurate solution. Produce a plot of your results.

9.  **9.9** Solve this differential equation using the Python built-in `solve _ ivp` function.

    $\frac{dy}{dt} = - 750y - 1100\, e^{- 2t}y(0) = 5\,\,\,\,\,\,\,\,\, 0 \leq t \leq 5$

    Compare the performance of the default RK45 method and the LSODA method. Adjust the error tolerances if needed. Produce a plot of your results.

10.  **9.10** [Figure P9.10](#ch09.xhtml_fP9_10) is a schematic diagram of a simple electrical circuit with five components, a battery source, on-off switch, coil or inductor, resistor, and capacitor.

    ![](images/Fig09P_10.jpg)

    **[FIGURE P9.10](#ch09.xhtml_fP9_10b)** Electrical circuit.

    When the switch is closed, the voltage shown initially as *V*[0] changes. A differential equation describes this:

    $LC\frac{d^{2}V}{dt^{2}} + RC\frac{dV}{dt} + V = 0\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\, V(0) = V_{0}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\frac{dV}{dt}(0) = 0$

    Solve this equation for 0 ≤ *t* ≤ 0.2 seconds, *V*[0] = 100 volts, and the parameter values[⁸](#ch09.xhtml_n9_8)

    1.  *C* = 2 × 10^(−6) farads *L* = 0.5 henries *R* = 100 ohms

    Compare the solution using the `eulerm` function with a step size, Δ*t* = 0.0001 seconds, and the `solve _ ivp` built-in function. Show the comparison on a plot.

11.  **9.11** In this chapter, we extended the `euler` function to its `eulerm` counterpart with the ability to solve multiple differential equations. In a similar fashion, extend the `heun` function to a new function called `heunm` that will solve multiple differential equations. Solve the Equations 9.8 using your `heunm` function and confirm the solution by comparison to [Figure 9.23](#ch09.xhtml_f9_23).

    Hint: The criterion to determine the convergence of the corrector step has to change from the `heun` function because there are multiple equations and thus multiple errors. One way to manage this is to use the maximum absolute error as the criterion. Another is to use the sum of squares of the errors of the equations.

12.  **9.12** For the second-order differential equation,

    $\frac{d^{2}y}{dt^{2}} = \frac{1}{4}\frac{dy}{dt} + yy(0) = 5\,\,\,\,\,\,\,\,\,\,\, y(10) = 80 \leq t \leq 10$

    you will note that there is no initial condition for *dy*/*dt*, but there is a final condition for *y*. To solve this problem, we suggest that you guess an initial condition for *dy*/*dt*. Then solve the equation with `solve _ ivp`. Check your solution’s value of *y*(10) versus the requirement of 8\. Then, adjust *dy*/*dt*(0), and, by trial-and-error, find a solution that matches closely the *y*(10) = 8 requirement. This is a manual strategy to solve a two-point boundary value problem. There are more sophisticated, automatic techniques, but these are not requested here.

13.  **9.13** Differential equations are important in structural engineering. [Figure P9.13](#ch09.xhtml_fP9_13) illustrates a cantilever beam (beam fixed at one end) subject to a load (force) at its end. The profile of deflection of the beam is described by a second-order differential equation,

    ![](images/Fig09P_13.jpg)

    **[FIGURE P9.13](#ch09.xhtml_fP9_13b)** Deflection of cantilever beam under a load placed at the end.

    1.  $\frac{d^{2}y}{dx^{2}} = - \frac{F}{E\, I}\,\left( {L - x} \right)\quad\quad y(0) = 0\quad\quad\frac{dy}{dx}(0) = 0\quad\quad 0 \leq x \leq L$

    where *y*: vertical displacement of the beam at a given value of *x*, m,

    1.  *x*: location on the beam from 0 to *L*, m,
    2.  *F*: downward load placed at the beam end, N,
    3.  *E*: modulus of elasticity (stiffness) of the beam material, Pa,
    4.  *I*: moment of inertia of the beam cross-section, m⁴, and
    5.  *L*: length of the beam, m.
    6.  For the following parameter values and conditions,
    7.  *L* = 4 m, *F* = 5,000 N, *E*  =  5 × 10^(11) Pa, *I* = 4 × 10^(−4 )m⁴, solve the differential equation using a numerical method of your choice.

        It turns out that there is an analytical solution to this differential equation,

        $y = - \frac{F\, L}{2E\, I}x^{2} + \frac{F}{6E\, I}x^{3}$

    Plot and compare the analytical result along with your numerical solution.

14.  **9.14** Use a modified version of the Python code from [Figure 9.10](#ch09.xhtml_f9_10) to evaluate the integral (Equation 9.9),

    *y* = ∫[0]^(*π*/2)*t* cos (*t*)*d**t*

    Starting with *n*  =  4, progressively double the number of intervals 20 times. For each function call, return the integral estimate, the step size, and the error, where

    1.  *error*  =  |*true value* – *estimated value*|

    where the *true value* is computed with Equation 9.10. Generate log-log plots of the step sizes and the errors versus *n*.

# 10 Working with Data

DOI: [10.1201/9781003256861-10](https://doi.org/10.1201/9781003256861-10)

## Chapter Objectives

*   Learn how to make initial observations on data sets with the help of graphical depictions.
*   Be able to compute typical sample statistics to characterize a data set.
*   Understand how data relate to populations, and how distributions describe the latter.
*   Learn how to simulate numbers drawn from different distributions using random number generators from the Python NumPy `random` module.
*   Be able to make claims with data − an introduction to hypothesis testing.
*   Learn how to fit mathematical models to data and evaluate their adequacy.

Scientists and engineers make discoveries and decisions based on information obtained through experiments and observations. Experiments are planned and carried out. Observations are made of phenomena, most often in nature, the laboratory, or existing processes. All yield data, and the field of *applied statistics* is dedicated to reaching conclusions from the examination of data.

The topic of statistics is very large. Many, perhaps most, engineers and scientists take a course in applied statistics as undergraduate students. Many universities offer entire degree programs in statistics, and these may be housed in their own academic unit or department. So, what can we do here to introduce this topic in the context of Python?

One of the common problems in the treatment and interpretation of data is the misapplication of statistics. There are countless examples of practitioners and researchers reaching erroneous conclusions, sometimes with disastrous results, because they applied statistical methods incorrectly.[¹](#ch10.xhtml_n10_1) A problem associated with this is the availability of statistical software packages that produce an avalanche of results which are difficult for engineers or scientists to understand unless they have a sound background in applied statistics.

What we will attempt to do here is introduce you to sound fundamentals and practices in the treatment of data. By doing this, we want to inspire you to further your education in this important topic. Along the way, we also warn you against using statistical results that you do not understand well to make conclusions. That is a typical trap that investigators fall into.

This chapter starts out with the typical initial steps taken to characterize a set of data. These include recognizing the data type and the constraints on the data. You will learn how to extract sample statistics from the data which help in their description. Since data contain random error, it is important to understand its nature and how the random error relates to the concept of a population from which the data are sampled. We will also introduce the process of simulating random numbers that are drawn from different populations.

With this background, this chapter continues to two important topics in applied statistics. The first, called *hypothesis testing*, has to do with making claims based on a set of data and assessing the uncertainty of the claims and decisions that might be made. The second introduces the important field of *regression* — fitting models to data. Mathematical models can be used in various ways to increase the understanding of phenomena and make predictions.

## 10.1 Characterizing Data Sets: Initial Observations and Sample Statistics

Data take different forms.[²](#ch10.xhtml_n10_2) A first distinction is whether the information is categorical or not. Categorical data take on only certain values which may or may not be numerical. Qualitative judgment of product quality is one example. Results might be classified as excellent, good, average, sub-par, or unacceptable. An even simpler scale for the quality of discrete products might be pass/fail. Once the scale of measurement is established, there are no values between the categories. We focus in this chapter on data which are measurements of continuous quantities and have numerical values.

### 10.1.1 General Data Concepts

The concept of *resolution* is a key aspect of making numerical measurements. This is illustrated in [Figure 10.1](#ch10.xhtml_f10_1) showing weather station pressure data acquired at 5-minute intervals. Observing closely, you can see that the measurements jump up and down in intervals of 0.01 inHg. There are no intermediate values. Of course, the true relative pressure is a continuous quantity, but, through the lens of the weather station’s pressure measurement, we only see it to the nearest 0.1 inHg. As we look at the figure, we judge that the resolution is fine enough so that our measurements provide a good profile and estimate of the variations in pressure.

![](images/Fig10_01.jpg)

**[FIGURE 10.1](#ch10.xhtml_f10_1b)** Weather station atmospheric pressure measurements relative to sea level.[³](#ch10.xhtml_n10_3)

However, if we observe the relative humidity measurements from the same weather station, we can look at [Figure 10.2](#ch10.xhtml_f10_2). Here, the matter of resolution is of concern because it is only to the nearest 1%. If these measurements do not provide enough detail, we will have to invest in a humidistat with higher resolution (and higher cost). As we can see here, over the range measured, there are only five possible values. This gives us the impression that these measurements are discrete and not a good representation of a continuous quantity, the true relative humidity.

![](images/Fig10_02.jpg)

**[FIGURE 10.2](#ch10.xhtml_f10_2b)** Weather station relative humidity measurements.

The next term we introduce is *stationarity*. This has to do with whether a set of measurements appear to have a trend in the order they are presented. The weather station data presented in [Figures 10.1](#ch10.xhtml_f10_1) and [10.2](#ch10.xhtml_f10_2) are taken chronologically. They reveal trends in time, so we conclude that the data do not represent a stationary series. If the data set is not stationary, it is difficult for us to estimate statistical quantities such as a central tendency or mean and dispersion or variance.

Terms that cause confusion and are frequently mis-applied are accuracy and precision. In brief, *accuracy* is how close a given set of measurements are to their true value, whereas *precision* is how close the measurements are to each other. Although these provide a simple description of the concepts, there are nuances that must be recognized to understand them fully.

Imagine we measure temperature with an instrument that provides a digital display with high resolution, 0.01°C. There is a natural temptation to presume that the measurements are “accurate” to the same extent. That is a mistake. *Accuracy* has to do with comparison to a standard of measurement. Standards of measurement are maintained by organizations such as the National Institute of Standards and Technology (NIST) in the U.S. and the Système International d’Unités (SI) in France. Secondary standards are calibrated against the primary NIST standards. Temperature instruments are generally accompanied with an accuracy specification. For our example above, that might be ± 0.1°C − ten times greater than the resolution. Many consider the term *precision* as a poor descriptor of data because it often refers to resolution, but it is easily confused with accuracy. Also, it may be confused with repeatability and dispersion. [Figure 10.3](#ch10.xhtml_f10_3) illustrates these concepts.

![](images/Fig10_03.jpg)

**[FIGURE 10.3](#ch10.xhtml_f10_3b)** Dot diagram of repeated measurements.

*Repeatability* corresponds to taking repeated measurements of the same quantity and obtaining consistent results. *Dispersion* describes this in the opposite way, as it refers to the scatter in the data set.

With a relatively small set of data, we can estimate a *central tendency*, most commonly by computing their average. If we were to increase the number of measurements to a very large number, our average would approach a constant value; yet this value might yet be displaced from the accurate value because of inaccuracy of our measurement system. So, there are two concepts here: first, as we increase our sample size, our average values (or mean estimates) approach a constant value with greater and greater certainty. Second, that constant value is still limited by the lack of accuracy or *bias error* of our measurement system. These two sources of error are combined in the measurements we take.

The *dispersion* of the data has to do with the noisiness of the measurements. Measurements may by noisy (or have random error) because of the nature of the quantity we are measuring or noise may be induced by our measurement instrumentation alone. The latter may be minimized through careful attention to the instrumentation. The former tends to be “the nature of the beast” that we must live with. The more the data are dispersed, the harder it is to estimate the central value with certainty. Where these concepts become very meaningful is when, from a set of data, we want to make a claim, and we must deal with the accuracy (or lack thereof) and the uncertainty.

To be clear, a set of data may have little dispersion and yet have a significant error when compared to a true or accurate value. And conversely, a set of measurements may be centered well on the true value, but, with a large amount of dispersion, may be difficult to make claims because of the associated uncertainty. This is illustrated in [Figure 10.4](#ch10.xhtml_f10_4).

![](images/Fig10_04.jpg)

**[FIGURE 10.4](#ch10.xhtml_f10_4b)** Comparison of low and high dispersion data sets with different bias errors.

To complete this discussion, we return to the concept of stationarity. The concept of a central value is a moving target for a data series that is non-stationary. For [Figures 10.1](#ch10.xhtml_f10_1) and [10.2](#ch10.xhtml_f10_2), we can certainly calculate the average temperature and relative humidity over the time period presented; however, calling that a central tendency will be overstating the case.

### 10.1.2 Sample Statistics: Central Tendency and Dispersion

When we collect a set of data, we introduce the concept that these data come from a *population*. There are occasions when populations are finite. For example, the entire student body of a university. If we select 100 students at random and measure their heights, this would be a *sample* with *n* = 100\. If we select another sample, we will have a different set of data. But both sets were obtained from the same population. With a finite population, the concept of measuring all members is feasible.

For most data samples in engineering and science, the population is infinite. In [Figure 10.1](#ch10.xhtml_f10_1), we can imagine that there are an infinite number of pressures possible in nature. Subsequently, our measurement system, with finite resolution, reduces this to a finite population of possible measured pressures. If the measurement resolution is fine, the measurement population approaches the population in nature.

#### 10.1.2.1 Central Tendency

In characterizing a data set, a first concept is that of *central tendency*. The most common measure of this is the *arithmetic average* of the sample {*x*[i], *i* = 1,…, *n*},

$\overline{x} = \frac{\sum\limits_{i = 1}^{n}x_{i}}{n}$(10.1)

Notice the notation, *x* with an overscore bar, $\overline{x}$. This is alternately called the *sample average* or the *sample mean*. Occasionally, it is referred to as the mean, but that is not appropriate.

Generally, the term *mean* corresponds to the central tendency of the entire population, and the symbol used is the Greek letter “mu,” *μ*. [Figure 10.5](#ch10.xhtml_f10_5) illustrates two data sets, their *dot diagrams*, and their corresponding sample average calculations. These data are measured or extracted from the same population. We note that the samples are different and yield average calculations that differ by about 3%.

![](images/Fig10_05.jpg)

**[FIGURE 10.5](#ch10.xhtml_f10_5b)** Average calculations and dot diagrams for two data sets from the same population.

The *dot diagrams* in [Figure 10.5](#ch10.xhtml_f10_5) raise another issue. Each data set contains one value that is significantly high and separated from the rest of the measurements. Such values are commonly called *outliers*. There is a temptation, and it is a trap fallen into by many investigators, to remove outliers from the data set without cause. This is absolutely a bad practice. The well-founded reason to remove an outlier is the discovery of a *blunder* in the experiments or data collection; otherwise, outliers should not be removed. After all, they could be telling you something exceedingly important about the phenomenon you are measuring. And one should always document removals.

When outliers exist, especially in smaller data sets, there is a concern that they may influence the average calculation inordinately. One answer to this is to use an alternate measure of central tendency. The most common of these is the *median*, designated *x̃*. The definition of the median is simple: sort the data and pick the one in the middle — if the number of the data is even, pick the two in the middle and compute their average. The calculation of the median for our two data sets in [Figure 10.5](#ch10.xhtml_f10_5) is shown in [Figure 10.6](#ch10.xhtml_f10_6). You will note that the median values are less than the average values, especially for the second data set. This is because the high values, possibly outliers, in the two data sets influence the average calculation more than the median calculation. The high value in the second data set is more extreme than that of the first data set. We will address diagnosing outliers a bit later.

![](images/Fig10_06.jpg)

**[FIGURE 10.6](#ch10.xhtml_f10_6b)** Computation of the median for two data sets.

There are other measures of central tendency, such as the *mode* (most frequently occurring value) and the *m*-*estimator* (gradually discounts values far from the central result), but we will not spend time on those here. They are used less frequently, but if you are curious about them see Chapra and Clough (2022) or a good statistics texts like [Montgomery and Runger (2018) or Mason, Gunst, and Hess (1989)](#ch11_ref.xhtml_r8).

It is useful to know how to compute the average and the median with Python. Here is a script that illustrates this for the second data set.

```
 import numpy as np

x = np.array([11.4,10.5,9.3,14.6,8.4,7.9,7.3,9.7,8.6,8.7])

xbar = np.mean(x)
xmed = np.median(x)
print('average = {0:5.2f}'.format(xbar))
print('median  = {0:5.2f}'.format(xmed))
```

The results displayed in the Console are

```
 average = 9.64
median =  9.00
```

Note that the function for average (or sample mean) in the NumPy module is `mean`.

#### 10.1.2.2 Spread or Dispersion

The next quantity of interest for a data sample and its population is a measure of spread or *dispersion*. Perhaps the easiest-to-compute measure of spread is the *range*. This is simply the difference between and maximum and minimum values in the data set. This is not a particularly good measure because it is too sensitive to extreme values and ignores the data interior to the minimum and maximum values. Further, it is not a stable estimator in that the range gets wider as the number of data points increases.

Just as the sample average is an estimate of the true central value or population mean, we commonly use a similar measure for dispersion. This is the *sample standard deviation* (or its square, the *sample variance*) as an estimate of the population standard deviation (or its square, the population variance). The formula for the sample standard deviation is

$s = \sqrt{\frac{\sum\limits_{i = 1}^{n}\left( {x_{i} - \overline{x}} \right)^{2}}{n - 1}}$(10.2)

In words, this measure sums the squares of the deviations between the individual data and the sample average, divides the result by *n*-1, and takes the square root. Without the square root, this is called the sample variance, *s*². Because of the square, you can see that larger deviations weigh more heavily into the result than small ones. As with the mean, the sample standard deviation is an estimate of the standard deviation of the population, which is designated by the Greek letter “sigma,” *σ*.

A question that arises frequently is why *n*−1 is used in the denominator of Equation 10.2 and not just *n*. We explain this here in two ways:

*   The number of *degrees of freedom* in the data set is *n*. When we calculate and use the sample average, that removes one degree of freedom, leaving *n* −1\. Another way to think of this is that if we know the mean and are given *n*–1 of the values, the *n*th value can be computed.
*   If we use *n*, instead of *n* −1, and increase the sample size gradually to high values of *n*, the result does not approach *σ*, but has an offset or *bias error*.

There is a way to demonstrate this second point with a mathematical derivation, but we choose not to include this since it involves the use of concepts beyond our scope here. It is worth mentioning that a common error in calculating the sample standard deviation is to use *n* when *n*−1 should be used. Conversely, in the case where the sample is the entire population, *n* should be used.

[Figure 10.7](#ch10.xhtml_f10_7) illustrates the calculation of the sample standard deviation for our two data sets. Note that the two results are quite different — the second is over three times the first. This reveals two issues with estimating the standard deviation. First, compared to the mean, it is more difficult to get a reliable estimate with smaller sample sizes, and second, potential outliers, such as that in the second data set, have a strong influence on the estimate.

![](images/Fig10_07.jpg)

**[FIGURE 10.7](#ch10.xhtml_f10_7b)** Sample standard deviation calculations.

This last observation leads us to consider another method for estimating the standard deviation, just as we did with the median as an estimator for the mean. An answer here is provided by the *median absolute deviation*, or *MAD*. This is a description of the steps in calculating the MAD:

1.  Find the median of the data.
2.  Compute the absolute values of the deviations of the data from the median.
3.  Find the median of those absolute values.
4.  Divide the result by 0.6745.

[Figure 10.8](#ch10.xhtml_f10_8) describes the calculation of the MAD for the two data sets. Notice that the MAD values are lower than the sample standard deviation values. This is because the MAD is less sensitive to outliers than the *s* value. Also, we observe that the two MAD values are different. This emphasizes the difficulty of getting a tight estimate of *σ* with small samples.

![](images/Fig10_08.jpg)

**[FIGURE 10.8](#ch10.xhtml_f10_8b)** Calculation of the median absolute deviation (MAD).

A natural question is about the use of the 0.6745 factor. This value comes from theory and is necessary so that the MAD approaches *σ* as the sample size becomes large.

Now we consider how to compute these estimates of dispersion with Python. See the script below.

```
 import numpy as np

x = np.array([10.1,11.5,9.6,9.6,10.4,9.4,10.2,9.9,9.1,9.8])

s = np.std(x,ddof=1)
```

```
 def MAD(x):
    xmed = np.median(x)
    xdev = abs(x-xmed)
    dmed = np.median(xdev)
    return dmed/0.6745

MADx = MAD(x)

print('sample standard deviation = {0:5.3f}'.format(s))
print('median absolute deviation (MAD)  = {0:5.3f}'.
format(MADx))
```

The results are

```
 sample standard deviation = 0.665
median absolute deviation (MAD) = 0.445
```

which duplicate those in [Figures 10.7](#ch10.xhtml_f10_7) and [10.8](#ch10.xhtml_f10_8). You will note that, in the `std` function, we use an optional argument, `ddof` = `1`. This is required for the sample standard deviation with its *n–*1 denominator. The default, `ddof` = `0`, uses a denominator *n* as appropriate for the population standard deviation. It is also worth mentioning that, from the `stats` submodule in SciPy, there is a `median_abs_deviation` function that performs the calculations of our MAD function in the script above. You will notice the argument, `scale`=`'normal'`. This incorporates a precise value of the 0.6745 constant.

```
 from scipy.stats import median_abs_deviation
MADx2 = median_abs_deviation(x, scale='normal')
```

As we leave this topic, we will mention that, for very small sample sizes, *n* ≤ 5, an adequate estimate of the standard deviation can be computed using the range, as

$\frac{range}{\sqrt{n}}$(10.3)

Although this value is not particularly applicable for our sample size of 10, the results for our two data sets are 0.76 and 2.31, respectively.

### 10.1.3 Using Boxplots to Diagnose Outliers

The *boxplot* is a useful graphical device to accompany the sample statistics calculations.[⁴](#ch10.xhtml_n10_4) It is especially effective in judging whether extreme results should be classified as outliers. Boxplots are also useful in comparing different data sets, and we will see their use for this later. These are the steps necessary in constructing a boxplot:

1.  Find the median of the data set.
2.  Compute the 25th percentile and 75th percentile of the data set.
3.  Draw a box on a vertical scale appropriate to the data with these two limits.
4.  Calculate the interquartile range (*iqr*) as the difference of these two percentiles.
5.  Draw lines, called *whiskers*, above and below the box that extend a maximum length of 1.5·*iqr*, but only to the largest (or smallest) data point still within 1.5·*iqr*.
6.  Identify any data beyond the whiskers as outliers by plotting them as points.

In [Chapter 4](#ch04.xhtml_c4), we developed a function `pctile` that computes a given percentile value of an array of values. We can include this in our previous script that computes the median for our second data set as follows:

```
 import numpy as np

def pctile(x,pct):
    y = np.sort(x)
    n = len(y)
    mp = pct/100*(n-1)
    mp1 = int(mp)
    xp = (mp-mp1)*y[mp1]+(1-(mp-mp1))*y[mp1+1]
    return xp

x = np.array([11.4,10.5,9.3,14.6,8.4,7.9,7.3,9.7,8.6,8.7])
n = len(x)

xmed = np.median(x)
x25 = pctile(x,25.)
x75 = pctile(x,75.)
iqr = x75 - x25
xwhiskhimax = x75 + 1.5*iqr
xwhisklomin = x25 - 1.5*iqr

xs = np.sort(x)
for i in range(n):
    if xs[i] > xwhisklomin:
        xwhisklo = xs[i]
        break
for i in range(n-1,-1,-1):
    if xs[i] < xwhiskhimax:
        xwhiskhi = xs[i]
        break

print('median =  {0:5.2f}'.format(xmed))
print('25th %-ile =  {0:5.2f}'.format(x25))
print('75th %-ile =  {0:5.2f}'.format(x75))
print('iqr =  {0:5.2f}'.format(iqr))
print('low whisker =  {0:5.2f}'.format(xwhisklo))
print('high whisker =  {0:5.2f}'.format(xwhiskhi))
```

These then are the parameters for the boxplot:

```
 median =   9.00
25th %-ile =   8.55
75th %-ile =   9.90
iqr =   1.35
low whisker =   7.30
high whisker =  11.40
```

Using these parameters, we can draw the boxplot and note any values that are outside the whiskers. Examining the array, we see one high value, 14.6\. The boxplot is shown in [Figure 10.9](#ch10.xhtml_f10_9). We note that the 14.6 value is an outlier; in fact, it appears to be an *extreme outlier*. This might not have been obvious just through an examination of the numbers in the set. Also, you will note that we draw a dashed line for the median location, and that line is not centered vertically in the box. When the median line is displaced from the 50th percentile, the middle of the box, that indicates that the distribution of the data, as would be shown in a *histogram* plot (recall [Section 5.4](#ch05.xhtml_h5_4)), is asymmetric. The histogram would show a tail in the direction of the greater box space, above or below the median.

![](images/Fig10_09.jpg)

**[FIGURE 10.9](#ch10.xhtml_f10_9b)** Boxplot of the second data set.

Python’s Matplotlib `pyplot` module provides a function that generates boxplots. Here is a very compact script that produces a similar plot to that in [Figure 10.9](#ch10.xhtml_f10_9). This is displayed in [Figure 10.10](#ch10.xhtml_f10_10). There is a red line across the box at *x* = 9, like our dashed line in [Figure 10.9](#ch10.xhtml_f10_9).

![](images/Fig10_10.jpg)

**[FIGURE 10.10](#ch10.xhtml_f10_10b)** Boxplot produced by the Matplotlib `pyplot` function `boxplot.`

```
 import matplotlib.pyplot as plt
plt.boxplot(x) 
```

For now, consider the use of boxplots to explore the characteristics of a data set. If outliers are identified, that should initiate an investigation to determine causes. If a cause associated with a blunder or other significant error can be identified, the outlier should be removed from the data set. This should be documented. Otherwise, the outlier should not be excluded.

## 10.2 Distributions

We have discussed the relationship between a data sample and its related population. [Figure 10.11](#ch10.xhtml_f10_11) describes this concept. We do not know the true nature of the population. Our data set represents sampled observations of the population. From the data, we would like to characterize the entire population, but we only have a partial, often very partial, view of it. That means that any sample statistics or estimates, like the average, which lacks certainty in its determination of the mean of the population.

![](images/Fig10_11.jpg)

**[FIGURE 10.11](#ch10.xhtml_f10_11b)** Relationship of data set to population through observation.

In this section, we are going to discuss how to describe the population. In most cases, the population is infinite in extent. This is common when the contents are real numbers. Our measurement lens, with finite resolution, may not allow us to see the infinite population, but, if the resolution is relatively fine, it may come close. The fundamental descriptor of a population is its *distribution*. We can relate this to the histogram plots from [Chapter 5](#ch05.xhtml_c5).

The histogram plot is generated from a data sample, or possibly an entire finite population. [Figure 5.19](#ch05.xhtml_f5_19) showed an example based on a data set of 40 piston ring measurements. We repeat that here as [Figure 10.12](#ch10.xhtml_f10_12). You will note that the ordinate here is frequency, the number of measurements that fall in the given interval. An alternate presentation is to represent the fraction of measurements that occur in each interval, called the *relative frequency*. This is shown in [Figure 10.13](#ch10.xhtml_f10_13).

![](images/Fig10_12.jpg)

**[FIGURE 10.12](#ch10.xhtml_f10_12b)** Histogram chart of piston data.

![](images/Fig10_13.jpg)

**[FIGURE 10.13](#ch10.xhtml_f10_13b)** Relative frequency histogram chart of piston data.

The sum of the heights of the bars in [Figure 10.12](#ch10.xhtml_f10_12) is 40, which is the sample size; whereas, the sum of the heights in [Figure 10.13](#ch10.xhtml_f10_13) is one. Given our data set, we can estimate that the probability of measuring a value in each interval is the height of its bar. Now, imagine that we increase the sample size greatly and narrow the bin widths to a tiny value. Concurrently, we divide the relative frequency by the interval width. If we just plot the peaks of the bars versus the piston diameter, the picture emerging might be that illustrated in [Figure 10.14](#ch10.xhtml_f10_14).

![](images/Fig10_14.jpg)

**[FIGURE 10.14](#ch10.xhtml_f10_14b)** Possible density function for distribution of piston diameters.

Instead of dealing with individual bar heights, in [Figure 10.14](#ch10.xhtml_f10_14) we have a continuous curve. The area under the curve is one, just as the sum of the heights in [Figure 10.13](#ch10.xhtml_f10_13) is one. To be clear, the area under one point on the curve is zero. This curve is called a *density function*, *f*(*x*). If we want to determine the probability of obtaining a measurement in a finite interval, that corresponds to the area under the curve for that interval, or

*P*[*a* ≤ *x* ≤ *b*] = ∫[*a*]^(*b*)*f*(*x*)*d**x*(10.4)

You will note that the density function must have the units of 1/*x*. We solved a problem like this in the previous chapter; see [Example 9.1](#ch09.xhtml_exa9_1) and [Figure 9.11](#ch09.xhtml_f9_11).

Given a density function for a population, we want to introduce the definitions of population mean and variance (square of the standard deviation). The formulas for these are[⁵](#ch10.xhtml_n10_5)

*μ* = ∫[−∞]^∞*x* *f*(*x*)*d**x*    *σ*² = ∫[−∞]^∞(*x* − *μ*)²*f*(*x*)*d**x*(10.5)

Taking a close look at the first formula, we see that the mean, *μ*, is a weighted average of the variable, *x*, over the entire domain, where the weighting is the density function, *f*(*x*). For the second formula, the variance is the weighted average of the squared deviation from the mean. These are the population parameters, and, in general, we do not have direct knowledge of them. However, if we have a mathematical model for the density, we can determine them.

### 10.2.1 Several Important Distributions

There are many different theoretical *density functions*. We will highlight three here because they are commonplace in reference or use.

#### 10.2.1.1 Uniform Distribution

The *uniform distribution* is illustrated in [Figure 10.15](#ch10.xhtml_f10_15). Evaluating the formulas in Equations 10.4 and [10.5](#ch10.xhtml_f10_5), we get

![](images/Fig10_15.jpg)

**[FIGURE 10.15](#ch10.xhtml_f10_15b)** Density function for the uniform distribution.

$P\left\lbrack {\alpha \leq x \leq \beta} \right\rbrack = \frac{\beta - \alpha}{b - a}\quad\quad\mu = \frac{b + a}{2}\quad\quad\sigma = \frac{b - a}{2\sqrt{3}}$(10.6)

For example, if *a* = −1 and *b* = +1,

$P\left\lbrack {\alpha \leq x \leq \beta} \right\rbrack = \frac{\beta - \alpha}{2}\quad\quad\mu = 0\quad\quad\sigma = \frac{1}{\sqrt{3}}$(10.7)

In practice, we don’t run into the uniform distribution that often. With discrete variables, it’s common in situations like coin tosses or the toss of a six-sided die. Each result is equally probable. With data acquired from measurements of physical and chemical phenomena, there is usually a central tendency that is more probable than values far from the mean. However, if the range is reasonably defined, but there is no evidence supporting a particular distribution, the uniform distribution is sometimes used to reflect our lack of knowledge.

#### 10.2.1.2 Normal Distribution

The most common and frequently encountered distribution is the *normal distribution* (also called *Gaussian distribution*). As we illustrated in [Example 9.1](#ch09.xhtml_exa9_1), its density function is

$f(x) = \frac{1}{\sigma\sqrt{2\pi}}\, e^{- \frac{1}{2}{(\frac{x - \mu}{\sigma})}^{2}}$(10.8)

As implied by the symbols used, its mean is *μ*, and standard deviation is *σ*. The density is a bell-shaped curve centered on *μ*. This is shown in [Figure 10.16](#ch10.xhtml_f10_16). We know how the curve is related to *μ*, but how is it related to *σ*? In the figure, since *σ* = 10, we can judge that most of the area under the curve is accounted for between *μ* ± 3*σ*. There is a useful interpretation called the *normal probability rule* relating the area (or probability) to multiples of *σ*.

![](images/Fig10_16.jpg)

**[FIGURE 10.16](#ch10.xhtml_f10_16b)** Normal distribution density function for *μ* = 100 and *σ* = 10.

| ± *σ* | probability |
| --- | --- |
| 1 | 68% |
| 2 | 95% |
| 3 | 99.7% |

As we mentioned in [Chapter 9](#ch09.xhtml_c9), there is a simplified version of this distribution called the *standard normal distribution* where *μ* = 0 and *σ* = 1\. Typically, the random variable name used with this distribution is *z*, and its relationship to *x* in the normal distribution is

$z = \frac{x - \mu}{\sigma}$(10.9)

#### 10.2.1.3 Weibull Distribution

As we observe histogram charts of data sets, we find many well-suited to modeling with the normal distribution. However, there is one characteristic we observe that is counter to that distribution. That is lack of symmetry, or *asymmetry*. There are several distributions that allow for the modeling of asymmetry. One which is commonly used in the manufacturing industry to model product reliability is the *Weibull distribution*. Its density function is

$f(x) = \frac{\alpha}{\beta^{\alpha}}x^{\alpha - 1}e^{- \,{({x/\beta})}^{\alpha}}\quad x \geq 0$(10.10)

where

1.  *α*: scale parameter > 0, and
2.  *β*: shape parameter > 0.

It is depicted in [Figure 10.17](#ch10.xhtml_f10_17). You can see how this example of the density function allows for asymmetry with a longer “tail” to the right. There are other distributions, such as the log-normal and gamma, that also provide asymmetric density functions.

![](images/Fig10_17.jpg)

**[FIGURE 10.17](#ch10.xhtml_f10_17b)** Density function for the Weibull distribution, *α* = 2.0 and *β* = 4.5.

### 10.2.2 Python and Distributions

The SciPy `stats` submodule provides functions to compute probabilities for various distributions. For example, the brief Python script below computes a value of the normal density and a probability for two values of *x*. The normal density is computed using the `norm.pdf` function. The `pdf` notation stands for “probability density function.” To compute the area between *a* and *b* values of *x*, the `norm.cdf` function is used twice. The `cdf` notation is for “cumulative probability function.” It calculates the area from the extreme left up to the first argument. First, the area up to *b* is computed; then the area up to *a* is computed. The area or probability between *a* and *b* is then the difference of the two cumulative probabilities.

```
 from scipy import stats

mu = 100
sigma = 10
a = 75
b = 95

f = stats.norm.pdf(b,mu,sigma)
print('normal density = {0:6.4f}'.format(f))
cp1 = stats.norm.cdf(b,mu,sigma)
cp2 = stats.norm.cdf(a,loc=mu,scale=sigma)
p = cp1-cp2
print('probability = {0:5.1f}%'.format(p*100))

normal density = 0.0352
probability =  30.2%
```

It is worth noting that, following [Example 9.1](#ch09.xhtml_exa9_1), we can compute probabilities using quadrature of the density function. Similar functions are available in the `stats` module for different distributions, e.g. uniform, Weibull, log-normal, and gamma.

A natural question to ask at this point is how we determine from our data set which distribution appears to be appropriate to represent the population. And, once a distribution is identified, how do we estimate the parameters of the distribution. We will get to that in the next main section.

### 10.2.3 Random Numbers

There are occasions in numerical calculations where we want to simulate values that are drawn at random from specific distributions. This is called *random number generation*. The methods used to generate random numbers are interesting, but they are beyond the scope of this text. Here, we will use Python’s built-in functions that provide these. Such random numbers are formally called *pseudorandom* since they are not ideally sampled from a population but are close to that.

An effective way to test random number generation is to create a histogram chart of the results and see how they relate to the corresponding density function. Here is an example Python script for the uniform distribution with 10,000 random samples.

```
 import numpy as np
import matplotlib.pyplot as plt

x = np.random.uniform(0,1,10000)

histvals,bin_edges = np.histogram(x)

bin_width = bin_edges[1]-bin_edges[0]
n = len(histvals)
bin_centers = np.zeros((n))
for i in range(n):
    bin_centers[i] = (bin_edges[i]+bin_edges[i+1])/2

plt.bar(bin_centers,histvals,width=bin_width,color='w',
edgecolor='k')
plt.title('uniform random numbers')
```

The histogram chart created is shown in [Figure 10.18](#ch10.xhtml_f10_18). We recognize the pattern as being relatively flat. That is what we would expect from the uniform distribution population.

![](images/Fig10_18.jpg)

**[FIGURE 10.18](#ch10.xhtml_f10_18b)** Uniform random number generation. Sample size = 10,000.

As a second example, we will create an array representing a sinusoidal signal with random noise added where the random number generator is for the normal distribution.

## 10.3 Making Claims Based on Data

The real world provides us with data that are variable and uncertain. This uncertainty must be assessed when data are used to make important decisions and claims. Here are several practical scenarios:

1.  A product must meet a certain specification. Data are collected and used to support a claim that the specification is met or not met.
2.  Environmental measurements were made decades ago. A new set of measurements is acquired, and a claim is made that there has been a significant change.
3.  A customer has noted that the variability in the quality of a product is too high. Measures are considered to reduce variability and need to be judged whether they would be successful.
4.  To proceed with an analysis, we must support a claim that the variability in a data set is adequately modeled by the normal distribution.

Although it may appear as an academic exercise to you now, sooner or later you will be required to make claims based on data. For example, most engineering and science curricula will require you to take one or more laboratory courses where conclusions must be made regarding measurements. Further, you should realize that, at some point in the coming years, your job and future may depend on doing this with care and taking uncertainty into account. This section is designed to introduce you to the methods and issues associated with doing this correctly.

There are two methods that are commonly used to analyze data for the purpose of making claims. These are called *parametric* and *non-parametric* tests. Parametric tests involve assuming a distribution for the population from which the data are sampled, and non-parametric tests do not. If the choice of the distribution is correct, parametric tests are more discriminatory than non-parametric tests.

In this section, we will consider two categories of tests on data. The first is comparison of the data to a standard. The second is comparing two data sets. This is a significant topic in applied statistics.[⁷](#ch10.xhtml_n10_7) Because our treatment here will be brief, we will consider one characteristic of data: the mean. We will also consider testing the data to evaluate whether they appear to be drawn from the normal distribution, since parametric tests can depend on this being supported.

### 10.3.1 Comparison of Data with a Standard

As a precaution, it is worth mentioning that statistical methods and arguments should not be used where they are not needed. [Figure 10.21](#ch10.xhtml_f10_21) illustrates one such situation with a boxplot. The data represent the weights in grams of 200 product packets. The specification is that the packets must weigh at least 40 g. We can see that all 200 weights are well above 40 g, despite four outliers. We can make a strong claim that the specification is met. We might be concerned about the variability and the outliers, but that is a separate issue. So, a first consideration before diving into statistical methods and analysis is whether they are needed at all. No need to do work that is not required.

![](images/Fig10_21.jpg)

**[FIGURE 10.21](#ch10.xhtml_f10_21b)** Boxplot of 200 product measurements.

First, we will consider how to use a data set to make a claim about the mean (or median) value of the population. It may be obvious, but is worth stating anyway, that the larger your sample size, the easier it will be to make a claim. The problem with this is that often collecting data is time-consuming and possibly expensive. So, you must find a middle ground where you have enough data to evaluate a claim without exceeding your time and budgetary constraints.

Since uncertainty is associated with any statistical analysis, there is the possibility that a claim may be false. One could describe this as “the risk of being wrong.” Formally, this is called a *Type I error*[⁸](#ch10.xhtml_n10_8) and is represented by a probability, *α*. Of course, we would like for this value to be small. Typical desired values are 5% and 1% (one chance in 20, and 1 in 100, respectively).

One of the simplest non-parametric tests is called the *sign test*. It applies to claims about the median value, not the mean value. If a histogram chart of the data looks symmetric, these two values will be close. The procedure for the sign test is as follows for a data set with a sample size, *n*, where the claim is *μ̃* > *μ̃*[0].

1.  Specify a standard value of the median, *μ̃*[0], for comparison.
2.  Compute the differences between the data and the standard.
3.  Count the numbers of +  signs, *r*^+, from the differences.

If *r*^+ > *n*/2, calculate this probability[⁹](#ch10.xhtml_n10_9)

$P = {\sum\limits_{r = r^{+}}^{n}{\begin{pmatrix} n \\ r \end{pmatrix}0.5^{r}0.5^{n - r}}}$(10.12)

where

1.  $\begin{pmatrix} n \\ r \end{pmatrix} = \frac{n!}{r!\left( {n - r} \right)!}$ ⇒ the number of combinations of *n* items taken *r* at a time
2.  *n*! ⇒ *n* factorial, *n* ⋅ (*n* − 1) ⋅ (*n* − 2)⋯2

The *P-value* is the probability that you could have counted *r*^+ or greater if *μ̃* = *μ̃*[0]. The *P-*value represents the risk of being wrong if we make the claim, *μ̃* > *μ̃*[0]. If it is small, we have grounds to make the claim.

Alternately, we can formulate the test for the claim, *μ̃* < *μ̃*[0]. Repeating steps 1 and 2 above, we replace step 3 with counting the − signs, *r*^−, from the differences. If *r*^− < *n*/2, this probability is calculated

$P = {\sum\limits_{r = 0}^{r^{-}}{\begin{pmatrix} n \\ r \end{pmatrix}0.5^{r}0.5^{n - r}}}$(10.13)

This *P*-value is the probability that you could have counted *r*^− or less if *μ̃* = *μ̃*[0]. A small *P*-value provides grounds to make the claim.

Let’s illustrate this with an example. Forty measurements of the weight of small sugar packets are shown in [Table 10.1](#ch10.xhtml_t10_1).

[**TABLE 10.1**](#ch10.xhtml_t10_1b) Weights of 40 Sugar Packets (g)

| 40.31 | 41.05 | 39.85 | 40.27 |
| 40.75 | 40.80 | 39.67 | 40.34 |
| 39.71 | 40.31 | 40.70 | 40.00 |
| 40.34 | 40.69 | 40.44 | 40.42 |
| 40.06 | 40.30 | 40.23 | 40.17 |
| 40.34 | 40.50 | 40.46 | 40.10 |
| 40.11 | 40.45 | 40.58 | 39.79 |
| 40.32 | 39.55 | 39.54 | 39.69 |
| 40.42 | 40.04 | 40.73 | 40.39 |
| 39.78 | 40.17 | 39.66 | 39.90 |

We would like to argue and claim that the median packet weight meets or exceeds the specification of 40 g. By calculating the differences between the measurements and 40 g and then counting the + signs, we come up with *r*^+ = 29\. Using Equation 10.12, *P* ≅ 0.1%. Consequently, with minimal risk of 1 in 1,000, we can support the claim that the specification is met. We should mention that there are other non-parametric tests than the sign test. One that is popular is the *Wilcoxon signed-rank test* ([Montgomery and Runger, 2018](#ch11_ref.xhtml_r9)).

Now we consider a corresponding parametric test where we assume that the population is well-modeled by the normal distribution. We’ll come back to check this assumption later. The first step is to obtain estimates for the parameters of the normal distribution of sample averages, *μ* and $\sigma/\sqrt{n}$.[^(10)](#ch10.xhtml_n10_10) For these, we use the sample average, $\overline{x}$, and sample standard deviation, *s*, divided by $\sqrt{n}$, respectively. Next, using the normal distribution with a mean of the standard, *μ*[0], and standard deviation, *s*, we calculate what the probability of computing a sample mean ≥ *μ*. If that probability is small, it supports our claim.[^(11)](#ch10.xhtml_n10_11)

For our packet data, $\overline{x}$ ≅ 40.22, *s* ≅ 0.37, *n* = 40\. The probability that the average of such a sample would be ≥ 40.22, if *μ* is actually 40, can be computed in a Python script as

```
 import numpy as np
from scipy import stats

mu0 = 40 # mean standard
n = 40 # sample size
xbar = 40.22 # sample average
s = 0.37 # sample standard deviation

# probability to the right of xbar
P = 1 - stats.norm.cdf(xbar,mu0,s/np.sqrt(n))

print('probability = {0:6.3f}%'.format(P*100))
```

and the result is

```
 probability = 0.008%
```

This small probability provides a strong basis to support our claim that *μ* > 40 g. Notice that the probability here is even smaller than that for the sign test. This is because the parametric test is more discriminatory, but it comes with the assumption of a normal distribution.

### 10.3.2 Comparison between Two Samples

Next, we will consider a comparison test between two samples, denoted A and B. First, we would like to claim that the means of the two samples are significantly different, for example, *μ*[B] > *μ*[A]. This is an important test that engineers and scientists encounter frequently. A common non-parametric test for this is the *Wilcoxon rank-sum test*. As above, we will illustrate this with two example data sets.

| A | B |
| --- | --- |
| 11.29 | 11.67 |
| 9.65 | 9.58 |
| 8.17 | 10.23 |
| 9.86 | 9.00 |
| 10.76 | 10.25 |
| 9.10 | 11.55 |
| 7.75 | 12.19 |
| 9.05 | 11.94 |
| 10.95 | 8.71 |
| 8.34 | 12.38 |

It is useful to examine a side-by-side boxplot of these data. Here is the Python script that produces that comparison in [Figure 10.22](#ch10.xhtml_f10_22).

![](images/Fig10_22.jpg)

**[FIGURE 10.22](#ch10.xhtml_f10_22b)** Side-by-side boxplot of samples A and B.

```
 import numpy as np
import matplotlib.pyplot as plt

xA = np.array([11.29,9.65,8.17,9.86,10.76,9.1,7.75 \
               ,9.05,10.95,8.34])
xB = np.array([11.67,9.58,10.23,9.,10.25,11.55\
               ,12.19,11.94,8.71,12.38])

x = np.array([xA, xB]).transpose()

plt.boxplot(x, labels =('A', 'B'))
plt.grid()
```

This is interesting because the box of sample B is above that of sample A, but the difference isn’t clear, as they overlap. The message here is that statistics are needed.

With the Wilcoxon test, we sift the two samples together, keeping track of their sample designation, and sort the result in ascending order. We assign the ranks (sequence of numbers 1, 2, 3,…) to the resulting array. Then, we sum the A and B ranks separately. If the means of the two samples are the same, we would expect these sums to be roughly equal. If the sums are different, we can judge if this difference is significant enough to support our claim.

The table below shows the combined samples with A and B designations and ranks. The sum of the ranks for A is 80 and for B is 130\. For these sample sizes, available tables for the Wilcoxon test[^(12)](#ch10.xhtml_n10_12) provide threshold values of 82 and 128 for an *α* risk value of 5% (i.e. a 1 in 20 chance that the conclusion is wrong). To support our claim for this level of risk, the sum of ranks for A must be ≤ 82 and for B must be ≥128\. That is the case here, so the claim would be supported. We would be taking a risk lower than 5% to support the claim that the two samples are different.

| 7.75 | A | 1 | 10.23 | B | 11 |
| 8.17 | A | 2 | 10.25 | B | 12 |
| 8.34 | A | 3 | 10.76 | A | 13 |
| 8.71 | B | 4 | 10.95 | A | 14 |
| 9.00 | B | 5 | 11.29 | A | 15 |
| 9.05 | A | 6 | 11.55 | B | 16 |
| 9.10 | A | 7 | 11.67 | B | 17 |
| 9.58 | B | 8 | 11.94 | B | 18 |
| 9.65 | A | 9 | 12.19 | B | 19 |
| 9.86 | A | 10 | 12.38 | B | 20 |

Python’s SciPy module has a `ranksums` function that performs the Wilcoxon test. Here is a script that shows you how to use it.

```
 import numpy as np
from scipy import stats

xA = np.loadtxt('SampleA.csv', delimiter =', ')
xB = np.loadtxt('SampleB.csv', delimiter =', ')

result = stats.ranksums(xA, xB, alternative ='less')
print('P-value = {0:5.2f}%'.format(result.pvalue*100))
```

The *P*-value displayed is

```
 P-value =  2.94%
```

which would support the claim that the means are different.

Alternately, we can use a parametric test to compare the means of two samples. We won’t go into details of the method here, as we did for the one-sample parametric test. Here is a Python script that performs the comparison test.

```
 import numpy as np
from scipy import stats

xA = np.loadtxt('SampleA.csv', delimiter =', ')
xB = np.loadtxt('SampleB.csv', delimiter =', ')

result = stats.ttest_ind(xA, xB)
p = result.pvalue/2
print('P-value = {0:5.2f}%'.format(p*100))
```

The *P*-value displayed in the Console is

```
 P-value = 2.20%
```

If our criterion for acceptable risk were 5%, the lower *P*-value meets that and supports our claim that the mean of sample A is less than the mean of sample B. You will note again that the *P*-value for the parametric test is lower than that for the Wilcoxon test, the parametric test being more discriminatory.

Tests on the variance, and related standard deviation, are important in the modeling and management of product variability. High variability impacts product quality and customer satisfaction negatively. Also, the lower the variability, the closer we can control the mean to meet a specification. These tests are important, but we don’t take the time to detail them here.

### 10.3.3 Determining Whether Data Are Normally Distributed

In the previous sections, we have seen that the more discriminatory parametric tests are only appropriate when we have confidence that the data adequately follow a particular distribution; in our examples, the normal distribution. Therefore, the final topic we address in this section is determining whether the population from which data are extracted is adequately modeled by the normal distribution. A useful tool in assessing this is the *cumulative distribution*, which is given by the following integral,

*F*(*x*) = ∫[−∞]^(*x*)*f*(*x*^′)*d**x*^′(10.13)

where *f* (*x*) : the normal density function and *x*΄ is a dummy variable.

In words, this is the area to the left of *x* on the plot of the density function. This is illustrated in [Figure 10.23](#ch10.xhtml_f10_23). Since the normal density cannot be integrated analytically, we must find the cumulative distribution numerically using quadrature, as we introduced in the previous chapter in [Example 9.1](#ch09.xhtml_exa9_1)[^(13)](#ch10.xhtml_n10_13).

![](images/Fig10_23.jpg)

**[FIGURE 10.23](#ch10.xhtml_f10_23b)** Relationship between the density function and cumulative probability function.

Plotting the cumulative distribution, we get an S-shaped or *sigmoidal curve* instead of the bell-shaped curve of the density function. To illustrate this, we will use the standard normal density (*μ* = 0 and *σ* = 1),

$f(z) = \frac{1}{\sqrt{2\pi}}e^{- \frac{z^{2}}{2}}$(10.14)

Based on [Example 9.1](#ch09.xhtml_exa9_1), we create a Python script to produce a plot of the cumulative distribution. The result is shown in [Figure 10.24](#ch10.xhtml_f10_24). Here, we have displayed the cumulative probability in per cent.

![](images/Fig10_24.jpg)

**[FIGURE 10.24](#ch10.xhtml_f10_24b)** Cumulative probability plot for the standard normal distribution.

```
 import numpy as np
from scipy.integrate import quad
import matplotlib.pyplot as plt

stdnormdens = lambda z: 1/np.sqrt(2*np.pi)*np.exp(-1/2*z**2)

z = np.linspace(-4,4,200)
n = len(z)
F = np.zeros(n)
for i in range(n):
F[i], eF = quad(stdnormdens, -4,z[i])

plt.plot(z, 100*F, c='k')
plt.grid()
plt.xlabel('z')
plt.ylabel('F(z) %') 
```

A data set can be displayed on this plot in order to judge whether the data follow a normal distribution. To do this, we first must “standardize” the data using the formula

$z = \frac{x - \mu}{\sigma} \cong \frac{x - \overline{x}}{s}$(10.15)

Next, we sort the `z` array and compute the percentile for each data point using

$pct = \frac{i - 0.5}{n} \cdot 100i = 1,\ldots,n$(10.16)

The `pct` array can then be added to the plot in [Figure 10.24](#ch10.xhtml_f10_24) as data markers.

Using the sugar packet data from [Table 10.1](#ch10.xhtml_t10_1), we can add to the above script to place the standardized data on the plot. This is shown in [Figure 10.25](#ch10.xhtml_f10_25). You can see that the data follow the standard normal curve closely. This leads us to conclude, at least qualitatively, that the data are representative of a normally distributed population.

![](images/Fig10_25.jpg)

**[FIGURE 10.25](#ch10.xhtml_f10_25b)** Cumulative probability plot with standardized data added.

```
 x = np.loadtxt('PacketData.csv', delimiter=', ')
xs = np.sort(x)
xbar = np.mean(xs)
s = np.std(xs)
z = (xs-xbar)/s
n = len(xs)
p = np.zeros(n)
for i in range(n):
    p[i] = (i+0.5)/n

plt.scatter(z, p*100,c = 'k', marker ='.')
```

This raises a question: How would it look if the data were not drawn from a normal population? Here is an alternate script line which uses data simulated from the Weibull distribution.

```
 x = np.random.weibull(1.2,100)
```

The plot is shown in [Figure 10.26](#ch10.xhtml_f10_26), and it is obvious that the data are not representative of samples from a normal distribution.

![](images/Fig10_26.jpg)

**[FIGURE 10.26](#ch10.xhtml_f10_26b)** Simulated data from the Weibull distribution on the standard normal cumulative probability plot.

It is also possible to create a nonlinear vertical scale that transforms the cumulative probability curve into a straight line. Then, judging the alignment of data is easier. This has been done manually for decades using *probability graph paper*.[^(14)](#ch10.xhtml_n10_14)

It is also possible to “linearize” the cumulative probability curve using *z-scores* instead of cumulative probabilities. For example, for a cumulative probability of 5%, the point on the *z* axis that corresponds is called the *z-score*. It is found by using the inverse of the cumulative probability function. In Python, via the SciPy `stats` module, you can compute this with the `norm.ppf` function. For the 5% *z*-score,

```
 from scipy import stats

cumP = 0.05
zscore = stats.norm.ppf(cumP)
print('z-score = {0:5.2f}'.format(zscore))

z-score = -1.64
```

If we modify the script that produces [Figure 10.25](#ch10.xhtml_f10_25) to replace percentiles with *z*-scores, here is the resulting script. The probability plot is then shown in [Figure 10.27](#ch10.xhtml_f10_27), where you can easily recognize the linearization.

![](images/Fig10_27.jpg)

**[FIGURE 10.27](#ch10.xhtml_f10_27b)** Probability plot with *z*-scores.

```
 import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

x = np.loadtxt('PacketData.csv', delimiter =', ')
xs = np.sort(x)
xbar = np.mean(xs)
s = np.std(xs)
z = (xs-xbar)/s
n = len(xs)
p = np.zeros(n)
zsc = np.zeros(n)
for i in range(n):
    p[i] = (i+0.5)/n
    zsc[i] = stats.norm.ppf(p[i])

plt.scatter(z, zsc, c = 'k', marker ='.')
plt.plot(z, z, c='k', ls='--')
plt.grid()
plt.xlabel('z')
plt.ylabel('z-score')
```

Note that Python SciPy’s `stats` module has a `probplot` function that produces a similar plot based on *z*-scores. The plot produced by `probplot` reverses the axes and doesn’t transform the data into a *z* array. We will illustrate the use of `probplot` in [Section 10.4.3](#ch10.xhtml_h10_4_3).

Earlier, we introduced the idea of a statistical test and a *P*-value to assess the Type I error (*α*) risk. There are similar tests for probability distributions. We will illustrate one here, called the *Anderson-Darling test*, with an addition to our Python script. This test seeks to prove that the distribution is not normal.

```
 result = stats.anderson(x, dist='norm')
print(result)
```

The display is

```
 AndersonResult(statistic=3.088203603370033, critical_
values=array([0.555, 0.632, 0.759, 0.885, 1.053]),
significance_level=array([15\. , 10\. , 5\. , 2.5, 1\. ]))
```

We interpret this in the following way. For a significance level of 5., the critical value of the statistic is 0.759\. Since the statistic, 3.088..., is greater than the critical value, it leads to the claim that the data do not follow a normal distribution. If we apply the same test to the sugar packet data, the results are

```
 AndersonResult(statistic=0.25340941601047007, critical_
values=array([0.565, 0.644, 0.772, 0.901, 1.071]),
significance_level=array([15\. , 10\. , 5\. , 2.5, 1\. ]))
```

and, since 0.253... < 0.772, the claim that the distribution is not normal is rejected.

As we have stated before, this section is, in fact, a brief introduction to statistical tests, often called *hypothesis tests*. In a course on applied statistics, you will acquire a broader knowledge of this topic. We recommend that you take such a course.

## 10.4 Fitting Mathematical Models to Data

Scientists and engineers frequently develop methods to interpret data to gain understanding and predict behavior and values not in the data set. This is most often done by developing mathematical models based on the data. We’ve seen an example of this in [Figure 9.13](#ch09.xhtml_f9_13). Although we show a proposed polynomial model there that appears to follow the data well, we deferred explaining how we came up with that model. We then utilized the model to accomplish a quadrature. We will show how we developed that model in this section.

### 10.4.1 Straight-line Linear Regression

The mathematical procedure to fit a model to data is called *regression*. We start here with the simple scenario of fitting a straight line to a data set. Then we move on to models which allow curvature, mainly polynomials. Finally, we review models for which we cannot use the linear regression methods developed for straight lines and polynomials.

Consider the scenario presented in [Figure 10.28](#ch10.xhtml_f10_28). Here we have plotted a set of 11 data from {*x*[i], *y*[i], *i* = 1,…, 11}. A straight-line model, *y* = *a x* + *b*, is proposed and plotted. For each value of *x*, we can use the model to compute a model prediction,

![](images/Fig10_28.jpg)

**[FIGURE 10.28](#ch10.xhtml_f10_28b)** Scenario for straight-line regression.

*ŷ*[*i*] = *a* *x*[*i*] + *b*(10.17)

For each prediction, there is a *residual error*,

*e*[*i*] = *ŷ*[*i*] − *y*[*i*](10.18)

A general sense of fitting the model to the data is that we would like the residual errors to be small. To do this, we need a single criterion or objective to use in judging the residual errors. We could use the sum of absolute values of the residuals, but it is preferred to use the sum of the squares of the residual errors because this is more sensitive to the influence of one or more large errors. We then want to adjust our straight line, the *a* and *b* parameters, to minimize this “least squares” criterion,

$V = \,{\sum\limits_{i = 1}^{n}e_{i}^{2}} = {\sum\limits_{i = 1}^{n}\left( {{\hat{y}}_{i} - y_{i}} \right)^{2}} = {\sum\limits_{i = 1}^{n}\left( {a\, x_{i} + b - y_{i}} \right)^{2}}$(10.19)

The question then is how do we minimize *V* by the selection of *a* and *b*? It turns out that we can use calculus to determine this by finding the partial derivatives of *V* with respect to those two parameters, setting those two expressions equal to zero, and solving for *a* and *b*. Here are the derivative expressions:

$\frac{\partial V}{\partial a} = 2{\sum\limits_{i = 1}^{n}{x_{i}\left( {a\, x_{i} + b - y_{i}} \right)}} = 2a{\sum\limits_{i = 1}^{n}x_{i}^{2}} + 2b{\sum\limits_{i = 1}^{n}x_{i}} - 2{\sum\limits_{i = 1}^{n}{x_{i}y_{i}}}$(10.20)

$\frac{\partial V}{\partial b} = 2{\sum\limits_{i = 1}^{n}\left( {a\, x_{i} + b - y_{i}} \right)} = 2a{\sum\limits_{i = 1}^{n}x_{i}} + 2nb - 2{\sum\limits_{i = 1}^{n}y_{i}}$(10.21)

Setting both derivative expressions equal to zero to find the minimum,

$a{\sum\limits_{i = 1}^{n}x_{i}^{2}} + b{\sum\limits_{i = 1}^{n}x_{i}} - {\sum\limits_{i = 1}^{n}{x_{i}y_{i}}} = 0$(10.22)

$a{\sum\limits_{i = 1}^{n}x_{i}} + nb - {\sum\limits_{i = 1}^{n}y_{i}} = 0$(10.23)

Solving Equation 10.23 for *b*, we get

$b = \frac{\sum\limits_{i = 1}^{n}y_{i}}{n} - a\frac{\sum\limits_{i = 1}^{n}x_{i}}{n} = \overline{y} - a\,\overline{x}$(10.24)

Substituting Equation 10.24 into Equation 10.23 and solving for *a*, the steps are

$\begin{array}{l} {a{\sum\limits_{i = 1}^{n}x_{i}^{2}} + \left( {\frac{\sum\limits_{i = 1}^{n}y_{i}}{n} - a\frac{\sum\limits_{i = 1}^{n}x_{i}}{n}} \right){\sum\limits_{i = 1}^{n}x_{i}} - {\sum\limits_{i = 1}^{n}{x_{i}y_{i}}} = 0} \\ {an{\sum\limits_{i = 1}^{n}x_{i}^{2}} - a\left( {\sum\limits_{i = 1}^{n}x_{i}} \right)^{2} + {\sum\limits_{i = 1}^{n}{x_{i}{\sum\limits_{i = 1}^{n}y_{i}}}} - n{\sum\limits_{i = 1}^{n}{x_{i}y_{i}}} = 0} \\ {a = \frac{n{\sum\limits_{i = 1}^{n}{x_{i}y_{i}}} - {\sum\limits_{i = 1}^{n}{x_{i}{\sum\limits_{i = 1}^{n}y_{i}}}}}{n{\sum\limits_{i = 1}^{n}x_{i}^{2}} - \left( {\sum\limits_{i = 1}^{n}x_{i}} \right)^{2}}} \end{array}$(10.25)

By solving for *a* using the final form of Equation 10.25, we can substitute that in Equation 10.24 to determine *b*.

### 10.4.2 Fitting Polynomials

Next, we will consider fitting models that are more complicated than just a straight line. For example, we might want to fit a second-order polynomial model,

*y* = *b*[0] + *b*[1]*x* + *b*[2]*x*²(10.26)

and we can generalize this to a polynomial of order *m*,

*y* = *b*[0] + *b*[1]*x* + … + *b*[*m* − 1]*x*^(*m* − 1) + *b*[*m*]*x*^(*m*)(10.27)

If we attempt to derive the formulas for the least squares fit of the model parameters in the same manner as we did for the straight line, these become very cumbersome. There is a more compact, efficient way to approach the problem using a vector/matrix description, but we do not introduce that here (see Chapra & Clough 2022 for more information on the vector/matrix description). It would be more appropriate for a course in applied statistics or numerical methods. Instead, we will rely on a function available from the NumPy module, `polyfit`.

The syntax for the `polyfit` function is

```
 coeff = polyfit(x,y,order)
```

where `x` is the independent variable array, `y` is the response array, and `order` is an integer for the order of the polynomial being fit. The `coeff` result is an array of the polynomial coefficients from highest order to the intercept. As a simple example, we can replicate our straight-line fit of the CO[2] data as follows:

```
 import numpy as np

yr, amt = np.loadtxt('CO2_Emissions.csv', delimiter=', ',
unpack=True)

b = np.polyfit(yr, amt, 1)
print(b)

[-7.00725275e+01 1.46438105e+05]
```

The coefficients displayed are the same as those we computed previously.

With the `polyfit` function in hand, we have a general method for polynomial models of any order. We can apply this to the data from [Chapter 9](#ch09.xhtml_c9), [Figure 9.13](#ch09.xhtml_f9_13).

| t | y |
| --- | --- |
| 0.09 | 15.1 |
| 0.32 | 57.3 |
| 0.69 | 103.3 |
| 1.51 | 174.6 |
| 2.29 | 191.5 |
| 3.06 | 193.2 |
| 3.39 | 178.7 |
| 3.63 | 172.3 |
| 3.77 | 167.5 |

We proposed a third-order polynomial to fit these data. Here is a Python script that carries that out.

```
 import numpy as np

t = np.array([0.09,0.32,0.69,1.51,2.29,3.06,3.39,3.63,3.77])
y = np.array([15.1,57.3,103.3,174.6,191.5,193.2,178.7,/
172.3, 167.5])

b = np.polyfit(t, y, 3)

print('cubic polynomial parameters:\n', b)
```

The results displayed in the Console are

```
 cubic polynomial parameters:
[  4.3507208  -53.87521322 185.62642213 0.55854906]
```

which yield the polynomial model we proposed in [Chapter 9](#ch09.xhtml_c9),

*y* = 0.559 + 185.6 *t* − 53.88 *t*² + 4.351 *t*³

[Figure 9.13](#ch09.xhtml_f9_13) shows the model line and the data.

### 10.4.3 General Issues and Precautions

To complete our discussion of polynomial regression, we will discuss some general issues and precautions. First, the concept of *parsimony* is important. By parsimony, we mean that we should seek the simplest model that fits the data well.[^(16)](#ch10.xhtml_n10_16) This leads us to the concept of *model adequacy*.

A way to quantify these concepts is to define the overall variability of the data, also called *the total corrected sum of squares*, *SS*[T].

$SS_{T} = {\sum\limits_{i = 1}^{n}\left( {y_{i} - \overline{y}} \right)^{2}}$(10.28)

You can see that this is the sum of squares of the differences between the data and their average value. When we are considering a model that involves an independent variable, also called a *regressor variable*, we expect that our model will account for some of that total variability. By our regression calculations, what is left over is the set of residual values, {*e*[i], *i* = 1,…, *n*}. These are computed by

*e*[*i*] = *y*[*i*] − *ŷ*[*i*]*i* = 1, …, *n*(10.29)

where *ŷ*[*i*] : the model prediction for the regressor variable *x*[i].

The residuals represent the remaining variability that the model couldn’t explain, and we can quantify that by

$SS_{E} = {\sum\limits_{i = 1}^{n}e_{i}^{2}}$(10.30)

A useful way to picture this is with a pie chart showing the partition of the total variability into that accounted for by the model, *SS*[R], and the residual error, *SS*[E]. See [Figure 10.31](#ch10.xhtml_f10_31). We can observe from the figure that the regression sum of squares, *SS*[R], can be obtained from *SS*[T] − *SS*[E]. An obvious goal then is to find a model that provides a small value of *SS*[E].

![](images/Fig10_31.jpg)

**[FIGURE 10.31](#ch10.xhtml_f10_31b)** Partition of total variability.

A common statistic used to quantify the performance of a model in fitting the data is *the coefficient of determination* or “*R-squared*.” This is the fraction of the total variability accounted for by the model or

$R^{2} = \frac{SS_{R}}{SS_{T}} = 1 - \frac{SS_{E}}{SS_{T}}$(10.31)

The *R*² value is often reported as a percentage.

With reference to polynomial models, there is a significant problem in using *R*² as a measure of performance of the model. As we increase the order of the polynomial, the number of fitted parameters obviously increases. As we do this, *R*² always increases up to the point where the number of parameters, *m* + 1, equals the number of data, *n*. At that point, the model will pass exactly through every data point, and *R*² will equal one. Generally, this latter model will be a poor one because it will have unusual behavior between the data points and so will not be suitable for predictions and understanding.

The Python script below computes and displays *R*² for the straight-line fit of the CO[2] emissions data.

```
import numpy as np

yr,amt = np.loadtxt('CO2_Emissions.csv',delimiter=',',
unpack=True)

b = np.polyfit(yr,amt,1)
print(b)

amtp = np.polyval(b,yr)

e = amt - amtp
SSE = e.dot(e)
n = len(yr)
amtbar = np.mean(amt)
SST = 0
for i in range(n):
    SST = SST + (amt[i]-amtbar)**2
SSR = SST - SSE
R2 = SSR/SST
print('R-squared = {0:6.1f}%'.format(R2*100))
```

You will note that we used the `polyval` function above. It gives us the ability to compute a polynomial with coefficients `b` for one or more values of the independent variable, `yr`. The *R*² value displayed is

```
 R-squared = 74.7%
```

Is a value of 74.7% good or bad? That is unclear. If the residual errors are mainly random noise, this *R*² value may be adequate. The residuals then represent random behavior that we can’t explain with a model. Along with many statisticians, we recommend against using *R*² as a measure of regression performance. A reasonable alternative is the *standard error of the estimate*, given by

$s_{e} = \sqrt{\frac{SS_{E}}{n - \left( {m + 1} \right)}}$(10.32)

This value for our straight-line fit is 177.4\. You can think of the standard error as the “standard deviation” relative to the fit. Thus, the lower the *s*[e], the better the fit.

An objective of regression is to determine the model that accounts for all the systematic behavior in the dependent or response, *y*, leaving a residual series that contains no systematic behavior. We also expect that the residuals will be random values that can be modeled adequately by the normal distribution with mean of zero and standard deviation, *σ*[e]. This is the concept of *adequacy*, and we often assess it with plots.

For our straight-line example, [Figure 10.32](#ch10.xhtml_f10_32) depicts a plot of the residual errors versus year. We connect the data markers with lines to help recognize any patterns or systematic behavior. Perhaps we judge that the residuals start high, drop down, and then return high. If this is the case, we might seek to fit the data with a second-order polynomial instead of a straight line. The model that results is

![](images/Fig10_32.jpg)

**[FIGURE 10.32](#ch10.xhtml_f10_32b)** Residual errors versus year for straight-line model.

*a**m**t* = 1.081*y**r*² − 4423*y**r* + 4.529 × 10⁶(10.33)

and the corresponding residuals plot is shown in [Figure 10.33](#ch10.xhtml_f10_33). There is very little change in the pattern, so we haven’t gained much by using the higher-order model. We note here that the *R*² and *s*[e] values for this fit are *R*² = 75% and *s*[e] = 184.4\. As expected, by adding a term to the model, the *R*² value increased, but only slightly, from 74.7%; however, the *s*[e] value also increased, indicating that the second-order fit doesn’t perform as well as the straight-line.

![](images/Fig10_33.jpg)

**[FIGURE 10.33](#ch10.xhtml_f10_33b)** Residual errors versus year for second-order model.

We can also test whether the residual errors appear to belong to a normally distributed population. Here is the addition to the straight-line script to do that.

```
 import matplotlib.pyplot as plt
from scipy import stats
stats.probplot(e, plot=plt)
plt.grid()
result = stats.anderson(e, dist='norm')
print(result)
```

The probability plot is created using the `probplot` function from the `stats` module and is shown in [Figure 10.34](#ch10.xhtml_f10_34). As noted previously, this plot has the *z*-scores on the abscissa called “Theoretical Quantities” and the data on the ordinate. The Anderson-Darling test results are

![](images/Fig10_34.jpg)

**[FIGURE 10.34](#ch10.xhtml_f10_34b)** Probability plot of residuals from straight-line fit of CO[2] emissions data.

```
 AndersonResult(statistic=0.3425761550939743, critical_
values=array([0.497, 0.566, 0.68 , 0.793, 0.943]),
significance_level=array([15\. , 10\. , 5\. , 2.5, 1\. ]))
```

Since the statistic, ≅ 0.34, is less than all the critical values, we cannot claim that the residuals are drawn from a distribution other than the normal.

This leads us to a strategy for building a polynomial model to represent a data set with a response or dependent variable, *y*, and a single regressor or independent variable, *x*. This is not the only strategy used, but it is a practical one.

1.  Start with a simple polynomial model based on observation of a plot of the data.
2.  Fit the model, compute *R*² and *s*[e], and make residual plots to judge adequacy.
3.  Increase the polynomial order and repeat step 2.
4.  Stop when the *s*[e] value no longer decreases.
5.  Select the simplest model that shows adequacy in the residual plots.

The method we have illustrated with polynomial models is called *linear regression* because the parameters enter the model linearly. Obviously, the polynomial terms are nonlinear in the independent, regressor variable, but the method applies as long as it is linear in the parameters, the *b*’s. There are many other model forms that work with linear regression. Here are several examples:

$y = b_{0} + b_{1}\frac{1}{x} + b_{2}\text{ln}(x)$(10.40)

*y* = *b*[0] + *b*[1]sin (*x*) + *b*[2]cos (*x*)(10.41)

*y* = *b*[0] + *b*[1]*x*[1] + *b*[2]*x*[2] + *b*[12]*x*[1]*x*[2](10.42)

The model shown in Equation 10.42 is often called *multilinear* because it includes two regressor (independent) variables, *x*[1] and *x*[2]. All three models can be regressed using a method similar to that we illustrated with polynomials.

There are models that appear as nonlinear but can be transformed into models suitable for linear regression. A common example is

*y* = *b*[0] *e*^( *b*[1]*x*) ⇒ ln(*y*) = ln(*b*[0]) + *b*[1]*x*(10.43)

We would regress a straight-line model of ln(*y*) versus *x*. The estimated intercept would be ln(*b*[0]), and we would calculate *b*[0] as the exponential of this.

And then there are models that are nonlinear in the parameters and cannot be transformed as above. Here are two examples:

$y = 10^{b_{0} + \frac{b_{1}}{b_{2} + x}}$(10.44)

$\frac{dy}{dt} = b_{0}t + b_{1}y + b_{2}y\, t$(10.45)

In the case of Equation 10.45, with a data set {*t*[i], *y*[i], *i* = 1,…, *n*}, we would have to solve the differential equation numerically with the methods of [Chapter 9](#ch09.xhtml_c9) to obtain model predictions, *ŷ*[*i*], for a given set of parameters. For models like those in Equations 10.44 and 10.45, the fitting method is called *nonlinear regression*. One needs a procedure to search iteratively for the parameters that minimize the *V* criterion.

Fitting models to data is important for engineers and scientists. In this section, we have provided you with a good start into this topic. Polynomial models are the ones most frequently fit to data, so you’re ready to go with that. We encourage that you learn more about this topic, especially extending the techniques for general linear and nonlinear regression.

## Problems

1.  **10.1** [Table 3.12](#ch03.xhtml_t3_12) lists the number of Atlantic hurricanes from 1851 to 2020, and the data are presented in a plot in [Figure 3.11](#ch03.xhtml_f3_11).
    1.  Using the concepts discussed in [Section 10.1.1](#ch10.xhtml_h10_1_1), describe this data set. Provide your observations from the plot.
    2.  Write a Python script to divide the data set into two parts, 1851–1949 and 1950–2020\. Compute the average of each subset and comment on the results.
2.  **10.2** The table below reports *biological oxygen demand* (BOD) measurements taken at 2-hour intervals from a small river. This measurement requires taking two samples at each site. One is tested immediately for dissolved oxygen, and the second is incubated in the dark at 20 °C for 5 days and then evaluated for the amount of dissolved oxygen remaining. The difference in these two measurements is the BOD.
    1.  Compute the average, median, sample standard deviation, and MAD for these data.
    2.  Create a boxplot of the data and interpret the result.
    3.  If there are one or more outliers, imagine that an investigation has justified its removal from the data set. Do so and repeat the calculations of part **(a)**. Comment on the results.

        | Sample Number | BOD (mg/L) |
        | --- | --- |
        | 1 | 6.5 |
        | 2 | 5.8 |
        | 3 | 13.1 |
        | 4 | 6.4 |
        | 5 | 7.0 |
        | 6 | 6.3 |
        | 7 | 7.0 |
        | 8 | 9.2 |
        | 9 | 6.7 |
        | 10 | 6.7 |

3.  **10.3** Conduct a study of the piston diameter data in [Table 5.6](#ch05.xhtml_t5_6) as follows:
    1.  Apply the sign test to support the claim that the median diameter is less than 74.01 mm.
    2.  Evaluate and test whether the data appear to have been drawn from a normal distribution.
    3.  Assuming the data appear normally distributed, carry out a parametric test to support the same claim as in part **(a)**.
4.  **10.4** A product is produced in batches. The process operates in batches of 16 hours/day in two shifts. Data in the table below have been collected during the day and night shifts.
    1.  Create side-by-side boxplots of the data, and comment on your observations.
    2.  Apply the Wilcoxon rank sum test to the data to assess whether the mean quality is different between shifts.
    3.  Apply the test illustrated with the A and B samples in this chapter to test whether the mean quality is different between shifts. Comment on the differences between the conclusions in part **(b)** and **(c)**.

        | Shift |
        | --- |
        | Day | Night |
        | --- | --- |
        | 40 | 47 |
        | 27 | 42 |
        | 39 | 41 |
        | 46 | 34 |
        | 32 | 45 |
        | 46 | 52 |
        | 40 | 49 |
        | 44 | 35 |
        | 48 | 43 |
        | 41 | 44 |

5.  **10.5** Fit a straight-line model to the data of Problem 10.1 and interpret the results.
6.  **10.6** [Table 5.1](#ch05.xhtml_t5_1) presents freezing point data for antifreeze solutions. Fit an appropriate polynomial model to these data. Document how you arrive at your final selection and be sure to address the adequacy of your model.
7.  **10.7** [Figure 5.3](#ch05.xhtml_f5_3) presents a plot of the Wolf sunspot data.
    1.  Based on observations from the plot, comment on the data set.
    2.  Fit a straight-line model to the data and add it to the plot. Comment on the stationarity of the data set.
    3.  Produce a histogram plot of the data. Analyze whether the data appear to be drawn from a normally distributed population.
8.  **10.8** [Table 5.5](#ch05.xhtml_t5_5) presents densities of NaCl and MgCl salt solutions at 0 °C for different salt concentrations.
    1.  Fit straight-line models for each salt and compare the results.
    2.  Analyze the residuals of each fit and comment on model adequacy.
9.  **10.9** Write a Python script that generates 100 random numbers according to the uniform distribution in the range -1 to 1.
    1.  Compute the average and sample standard deviation of the data set and compare that to the theoretical values for the uniform distribution.
    2.  Modify your script to compute the 100-sample data set 100 times. Store the 100 sample averages in an array and create a histogram plot of the results. Comment on the plot.
    3.  Create a probability plot based on the normal distribution of your 100 averages from part **(b)**. Also, perform and interpret the Anderson-Darling test. Interpret your results. You may have illustrated a principle named the *Central Limit Theorem*. Look this up and document it as part of your solution.
10.  **10.10** [Table 5.6](#ch05.xhtml_t5_6) presents 40 measurements of the inside diameter of piston rings, and these data are used in the histogram plots of [Figures 10.12](#ch10.xhtml_f10_12) and [10.13](#ch10.xhtml_f10_13). Analyze whether it is likely that these data are drawn from a normally distributed population. Utilize a probability plot and the Anderson-Darling test.
11.  **10.11** Compute and plot the cumulative probability distribution for the Weibull distribution with *α*  =  2.0 and *β*  =  4.5 for 0 ≤ *x* ≤ 12.
12.  **10.12** In the sugar industry, a concentrated sucrose solution is produced and then sent to a crystallizer. The sugar concentration in the solution is measured with the refractive index.[^(17)](#ch10.xhtml_n10_17) The table below reports careful laboratory measurements of per cent sucrose versus refractive index. Plot the data and fit an appropriate model. Add your model curve to the plot. Assess model adequacy and check whether the residuals appear to be normally distributed.

    | Per cent Sucrose | Refractive Index | Per cent Sucrose | Refractive Index | Per cent Sucrose | Refractive Index |
    | --- | --- | --- | --- | --- | --- |
    | 0 | 1.3330 | 30 | 1.3811 | 60 | 1.4418 |
    | 5 | 1.3403 | 35 | 1.3902 | 65 | 1.4532 |
    | 10 | 1.3479 | 40 | 1.3997 | 70 | 1.4651 |
    | 15 | 1.3557 | 45 | 1.4096 | 75 | 1.4774 |
    | 20 | 1.3639 | 50 | 1.4200 | 80 | 1.4901 |
    | 25 | 1.3723 | 55 | 1.4307 | 85 | 1.5033 |

13.  **10.13** The data in the table below show the depression in the freezing point of water (H[2]O) that occurs with the addition of hydrochloric acid (HCl) to different concentrations.
    1.  Create a plot of the data as shown in the table. Then create a plot of freezing point depression versus log[10](HCl concentration).
    2.  Fit an appropriate model based on the second plot of part (a). Assess the adequacy of the model.

        | HCl Concentration (mol/kgH[2]O) | Freezing Pt Depression (°C) |
        | --- | --- |
        | 0.001 | 3.690 |
        | 0.005 | 3.635 |
        | 0.01 | 3.601 |
        | 0.02 | 3.568 |
        | 0.05 | 3.532 |
        | 0.1 | 3.523 |
        | 0.2 | 3.540 |
        | 0.5 | 3.680 |
        | 1 | 3.950 |
        | 2 | 4.430 |

14.  **10.14** [Table 5.7](#ch05.xhtml_t5_7) shows the wind capacity in GW for the ten countries that are the largest producers of wind power. Collect data on the population of each country and compute the wind power generation per capita. Study the results, apply any calculations you see as appropriate, and comment on your observations.
15.  **10.15** Global temperature data can be obtained from [https://www.ncdc.noaa.gov/cag/global/time-series](https://www.ncdc.noaa.gov/) for the years 1880–2021\. These data are reported as a *temperature anomaly*, the difference to the Jan 1951–Dec 1980 average temperature.
    1.  Download these data in a text file. Using either a text editor, for example, Notepad, WordPad, or Excel, create a text file with only the data, no headings. Write a Python script that loads the text file and creates a plot of the data, just lines connecting the data points and no markers. Comment on your observations of the plot.
    2.  Fit a straight-line model to the data. Report the *R*² and *s*[e] values. Assess the model’s adequacy by plotting the residuals versus year.
    3.  Fit an appropriate higher-order polynomial model to the data and carry out the same steps as in part **(b)**. You may need to evaluate several polynomial models.
    4.  Use your chosen model to predict the temperature anomaly in 2030, 2040, and 2050.

# References

*   [Burglund, B. and Street, R.](#ch09.xhtml_r1b), 2011\. Golf Ball Flight Dynamics. Flathead Valley Community College. Available online: [http://www.math.union.edu/~wangj/courses/previous/math238w13/Golf%20Ball%20Flight%20Dynamics2.pdf](http://www.math.union.edu/).
*   [Chapra, S.C. and Canale, R.P.](#ch07.xhtml_r2b), 2019\. Numerical Methods for Engineers with Software Applications and Programming, 8th ed., WCB/McGraw-Hill, New York, NY.
*   [Chapra, S.C. and Clough, D.E.](#ch00_fm07_preface.xhtml_r3b), 2022\. Applied Numerical Methods with Python for Engineers and Scientists. WCB/McGraw-Hill, New York, NY.
*   [Deitel, P. and Deitel, H.](#ch03.xhtml_r4b), 2020\. Intro to Python for Computer Science and Data Science. Pearson, New York, NY.
*   [Gaddis, T.](#ch03.xhtml_r5b), 2018\. Starting Out with Python, 4th ed., Pearson, New York, NY.
*   Hill, C., 2015\. Learning Scientific Programming with Python. Cambridge University Press, Cambridge, UK.
*   [Hornbeck, R. W.](#ch09.xhtml_r7b), 1975\. Numerical Methods. Quantum, New York, NY.
*   [Mason, R. L., Gunst, R. F., and Hess, J. L.](#ch10.xhtml_r8b), 1989\. Statistical Design and Analysis of Experiments with Applications to Engineering and Science. Wiley, New York, NY, p. 37.
*   [Montgomery, D.C. and Runger, G.C.](#ch10.xhtml_r9b), 2018\. Applied Statistics and Probability for Engineers, 7th ed., Wiley, New York, NY.
*   [Moré, J.J., Garbow, B. S., and Hillstrom, K. E.](#ch08.xhtml_r10b), 1980\. User Guide for MINPACK-1, Argonne National Laboratory Report ANL-80-74, Argonne, Ill.

# Index

*   absolute value, abs() [9](#ch01.xhtml_term-1), [61](#ch03.xhtml_term-2)
*   accuracy [4](#ch01.xhtml_term-3), [331](#ch10.xhtml_term-4)
*   AFNOR [4](#ch01.xhtml_term-5)
*   algebraic equation [199](#ch07.xhtml_term-6)
*   amplitude [19](#ch01.xhtml_term-7)
*   Anaconda [56](#ch03.xhtml_term-8)
*   Anderson-Darling test [363](#ch10.xhtml_term-9), [373–374](#ch10.xhtml_term-10), [381](#ch10.xhtml_term-11)
*   anonymous functions [120](#ch04.xhtml_term-12)
*   Antoine equation [160](#ch05.xhtml_term-13)
*   applied statistics [329](#ch10.xhtml_term-14)
*   arguments [68](#ch03.xhtml_term-15)
*   arithmetic average [334](#ch10.xhtml_term-16)
*   arithmetic expressions [57](#ch03.xhtml_term-17)
*   arithmetic operators [57–59](#ch03.xhtml_term-18)
*   array [73](#ch03.xhtml_term-19)
*   array operations [75](#ch03.xhtml_term-20), [166](#ch05.xhtml_term-21), [184](#ch06.xhtml_term-22), [175](#ch06.xhtml_term-23), [177](#ch06.xhtml_term-24)
*   ASCII [49](#ch02.xhtml_term-25)
*   asymmetry [347](#ch10.xhtml_term-26)
*   Atlantic hurricanes [89–91](#ch03.xhtml_term-27)
*   attributes [68](#ch03.xhtml_term-28)
*   axes 180n1
*   axis limits [147](#ch05.xhtml_term-29)

*   back substitution [261](#ch08.xhtml_term-30), [264](#ch08.xhtml_term-31)
*   backward compatibility [56](#ch03.xhtml_term-32)
*   bar plots [154](#ch05.xhtml_term-33)
*   base-e (natural) logarithm [11](#ch01.xhtml_term-34)
*   base-60 numbers 41n1
*   base-10 (common) logarithm [11](#ch01.xhtml_term-35)
*   base-10 system [41](#ch02.xhtml_term-36)
*   base-2 system [41](#ch02.xhtml_term-37)
*   bias error [333](#ch10.xhtml_term-38), [337](#ch10.xhtml_term-39)
*   biased exponent [47](#ch02.xhtml_term-40)
*   binary
    *   digits [74](#ch03.xhtml_term-41)
    *   point [48](#ch02.xhtml_term-42)
    *   subtraction operator [58](#ch03.xhtml_term-43)
    *   system [41](#ch02.xhtml_term-44)
*   biological oxygen demand (BOD) [379](#ch10.xhtml_term-45)
*   bisection method [203](#ch07.xhtml_term-46)
*   bit [43](#ch02.xhtml_term-47)
*   bits [74](#ch03.xhtml_term-48)
*   black boxes [233](#ch07.xhtml_term-49)
*   block diagrams [295](#ch09.xhtml_term-50)
*   blunder [335](#ch10.xhtml_term-51)
*   Boolean [49](#ch02.xhtml_term-52), [69–70](#ch03.xhtml_term-53)
*   box and whisker plot [339n4](#ch10.xhtml_term-54)
*   boxplot [339–342](#ch10.xhtml_term-55), [353](#ch10.xhtml_term-56), [356–357](#ch10.xhtml_term-57), [379](#ch10.xhtml_term-58)
*   bracketing methods [202](#ch07.xhtml_term-59)
*   breakpoint [84](#ch03.xhtml_term-60)
*   Brent’s method [230](#ch07.xhtml_term-61)
*   bridge truss structure [288](#ch08.xhtml_term-62)
*   byte [43](#ch02.xhtml_term-63)

*   cantilever beam [327](#ch09.xhtml_term-64)
*   cartographer’s planimeter [299](#ch09.xhtml_term-65)
*   case sensitive [66](#ch03.xhtml_term-66)
*   case studies [186](#ch06.xhtml_term-67)
*   categorical chart [156](#ch05.xhtml_term-68)
*   catenary cable [21](#ch01.xhtml_term-69)
*   Celsius 5n3
*   central limit theorem [381](#ch10.xhtml_term-70)
*   central tendency [332–334](#ch10.xhtml_term-71)
*   character type [69](#ch03.xhtml_term-72)
*   characteristic [4](#ch01.xhtml_term-73)
*   chemical reaction equilibrium [291](#ch08.xhtml_term-74)
*   circle
    *   sector [38](#ch01.xhtml_term-75)
    *   segment [38–39](#ch01.xhtml_term-76)
*   circular calculation scheme [222](#ch07.xhtml_term-77)
*   circular matrix [271](#ch08.xhtml_term-78)
*   circular methods [221](#ch07.xhtml_term-79)
*   class [74](#ch03.xhtml_term-80)
*   clearing [87](#ch03.xhtml_term-81)
*   cobweb plots [225](#ch07.xhtml_term-82)
*   code-readability [55](#ch03.xhtml_term-83)
*   coefficient of determination [371](#ch10.xhtml_term-84)
*   collections of data [72](#ch03.xhtml_term-85)
*   colon (:) indexing [182](#ch06.xhtml_term-86)
*   color codes [79](#ch03.xhtml_term-87), [142](#ch05.xhtml_term-88)
*   Colorado River Aqueduct [99](#ch03.xhtml_term-89)
*   column vector [178](#ch06.xhtml_term-90)
*   combining arrays [179](#ch06.xhtml_term-91)
*   comma delimited [89](#ch03.xhtml_term-92)
*   comments, # [85](#ch03.xhtml_term-93)
*   common logarithm *see* [base-10 logarithm](#ch12_index.xhtml_idx29)
*   commutative operations [195](#ch06.xhtml_term-94)
*   Complete NumPy Manual [95](#ch03.xhtml_term-95)
*   complex conjugate pair [200](#ch07.xhtml_term-96), [234](#ch07.xhtml_term-97)
*   complex numbers [22](#ch01.xhtml_term-98)
*   computer storage [51](#ch02.xhtml_term-99)
*   computer word [43](#ch02.xhtml_term-100)
*   concatenation [72](#ch03.xhtml_term-101)
*   conjugate pair [22](#ch01.xhtml_term-102)
*   construction materials blending problem [272](#ch08.xhtml_term-103)
*   continue execution button [84](#ch03.xhtml_term-104)
*   contour plots [164](#ch05.xhtml_term-105)
*   count-controlled loop [104](#ch04.xhtml_term-106)
*   counting the squares [298](#ch09.xhtml_term-107)
*   Cramer’s rule [256](#ch08.xhtml_term-108), [258](#ch08.xhtml_term-109)
*   creating plots [76](#ch03.xhtml_term-110)
*   cumulative binomial distribution [354n9](#ch10.xhtml_term-111)
*   cumulative distribution [347](#ch10.xhtml_term-112), [358–362](#ch10.xhtml_term-113), [381](#ch10.xhtml_term-114)
*   customizing plots [140](#ch05.xhtml_term-115)

*   data types [68](#ch03.xhtml_term-116)
*   deadweight ton [37](#ch01.xhtml_term-117)
*   debug file button [84](#ch03.xhtml_term-118)
*   debug tracing [82](#ch03.xhtml_term-119)
*   decimal system [41](#ch02.xhtml_term-120)
*   decision structure [102](#ch04.xhtml_term-121)
*   deflation [236](#ch07.xhtml_term-122)
*   degree [14–17](#ch01.xhtml_term-123)
*   degrees of freedom [337](#ch10.xhtml_term-124)
*   densities, salt and mag chloride solutions [145](#ch05.xhtml_term-125)
*   density function [343](#ch10.xhtml_term-126)
*   density of water [99](#ch03.xhtml_term-127)
*   determinant [254–257](#ch08.xhtml_term-128), [267](#ch08.xhtml_term-129)
*   dictionary [73](#ch03.xhtml_term-130)
*   differential equations [293](#ch09.xhtml_term-131)
*   dimensional drag coefficient [316](#ch09.xhtml_term-132)
*   dimensionless drag coefficient [317](#ch09.xhtml_term-133)
*   discriminant [22](#ch01.xhtml_term-134)
*   dispersion [332](#ch10.xhtml_term-135), [336](#ch10.xhtml_term-136)
*   distribution [342](#ch10.xhtml_term-137), [345](#ch10.xhtml_term-138)
*   docustring [85](#ch03.xhtml_term-139)
*   dot diagrams [334](#ch10.xhtml_term-140)
*   dot product [190](#ch06.xhtml_term-141)
*   drag coefficient [316–317](#ch09.xhtml_term-142)
*   dynamic range [46](#ch02.xhtml_term-143)

*   *e see* Euler’s number
*   Earth
    *   radius [41](#ch02.xhtml_term-144)
    *   volume [1](#ch01.xhtml_term-145)
*   80/20 rule 156n4
*   elimination of unknowns [258–259](#ch08.xhtml_term-146)
*   engineering units [24](#ch01.xhtml_term-147)
*   error diagnostics [82](#ch03.xhtml_term-148)
*   escape velocity [172](#ch05.xhtml_term-149)
*   ethylene glycol freezing point [138](#ch05.xhtml_term-150)
*   Euler’s method [307–310](#ch09.xhtml_term-151)
*   Euler’s number, *e* [60–61](#ch03.xhtml_term-152)
*   execution error [83](#ch03.xhtml_term-153)
*   expansion coefficient [134](#ch04.xhtml_term-154)
*   exponent [4](#ch01.xhtml_term-155), [10](#ch01.xhtml_term-156)
*   extreme outlier [341](#ch10.xhtml_term-157)

*   Fahrenheit 5n3
*   false position [207](#ch07.xhtml_term-158)
*   Fibonacci series [133](#ch04.xhtml_term-159)
*   figure window objects [151](#ch05.xhtml_term-160)
*   file input and output [89](#ch03.xhtml_term-161)
*   fitting a straight line [364](#ch10.xhtml_term-162)
*   fitting polynomial to water density [374–377](#ch10.xhtml_term-163)
*   fitting polynomials [368–370](#ch10.xhtml_term-164)
*   fixed-point iteration
    *   single equation [32](#ch01.xhtml_term-165), [221–227](#ch07.xhtml_term-166)
    *   systems of equations [275–278](#ch08.xhtml_term-167)
*   float64 [74](#ch03.xhtml_term-168)
*   floating point division [59](#ch03.xhtml_term-169)
*   floating tooltip [93](#ch03.xhtml_term-170)
*   flow totalization [324](#ch09.xhtml_term-171)
*   forcing variable [295](#ch09.xhtml_term-172)
*   formatting output [91](#ch03.xhtml_term-173)
*   forward elimination step [261](#ch08.xhtml_term-174)
*   fossil fuel emissions [366](#ch10.xhtml_term-175)
*   four-bar linkage [246–247](#ch07.xhtml_term-176)
*   Fourier series [173](#ch05.xhtml_term-177)
*   frequency [19](#ch01.xhtml_term-178)
*   Frobenius norm [197](#ch06.xhtml_term-179)
*   fuel economy [37](#ch01.xhtml_term-180)
*   function arguments [121](#ch04.xhtml_term-181)
*   function functions [124](#ch04.xhtml_term-182)

*   Gaia Space Observatory [245](#ch07.xhtml_term-183)
*   gas law constant [221](#ch07.xhtml_term-184)
*   Gaussian distribution [118](#ch04.xhtml_term-185), [303](#ch09.xhtml_term-186), [346](#ch10.xhtml_term-187)
*   Gaussian elimination [260–261](#ch08.xhtml_term-188)
*   general loop [102](#ch04.xhtml_term-189)
    *   structure [110](#ch04.xhtml_term-190)
*   gigabyte [51](#ch02.xhtml_term-191)
*   global average temperature [99](#ch03.xhtml_term-192)
    *   CO[2] concentration [99](#ch03.xhtml_term-193)
    *   temperature anomaly [382–383](#ch10.xhtml_term-194)
*   global scope [128](#ch04.xhtml_term-195)
*   Golden Ratio [133](#ch04.xhtml_term-196)
*   grad 16n5
*   grain bin [129](#ch04.xhtml_term-197)
*   graphical method to solve linear equations [252](#ch08.xhtml_term-198)
*   Great Circle [62–63](#ch03.xhtml_term-199), [66](#ch03.xhtml_term-200)
    *   distance [63](#ch03.xhtml_term-201), [243](#ch07.xhtml_term-202)
    *   script [85](#ch03.xhtml_term-203)
*   greenhouse gas emissions [170](#ch05.xhtml_term-204)
*   gridlines [77](#ch03.xhtml_term-205)

*   header information [85](#ch03.xhtml_term-206)
*   heat capacity of water vapor [244](#ch07.xhtml_term-207)
*   help *see* [obtaining help](#ch12_index.xhtml_idx335)
*   Heun’s method [311–313](#ch09.xhtml_term-208)
*   hexadecimal [42](#ch02.xhtml_term-209)
*   Hilbert matrix [287](#ch08.xhtml_term-210)
*   histogram charts [154](#ch05.xhtml_term-211)
*   hole at zero [47](#ch02.xhtml_term-212)
*   Hooke’s Law [296](#ch09.xhtml_term-213)
*   horizontal cylinder with hemispherical ends [243](#ch07.xhtml_term-214)
*   “How do I . . .” inquiry [97](#ch03.xhtml_term-215)
*   hydraulic jump [247–248](#ch07.xhtml_term-216)
*   hyperbolic functions [20–21](#ch01.xhtml_term-217), [62](#ch03.xhtml_term-218)
*   hypothesis tests [330](#ch10.xhtml_term-219), [363](#ch10.xhtml_term-220)

*   IDE [55](#ch03.xhtml_term-221)
*   identity array [179](#ch06.xhtml_term-222)
*   identity matrix [193](#ch06.xhtml_term-223)
*   IEEE 754
    *   double precision [46](#ch02.xhtml_term-224)
    *   representation of *π* [48](#ch02.xhtml_term-225)
*   ill-conditioned systems [253–254](#ch08.xhtml_term-226), [270](#ch08.xhtml_term-227)
*   imaginary part [22–23](#ch01.xhtml_term-228)
*   immutable [74](#ch03.xhtml_term-229)
*   independent equations [254](#ch08.xhtml_term-230)
*   indexing [181](#ch06.xhtml_term-231)
*   infinite loop [103](#ch04.xhtml_term-232)
*   information flow diagram [296](#ch09.xhtml_term-233)
*   initial value problems (IVP) [295](#ch09.xhtml_term-234)
*   inner product [190](#ch06.xhtml_term-235)
*   input
    *   and output [87](#ch03.xhtml_term-236)
    *   validation [111](#ch04.xhtml_term-237)
    *   variable [295](#ch09.xhtml_term-238)
*   int32 [74](#ch03.xhtml_term-239)
*   integer division [59](#ch03.xhtml_term-240)
*   integers [43](#ch02.xhtml_term-241)
*   integrated development environment [55](#ch03.xhtml_term-242)
*   interquartile range - iqr [123](#ch04.xhtml_term-243), [340](#ch10.xhtml_term-244)
*   inverse matrix [193](#ch06.xhtml_term-245)
*   inverse trigonometric functions [17–18](#ch01.xhtml_term-246)
*   IPython [55](#ch03.xhtml_term-247)
    *   Console [57](#ch03.xhtml_term-248)
*   iron-constantan [108](#ch04.xhtml_term-249)
*   ISO [4](#ch01.xhtml_term-250)
*   isobars [164](#ch05.xhtml_term-251)

*   Jacobian matrix [279–282](#ch08.xhtml_term-252)
*   James Webb Space Telescope [245](#ch07.xhtml_term-253)

*   keyword [66](#ch03.xhtml_term-254)
    *   arguments [122](#ch04.xhtml_term-255)
*   kilobyte [51](#ch02.xhtml_term-256)
*   Kirchhoff’s law [290](#ch08.xhtml_term-257)

*   ladder in hallway [29–35](#ch01.xhtml_term-258)
*   Lagrange points [245](#ch07.xhtml_term-259)
*   lambda functions [120](#ch04.xhtml_term-260)
*   LAPACK [273](#ch08.xhtml_term-261)
*   latitude [63](#ch03.xhtml_term-262)
*   launch angle versus range [237–238](#ch07.xhtml_term-263)
*   leading zero [6](#ch01.xhtml_term-264)
*   legend with twin axes [150](#ch05.xhtml_term-265)
*   line continuation character, \ [64](#ch03.xhtml_term-266)
*   linear interpolation [130](#ch04.xhtml_term-267)
*   linear regression [377](#ch10.xhtml_term-268)
*   linear sequence [102](#ch04.xhtml_term-269)
*   linear systems of equations
    *   graphical methods [252](#ch08.xhtml_term-270)
*   linearization [378–379](#ch10.xhtml_term-271)
*   linestyle codes [82](#ch03.xhtml_term-272), [142](#ch05.xhtml_term-273)
*   list [73](#ch03.xhtml_term-274)
*   list-driven
    *   loop [112](#ch04.xhtml_term-275), [104](#ch04.xhtml_term-276)
    *   structure [104](#ch04.xhtml_term-277)
*   literal [69](#ch03.xhtml_term-278)
*   local scope [128](#ch04.xhtml_term-279)
*   logarithm [10](#ch01.xhtml_term-280)
*   logarithmic scale [162](#ch05.xhtml_term-281)
*   logical operators [70](#ch03.xhtml_term-282)
*   logical type [69](#ch03.xhtml_term-283) *see also* [Boolean](#ch12_index.xhtml_idx46)
*   long integer [45](#ch02.xhtml_term-284)
*   longitude [63](#ch03.xhtml_term-285)
*   loop structure [102](#ch04.xhtml_term-286)
*   LSODA method [319](#ch09.xhtml_term-287)
*   lune [98](#ch03.xhtml_term-288)

*   MAD *see* [median absolute deviation](#ch12_index.xhtml_idx297)
*   magic number [28](#ch01.xhtml_term-289)
*   Magnus effect [318](#ch09.xhtml_term-290)
*   mailbox analogy [64](#ch03.xhtml_term-291)
*   making claims [333](#ch10.xhtml_term-292), [352–363](#ch10.xhtml_term-293)
*   Manning’s equation [186](#ch06.xhtml_term-294)
*   mantissa [4](#ch01.xhtml_term-295), [47](#ch02.xhtml_term-296)
*   marker [77](#ch03.xhtml_term-297)
    *   codes [80](#ch03.xhtml_term-298), [143](#ch05.xhtml_term-299)
    *   color [143](#ch05.xhtml_term-300)
*   mass balances [250–251](#ch08.xhtml_term-301)
*   Math module [62](#ch03.xhtml_term-302)
*   mathematical functions [61](#ch03.xhtml_term-303)
*   Matplotlib [76](#ch03.xhtml_term-304)
    *   documentation [145](#ch05.xhtml_term-305)
    *   module [137](#ch05.xhtml_term-306)
*   matrices [177](#ch06.xhtml_term-307)
*   matrix
    *   array type [178](#ch06.xhtml_term-308)
    *   elements [261](#ch08.xhtml_term-309)
    *   inverse [193](#ch06.xhtml_term-310)
    *   minors [255](#ch08.xhtml_term-311)
    *   multiplication [190](#ch06.xhtml_term-312)
    *   operations [175](#ch06.xhtml_term-313)
*   median absolute deviation (MAD) [337](#ch10.xhtml_term-314)
*   megabyte [51](#ch02.xhtml_term-315)
*   mesh plot [168](#ch05.xhtml_term-316)
*   m-estimator [335](#ch10.xhtml_term-317)
*   methods [68](#ch03.xhtml_term-318)
*   mid-test loop [104](#ch04.xhtml_term-319)
*   minimal arc distance [63](#ch03.xhtml_term-320)
*   MINPACK [285](#ch08.xhtml_term-321)
*   mode [335](#ch10.xhtml_term-322)
*   model adequacy [370](#ch10.xhtml_term-323)
*   modified secant method [220](#ch07.xhtml_term-324)
*   modulus (modulo) operator [60](#ch03.xhtml_term-325)
*   Muller’s method [236](#ch07.xhtml_term-326)
*   multi-alternative if [105–106](#ch04.xhtml_term-327)
*   multilinear [378](#ch10.xhtml_term-328)

*   naive Gaussian elimination [261](#ch08.xhtml_term-329), [268](#ch08.xhtml_term-330)
*   Napierian (natural) logarithm [11](#ch01.xhtml_term-331)
*   ndarray [74](#ch03.xhtml_term-332), [76](#ch03.xhtml_term-333)
    *   class [176](#ch06.xhtml_term-334)
*   Newton-Raphson
    *   formula [215](#ch07.xhtml_term-335), [212](#ch07.xhtml_term-336)
    *   method [212](#ch07.xhtml_term-337)
    *   for multiple roots [215](#ch07.xhtml_term-338), [278](#ch08.xhtml_term-339)
*   Newton’s Universal Law of Gravitation [100](#ch03.xhtml_term-340)
*   nibble 43n4
*   NIST [4](#ch01.xhtml_term-341)
*   noisy signal [350](#ch10.xhtml_term-342), [374](#ch10.xhtml_term-343)
*   nonlinear algebraic equations [274](#ch08.xhtml_term-344)
*   nonlinear regression [379](#ch10.xhtml_term-345)
*   non-parametric tests [352](#ch10.xhtml_term-346)
*   normal distribution [118](#ch04.xhtml_term-347), [303](#ch09.xhtml_term-348), [346](#ch10.xhtml_term-349)
*   normal probability rule [346](#ch10.xhtml_term-350)
*   normalization [262](#ch08.xhtml_term-351)
*   normalize [4](#ch01.xhtml_term-352)
*   numerical quantities [3](#ch01.xhtml_term-353)
*   NumPy [74](#ch03.xhtml_term-354)

*   objects [67](#ch03.xhtml_term-355)
*   oblate spheroid [2](#ch01.xhtml_term-356)
*   obtaining help [93](#ch03.xhtml_term-357)
*   occurrence matrix [31](#ch01.xhtml_term-358)
*   Ockham’s razor 370n16
*   octal [42](#ch02.xhtml_term-359)
*   Ohm’s law [135](#ch04.xhtml_term-360), [289](#ch08.xhtml_term-361)
*   one-line if [105](#ch04.xhtml_term-362)
*   one-way if [102](#ch04.xhtml_term-363)
*   open channel flow [186](#ch06.xhtml_term-364)
*   open methods [213](#ch07.xhtml_term-365)
*   operator priority order
    *   arithmetic [58](#ch03.xhtml_term-366)
    *   logical [70](#ch03.xhtml_term-367)
    *   relational [70](#ch03.xhtml_term-368)
*   optimization problem [34](#ch01.xhtml_term-369)
*   ordinary differential equations [297](#ch09.xhtml_term-370)
*   outlier [334](#ch10.xhtml_term-371)
*   overdetermined 31n11

*   parallax errors [141](#ch05.xhtml_term-372)
*   parametric tests [352](#ch10.xhtml_term-373)
*   parasitic solution [322](#ch09.xhtml_term-374)
*   parentheses matching [85](#ch03.xhtml_term-375)
*   Pareto
    *   chart [156](#ch05.xhtml_term-376)
    *   principle [156n4](#ch05.xhtml_term-377)
*   parsimony [370](#ch10.xhtml_term-378)
*   partial derivatives [279](#ch08.xhtml_term-379)
*   partial differential equations [297](#ch09.xhtml_term-380)
*   partial pivoting [268](#ch08.xhtml_term-381)
*   percent relative error [210](#ch07.xhtml_term-382)
*   percentile value [122](#ch04.xhtml_term-383)
*   period [19](#ch01.xhtml_term-384)
*   phase plot [151](#ch05.xhtml_term-385)
*   phase shift [20](#ch01.xhtml_term-386)
*   physical modeling [29](#ch01.xhtml_term-387)
*   pi, π [60](#ch03.xhtml_term-388)
*   pie charts [162](#ch05.xhtml_term-389)
*   piston ring inside diameter measurements [154](#ch05.xhtml_term-390)
*   pivot element [261](#ch08.xhtml_term-391)
*   planning solutions [28–36](#ch01.xhtml_term-392)
*   plotting weather data [148](#ch05.xhtml_term-393)
*   polar
    *   coordinates [23](#ch01.xhtml_term-394), [158](#ch05.xhtml_term-395)
    *   form [23](#ch01.xhtml_term-396)
    *   planimeter [299](#ch09.xhtml_term-397)
    *   plot [158](#ch05.xhtml_term-398)
*   polynomials *see* [roots of polynomials](#ch12_index.xhtml_idx425)
*   positional notation [3](#ch01.xhtml_term-399), [41–42](#ch02.xhtml_term-400)
*   post-test loop [103](#ch04.xhtml_term-401)
*   precision [4](#ch01.xhtml_term-402), [331](#ch10.xhtml_term-403)
*   predictor-corrector method [311](#ch09.xhtml_term-404)
*   preferences window [87](#ch03.xhtml_term-405)
*   pre-test loop [103](#ch04.xhtml_term-406)
*   Prime Meridian [63](#ch03.xhtml_term-407)
*   priority *see* [operator priority order](#ch12_index.xhtml_idx344)
*   probability graph paper [361](#ch10.xhtml_term-408)
*   problem solving [28–34](#ch01.xhtml_term-409)
*   program structure [102](#ch04.xhtml_term-410)
*   projectile trajectory [237–238](#ch07.xhtml_term-411)
    *   with air resistance [316–319](#ch09.xhtml_term-412)
*   properties [68](#ch03.xhtml_term-413)
*   pseudorandom [349](#ch10.xhtml_term-414)

*   quadrants [17–18](#ch01.xhtml_term-415)
*   quadratic form [197](#ch06.xhtml_term-416)
*   quadratic formula [200](#ch07.xhtml_term-417)
*   quadrature [293](#ch09.xhtml_term-418), [298](#ch09.xhtml_term-419)

*   R language [56](#ch03.xhtml_term-420)
*   radian [14](#ch01.xhtml_term-421), [17](#ch01.xhtml_term-422)
*   random number generation [348–352](#ch10.xhtml_term-423)
*   range [336](#ch10.xhtml_term-424), [339](#ch10.xhtml_term-425)
*   range type with array subscripting [182–183](#ch06.xhtml_term-426)
*   rate equations [293](#ch09.xhtml_term-427)
*   real part [22–23](#ch01.xhtml_term-428)
*   rectangular hyperbola [20](#ch01.xhtml_term-429)
    *   integration [299](#ch09.xhtml_term-430)
*   refractive index of sucrose solutions [171](#ch05.xhtml_term-431)
*   refractometer [171](#ch05.xhtml_term-432)
*   regression [330](#ch10.xhtml_term-433), [364](#ch10.xhtml_term-434), [372](#ch10.xhtml_term-435), [377](#ch10.xhtml_term-436)
*   regressor variable [370](#ch10.xhtml_term-437)
*   regula falsi [208](#ch07.xhtml_term-438)
*   relational operators [70](#ch03.xhtml_term-439)
*   relative frequency [342](#ch10.xhtml_term-440)
*   remove variables icon [87](#ch03.xhtml_term-441)
*   repeatability [332](#ch10.xhtml_term-442)
*   repeated exponentiation [58](#ch03.xhtml_term-443)
*   repetition [102](#ch04.xhtml_term-444)
*   reshaping arrays [180](#ch06.xhtml_term-445)
*   residual error [364](#ch10.xhtml_term-446), [371](#ch10.xhtml_term-447)
*   resolution [4](#ch01.xhtml_term-448), [330](#ch10.xhtml_term-449)
*   RGB color model [52](#ch02.xhtml_term-450)
*   roots of polynomials [233](#ch07.xhtml_term-451)
*   rounding [4](#ch01.xhtml_term-452)
    *   rules for [6–7](#ch01.xhtml_term-453)
*   rounding function, round () [61](#ch03.xhtml_term-454)
*   R-squared [371](#ch10.xhtml_term-455)
*   RStudio [56](#ch03.xhtml_term-456)
*   Runge-Kutta method (RK45) [319](#ch09.xhtml_term-457)
*   runtime error [83](#ch03.xhtml_term-458)

*   salt and mag chloride solutions [145](#ch05.xhtml_term-459)
*   salt solution density [167](#ch05.xhtml_term-460)
*   sample mean [334](#ch10.xhtml_term-461), [336](#ch10.xhtml_term-462)
    *   standard deviation [336](#ch10.xhtml_term-463)
    *   variance [336](#ch10.xhtml_term-464)
*   scientific notation [2–3](#ch01.xhtml_term-465)
*   SciPy Reference Guide [95](#ch03.xhtml_term-466)
*   second derivatives [295](#ch09.xhtml_term-467)
*   sector of a circle [38](#ch01.xhtml_term-468)
*   Seebeck effect [107](#ch04.xhtml_term-469)
*   segment of a circle [38–39](#ch01.xhtml_term-470)
*   select-case [107](#ch04.xhtml_term-471)
*   selection [102](#ch04.xhtml_term-472)
*   semiaxis [2](#ch01.xhtml_term-473)
*   sensitivity analysis [14](#ch01.xhtml_term-474)
*   sentinel [117](#ch04.xhtml_term-475)
*   separable equation [295](#ch09.xhtml_term-476)
*   set [73](#ch03.xhtml_term-477)
*   shock absorber model [296](#ch09.xhtml_term-478), [314–316](#ch09.xhtml_term-479)
*   short integer [45](#ch02.xhtml_term-480)
*   shotgun programming [97](#ch03.xhtml_term-481)
*   SI system [25](#ch01.xhtml_term-482)
*   sigmoidal (S) curve [359](#ch10.xhtml_term-483)
*   sign function [10](#ch01.xhtml_term-484)
    *   test [353–354](#ch10.xhtml_term-485), [380](#ch10.xhtml_term-486)
*   significand [4](#ch01.xhtml_term-487)
*   significant figures [2](#ch01.xhtml_term-488), [4–5](#ch01.xhtml_term-489), [7](#ch01.xhtml_term-490)
    *   rules [7](#ch01.xhtml_term-491)
*   signum (sgn) function [10](#ch01.xhtml_term-492)
*   single step icon [84](#ch03.xhtml_term-493)
*   singular systems [253–254](#ch08.xhtml_term-494)
*   sinusoidal signal [19](#ch01.xhtml_term-495)
*   Soave, Redlich, Kwong (SRK) [244](#ch07.xhtml_term-496)
*   solving sets of nonlinear algebraic equations [274](#ch08.xhtml_term-497)
*   special arrays [178](#ch06.xhtml_term-498)
*   spherical tank [217](#ch07.xhtml_term-499)
*   spherical tank volume [205](#ch07.xhtml_term-500)
*   spherical trigonometry [63](#ch03.xhtml_term-501)
*   splitting arrays [179–180](#ch06.xhtml_term-502)
*   Spyder [55](#ch03.xhtml_term-503)
    *   Editor [78](#ch03.xhtml_term-504), [82](#ch03.xhtml_term-505)
    *   Help Menu [94](#ch03.xhtml_term-506)
*   standard error of the estimate [372](#ch10.xhtml_term-507), [377](#ch10.xhtml_term-508)
*   standard normal density [303](#ch09.xhtml_term-509), [346–347](#ch10.xhtml_term-510)
*   standard normal distribution [346–347](#ch10.xhtml_term-511)
*   stationarity [330](#ch10.xhtml_term-512)
*   steam boiler equilibrium [283](#ch08.xhtml_term-513)
*   steam tables [160](#ch05.xhtml_term-514)
*   STEM [55](#ch03.xhtml_term-515)
*   stem plot [159](#ch05.xhtml_term-516)
*   stone [37](#ch01.xhtml_term-517)
*   stop button [84](#ch03.xhtml_term-518)
*   string [49](#ch02.xhtml_term-519)
    *   functions [72](#ch03.xhtml_term-520)
    *   string type [69](#ch03.xhtml_term-521), [71](#ch03.xhtml_term-522)
*   structured programming [102](#ch04.xhtml_term-523)
*   Student’s t 355n11
*   subscript [73](#ch03.xhtml_term-524)
    *   origin, 1 or 0 [181](#ch06.xhtml_term-525)
*   subscripting [181](#ch06.xhtml_term-526)
*   substitution method [32](#ch01.xhtml_term-527)
*   successive approximation [42](#ch02.xhtml_term-528)
*   successive division [42](#ch02.xhtml_term-529)
*   successive substitution [222–223](#ch07.xhtml_term-530), [275](#ch08.xhtml_term-531)
*   sucrose refractive index [381–382](#ch10.xhtml_term-532)
*   sugar packet data [354–355](#ch10.xhtml_term-533), [360](#ch10.xhtml_term-534), [363](#ch10.xhtml_term-535)
*   sum of angles [20](#ch01.xhtml_term-536)
*   surface plot [168](#ch05.xhtml_term-537)
*   switch [107](#ch04.xhtml_term-538)
*   syntax error [83](#ch03.xhtml_term-539)
*   systems of differential equations [313–316](#ch09.xhtml_term-540)
*   systems of linear algebraic equations [250](#ch08.xhtml_term-541)

*   terabyte [51](#ch02.xhtml_term-542)
*   text files [89](#ch03.xhtml_term-543)
*   thermocouple [107–110](#ch04.xhtml_term-544)
*   tick intervals [148](#ch05.xhtml_term-545)
*   topographic map [164](#ch05.xhtml_term-546)
*   total corrected sum of squares [370](#ch10.xhtml_term-547)
*   transcendental equation [199](#ch07.xhtml_term-548)
*   trapezoidal rule [300](#ch09.xhtml_term-549)
*   trial-and-error [201](#ch07.xhtml_term-550)
*   trigonometric functions [14](#ch01.xhtml_term-551), [62](#ch03.xhtml_term-552)
*   truth table [70](#ch03.xhtml_term-553)
*   Tukey, John 339n4
*   tuple [73](#ch03.xhtml_term-554)
*   2’s complement [45](#ch02.xhtml_term-555)
*   two-way if [102](#ch04.xhtml_term-556), [105](#ch04.xhtml_term-557)
*   Type 1 (I) error [353](#ch10.xhtml_term-558)
*   Type 2 (II) error 353n8
*   Type J thermocouple [108](#ch04.xhtml_term-559), [115](#ch04.xhtml_term-560)

*   unary minus operator [58](#ch03.xhtml_term-561)
*   underdetermined [31n11](#ch01.xhtml_term-562)
*   underscore [66](#ch03.xhtml_term-563)
*   uniform distribution [118](#ch04.xhtml_term-564), [345](#ch10.xhtml_term-565)
*   unit circle [14–18](#ch01.xhtml_term-566)
*   universal gas constant [26](#ch01.xhtml_term-567)
*   up-arrow key [66](#ch03.xhtml_term-568)
*   upper triangular form [261](#ch08.xhtml_term-569), [263](#ch08.xhtml_term-570)
*   upward rocket velocity [245](#ch07.xhtml_term-571)
*   USB ‘thumb drive’ [51](#ch02.xhtml_term-572)
*   user-defined functions [118](#ch04.xhtml_term-573)

*   van der Waals equation [221](#ch07.xhtml_term-574)
*   van Rossum, Guido [55](#ch03.xhtml_term-575)
*   vapor pressure of water [160](#ch05.xhtml_term-576)
*   Variable Explorer [66](#ch03.xhtml_term-577)
*   variable names [64](#ch03.xhtml_term-578)
    *   scope [127](#ch04.xhtml_term-579)
*   vary subscripts [114](#ch04.xhtml_term-580)
*   vector arrays [177](#ch06.xhtml_term-581)
    *   product [197](#ch06.xhtml_term-582)
*   vector/matrix operations [189](#ch06.xhtml_term-583), [195](#ch06.xhtml_term-584)
    *   solution of linear equations [195](#ch06.xhtml_term-585)
*   vectorized calculations [186](#ch06.xhtml_term-586)
*   vectors [177](#ch06.xhtml_term-587)
*   view of an array [180](#ch06.xhtml_term-588)

*   wastewater treatment plant [251](#ch08.xhtml_term-589)
*   water density [374–377](#ch10.xhtml_term-590)
*   Wegstein method [227](#ch07.xhtml_term-591), [278](#ch08.xhtml_term-592)
*   Weibull distribution [347](#ch10.xhtml_term-593)
*   weighing the curve method [298](#ch09.xhtml_term-594)
*   well-conditioned [274](#ch08.xhtml_term-595)
*   whiskers [340–341](#ch10.xhtml_term-596)
*   Wilcoxon rank-sum test [356](#ch10.xhtml_term-597)
*   Wilcoxon signed-rank test [354](#ch10.xhtml_term-598)
*   Wolf, Johann Rudolf [139](#ch05.xhtml_term-599)
*   Wolf sunspot number [139](#ch05.xhtml_term-600)
*   Wölfer sunspot numbers 139n2
*   Wolfram Alpha [219](#ch07.xhtml_term-601)
*   world energy production by source [163](#ch05.xhtml_term-602)
*   worldwide wind power [156](#ch05.xhtml_term-603)

*   z-score [361–363](#ch10.xhtml_term-604), [374](#ch10.xhtml_term-605)

# Index of Python Terminology

*   `abs` [61](#ch03.xhtml_term-606)
*   `absnorm` [198](#ch06.xhtml_term-607)
*   `add_subplot` [152](#ch05.xhtml_term-608)
*   `and` [70–71](#ch03.xhtml_term-609)
*   `anderson` [363](#ch10.xhtml_term-610)
*   `append` [116](#ch04.xhtml_term-611), [118](#ch04.xhtml_term-612), [121](#ch04.xhtml_term-613), [125](#ch04.xhtml_term-614), [121](#ch04.xhtml_term-615), [125](#ch04.xhtml_term-616), [308n5](#ch09.xhtml_term-617)
*   `*args` [125](#ch04.xhtml_term-618)
*   `array` [74](#ch03.xhtml_term-619), [176](#ch06.xhtml_term-620)
*   `atol` [322](#ch09.xhtml_term-621)
*   `Axes3D` [169](#ch05.xhtml_term-622)
*   `axis` [156](#ch05.xhtml_term-623)

*   `bar` [155](#ch05.xhtml_term-624), [349](#ch10.xhtml_term-625)
*   `basefmt` [159](#ch05.xhtml_term-626)
*   `bisect` [204–207](#ch07.xhtml_term-627)
*   `bit_length` [68](#ch03.xhtml_term-628)
*   `boxplot` [341–342](#ch10.xhtml_term-629), [356](#ch10.xhtml_term-630)
*   `break` [110–111](#ch04.xhtml_term-631), [116–118](#ch04.xhtml_term-632)
*   `brentq` [230–233](#ch07.xhtml_term-633)

*   `clabel` [166](#ch05.xhtml_term-634)
*   `cm` [169](#ch05.xhtml_term-635)
*   `cmap` [169](#ch05.xhtml_term-636)
*   `color (c)` [141–142](#ch05.xhtml_term-637)
*   `colors` [165](#ch05.xhtml_term-638)
*   `continue` [118](#ch04.xhtml_term-639)
*   `contour` [165](#ch05.xhtml_term-640)
*   `contourf` [166](#ch05.xhtml_term-641)
*   `cstride` [169](#ch05.xhtml_term-642)

*   `def` [119–126](#ch04.xhtml_term-643)
*   `det` [274](#ch08.xhtml_term-644)
*   `dot` [190–193](#ch06.xhtml_term-645), [273](#ch08.xhtml_term-646)
*   `edgecolors` [144](#ch05.xhtml_term-647)
*   `elif` [106](#ch04.xhtml_term-648)
*   `else` [105](#ch04.xhtml_term-649)
*   `euler` [309](#ch09.xhtml_term-650)
*   `eulerm` [313](#ch09.xhtml_term-651)
*   `eye` [179](#ch06.xhtml_term-652)

*   `falpos` [209](#ch07.xhtml_term-653)
*   `falpos1` [210](#ch07.xhtml_term-654)
*   `falpos2` [211–212](#ch07.xhtml_term-655)
*   `False` [69–70](#ch03.xhtml_term-656)
*   `figsize` [153](#ch05.xhtml_term-657)
*   `figure` [151](#ch05.xhtml_term-658)
*   `fixpt` [227](#ch07.xhtml_term-659), [277](#ch08.xhtml_term-660)
*   `flatten` [180](#ch06.xhtml_term-661), [181](#ch06.xhtml_term-662)
*   `float` [72](#ch03.xhtml_term-663), [88](#ch03.xhtml_term-664)
*   `for` [112](#ch04.xhtml_term-665)
*   `funavg` [124–126](#ch04.xhtml_term-666)
*   `func` [124–128](#ch04.xhtml_term-667)

*   `gausselim` [266](#ch08.xhtml_term-668)
*   `gausselim1` [268](#ch08.xhtml_term-669)
*   `gausselimpivot` [269](#ch08.xhtml_term-670)
*   `gausselimpivot1` [271](#ch08.xhtml_term-671)
*   `genrand` [125–126](#ch04.xhtml_term-672)
*   `gety` [120–121](#ch04.xhtml_term-673)
*   `grid` [141](#ch05.xhtml_term-674)

*   `halfrand` [121–122](#ch04.xhtml_term-675)
*   `heun` [312](#ch09.xhtml_term-676)
*   `heunm` [326](#ch09.xhtml_term-677)
*   `histogram` [155](#ch05.xhtml_term-678), [349](#ch10.xhtml_term-679)
*   `hspace` [153](#ch05.xhtml_term-680)
*   `hsplit` [180](#ch06.xhtml_term-681)
*   `hstack` [179](#ch06.xhtml_term-682)

*   `if` [105](#ch04.xhtml_term-683)
*   `imag` [69](#ch03.xhtml_term-684)
*   `input` [88](#ch03.xhtml_term-685), [109](#ch04.xhtml_term-686), [111](#ch04.xhtml_term-687), [113](#ch04.xhtml_term-688), [120](#ch04.xhtml_term-689)
*   `int` [72](#ch03.xhtml_term-690), [123](#ch04.xhtml_term-691)
*   `integrate` [304–306](#ch09.xhtml_term-692), [319](#ch09.xhtml_term-693)
*   `inv` [194](#ch06.xhtml_term-694), [273](#ch08.xhtml_term-695)
*   `iqr` [123–124](#ch04.xhtml_term-696)

*   `**kwargs` [126](#ch04.xhtml_term-697)

*   `label` [162](#ch05.xhtml_term-698)
*   `lambda` [120–121](#ch04.xhtml_term-699), [124–125](#ch04.xhtml_term-700), [135](#ch04.xhtml_term-701)
*   `launch_angle` [241](#ch07.xhtml_term-702)
*   `legend` [146](#ch05.xhtml_term-703)
*   `len` [72](#ch03.xhtml_term-704), [114](#ch04.xhtml_term-705)
*   `linalg` [194–196](#ch06.xhtml_term-706), [273](#ch08.xhtml_term-707)
*   `linefmt` [159](#ch05.xhtml_term-708)
*   `linestype (ls)` [142](#ch05.xhtml_term-709)
*   `linewidth (lw)` [142](#ch05.xhtml_term-710)
*   `linspace` [138](#ch05.xhtml_term-711)
*   `loadtxt delimiter` [89–90](#ch03.xhtml_term-712)
*   `loadtxt unpack` [89–90](#ch03.xhtml_term-713)
*   `loc` [147](#ch05.xhtml_term-714)

*   `MAD` [339](#ch10.xhtml_term-715)
*   `Manning` [186–188](#ch06.xhtml_term-716)
*   `markeredgecolor (mec)` [145](#ch05.xhtml_term-717)
*   `markerfacecolor (mfc)` [145](#ch05.xhtml_term-718)
*   `markerfmt` [159](#ch05.xhtml_term-719)
*   `math module` [62](#ch03.xhtml_term-720), [76](#ch03.xhtml_term-721), [83](#ch03.xhtml_term-722)
*   `math.acos` [62](#ch03.xhtml_term-723)
*   `math.acosh` [62](#ch03.xhtml_term-724)
*   `math.asin` [62](#ch03.xhtml_term-725)
*   `math.asinh` [62](#ch03.xhtml_term-726)
*   `math.atan` [62](#ch03.xhtml_term-727)
*   `math.atanh` [62](#ch03.xhtml_term-728)
*   `math.cos` [62](#ch03.xhtml_term-729)
*   `math.cosh` [62](#ch03.xhtml_term-730)
*   `math.degrees` [62](#ch03.xhtml_term-731)
*   `math.e` [61–62](#ch03.xhtml_term-732)
*   `math.exp` [62](#ch03.xhtml_term-733), [65](#ch03.xhtml_term-734)
*   `math.inf` [61](#ch03.xhtml_term-735)
*   `math.log` [62](#ch03.xhtml_term-736)
*   `math.log10` [62](#ch03.xhtml_term-737)
*   `math.nan` [61](#ch03.xhtml_term-738)
*   `math.pi` [60–61](#ch03.xhtml_term-739)
*   `math.radians` [62](#ch03.xhtml_term-740)
*   `math.sin` [62](#ch03.xhtml_term-741)
*   `math.sinh` [62](#ch03.xhtml_term-742)
*   `math.sqrt` [62](#ch03.xhtml_term-743)
*   `math.tan` [62](#ch03.xhtml_term-744)
*   `math.tanh` [62](#ch03.xhtml_term-745)
*   `matmul` [273](#ch08.xhtml_term-746)
*   `matmult` [191–193](#ch06.xhtml_term-747)
*   `matplotlib` [137](#ch05.xhtml_term-748)
*   `mean` [336](#ch10.xhtml_term-749)
*   `median` [336](#ch10.xhtml_term-750)
*   `median_abs_deviation` [339](#ch10.xhtml_term-751)
*   `meshgrid` [164](#ch05.xhtml_term-752), [166](#ch05.xhtml_term-753)
*   `modsec` [220](#ch07.xhtml_term-754), [220](#ch07.xhtml_term-755)
*   `modsec` [220](#ch07.xhtml_term-756)
*   `mpl_toolkits` [169](#ch05.xhtml_term-757)
*   `mplot3d` [169](#ch05.xhtml_term-758)
*   `multinewt` [282](#ch08.xhtml_term-759)

*   `newtraph` [215](#ch07.xhtml_term-760)
*   `norm.cdf` [347–348](#ch10.xhtml_term-761), [355](#ch10.xhtml_term-762)
*   `norm.pdf` [347](#ch10.xhtml_term-763)
*   `norm.ppf` [361](#ch10.xhtml_term-764)
*   `normal` [351](#ch10.xhtml_term-765)
*   `not` [70–71](#ch03.xhtml_term-766)
*   `numpy (np)` [69](#ch03.xhtml_term-767), [74](#ch03.xhtml_term-768)
*   `numpy.append` [116](#ch04.xhtml_term-769), [118](#ch04.xhtml_term-770)
*   `numpy.arctan` [99](#ch03.xhtml_term-771)
*   `numpy.arctan2` [95–96](#ch03.xhtml_term-772), [99](#ch03.xhtml_term-773)
*   `numpy.array` [74](#ch03.xhtml_term-774)
*   `numpy.linspace` [124–125](#ch04.xhtml_term-775)
*   `numpy.load` [90](#ch03.xhtml_term-776)
*   `numpy.loadtxt` [89–90](#ch03.xhtml_term-777), [93](#ch03.xhtml_term-778)
*   `numpy.log10` [62](#ch03.xhtml_term-779), [76](#ch03.xhtml_term-780)
*   `numpy.matrix` [114](#ch04.xhtml_term-781)
*   `numpy.save` [90](#ch03.xhtml_term-782)
*   `numpy.savetxt` [90](#ch03.xhtml_term-783), [93](#ch03.xhtml_term-784)

*   `ones` [178](#ch06.xhtml_term-785)
*   `optimize` [285](#ch08.xhtml_term-786)
*   `or` [70–71](#ch03.xhtml_term-787)

*   `pctile` [122–123](#ch04.xhtml_term-788), [340](#ch10.xhtml_term-789)
*   `pie` [163](#ch05.xhtml_term-790)
*   `pivotswap` [269](#ch08.xhtml_term-791)
*   `plot` [139](#ch05.xhtml_term-792)
*   `plot_surface` [169](#ch05.xhtml_term-793)
*   `plot_wireframe` [169](#ch05.xhtml_term-794)
*   `polar` [158](#ch05.xhtml_term-795)
*   `poly` [236](#ch07.xhtml_term-796)
*   `polyfit` [369](#ch10.xhtml_term-797)
*   `polyval` [237](#ch07.xhtml_term-798), [372](#ch10.xhtml_term-799)
*   `print` [85](#ch03.xhtml_term-800)
*   `print format` [91–92](#ch03.xhtml_term-801)
*   `probplot` [373](#ch10.xhtml_term-802)
*   `pylab` [76](#ch03.xhtml_term-803)
*   `pylab color (c)` [79](#ch03.xhtml_term-804)
*   `pylab label` [82](#ch03.xhtml_term-805)
*   `pylab linestyle (ls)` [82](#ch03.xhtml_term-806)
*   `pylab marker` [80](#ch03.xhtml_term-807)
*   `pylab.grid` [78](#ch03.xhtml_term-808)
*   `pylab.hist` [118](#ch04.xhtml_term-809), [125](#ch04.xhtml_term-810)
*   `pylab.legend` [81](#ch03.xhtml_term-811)
*   `pylab.plot` [80](#ch03.xhtml_term-812)
*   `pylab.scatter` [77](#ch03.xhtml_term-813)
*   `pylab.show` [82](#ch03.xhtml_term-814)
*   `pylab.title` [78](#ch03.xhtml_term-815)
*   `pylab.xlabel` [78](#ch03.xhtml_term-816)
*   `pylab.ylabel` [78](#ch03.xhtml_term-817)
*   `pyplot` [137](#ch05.xhtml_term-818)

*   `quad` [304–305](#ch09.xhtml_term-819), [359](#ch10.xhtml_term-820)

*   `random` [118](#ch04.xhtml_term-821), [349](#ch10.xhtml_term-822)
*   `random.normalvariate` [118](#ch04.xhtml_term-823), [121–122](#ch04.xhtml_term-824), [125–126](#ch04.xhtml_term-825)
*   `range` [112](#ch04.xhtml_term-826)
*   `ranksums` [357](#ch10.xhtml_term-827)
*   `ravel` [181](#ch06.xhtml_term-828)
*   `real` [69](#ch03.xhtml_term-829)
*   `reshape` [181](#ch06.xhtml_term-830)
*   `resize` [181](#ch06.xhtml_term-831)
*   `root` [285–286](#ch08.xhtml_term-832)
*   `roots` [206](#ch07.xhtml_term-833), [234](#ch07.xhtml_term-834), [234](#ch07.xhtml_term-835)
*   `rotation` [156–157](#ch05.xhtml_term-836)
*   `round` [61–62](#ch03.xhtml_term-837)
*   `rstride` [169](#ch05.xhtml_term-838)
*   `rtol` [322](#ch09.xhtml_term-839)

*   `scatter` [139](#ch05.xhtml_term-840)
*   `semilogy` [162](#ch05.xhtml_term-841)
*   `set_title` [152–153](#ch05.xhtml_term-842), [163](#ch05.xhtml_term-843)
*   `set_xticks` [169](#ch05.xhtml_term-844)
*   `set_yticks` [169](#ch05.xhtml_term-845)
*   `set_zlim` [169](#ch05.xhtml_term-846)
*   `set_zticks` [169](#ch05.xhtml_term-847)
*   `sgnsqr` [119–120](#ch04.xhtml_term-848)
*   `shape` [191](#ch06.xhtml_term-849)
*   `shape attribute` [192](#ch06.xhtml_term-850)
*   `show` [141](#ch05.xhtml_term-851)
*   `solve` [273](#ch08.xhtml_term-852)
*   `solve_ivp` [319–322](#ch09.xhtml_term-853)
*   `stats` [304](#ch09.xhtml_term-854), [339](#ch10.xhtml_term-855)
*   `std` [338–339](#ch10.xhtml_term-856)
*   `stem` [159](#ch05.xhtml_term-857)
*   `str` [72](#ch03.xhtml_term-858)
*   `subplots_adjust` [153](#ch05.xhtml_term-859)
*   `sys.exit` [113](#ch04.xhtml_term-860)

*   `title` [141](#ch05.xhtml_term-861)
*   `trace` [198](#ch06.xhtml_term-862)
*   `transpose` [193](#ch06.xhtml_term-863)
*   `trap` [302](#ch09.xhtml_term-864)
*   `trap1` [301](#ch09.xhtml_term-865)
*   `trapdata` [305](#ch09.xhtml_term-866)
*   `trapz` [305–306](#ch09.xhtml_term-867)
*   `True` [69](#ch03.xhtml_term-868), [89](#ch03.xhtml_term-869)
*   `ttest_ind` [358](#ch10.xhtml_term-870)
*   `twinx` [149](#ch05.xhtml_term-871)

*   `uniform` [349](#ch10.xhtml_term-872)
*   `use_line_collection` [159](#ch05.xhtml_term-873)

*   `vdot` [190–193](#ch06.xhtml_term-874)
*   `view_init` [169](#ch05.xhtml_term-875)
*   `vsplit` [180](#ch06.xhtml_term-876)
*   `vstack` [179](#ch06.xhtml_term-877)

*   `wegstein` [228](#ch07.xhtml_term-878)
*   `weibull` [361](#ch10.xhtml_term-879)
*   `while` [110–111](#ch04.xhtml_term-880), [113](#ch04.xhtml_term-881)
*   `width` [155](#ch05.xhtml_term-882)
*   `wspace` [153](#ch05.xhtml_term-883)

*   `xlabel` [141](#ch05.xhtml_term-884), [169](#ch05.xhtml_term-885)
*   `xlim` [148](#ch05.xhtml_term-886)
*   `xticks` [156–157](#ch05.xhtml_term-887)

*   `ylabel` [141](#ch05.xhtml_term-888), [169](#ch05.xhtml_term-889)
*   `ylim` [148](#ch05.xhtml_term-890)

*   `zeros` [178](#ch06.xhtml_term-891)