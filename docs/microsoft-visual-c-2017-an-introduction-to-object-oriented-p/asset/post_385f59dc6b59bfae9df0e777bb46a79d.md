
# Joyce Farrell

# Microsoft®

# Visual C# 2017

# An Introduction to Object-Oriented Programming

# Seventh Edition

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202

# MICROSOFT® VISUAL C#® 2017

AN INTRODUCTION TO OBJECT-ORIENTED PROGRAMMING, SEVENTH EDITION

# JOYCE FARRELL

CENGAGE Australia • Brazil • Mexico • Singapore • United Kingdom • United States

# Microsoft® Visual C# 2017: Introduction to Object-Oriented Programming, Seventh Edition Joyce Hefferon

© 2018, Cengage Learning

Unless otherwise noted, all content is © Cengage.

ALL RIGHTS RESERVED. No part of this work covered by the copyright may be reproduced or distributed in any form or by any means, except as permitted by U.S. copyright law, without the prior permission of the copyright owner.

SVP, GM Science, Technology & Math; Balraj S. Kohli

Unless otherwise noted all screenshots are courtesy of Microsoft Corporation
Unless otherwise noted all tables/figures exhibits are © 2018 Cengage *

Senior Product Director: Kathleen McMahon

Product Team Manager: Kristin McNary

Associate Product Manager: Kate Mason

| For product information and technology assistance, contact us at Cengage Learning Customer & Sales Support, 1-800-354-9706 |
| For permission to use material from this or product, submit all requests online at www.cengage.com/permissions. Further permissions questions can be e-mailed to permissionrequest@cengage.com |

Senior Director, Development: Julia Callabero

Senior Content Development: Leigh Hefferson

Library of Control Number: 201794107

Senior Content Developer: Alyssa Pratt

Softbound ISBN: 978-1-337-10210-0
Loose Leaf ISBN: 978-1-337-68577-1

Product Assistant: Jake Toth

Cengage Learning
20 Channel Center Street
Boston, MA 02210

Marketing Manager: Michele Micighe

Marketing Manager: Jeffrey A. Tuson

Cengage is a leading provider of creating learning solutions with employees residing in nearly 40 countries and in over 125 countries around the world. Find your local representative at www.cengage.com

Senior Content Project Manager: Jennifer Ferrari-Geroy

Cengage products are produced in Canada by Nelson Education, Ltd.

Senior Designer/Art Director: Diana Graham

To learn more about Cengage Learning, visit www.cengage.com
Purchase any of your products at your local college store or at our online store at www.cengage.com

Production Service/Composition: SPI Global

Notice to the Reader

Publisher does not warrant or guarantee any of the products described herein or perform any independent analysis in connection with any product information contained herein. Publisher does not assume, and expressly claims, any information other than that provided by the manufacturer. The reader is expressly warned to consider and adopt all safety precautions that might be indicated by the activities described herein and avoid all potential hazards. By following the instructions contained herein, the reader wisely assumes all risks with such instructions. The publisher makes no representations or warranties of any kind, including not limited to, the warranties of fitness for particular purpose or merchant, are any representations implied with respect to the matter set herein, and the publisher takes no responsibility with respect to such material. The publisher shall not be liable for any special, consequential, or exemplary damages resulting, in whole or part, from the readers' use of, or reliance upon, this material.

Cover image: Colormos/Photodisc/
Getty Images

Printed in the United States of America
Print Number: 01

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-02-200-2022

# Brief Contents

- Preface . . . . . . . . . . . . . . . . . . . . . . XV
- CHAPTER 1 A First Program Using C# . . . . . . . . . . . . . . . . . . 1
- CHAPTER 2 Using Data . . . . . . . . . . . . . . . . . . . . . . 47
- CHAPTER 3 Using GUI Objects and the Visual Studio IDE . . . . . . . . . . . . . 99
- CHAPTER 4 Making Decisions . . . . . . . . . . . . . . . . . . . . . . 133
- CHAPTER 5 Looping . . . . . . . . . . . . . . . . . . . . . . . . 185
- CHAPTER 6 Using Arrays . . . . . . . . . . . . . . . . . . . . . . . 223
- CHAPTER 7 Using Methods . . . . . . . . . . . . . . . . . . . . . . . 265
- CHAPTER 8 Advanced Concepts. . . . . . . . . . . . . . . . . 307
- CHAPTER 9 Using Classes and Objects . . . . . . . . . . . . . . . . . 351
- CHAPTER 10 Introduction to Inheritance . . . . . . . . . . . . . . . . 421
- CHAPTER 11 Exception Handling . . . . . . . . . . . . . . . . . . . . . 483
- CHAPTER 12 Using Controls . . . . . . . . . . . . . . . . . . . . . . 535
- CHAPTER 13 Handling Events . . . . . . . . . . . . . . . . . . . . . . . 597
- CHAPTER 14 Files and Streams . . . . . . . . . . . . . . . . . . . . . . 645
- APPENDIX A Operator Precedence and Associativity. . . . . . . . . 695
- APPENDIX B Understanding Number Systems and Codes. . . . . . . . . . . 697
- APPENDIX C Using the IDE Editor . . . . . . . . . . . . . . . . . . . . . 707
- Glossary . . . . . . . . . . . . . . . . . . . . . . . 711
- Index . . . . . . . . . . . . . . . . . . . . . . . 729

# Contents

- Preface . . . . . . . . . . . . . . . . . . . xv
- CHAPTER 1 A First Program Using C# . . . . . . . . . . . 1
- The Programming Process . . . . . . . . . . . . . . . . 2
- Procedural and Object-Oriented Programming . . . . 4
- Features of Object-Oriented Programming Languages . . . 7
- The C# Programming Language. . . . . . . . . . . . . . . . . . . 9
- Writing a C# Program that Produces Output . . . . . 11
- Selecting Identifiers . . . . . . . . . . . . . . . . . . . . 14
- Improving Programs by Adding Comments . . . . . 18
- and Using the System Namespace . . . . . . . . . . . 18
- Adding Program Comments. . . . . . . . . . . . . . . . 18
- Using the System Namespace . . . . . . . . . . . 19
- Compiling and Executing a C# Program . . . . . . 23
- Compiling Code from the Command Prompt . . . . . 24
- Compiling Code Using the Visual Studio IDE . . . . 26
- Noticing the Differences Between the Programs in the Text Editor and the IDE . . . . . . . . . . . . . . . . . 29
- Deciding Which Environment to Use . . . . . . . . . . . 30
- Chapter Summary . . . . . . . . . . . . . . . . . . 38
- Key Terms . . . . . . . . . . . . . . . . . . . . . . 38
- Review Questions . . . . . . . . . . . . . . . . . 42
- Exercises . . . . . . . . . . . . . . . . . . . . . 44
- CHAPTER 2 Using Data . . . . . . . . . . . . . . . . . 47
- Declaring Variables . . . . . . . . . . . . . . . . . 48
- Displaying Variable Values . . . . . . . . . . . 52
- Variable Alignment . . . . . . . . . . . . . 55
- Using the Integral Data Types. . . . . . . . . . . . . 56
- Using Floating-Point Data Types. . . . . . . . 59
- Formatting Floating-Point Values. . . . . . . 60
- Using Arithmetic Operators. . . . . . . . 63
- Using Shortcut Arithmetic Operators. . . . . . . 64
- Using the bool Data Type . . . . . . . . . . . . . . . . . 68
- Understanding Numeric Type Conversion. . . . . . . . . . . . . 71
- Using the char Data Type . . . . . . . . . . . . . . . . . 74
- Using the string Data Type . . . . . . . . . . . . . . . . . 76
- Defining Constants . . . . . . . . . . . . . . . 80
- Working with Enumerations . . . . . . . . . . . . 81
- Accepting Console Input . . . . . . . . . . . . . . 84
- Using the Convert Class . . . . . . . . . . . . 84
- Using the Parse() Methods . . . . . . . . . . . . . 86
- Chapter Summary . . . . . . . . . . . . . . . . . . . 89
- Key Terms . . . . . . . . . . . . . . . . . . . . . 90
- Review Questions . . . . . . . . . . . . . . . . . 93
- Exercises . . . . . . . . . . . . . . . . . . . . 96
- CHAPTER 3 Using GUI Objects and the Visual Studio IDE . . . . 99
- Creating a Form in the IDE . . . . . . . . . . . . . . . 100
- Using the Toolbox to Add a Button to a Form . . . . . 105
- Adding Functionality to a Button on a Form . . . . . 107
- Adding Labels and TextBoxes to a Form . . . . . . 109
- Understanding Focus and Tab Control . . . . . . . . 112
- Formatting Data in GUI Applications . . . . . . . . 113
- Changing a Label's Font. . . . . . . . . . . . . . . . . 114
- Naming Forms and Controls . . . . . . . . . . . . . 114
- Correcting Errors . . . . . . . . . . . . . . . . 116
- Deleting an Unwanted Event-Handling Method. . . . . 117
- Failing to Close a Form Before Attempting . . . . 118
- To Reexecute a Program . . . . . . . . . . . . . . . 118
- Using Visual Studio Help . . . . . . . . . . . . . 118
- Deciding Which Interface to Use . . . . . . . . . . 119
- Chapter Summary . . . . . . . . . . . . . . . . . . . 125
- Key Terms . . . . . . . . . . . . . . . . . . . . . . 126
- Review Questions . . . . . . . . . . . . . . . . . 127
- Exercises . . . . . . . . . . . . . . . . . . . . 130
- CHAPTER 4 Making Decisions . . . . . . . . . . . . . . . . . . 133
- Understanding Logic-Planning Tools and Decision Making . . 134
- Making Decisions Using the if Statement . . . . . . . 137
- A Note on Equivalency Comparisons. . . . . . . . . . . . 143
- Making Decisions Using the if-else Statement. . . . . 145
