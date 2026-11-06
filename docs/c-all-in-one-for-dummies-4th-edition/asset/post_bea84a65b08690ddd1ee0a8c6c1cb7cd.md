
LEARNING MADE EASY

![](img/128ab511de4e7360e167e3b15cdd5dd0_0_0.png)

4th Edition

## C++ ALL-IN-ONE

for dummies®

A Wiley Brand

![](img/128ab511de4e7360e167e3b15cdd5dd0_0_1.png)

**7 Books in one!**

John Paul Mueller, Author of *Functional Programming For Dummies*

![](img/128ab511de4e7360e167e3b15cdd5dd0_2_0.png)

## C++ ALL-IN-ONE

4th Edition

by John Paul Mueller

![](img/128ab511de4e7360e167e3b15cdd5dd0_2_1.png)

## C++ All-in-One For Dummies®, 4th Edition

Published by: John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030-5774, www.wiley.com

Copyright © 2021 by John Wiley & Sons, Inc., Hoboken, New Jersey

Published simultaneously in Canada

No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning or otherwise, except as permitted under Sections 107 or 108 of the 1976 United States Copyright Act, without the prior written permission of the Publisher. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748-6011, fax (201) 748-6008, or online at http://www.wiley.com/go/permissions.

Trademarks: Wiley, For Dummies, the Dummies Man logo, Dummies.com, Making Everything Easier, and related trade dress are trademarks or registered trademarks of John Wiley & Sons, Inc. and may not be used without written permission. All other trademarks are the property of their respective owners. John Wiley & Sons, Inc. is not associated with any product or vendor mentioned in this book.

LIMIT OF LIABILITY/DISCLAIMER OF WARRANTY: THE PUBLISHER AND THE AUTHOR MAKE NO REPRESENTATIONS OR WARRANTIES WITH RESPECT TO THE ACCURACY OR COMPLETENESS OF THE CONTENTS OF THIS WORK AND SPECIFICALLY DISCLAIM ALL WARRANTIES, INCLUDING WITHOUT LIMITATION WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE. NO WARRANTY MAY BE CREATED OR EXTENDED BY SALES OR PROMOTIONAL MATERIALS. THE ADVICE AND STRATEGIES CONTAINED HEREIN MAY NOT BE SUITABLE FOR EVERY SITUATION. THIS WORK IS SOLD WITH THE UNDERSTANDING THAT THE PUBLISHER IS NOT ENGAGED IN RENDERING LEGAL, ACCOUNTING, OR OTHER PROFESSIONAL SERVICES. IF PROFESSIONAL ASSISTANCE IS REQUIRED, THE SERVICES OF A COMPETENT PROFESSIONAL PERSON SHOULD BE SOUGHT. NEITHER THE PUBLISHER NOR THE AUTHOR SHALL BE LIABLE FOR DAMAGES ARISING HEREFROM. THE FACT THAT AN ORGANIZATION OR WEBSITE IS REFERRED TO IN THIS WORK AS A CITATION AND/OR A POTENTIAL SOURCE OF FURTHER INFORMATION DOES NOT MEAN THAT THE AUTHOR OR THE PUBLISHER ENDORSES THE INFORMATION THE ORGANIZATION OR WEBSITE MAY PROVIDE OR RECOMMENDATIONS IT MAY MAKE. FURTHER, READERS SHOULD BE AWARE THAT INTERNET WEBSITES LISTED IN THIS WORK MAY HAVE CHANGED OR DISAPPEARED BETWEEN WHEN THIS WORK WAS WRITTEN AND WHEN IT IS READ.

For general information on our other products and services, please contact our Customer Care Department within the U.S. at 877-762-2974, outside the U.S. at 317-572-3993, or fax 317-572-4002. For technical support, please visit https://hub.wiley.com/community/support/dummies.

Wiley publishes in a variety of print and electronic formats and by print-on-demand. Some material included with standard print versions of this book may not be included in e-books or in print-on-demand. If this book refers to media such as a CD or DVD that is not included in the version you purchased, you may download this material at http://booksupport.wiley.com. For more information about Wiley products, visit www.wiley.com.

Library of Congress Control Number: 2020949804

ISBN: 978-1-119-60174-6

ISBN 978-1-119-60175-3 (ebk); ISBN 978-1-119-60173-9 (ebk)

Manufactured in the United States of America

10 9 8 7 6 5 4 3 2 1

## Contents at a Glance

- Introduction — 1
- **Book 1: Getting Started with C++** — 7
  - CHAPTER 1: Configuring Your Desktop System — 9
  - CHAPTER 2: Configuring Your Mobile System — 27
  - CHAPTER 3: Creating Your First C++ Application — 45
  - CHAPTER 4: Storing Data in C++ — 69
  - CHAPTER 5: Directing the Application Flow — 105
  - CHAPTER 6: Dividing Your Work with Functions — 139
  - CHAPTER 7: Splitting Up Source Code Files — 169
  - CHAPTER 8: Referring to Your Data Through Pointers — 187
- **Book 2: Understanding Objects and Classes** — 225
  - CHAPTER 1: Working with Classes — 227
  - CHAPTER 2: Using Advanced C++ Features — 269
  - CHAPTER 3: Planning and Building Objects — 309
  - CHAPTER 4: Building with Design Patterns — 335
- **Book 3: Understanding Functional Programming** — 367
  - CHAPTER 1: Considering Functional Programming — 369
  - CHAPTER 2: Working with Lambda Expressions — 397
  - CHAPTER 3: Advanced Lambda Expressions — 415
- **Book 4: Fixing Problems** — 427
  - CHAPTER 1: Dealing with Bugs — 429
  - CHAPTER 2: Debugging an Application — 443
  - CHAPTER 3: Stopping and Inspecting Your Code — 457
  - CHAPTER 4: Traveling About the Stack — 469
- **Book 5: Advanced Programming** — 479
  - CHAPTER 1: Working with Arrays, Pointers, and References — 481
  - CHAPTER 2: Creating Data Structures — 515
  - CHAPTER 3: Constructors, Destructors, and Exceptions — 541
  - CHAPTER 4: Advanced Class Usage — 571
  - CHAPTER 5: Creating Classes with Templates — 601
  - CHAPTER 6: Programming with the Standard Library — 637
- **Book 6: Reading and Writing Files** — 681
  - CHAPTER 1: Filing Information with the Streams Library — 683
  - CHAPTER 2: Writing with Output Streams — 697
  - CHAPTER 3: Reading with Input Streams — 711
  - CHAPTER 4: Building Directories and Contents — 727
  - CHAPTER 5: Streaming Your Own Classes — 737
- **Book 7: Advanced Standard Library Usage** — 751
  - CHAPTER 1: Exploring the Standard Library Further — 753
  - CHAPTER 2: Working with User-Defined Literals (UDLs) — 779
  - CHAPTER 3: Building Original Templates — 795
  - CHAPTER 4: Investigating Boost — 817
  - CHAPTER 5: Boosting up a Step — 849
- **Index** — 869

- Obtaining CppDroid Help — 40
  - Working with the Help documentation — 40
  - Getting community support — 41
  - Using the free examples — 42
  - Accessing the tutorials — 43

### CHAPTER 3: Creating Your First C++ Application — 45

- Code::Blocks Creating a Project — 46
  - Understanding projects — 46
  - Defining your first project — 47
  - Building and executing your first application — 52
- Typing the Code — 53
- Starting with Main — 55
- Showing Information — 55
  - Doing some math — 60
  - Tabbing your output — 66
- Let Your Application Run Away — 67

### CHAPTER 4: Storing Data in C++ — 69

- Putting Your Data Places: Variables — 70
  - Creating an integer variable — 70
  - Declaring multiple variables — 73
  - Changing values — 74
  - Setting one variable equal to another — 74
  - Initializing a variable — 75
  - Creating a great name for yourself — 76
- Manipulating Integer Variables — 78
  - Adding integer variables — 78
  - Subtracting integer variables — 82
  - Multiplying integer variables — 84
  - Dividing integer variables — 86
- Characters — 88
  - Null character — 89
  - Nonprintable and other cool characters — 89
- Strings — 93
  - Getting a part of a string — 94
  - Changing part of a string — 95
  - Adding onto a string — 96
  - Adding two strings — 97
- Making Decisions Using Conditional Operators — 98
- Telling the Truth with Boolean Variables — 100
- Reading from the Console — 102
