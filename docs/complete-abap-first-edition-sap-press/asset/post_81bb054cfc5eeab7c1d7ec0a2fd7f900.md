
![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_0_0.png)
![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_0_1.png)

## Complete ABAP®

- An everyday reference for ABAP programmers of all levels
- Learn language elements, syntax, concepts, and more
- Explore modularization, modifications, and enhancements

Kiran Bandari

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_0_2.png)

SAP PRESS is a joint initiative of SAP and Rheinwerk Publishing. The know-how offered by SAP specialists combined with the expertise of Rheinwerk Publishing offers the reader expert books in the field. SAP PRESS features first-hand information and expert advice, and provides useful skills for professional decision-making.

SAP PRESS offers a variety of books on technical and business-related topics for the SAP user. For further information, please visit our website: http://www.sap-press.com.

- James Wood, Joseph Rupert  
  Object-Oriented Programming with ABAP Objects (2nd edition)  
  2016, 470 pages, hardcover and e-book  
  www.sap-press.com/3597
- Paul Hardy  
  ABAP to the Future (2nd edition)  
  2016, 801 pages, hardcover and e-book  
  www.sap-press.com/4161
- Kerem Koseoglu  
  Design Patterns in ABAP Objects  
  2017, 387 pages, hardcover and e-book  
  www.sap-press.com/4277
- Gahm, Schneider, Swanepoel, Westenberger  
  ABAP Development for SAP HANA (2nd edition)  
  2016, 641 pages, hardcover and e-book  
  www.sap-press.com/3973

Kiran Bandari

## Complete ABAP®

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_2_0.png)

Bonn · Boston

## Dear Reader

Flexing your linguistic muscle can be both a rewarding and nerve-wracking experience. When traveling in Spain, I may have, for example, accidentally asked for no octopus (pulpo) in my orange juice instead of no pulp (pulpa). The truth of the matter is, learning a new language is no easy task—programming not excluded.

Whether you’re an ABAP newbie or need a refresher on key concepts, this book offers a 360-degree view of everything you need to know about ABAP. From introductions to ABAP keywords to techniques and best practices every good ABAP developer should know, this heavyweight guide is your key to mastering the ABAP language. And since the best way to learn a language is via the help of a native speaker, you’ll be in good company with the expertise of author Kiran Bandari.

What did you think about *Complete ABAP*? Your comments and suggestions are the most useful tools to help us make our books the best they can be. Please feel free to contact me and share any praise or criticism you may have.

Thank you for purchasing a book from SAP PRESS!

**Sarah Frazier**  
Editor, SAP PRESS

Rheinwerk Publishing  
Boston, MA

[editorial@rheinwerk-publishing.com](mailto:editorial@rheinwerk-publishing.com)  
[http://www.sap-press.com](http://www.sap-press.com)

## Notes on Usage

This e-book is **protected by copyright**. By purchasing this e-book, you have agreed to accept and adhere to the copyrights. You are entitled to use this e-book for personal purposes. You may print and copy it, too, but also only for personal use. Sharing electronic or printed copy with others, however, is not permitted, neither as a whole nor in parts. Of course, making them available on the Internet or in a company network is illegal as well.

For detailed and legally binding usage conditions, please refer to the section [Legal Notes](#).

This e-book copy contains a **digital watermark**, a signature that indicates which person may use this copy:

## Imprint

This e-book is a publication many contributed to, specifically:

- Editor  Sarah Frazier
- Acquisitions Editor  Kelly Grace Weaver
- Copyeditor  Melinda Rankin
- Cover Design  Graham Geary
- Photo Credit  Shutterstock.com/167078399/© Africa Studio
- Production E-Book  Kelly O'Callaghan
- Typesetting E-Book  SatzPro, Krefeld (Germany)

We hope that you liked this e-book. Please share your feedback with us and read the [Service Pages](#) to find out how to contact us.

### The Library of Congress has cataloged the printed edition as follows:

Names: Bandari, Kiran, author.  
Title: Complete ABAP / Kiran Bandari.  
Description: 1st edition. | Bonn ; Boston : Rheinwerk Publishing, 2016. | Includes index.  
Identifiers: LCCN 2016016863 | ISBN 9781493212729 (print : alk. paper) | ISBN 9781493212743 (print and ebook : alk. paper) | ISBN 9781493212736 (ebook)  
Subjects: LCSH: ABAP/4 (Computer program language) | SAP ERP.  
Classification: LCC QA76.73.A12 B36 2016 | DDC 005.1/17--dc23 LC record available at https://lccn.loc.gov/2016016863

- **ISBN 978-1-4932-1272-9 (print)**
- **ISBN 978-1-4932-1273-6 (e-book)**
- **ISBN 978-1-4932-1274-3 (print and e-book)**

© 2017 by Rheinwerk Publishing, Inc., Boston (MA)  
1st edition 2017

## Contents

- Acknowledgments — 21
- Preface — 23

### 1 Introduction to ERP and SAP — 29

- 1.1 Historical Overview — 29
- 1.2 Understanding an ERP System — 32
  - 1.2.1 What Is ERP? — 32
  - 1.2.2 ERP vs. Non-ERP Systems — 33
  - 1.2.3 Advantages of an ERP System — 35
- 1.3 Introduction to SAP — 36
  - 1.3.1 Modules in SAP — 36
  - 1.3.2 Types of Users — 37
  - 1.3.3 Role of an ABAP Consultant — 38
  - 1.3.4 Changing and Adapting the Data Structure — 40
- 1.4 ABAP Overview — 43
  - 1.4.1 Types of Applications — 43
  - 1.4.2 RICEF Overview — 43
- 1.5 System Requirements — 48
- 1.6 Summary — 48

### 2 Architecture of an SAP System — 49

- 2.1 Introduction to the Three-Tier Architecture — 49
- 2.2 SAP Implementation Overview — 52
  - 2.2.1 SAP GUI: Presentation Layer — 52
  - 2.2.2 Application Servers and Message Servers: Application Layer — 54
  - 2.2.3 Database Server/RDBMS: Database Layer — 61
- 2.3 Data Structures — 64
  - 2.3.1 Client Overview — 64
  - 2.3.2 Client-Specific and Cross-Client Data — 65
  - 2.3.3 Repository — 68
  - 2.3.4 Packages — 68
  - 2.3.5 Transport Organizer — 70
- 2.4 Summary — 75

### 3 Introduction to the ABAP Environment — 77

- 3.1 SAP Environment — 78
  - 3.1.1 ABAP Programming Environment — 78
  - 3.1.2 Logging On to the SAP Environment — 78
  - 3.1.3 Elements of the SAP Screen — 79
  - 3.1.4 Transaction Codes — 82
  - 3.1.5 Navigating and Opening Transactions — 83
- 3.2 ABAP Workbench Overview — 87
  - 3.2.1 ABAP Editor — 88
  - 3.2.2 Function Builder — 90
  - 3.2.3 Class Builder — 91
  - 3.2.4 Screen Painter — 92
  - 3.2.5 Menu Painter — 95
  - 3.2.6 ABAP Data Dictionary — 96
  - 3.2.7 Object Navigator — 98
- 3.3 Eclipse IDE Overview — 99
- 3.4 Summary — 105

### 4 ABAP Programming Concepts — 107

- 4.1 General Program Structure — 108
  - 4.1.1 Global Declarations — 108
  - 4.1.2 Procedural — 109
- 4.2 ABAP Syntax — 110
  - 4.2.1 Basic Syntax Rules — 110
  - 4.2.2 Chained Statements — 111
  - 4.2.3 Comment Lines — 112
- 4.3 ABAP Keywords — 113
- 4.4 Introduction to the TYPE Concept — 114
  - 4.4.1 Data Types — 115
  - 4.4.2 Data Elements — 130
  - 4.4.3 Domains — 134
  - 4.4.4 Data Objects — 137
- 4.5 ABAP Statements — 141
- 4.6 Creating Your First ABAP Program — 143
- 4.7 Summary — 149

### 5 Structures and Internal Tables — 151

- 5.1 Defining Structures — 152
  - 5.1.1 When to Define Structures — 154
  - 5.1.2 Local Structures — 155
  - 5.1.3 Global Structures — 158
  - 5.1.4 Working with Structures — 162
  - 5.1.5 Use Cases — 163
- 5.2 Internal Tables — 164
  - 5.2.1 Defining Internal Tables — 164
  - 5.2.2 Types of Internal Tables — 167
  - 5.2.3 Table Keys — 171
  - 5.2.4 Working with Internal Tables — 175
  - 5.2.5 Control Break Statements — 182
- 5.3 Introduction to Open SQL Statements — 187
  - 5.3.1 Database Overview — 189
  - 5.3.2 Selecting Data from Database Tables — 198
  - 5.3.3 Selecting Data from Multiple Tables — 200
- 5.4 Processing Data from Database via Internal Tables and Structures — 203
- 5.5 Introduction to the Debugger — 205
- 5.6 Practice — 209
- 5.7 Summary — 209

### 6 User Interaction — 211

- 6.1 Selection Screen Overview — 212
  - 6.1.1 PARAMETERS — 214
  - 6.1.2 SELECT-OPTIONS — 221
  - 6.1.3 SELECTION-SCREEN — 229
  - 6.1.4 Selection Texts — 230
- 6.2 Messages — 231
  - 6.2.1 Types of Messages — 231
  - 6.2.2 Messages Using Text Symbols — 233
  - 6.2.3 Messages Using Message Classes — 235
  - 6.2.4 Dynamic Messages — 237
  - 6.2.5 Translation — 238
- 6.3 Summary — 239
