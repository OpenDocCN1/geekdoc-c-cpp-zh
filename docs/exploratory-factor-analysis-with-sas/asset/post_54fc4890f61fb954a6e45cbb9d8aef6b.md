
## Exploratory Factor Analysis with SAS®

Jason W. Osborne • Erin S. Banjanovic

## Exploratory Factor Analysis with SAS®

Jason W. Osborne • Erin S. Banjanovic

![](img/29951003f0d11c9d825feb73bff9c8e6_1_0.png)

The correct bibliographic citation for this manual is as follows: Osborne, Jason W., and Erin S. Banjanovic. 2016. Exploratory Factor Analysis with SAS®. Cary, NC: SAS Institute Inc.

## Exploratory Factor Analysis with SAS®

Copyright © 2016, SAS Institute Inc., Cary, NC, USA

- ISBN 978-1-62960-064-2 (Hard copy)
- ISBN 978-1-62960-241-7 (Epub)
- ISBN 978-1-62960-242-4 (Mobi)
- ISBN 978-1-62960-243-1 (PDF)

All Rights Reserved. Produced in the United States of America.

For a hard copy book: No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or by any means, electronic, mechanical, photocopying, or otherwise, without the prior written permission of the publisher, SAS Institute Inc.

For a web download or e-book: Your use of this publication shall be governed by the terms established by the vendor at the time you acquire this publication.

The scanning, uploading, and distribution of this book via the Internet or any other means without the permission of the publisher is illegal and punishable by law. Please purchase only authorized electronic editions and do not participate in or encourage electronic piracy of copyrighted materials. Your support of others' rights is appreciated.

U.S. Government License Rights; Restricted Rights: The Software and its documentation is commercial computer software developed at private expense and is provided with RESTRICTED RIGHTS to the United States Government. Use, duplication, or disclosure of the Software by the United States Government is subject to the license terms of this Agreement pursuant to, as applicable, FAR 12.212, DFAR 227.7202-1(a), DFAR 227.7202-3(a), and DFAR 227.7202-4, and, to the extent required under U.S. federal law, the minimum restricted rights as set out in FAR 52.227-19 (DEC 2007). If FAR 52.227-19 is applicable, this provision serves as notice under clause (c) thereof and no other notice is required to be affixed to the Software or documentation. The Government's rights in Software and documentation shall be only those set forth in this Agreement.

SAS Institute Inc., SAS Campus Drive, Cary, NC 27513-2414

March 2016

SAS® and all other SAS Institute Inc. product or service names are registered trademarks or trademarks of SAS Institute Inc. in the USA and other countries. ® indicates USA registration.

Other brand and product names are trademarks of their respective companies.

## Contents

- About This Book .................................................... vii
- About the Author .................................................... xi

## Chapter 1 / Introduction to Exploratory Factor Analysis .................... 1

- A Tool for Exploration .................................................... 1
- EFA vs PCA .................................................... 2
- Steps to Follow When Conducting EFA .................................................... 5
- Basic Syntax for EFA .................................................... 7
- Summary .................................................... 9
- References .................................................... 9

## Chapter 2 / Extraction Method .................................................... 11

- What Is Extraction? .................................................... 11
- Key Concepts .................................................... 12
- Extraction Techniques .................................................... 13
- Three Pedagogical Examples .................................................... 15
- Example Syntax and Output .................................................... 16
- Does Extraction Method Matter? .................................................... 20
- Summary .................................................... 25
- Exercises .................................................... 26
- Instruments Used in Examples .................................................... 27
- References .................................................... 31

## Chapter 3 / Factor Extraction Criteria ........................................ 33

- How Many Factors? .................................................... 33
- Extraction Criteria .................................................... 34
- Example Syntax and Output .................................................... 36
- How Do the Criteria Compare? .................................................... 45
- Summary .................................................... 57
- Exercises .................................................... 58
- References .................................................... 58

## Chapter 4 / Rotation ............................................................ 61

- The Magic of Rotation .................................................... 61
- Types of Rotation .................................................... 63
- Orthogonal vs Oblique Rotation .................................................... 64
- Interpretation of Factor Matrices .................................................... 65
- Example Syntax and Output ......... 66
- Which Method? ......... 69
- Exploring Multiple Solutions ......... 75
- Summary ......... 80
- Exercises ......... 81
- References ......... 82

## Chapter 5 / Sample Size Matters ......... 83

- Why Is Sample Size Important? ......... 83
- Published Guidelines ......... 84
- Sample Size in Practice ......... 85
- An Empirical Investigation in Sample Size ......... 86
- An Applied Example from Costello & Osborne ......... 87
- Application: Impact of Sample Size on Interpretation ......... 89
- Summary ......... 93
- Exercises ......... 93
- References ......... 94

## Chapter 6 / Replication Statistics ......... 97

- Importance of Replication ......... 97
- Let's Bring Replication to EFA ......... 98
- Procedural Aspects of Replicability Analysis ......... 99
- Quantifying Replicability in EFA ......... 100
- Application: Replication of Marsh SDQ Data ......... 102
- Summary ......... 109
- Exercises ......... 110
- References ......... 110

## Chapter 7 / Bootstrap Applications ......... 113

- How Does Bootstrap Resampling Fit into EFA? ......... 113
- The Rise of Resampling ......... 114
- Bootstrap Resampling Methods ......... 115
- What Can Bootstrap Resampling Do, and What Should It Not Be Used For? ......... 116
- Example Syntax and Output ......... 117
- Application ......... 126
- Summary ......... 137
- Exercises ......... 138
- References ......... 138

## Chapter 8 / Data Cleaning ......... 141

- The Importance of Data Cleaning ......... 141
- Outliers .................................... 142
- Application: Random vs Constant Responding ........ 147
- Missing Data ................................ 149
- Application: Nonrandom Missingness and Imputation .... 152
- Summary ..................................... 155
- Exercises ................................... 155
- References .................................. 156

## Chapter 9 / Factor Scores .................... 159

- Factor Scores 101 ........................... 159
- Example Syntax and Output ................... 160
- Application: Factor Score Estimation ........ 162
- What Are Modern Alternatives? ............... 168
- Summary ..................................... 169
- Exercises ................................... 169
- References .................................. 170

## Chapter 10 / Higher-Order Factors ............ 171

- What Is a Higher-Order Factor? .............. 171
- Did the Initial Solution Get It Right? ...... 172
- Mechanics of Performing Second-Order Factor Analysis ... 173
- Application: Replication of Second-Order Factor ... 177
- Summary ..................................... 179
- Exercises ................................... 179
- References .................................. 179

## Chapter 11 / After the EFA: Internal Consistency ... 181

- What Comes Next? ............................ 181
- What Is Cronbach's Alpha (And What Is It Not)? ... 182
- What Is "Good Enough" for Alpha? ............ 184
- Factors That Influence Alpha and Its Use .... 185
- Estimation of Alpha in SAS .................. 187
- Would Error-Free Measurement Make a Real Difference? ... 189
- Application ................................. 191
- Summary ..................................... 202
- Exercises ................................... 203
- References .................................. 204

## Chapter 12 / Summary and Conclusions ........ 207

- Best Practices for EFA ...................... 207
- References .................................. 209
