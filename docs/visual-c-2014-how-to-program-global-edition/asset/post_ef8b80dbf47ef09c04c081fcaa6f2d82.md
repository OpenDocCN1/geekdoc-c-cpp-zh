
# GLOBAL EDITION

# Visual C#

# How to Program

SIXTH EDITION

Paul Deitel • Harvey Deitel

![](img/57baed2319be0bb1b5f98674846f2711_0_0.png)

![](img/57baed2319be0bb1b5f98674846f2711_0_1.png)

# Visual C#

# HOW TO PROGRAM

![](img/57baed2319be0bb1b5f98674846f2711_1_0.png)

This page intentionally left blank

# Visual C#

# HOW TO PROGRAM

SIXTH EDITION

GLOBAL EDITION

# Paul Deitel
Harvey Deitel

Deitel & Associates, Inc.

![](img/57baed2319be0bb1b5f98674846f2711_3_0.png)

Boston Columbus Hoboken Indianapolis New York San Francisco
Amsterdam Cape Town Dubai London Madrid Milan Munich Paris Montreal
Toronto Delhi Mexico City Sao Paulo Sydney Hong Kong Seoul Singapore Taipei Tokyo

Vice President, Editorial Director: Marcia Horton
Acquisitions Editor: Tracy Johnson
Editorial Assistant: Krizty Alura
Acquisitions Editor, Global Editions: Sourabh Maheshwari
VP of Marketing: Christy Lesko
Field Marketing Manager: Demeterius Hall
Marketing Assistant: Joe Bryan
Director of Product Management: Erik Gregg
Team Lead, Program and Project Management: Scott Diansco
Program Manager: Carolle Snyder
Project Manager: Robert Engelhardt
Project Editor, Global Editions: K.K. Neelakantan
Manufacturing Boys: Higher Ed | RR Donnelly: Maura Calidars-Garcia
Senior Manufacturing Controller, Global Editions: Trudy Kimber
Media Production, Global Editions: Vikram Kumar
Cover Design: Lumina Datamatics
R&P Manager: Ben Ferrini
Inventory Manager: Ann Lam

Credits and acknowledgments borrowed from other sources and reproduced, in this textbook appear on page 6.
The authors and publisher of this book have used their best efforts in preparing this book. These efforts include the development, research and testing of the theories and programs to determine their effectiveness. The authors and publisher make no warranty of any kind, expressed or implied, with regard to these programs or the documentation contained in this book. The authors and publisher shall not be liable for any incidental or consequential damages in connection with, or out of, the furnishing, performance, or use of these programs.

Pearson Education Limited
Edinburgh Gate
Harlow
nex CM20 2JE

England and Associated Companies throughout the World Wide Web at:
www.pearonglobaleditions.com
© Pearson Education Limited 2018

The rights of Paul Deital and Harvey Deital to be identified as the authors of this work have been asserted by them in accordance with the Copyright, Designs and Patents Act 1988.
Adapted from the United States edition, visual C# How to Program, 6th Edition, ISBN-978-360154-0 by Paul Deital and Harvey Deital published by Pearson Education © 2017.

All rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any electronic, mechanical, photocopying, recording or otherwise, without either the prior written permission of the publisher or a license permitting restricted copying in the United Kingdom by the Copyright Licensing Agency Ltd, Sutton House, 60 Girby Street, London EC1 8HT.
Trademarks used herein are the property of their respective owners. The use of any trademark in this text does not grant the author or publisher any trademark ownership rights in such trademarks, nor does the use of such trademarks imply any affiliation or endorsement of this book by such owners.

British Library Cataloguing-in-Publication A catalogue for this book is available from the British Library
1 9 8 7 6 5 4 3 2 1
ISBN-10: 1-292-15346-6
ISBN-13: 978-1-292-15346-9
Typeset by GEX Publishing Services
Printed and bound in Malaysia

In memory of William Siebert, Professor Emeritus of Electrical Engineering and Computer Science at MIT:

Your use of visualization techniques in your Signals and Systems lectures inspired the way generations of engineers, computer scientists, educators and authors present their work.

Harvey and Paul Deitel

# Trademarks

DEITEL® and the double-thumbs-up bug are registered trademarks of Deitel and Associates, Inc.
Microsoft® Windows®, and Microsoft Visual C#® are registered trademarks of the Microsoft Corporation in the U.S.A. And Other other countries. This book is not sponsored or endorsed by or affiliated with the Microsoft Corporation.

UNIX is a registered trademark of The Open Group.

> Throughout this book, trademarks are used. Rather than put a trademark symbol in every occurrence of a trademarked name, we state that we are using the names in an editorial fashion only and to the benefit of the trademark owner, with no intention of infringement of the trademark.

# Contents

# Preface 23

# Before You Begin 37

# I Introduction to Computers, the Internet and Visual C# 41

- 1.1 Introduction 42
- 1.2 Computers and the Internet in Industry and Research 42
- 1.3 Hardware and Software 45
- 1.3.1 Moore's Law 45
- 1.3.2 Computer Organization 46
- 1.4 Data Hierarchy 47
- 1.5 Machine Languages, Assembly Languages and High-Level Languages 50
- 1.6 Object Technology 51
- 1.7 Internet and World Web 53
- 1.8 C# 55
- 1.8.1 Object-Oriented Programming 56
- 1.8.2 Event-Driven Programming 56
- 1.8.3 Visual Programming 56
- 1.8.4 Generic and Functional Programming 56
- 1.8.5 An International Standard 57
- 1.8.6 C# on Non-Windows Platforms 57
- 1.8.7 Internet and Web Programming 57
- 1.8.8 Asynchronous Programming with async and await 57
- 1.8.9 Other Key Programming Languages 58
- 1.9 .NET 60
- 1.9.1 .NET Framework 60
- 1.9.2 Common Language Runtime 60
- 1.9.3 Platform Independence 61
- 1.9.4 Language Interoperability 61
- 1.10 Microsoft's Windows® Operating System 61
- 1.11 Integrated Development Environment 61
- 1.12 Visual Programming 63

![](img/57baed2319be0bb1b5f98674846f2711_7_0.png)

# Visual Programming

- 2.1 Introduction 63
- 2.2 Overview of Visual Studio 63
- 2.2.1 Integrated Development Environment 63
- 2.2.2 Features 63
- 2.3 Help 63
- 2.4 Solution Explorer 63
- 2.4.1 Toolbar 63
- 2.4.2 Properties 63
- 2.5 Controls 63
- 2.6 Window 63
- 2.7 Wrap-Up 63

- 3.1 Introduction 123
- 3.7 Memory Concepts 25
- 3.8 Arithmetic 26
- 3.8.1 Arithmetic in Straight-Line Form 27
- 3.8.2 Parentheses for Grouping Subexpressions 27
- 3.8.3 Rules of Operator Precedence 27
- 3.8.4 Sample Algebraic and C# Expressions 28
- 3.8.5 Redundant Parentheses 29
- 3.9 Decision Making: Equality and Relational Operators 29
- 3.10 Wrap-Up 34

# 4 Introduction to Classes, Objects and strings 146

- 4.1 Introduction 147
- 4.2 Test-Driving an Account Class 148
- 4.2.1 Instantiating an Object—Keyword new 148
- 4.2.2 Calling Class Account's GetName Method 149
- 4.2.3 Inputting a Name from the User 149
- 4.2.4 Calling Class Account's SetName Method 150
- 4.3 Account with an Instance Variable and Get Methods 150
- 4.3.1 Account Class Declaration 150
- 4.3.2 Keyword class and the Class Body 151
- 4.3.3 Instance Variable name of Type string 151
- 4.3.4 SetName Method 152
- 4.3.5 GetName Method 154
- 4.3.6 Access Modifiers private and public 154
- 4.3.7 Account UML Class Diagram 155
- 4.4 Creating, Compiling, and Running a Visual C Project with Two Classes 156
- 4.5 Software Engineering with Set and Get Methods 157
- 4.6 Account with Proper Set and Get Methods 158
- 4.6.1 Class Account Using Account's Name Property 158
- 4.6.2 Account Class with an Instance Variable and a Property 160
- 4.6.3 Account UML Class Diagram with a Property 162
- 4.7 Auto-Implemented Properties 162
- 4.8 Account Class: Initializing Objects with Constructors 163
- 4.8.1 Declaring an Account Constructor for Custom Object Initialization 163
- 4.8.2 Class AccountTest: Initializing Account Objects When They Created 164
