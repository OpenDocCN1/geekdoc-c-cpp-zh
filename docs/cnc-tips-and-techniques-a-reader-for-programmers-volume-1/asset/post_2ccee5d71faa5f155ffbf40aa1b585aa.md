
ACPL ITEM DISCARDED

S1

## CNC Tips and Techniques

Peter Smid

![](img/0023bd5cc50494e6d7799ab76d437c8d_0_0.png)

## CNC Tips and Techniques

### A Reader for Programmers

Peter Smid

Industrial Press Inc.  
New York

A full catalog record for this book will be available from the Library of Congress.

ISBN: 978-0-8311-3472-3

Industrial Press, Inc.  
989 Avenue of the Americas  
New York, NY 10018

- Sponsoring Editor: John Carleo
- Developmental Editor: Robert Weinstein
- Interior Text and Cover Design: Janet Romano
- Cover Photo courtesy of: James A. Harvey

Copyright © 2013 by Industrial Press. Printed in the United States of America. All rights reserved. This book, or any parts thereof, may not be reproduced, stored in a retrieval system, or transmitted in any form without the permission of the publisher.

## About the Book

Since 2000, Industrial Press has been fortunate to include Peter Smid among its family of authors. Both a popular and prolific author, Peter has anchored the CNC portion of our list, headed by the worldwide bestseller, *CNC Programming Handbook*, now in its third edition.

*CNC Tips and Techniques: A Reader for Programmers* is Peter’s fifth book with Industrial Press. During the past decade, in addition to all of his responsibilities as book author, consultant, and educator, Peter wrote a regular column for *Shop Talk*, a monthly magazine that offered “metalworking solutions for the manufacturing and machining industry.”

Peter wrote dozens of columns for *Shop Talk*, and his columns addressed the full gamut of CNC topics. They addressed tapping and threading and knurling. They addressed program length and memory needs. They addressed personnel issues, for example, the advantages and disadvantages of having programmers and operators as separate positions or merged. A variety of columns focused on G-codes, M-functions, cycles, and macros. And there were still more.

Ever since *Shop Talk* ceased publication, these columns have been unavailable. Now, in *CNC Tips and Techniques*, Industrial Press is delighted to bring them back to you—over 60 of the best of Peter’s columns—under one cover, so that you can have full and easy access to the advice Peter has been sharing over the past decade.

Each of these essays has been thoroughly reviewed since its initial publication and updated as needed to reflect ongoing changes in the field. They are presented here in chronological order of when they first appeared. An alternative table of contents, organized by topic, has been included, and at the back of the book you’ll also find several useful appendices and an extensive index.

We hope you’ll find *CNC Tips and Techniques* a valuable addition to your CNC library, and that Peter’s advice will make your work more efficient, more effective, and more rewarding.

Peter joins us in welcoming your feedback and questions. Simply write to us at info@industrialpress.com, and we’ll be sure to share your messages with him.

*Industrial Press*  
*April 2013*

![](img/0023bd5cc50494e6d7799ab76d437c8d_5_0.png)

Digitized by the Internet Archive in 2018 with funding from Kahle/Austin Foundation

## About the Author

**Peter Smid** has been a professional consultant, educator, and speaker, with many years of practical, hands-on experience in industry and education, including CNC and CAD/CAM applications on all levels. His consulting has focused on the practical use of CNC technology, part programming, AutoCAD®, Mastercam® and other CAD/CAM software, as well as advanced machining, tooling, setup, and many related fields. As a consultant he has successfully assisted several hundred companies with his wide-ranging knowledge.

Over the years, Peter has developed and delivered hundreds of customized educational programs to thousands of instructors and students at colleges and universities across United States, Canada and Europe, as well as to many manufacturing companies and private sector organizations. He has actively participated in many industrial trade shows, conferences, workshops and seminars.

Peter has also written many articles and in-house publications on the subject of CNC and CAD/CAM and for six years he wrote a monthly column in the *Shop Talk* magazine.

Peter Smid is the author of four other best-selling CNC books published by Industrial Press, Inc. and all books are also available as e-books. For more information, go to *www.industrialpress.com*.

- **CNC PROGRAMMING HANDBOOK**  
  A Comprehensive Guide to Practical CNC Programming  
  *Third Edition – ISBN 978-0-8311-3347-4*

- **CNC CONTROL SETUP for MILLING AND TURNING**  
  Mastering CNC Control Systems  
  *ISBN 978-0-8311-3350-4*

- **FANUC CNC CUSTOM MACROS**  
  Programming Resources for Fanuc Custom Macro B Users  
  *ISBN 978-0-8311-3157-9*

- **CNC PROGRAMMING TECHNIQUES**  
  An Insider’s Guide to Effective Methods and Applications  
  *ISBN 978-0-8311-3185-2*

Peter welcomes your comments, suggestions and questions. Please write to him at info@industrialpress.com

## Acknowledgements

I have made a number of references to several manufacturers and software developers in this book. It is only fair to list them below:

- FANUC and CUSTOM MACRO or USER MACRO or MACRO B are registered trademarks of Fanuc Ltd, Japan
- Mastercam is a registered trademark of CNC Software Inc., Tolland, CT, USA
- Edgecam is a registered trademark of Pathtrace, Inc., UK
- NCPlot is a registered trademark of NCPlot LLC, Muskegon, MI, USA
- AutoCAD is a registered trademark of Autodesk, Inc., San Rafael, CA, USA
- WINDOWS is a registered trademark of Microsoft, Inc., Redmond, WA, USA

There are other companies mentioned in this book.

Caterpillar, Fadal, Haas, Iscar, Makino, Mitsubishi, Okuma, Sandvik, Siemens, Yasnac ... and some others that may have escaped me.

Also, my thanks to the publishing team at Industrial Press.

John Carleo, Janet Romano, Robert Weinstein  
...without you, this book would not have happened

## Table of Contents

- About the Book ................................ iii
- About the Author .............................. v
- Table of Contents by Topic .................... xiii

### 2004

- CNC Turning — Why Are There So Many Errors? ........ 3
- Why Should I Know Manual Programming? ............... 6
- Running the First Part — Economically, That Is ...... 9
- Are You a CAM Machinist? ............................ 12
- CAD/CAM or CAD and CAM? ............................. 14
- Part Program Upgrading and Updating ................ 16
- Lathe Cycles — To Use or Not to Use? ................ 19
- Short Suggestions for Long Programs ................. 22
- Keep Records — Document Your Programs .............. 25
- Focus on Numbers .................................... 28
- CNC Programmer/Operator — Should One Person Be Both? 30
- Using CAM Software in Small Shops ................... 33

### 2005

- Minimizing Program Length ........................ 43
- Conversion of Lathe Cycles ........................ 46
- Shifting Program Zero — Part 1 .................... 49
- Shifting Program Zero — Part 2 .................... 51
- Threading Methods Compared ......................... 54
- When 1 Thou Equals 65 Dollars ...................... 56
- Alternate CNC Machine Selection .................... 59
- Standard and Rigid Tapping — Part 1 ................ 62

### 2006

- Standard and Rigid Tapping — Part 2 ................ 67
- Mastering M-Functions .............................. 70
- Tool Length Setup — Three Methods ................... 73
- (Extreme) Power of Subprograms ...................... 75
- Special Purpose G-Codes ............................ 78
- Well-Structured Program Structure ................................ 82
- Imaging a Mirror Image ............................................. 84
- Homeward Bound with G28 ............................................ 87
- Block Skip Adds Flexibility ........................................ 91
- Simulating the Toolpath ............................................ 94
- Automatic Corner Breaking .......................................... 97
- Working in Planes ................................................. 100

### 2007

- A Case for Polar Coordinates ...................................... 107
- The “Other” Work Offset ............................................ 110
- Going Helical with Threads ......................................... 113
- G76: Two Formats, One Cycle ........................................ 116
- Multi-Start Threading .............................................. 119
- Automatic Tool Change — ATC ........................................ 122
- Maximum Tool Specifications ........................................ 125
- Control Features — Optional or Standard? ........................... 127
- Fixed Cycles Repetition ............................................. 130
- Programming Process — When Is It Completed? .......................... 133
- Quality in CNC Programming .......................................... 136
- Short Ideas and Observations ........................................ 138

### 2008

- Spindle Speed Control on CNC Lathes ................................ 145
- Live Tooling on CNC Lathes ............................................ 148
- Trial Cut for Measuring .............................................. 151
- Easing Up on Calculations ............................................. 154
- Preventing Scrap with Offsets ......................................... 157
- Interpreting a CNC Program ............................................ 160
- Default Settings in Macros ............................................ 164
- Create Your Own G-Code ................................................ 167
- Scaling Option ......................................................... 170
- Safety and CNC Programming ............................................ 173
- Special Tapping Macro .................................................. 176
- Setting Up a New Part .................................................. 178
