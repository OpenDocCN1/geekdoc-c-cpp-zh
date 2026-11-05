
## C# Programming

### From Problem Analysis to Program Design

Fourth Edition

![](img/36e48639a06772bcb0fa1ea2525b33a3_0_0.png)

Microsoft Visual C# 2012

Barbara Doyle

## C# PROGRAMMING:

### From Problem Analysis to Program Design

### Fourth Edition

This is an electronic version of the print textbook. Due to electronic rights restrictions, some third party content may be suppressed. Editorial review has deemed that any suppressed content does not materially affect the overall learning experience. The publisher reserves the right to remove content from this title at any time if subsequent rights restrictions require it. For valuable information on pricing, previous editions, changes to current editions, and alternate formats, please visit www.cengage.com/highered to search by ISBN#, author, title, or keyword for materials in your areas of interest.

## C# Programming:

### From Problem Analysis to Program Design

Fourth Edition

Barbara Doyle

![](img/36e48639a06772bcb0fa1ea2525b33a3_4_0.png)

## C# Programming: From Problem Analysis to Program Design, Fourth Edition

Barbara Doyle

- Executive Editor: Kathleen McMahon
- Senior Product Manager: Alyssa Pratt
- Editorial Assistant: Sarah Ryan
- Content Project Manager: Jennifer Feltri-George
- Art Director: Cheryl Pearl, GEX
- Manufacturing Planner: Julio Esperas
- Cover Designer: GEX Publishing Services
- Cover Photo: ©iurii/Shutterstock
- Copyeditor: Andrea Schein
- Indexer: Sharon Hilgenberg
- Compositor: Integra

© 2014 Cengage Learning

ALL RIGHTS RESERVED. No part of this work covered by the copyright herein may be reproduced, transmitted, stored, or used in any form or by any means graphic, electronic, or mechanical, including but not limited to photocopying, recording, scanning, digitizing, taping, Web distribution, information networks, or information storage and retrieval systems, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act, without the prior written permission of the publisher.

For product information and technology assistance, contact us at

Cengage Learning Customer & Sales Support,
www.cengage.com/support

For permission to use material from this text or product,
submit all requests online at cengage.com/permissions
Further permissions questions can be e-mailed to
permissionrequest@cengage.com

Library of Congress Control Number: 2013932312
ISBN-13: 978-1-285-09626-1
ISBN-10: 1-285-09626-6

Cengage Learning
20 Channel Center Street
Boston, MA 02210
USA

Some of the product names and company names used in this book have been used for identification purposes only and may be trademarks or registered trademarks of their respective manufacturers and sellers.

Any fictional data related to persons or companies or URLs used throughout this book is intended for instructional purposes only. At the time this book was printed, any such data was fictional and not belonging to any real persons or companies.

Cengage Learning reserves the right to revise this publication and make changes from time to time in its content without notice.

The programs in this book are for instructional purposes only. They have been tested with care, but are not guaranteed for any particular intent beyond educational purposes. The author and the publisher do not offer any warranties or representations, nor do they accept any liabilities with respect to the programs.

Cengage Learning is a leading provider of customized learning solutions with office locations around the globe, including Singapore, the United States, the United Kingdom, Australia, Mexico, Brazil, and Japan. Locate your local office at: www.cengage.com/global

Cengage Learning products are represented in Canada by Nelson Education, Ltd.

To learn more about Cengage Learning visit www.cengage.com.

Purchase any of our products at your local college store or at our preferred online store: www.cengagebrain.com

## BRIEF CONTENTS

Neale Cousland / Shutterstock.com

- PREFACE xxi
- 1. Introduction to Computing and Programming 1
- 2. Data Types and Expressions 65
- 3. Methods and Behaviors 131
- 4. Creating Your Own Classes 191
- 5. Making Decisions 247
- 6. Repeating Instructions 313
- 7. Arrays 383
- 8. Advanced Collections 439
- 9. Introduction to Windows Programming 493
- 10. Programming Based on Events 577
- 11. Advanced Object-Oriented Programming Features 691
- 12. Debugging and Handling Exceptions 775
- 13. Working with Files 837
- 14. Working with Databases 893
- 15. Web-Based Applications 979
- APPENDIX A Visual Studio Configuration 1083
- APPENDIX B Code Editor Tools 1099
- APPENDIX C Character Sets 1111
- APPENDIX D Operator Precedence 1113
- APPENDIX E C# Keywords 1115
- GLOSSARY 1117
- INDEX 1131

![](img/36e48639a06772bcb0fa1ea2525b33a3_8_0.png)

## TABLE OF CONTENTS

Neale Cousland / Shutterstock.com

- Preface xxi
- **1 INTRODUCTION TO COMPUTING AND PROGRAMMING** — 1
  - History of Computers — 2
  - System and Application Software — 4
    - System Software — 4
    - Application Software — 6
  - Software Development Process — 6
    - Steps in the Program Development Process — 7
  - Programming Methodologies — 13
    - Structured Procedural Programming — 14
    - Object-Oriented Programming — 16
  - Evolution of C# and .NET — 19
    - Programming Languages — 19
    - .NET — 21
    - Why C#? — 23
  - Types of Applications Developed with C# — 24
    - Web Applications — 24
    - Windows Applications — 25
    - Console Applications — 26
  - Exploring the First C# Program — 27
    - Elements of a C# Program — 28
      - Comments — 28
      - Using Directive — 30
      - Namespace — 32
      - Class Definition — 32
      - Main() Method — 33
      - Method Body Statements — 34
  - Compiling, Building, and Running an Application — 38
    - Typing Your Program Statements — 38
    - Compilation and Execution Process — 39
    - Compiling the Source Code Using Visual Studio IDE — 39
  - Debugging an Application — 45
    - Syntax Errors — 45
    - Run-time Errors — 47
  - Creating an Application — 47
  - Coding Standards — 52
    - Pseudocode — 52
  - Resources — 53
  - Quick Review — 53
  - Exercises — 56
  - Programming Exercises — 61
- **2. DATA TYPES AND EXPRESSIONS** — 65
  - Data Representation — 66
    - Bits — 66
    - Bytes — 66
    - Binary Numbering System — 66
    - Character Sets — 69
    - Kilobyte, Megabyte, Gigabyte, Terabyte, Petabyte... — 70
  - Memory Locations for Data — 70
    - Identifiers — 71
    - Variables — 75
    - Literal Values — 75
  - Types, Classes, and Objects — 76
    - Types — 76
    - Classes — 77
    - Objects — 78
  - Predefined Data Types — 79
    - Value Types — 80
      - Integral Data Types — 82
      - Floating-Point Types — 85
      - Decimal Types — 86
      - Boolean Variables — 87
    - Declaring Strings — 88
    - Making Data Constant — 88
  - Assignment Statements — 89
    - Basic Arithmetic Operations — 92
    - Increment and Decrement Operations — 95
    - Compound Operations — 98
  - Order of Operations — 100
    - Mixed Expressions — 102
    - Casts — 103
  - Formatting Output — 104
    - Width Specifier — 109
  - Coding Standards — 119
    - Naming Conventions — 119
    - Spacing Conventions — 119
    - Declaration Conventions — 120
  - Resources — 120
  - Quick Review — 120
  - Exercises — 121
  - Programming Exercises — 127
- **3 METHODS AND BEHAVIORS** — 131
  - Anatomy of a Method — 132
    - Modifiers — 134
    - Return Type — 137
    - Method Name — 138
    - Parameters — 138
    - Method Body — 139
  - Calling Class Methods — 141
  - Predefined Methods — 143
  - Writing Your Own Class Methods — 157
    - Void Methods — 157
    - Value-Returning Method — 159
    - Types of Parameters — 164
    - Named and Optional Parameters — 169
      - Default Values with Optional Parameters — 170
      - Named Parameters — 171
  - Coding Standards — 180
    - Naming Conventions — 180
    - Spacing Conventions — 180
    - Declaration Conventions — 180
    - Commenting Conventions — 181
  - Resources — 181
  - Quick Review — 181
  - Exercises — 182
  - Programming Exercises — 189
- **4 CREATING YOUR OWN CLASSES** — 191
  - The Object Concept — 192
    - Private Member Data — 193
  - Constructor — 197
  - Writing Your Own Instance Methods — 200
    - Accessor — 200
    - Mutators — 201
    - Other Instance Methods — 202
  - Property — 202
  - ToString() Method — 204
  - Calling Instance Methods — 206
    - Calling the Constructor — 206
    - Calling Accessor and Mutator Methods — 208
    - Calling Other Instance Methods — 209
  - Testing Your New Class — 210
  - Coding Standards — 235
    - Naming Conventions — 235
    - Classes — 235
    - Properties — 235
    - Methods — 236
