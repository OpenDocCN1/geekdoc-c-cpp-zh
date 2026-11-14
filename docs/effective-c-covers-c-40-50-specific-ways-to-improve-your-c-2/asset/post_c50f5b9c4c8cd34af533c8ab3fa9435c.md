
## Effective SOFTWARE DEVELOPMENT SERIES
Scott Meyers, Consulting Editor

## Effective C#
### 50 Specific Ways to Improve Your C#
SECOND EDITION

![](img/28c59cb6ec56b677835aaafe709bff66_0_0.png)

Bill Wagner

## Praise for Effective C#, Second Edition

> "Being an effective .NET developer requires one to have a deep understanding of the language of their choice. Wagner's book provides the reader with that knowledge via well-reasoned arguments and insight. Whether you're new to C# or you've been using it for years, you'll learn something new when you read this book."
>
> —Jason Bock, Principal Consultant, Magenic

> "If you're at all like me, you have collected a handful of C# language pearls that have immediately transformed your abilities as a professional developer. What you hold in your hands is quite possibly the best collection of these tips that have ever been assembled. Bill has managed to exceed my wildest expectations with the latest edition in his exemplary _Effective C#_."
>
> —Bill Craun, Principal Consultant, Ambassador Solutions

> "_Effective C#, Second Edition_, is a must-read for anyone building high performance and/or highly scalable applications. Bill has that rare and awesome ability to take an amazing complex problem and break it down into human, digestible, and understandable chunks."
>
> —Josh Holmes, Architect Evangelist, Microsoft

> "Bill has done it again. This book is a concise collection of invaluable tips for any C# developer. Learn one tip every day, and you'll become a much better C# developer after fifty days!"
>
> —Claudio Lassala, Lead Developer, EPS Software/CODE Magazine

> "A fountain of knowledge and understanding of the C# language. Bill gives insight to what happens under the covers of the .NET runtime based on what you write in your code and teaches pragmatic practices that lead to cleaner, easier to write, and more understandable code. A great mix of tips, tricks, and deep understanding—including things true since C# 1.0 up through new capabilities in C# 4.0—that every C# developer should read."
>
> —Brian Noyes, Chief Architect, IDesign Inc. (www.idesign.net)

> "_Effective C#_ is a must for every C# developer. Period. Its pragmatic advice on code design is invaluable."
>
> —Shawn Wildermuth, Microsoft MVP (C#), Author, Trainer, and Speaker

> "In this book Wagner provides practical explanations of how to use the most important features in the C# language. His deep knowledge and sophisticated communication skills illuminate the new features in C# so that you can use them to write programs that are more concise and easier to maintain."
>
> —Charlie Calvert, Microsoft C# Community Program Manager

## Effective C#
### Second Edition

![](img/28c59cb6ec56b677835aaafe709bff66_4_0.png)

Visit informit.com/esds for a complete list of available publications.

**The Effective Software Development Series** provides expert advice on all aspects of modern software development. Books in the series are well written, technically sound, and of lasting value. Each describes the critical things experts always do—or always avoid—to produce outstanding software.

Scott Meyers, author of the best-selling books *Effective C++* (now in its third edition), *More Effective C++*, and *Effective STL* (all available in both print and electronic versions), conceived of the series and acts as its consulting editor. Authors in the series work with Meyers to create essential reading in a format that is familiar and accessible for software developers of every stripe.

## Effective C#
### 50 Specific Ways to Improve Your C#
### Second Edition

Bill Wagner

Addison-Wesley
Upper Saddle River, NJ • Boston • Indianapolis • San Francisco
New York • Toronto • Montreal • London • Munich • Paris • Madrid
Capetown • Sydney • Tokyo • Singapore • Mexico City

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

The author and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

The publisher offers excellent discounts on this book when ordered in quantity for bulk purchases or special sales, which may include electronic versions and/or custom covers and content particular to your business, training goals, marketing focus, and branding interests. For more information, please contact:

## U.S. Corporate and Government Sales

(800) 382-3419
corpsales@pearsontechgroup.com

For sales outside the United States please contact:

International Sales
international@pearson.com

Visit us on the Web: informit.com/aw

## Library of Congress Cataloging-in-Publication Data

Wagner, Bill.
Effective C# : 50 specific ways to improve your C# / Bill Wagner.--2nd ed.
p. cm.
Includes index.
ISBN: 978-0-321-65870-8 (pbk. : alk. paper)
1. C# (Computer program language) 2. Database management. 3. Microsoft .NET Framework.
I. Title.
QA76.73.C154W343 2010
005.13'3--dc22

## Copyright © 2010 Pearson Education, Inc.

All rights reserved. Printed in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. For information regarding permissions, write to:

Pearson Education, Inc.
Rights and Contracts Department
501 Boylston Street, Suite 900
Boston, MA 02116
Fax: (617) 671-3447

ISBN-13: 978-0-321-65870-8
ISBN-10: 0-321-65870-1

Text printed in the United States on recycled paper at Courier in Stoughton, Massachusetts.

First printing, March 2010

To my parents, Bill and Alice Wagner.
They continue to demonstrate great strength and inspiration.

## Contents at a Glance

- Introduction xiii
- Chapter 1 C# Language Idioms 1
- Chapter 2 .NET Resource Management 69
- Chapter 3 Expressing Designs in C# 125
- Chapter 4 Working with the Framework 179
- Chapter 5 Dynamic Programming in C# 227
- Chapter 6 Miscellaneous 275
- Index 309

## Contents

- Introduction xiii
- Chapter 1 C# Language Idioms 1
  - Item 1: Use Properties Instead of Accessible Data Members 1
  - Item 2: Prefer readonly to const 8
  - Item 3: Prefer the is or as Operators to Casts 12
  - Item 4: Use Conditional Attributes Instead of #if 20
  - Item 5: Always Provide ToString() 28
  - Item 6: Understand the Relationships Among the Many Different Concepts of Equality 36
  - Item 7: Understanding the Pitfalls of GetHashCode() 44
  - Item 8: Prefer Query Syntax to Loops 51
  - Item 9: Avoid Conversion Operators in Your APIs 56
  - Item 10: Use Optional Parameters to Minimize Method Overloads 60
  - Item 11: Understand the Attraction of Small Functions 64
- Chapter 2 .NET Resource Management 69
  - Item 12: Prefer Member Initializers to Assignment Statements 74
  - Item 13: Use Proper Initialization for Static Class Members 77
  - Item 14: Minimize Duplicate Initialization Logic 79
  - Item 15: Utilize using and try/finally for Resource Cleanup 87
  - Item 16: Avoid Creating Unnecessary Objects 94
  - Item 17: Implement the Standard Dispose Pattern 98
  - Item 18: Distinguish Between Value Types and Reference Types 104
  - Item 19: Ensure That 0 Is a Valid State for Value Types 110
  - Item 20: Prefer Immutable Atomic Value Types 114
- Chapter 3 Expressing Designs in C# 125
  - Item 21: Limit Visibility of Your Types 126
  - Item 22: Prefer Defining and Implementing Interfaces to Inheritance 129
  - Item 23: Understand How Interface Methods Differ from Virtual Methods 139
  - Item 24: Express Callbacks with Delegates 143
  - Item 25: Implement the Event Pattern for Notifications 146
  - Item 26: Avoid Returning References to Internal Class Objects 154
