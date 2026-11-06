
## Get More and Do More at Dummies.com®

![](img/6ba99460b0feb3585671a4612ff5fabb_1_0.png)

### Start with **FREE** Cheat Sheets

Cheat Sheets include

- Checklists
- Charts
- Common Instructions
- And Other Good Stuff!

**To access the Cheat Sheet created specifically for this book, go to www.dummies.com/cheatsheet/cplusplusaio**

### Get Smart at Dummies.com

Dummies.com makes your life easier with 1,000s of answers on everything from removing wallpaper to using the latest version of Windows.

Check out our

- Videos
- Illustrated Articles
- Step-by-Step Instructions

Plus, each month you can win valuable prizes by entering our Dummies.com sweepstakes. *

Want a weekly dose of Dummies? Sign up for Newsletters on

- Digital Photography
- Microsoft Windows & Office
- Personal Finance & Investing
- Health & Wellness
- Computing, iPods & Cell Phones
- eBay
- Internet
- Food, Home & Garden

### Find out “HOW” at Dummies.com

*Sweepstakes not currently available in all countries; visit Dummies.com for official rules.

![](img/6ba99460b0feb3585671a4612ff5fabb_1_1.png)

## C++ All-in-One For Dummies

A Wiley Brand

3rd Edition

by John Paul Mueller and Jeff Cogswell

## C++ All-in-One For Dummies®, 3rd Edition

Published by: John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030-5774, www.wiley.com

Copyright © 2014 by John Wiley & Sons, Inc., Hoboken, New Jersey

Published simultaneously in Canada

No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning or otherwise, except as permitted under Sections 107 or 108 of the 1976 United States Copyright Act, without the prior written permission of the publisher. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748-6011, fax (201) 748-6008, or online at http://www.wiley.com/go/permissions.

**Trademarks:** Wiley, For Dummies, the Dummies Man logo, Dummies.com, Making Everything Easier, and related trade dress are trademarks or registered trademarks of John Wiley & Sons, Inc. and may not be used without written permission. All other trademarks are the property of their respective owners. John Wiley & Sons, Inc. is not associated with any product or vendor mentioned in this book.

> **LIMIT OF LIABILITY/DISCLAIMER OF WARRANTY: THE PUBLISHER AND THE AUTHOR MAKE NO REPRESENTATIONS OR WARRANTIES WITH RESPECT TO THE ACCURACY OR COMPLETENESS OF THE CONTENTS OF THIS WORK AND SPECIFICALLY DISCLAIM ALL WARRANTIES, INCLUDING WITHOUT LIMITATION WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE. NO WARRANTY MAY BE CREATED OR EXTENDED BY SALES OR PROMOTIONAL MATERIALS. THE ADVICE AND STRATEGIES CONTAINED HEREIN MAY NOT BE SUITABLE FOR EVERY SITUATION. THIS WORK IS SOLD WITH THE UNDERSTANDING THAT THE PUBLISHER IS NOT ENGAGED IN RENDERING LEGAL, ACCOUNTING, OR OTHER PROFESSIONAL SERVICES. IF PROFESSIONAL ASSISTANCE IS REQUIRED, THE SERVICES OF A COMPETENT PROFESSIONAL PERSON SHOULD BE SOUGHT. NEITHER THE PUBLISHER NOR THE AUTHORS SHALL BE LIABLE FOR DAMAGES ARISING HEREFROM. THE FACT THAT AN ORGANIZATION OR WEBSITE IS REFERRED TO IN THIS WORK AS A CITATION AND/OR A POTENTIAL SOURCE OF FURTHER INFORMATION DOES NOT MEAN THAT THE AUTHOR OR THE PUBLISHER ENDORSES THE INFORMATION THE ORGANIZATION OR WEBSITE MAY PROVIDE OR RECOMMENDATIONS IT MAY MAKE. FURTHER, READERS SHOULD BE AWARE THAT INTERNET WEBSITES LISTED IN THIS WORK MAY HAVE CHANGED OR DISAPPEARED BETWEEN WHEN THIS WORK WAS WRITTEN AND WHEN IT IS READ.**

For general information on our other products and services, please contact our Customer Care Department within the U.S. at 877-762-2974, outside the U.S. at 317-572-3993, or fax 317-572-4002. For technical support, please visit www.wiley.com/techsupport.

Wiley publishes a variety of print and electronic formats and by print-on-demand. Some material included with standard print versions of this book may not be included in e-books or in print-on-demand. If this book refers to media such as a CD or DVD that is not included in the version you purchased, you may download this material at http://booksupport.wiley.com. For more information about Wiley products, visit www.wiley.com.

Library of Congress Control Number: 2014935515

ISBN: 978-1-118-82378-1 (pbk); ISBN 978-1-118-82379-8 (ebk); ISBN: 978-1-118-82385-9 (ebk)

Manufactured in the United States of America

10  9  8  7  6  5  4  3  2  1

## Contents at a Glance

- ***Introduction*** .......... 1
- ***Book I: Getting Started with C++*** .......... 7
  - Chapter 1: Configuring Your System .......... 9
  - Chapter 2: Creating Your First C++ Application .......... 27
  - Chapter 3: Storing Data in C++ .......... 47
  - Chapter 4: Directing the Application Flow .......... 77
  - Chapter 5: Dividing Your Work with Functions .......... 101
  - Chapter 6: Splitting Up Source Code Files .......... 129
  - Chapter 7: Referring to Your Data Through Pointers .......... 145
  - Chapter 8: Working with Classes .......... 175
  - Chapter 9: Using Advanced C++ Features .......... 211
- ***Book II: Understanding Objects and Classes*** .......... 247
  - Chapter 1: Planning and Building Objects .......... 249
  - Chapter 2: Describing Your Program with UML .......... 279
  - Chapter 3: Structuring Your Classes with UML .......... 299
  - Chapter 4: Demonstrating Behavior with UML .......... 313
  - Chapter 5: Modeling Your Applications with UML .......... 331
  - Chapter 6: Building with Design Patterns .......... 343
- ***Book III: Fixing Problems*** .......... 373
  - Chapter 1: Dealing with Bugs .......... 375
  - Chapter 2: Debugging an Application .......... 387
  - Chapter 3: Stopping and Inspecting Your Code .......... 399
  - Chapter 4: Traveling About the Stack .......... 411
- ***Book IV: Advanced Programming*** .......... 421
  - Chapter 1: Working with Arrays, Pointers, and References .......... 423
  - Chapter 2: Creating Data Structures .......... 455
  - Chapter 3: Constructors, Destructors, and Exceptions .......... 477
  - Chapter 4: Advanced Class Usage .......... 505
  - Chapter 5: Creating Classes with Templates .......... 529
  - Chapter 6: Programming with the Standard Library .......... 561
  - Chapter 7: Working with Lambda Expressions .......... 599

## Table of Contents

- Introduction — 1
  - No Experience Necessary — 1
  - Great for Advanced Folks, Too! — 2
  - For All Computers — 2
  - Conventions — 3
  - Organization — 3
  - Icons Galore — 4
  - What's Next? — 5
  - Beyond the Book — 5
- Book 1: Getting Started with C++ — 7
  - Chapter 1: Configuring Your System — 9
    - Obtaining a Copy of C++ 14 — 10
    - Obtaining Code::Blocks — 10
    - Installing Code::Blocks — 11
      - Working with Windows — 11
      - Working with Mac OS/X — 13
      - Using the standard Linux installation — 14
      - Using the graphical Linux installation — 14
    - Touring the Essential Code::Blocks Features — 17
      - Starting Code::Blocks for the first time — 17
      - Opening the sample projects — 19
      - Viewing the essential windows — 20
    - Using Other IDEs — 25
  - Chapter 2: Creating Your First C++ Application — 27
    - Code::Blocks Creating a Project — 27
      - Understanding projects — 28
      - Defining your first project — 28
      - Building and executing your first application — 33
    - Typing the Code — 34
    - Starting with Main — 36
    - Showing Information — 36
      - Doing some math — 40
      - Tabbing your output — 44
    - Let Your Application Run Away — 46
