
![](img/34f09be0ed6217c465debc4490197d4f_0_0.png)

# BEGINNING
C++
THROUGH
GAME PROGRAMMING,
THIRD EDITION

MICHAEL DAWSON

# BEGINNING C++
THROUGH GAME
PROGRAMMING,
THIRD EDITION

MICHAEL DAWSON

Course Technology PTR
*A part of Cengage Learning*

![](img/34f09be0ed6217c465debc4490197d4f_1_0.png)

# Beginning C++ Through Game Programming, Third Edition
Michael Dawson

Publisher and General Manager, Course Technology PTR: Stacy L. Hiquet

Associate Director of Marketing: Sarah Panella

Manager of Editorial Services: Heather Talbot

Marketing Manager: Jordan Castellani

Senior Acquisitions Editor: Emi Smith

Project Editor: Jenny Davidson

Technical Reviewer: Maneesh Sethi

Interior Layout Tech: MPS Limited, a Macmillan Company

Cover Designer: Mike Tanamachi

Indexer: Kevin Broccoli

Proofreader: Michael Beady

© 2011 Course Technology, a part of Cengage Learning.

ALL RIGHTS RESERVED. No part of this work covered by the copyright herein may be reproduced, transmitted, stored, or used in any form or by any means graphic, electronic, or mechanical, including but not limited to photocopying, recording, scanning, digitizing, taping, Web distribution, information networks, or information storage and retrieval systems, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act, without the prior written permission of the publisher.

For product information and technology assistance, contact us at Cengage Learning Customer & Sales Support, 1-800-354-9706

For permission to use material from this text or product, submit all requests online at www.cengage.com/permissions
Further permissions questions can be emailed to permissionrequest@cengage.com

All trademarks are the property of their respective owners.
All images © Cengage Learning unless otherwise noted.

Library of Congress Control Number: 2010928011

ISBN-13: 978-1-4354-5742-3

ISBN-10: 1-4354-5742-0

eISBN-10:1-4354-5743-9

Course Technology, a part of Cengage Learning
20 Channel Center Street
Boston, MA 02210
USA

Cengage Learning is a leading provider of customized learning solutions with office locations around the globe, including Singapore, the United Kingdom, Australia, Mexico, Brazil, and Japan. Locate your local office at: international.cengage.com/region

Cengage Learning products are represented in Canada by Nelson Education, Ltd.

For your lifelong learning solutions, visit courseptr.com

Visit our corporate website at cengage.com

# ACKNOWLEDGMENTS

![](img/34f09be0ed6217c465debc4490197d4f_4_0.png)

Every book you’ve ever read perpetuates a big fat lie. And I’m here to out the publishing industry’s dirty little secret—books are not “by” only one person. Yes, you see only one name on book covers (including this one), but it takes a team of dedicated people to pull off the final product. Authors could not do it alone; I certainly could not have done it alone. So I want to thank all those who helped make this book a reality.

Thanks to Jenny Davidson for her dual role as Project Editor and Copy Editor. Jenny kept me on schedule and my commas in place.

Thanks to Maneesh Sethi, my Technical Reviewer, who made sure my programs worked the way I said they did.

Thanks to Michael Beady, my Proofreader. His work makes this book look good—literally.

I also want to thank Emi Smith, my Senior Acquisitions Editor, for all of her encouragement.

Finally, I want to thank all of the game programmers who created the games I played while growing up. They inspired me to work in the industry and create games of my own. I hope I can inspire a few readers to do the same.

# ABOUT THE AUTHOR

![](img/34f09be0ed6217c465debc4490197d4f_5_0.png)

**Michael Dawson** is a game programming author and instructor who teaches students the art and science of writing their own games. Mike has developed and taught game programming courses for UCLA Extension, The Digital Media Academy, and The Los Angeles Film School. In addition, his books have been required reading in colleges and universities around the country.

Mike got his start in the game industry as a producer and designer, but he also “starred” in an adventure game in which the player controls the main character, named Mike Dawson. In the game, the player directs the digitized images of Dawson, who must stop an extraterrestrial invasion before an implanted alien embryo is born from his head.

In real life, Mike is the author of *Beginning C++ Through Game Programming*, *Python Programming for the Absolute Beginner*, *C++ Projects: Programming with Text-Based Games*, and *Guide to Programming with Python*. He earned his bachelor’s degree in Computer Science from the University of Southern California. Visit his website at www.programgames.com to learn more or to get support for any of his books.

# CONTENTS

Introduction ........................................ xviii

# Chapter 1    Types, Variables, and Standard I/O: Lost Fortune ........ 1

- Introducing C++ ........................................ 1
- Using C++ for Games .................................. 2
- Creating an Executable File ........................... 2
- Dealing with Errors ................................... 4
- Understanding the ISO Standard ........................ 5
- Writing Your First C++ Program .......................... 5
- Introducing the Game Over Program ..................... 5
- Commenting Code ....................................... 7
- Using Whitespace ...................................... 7
- Including Other Files .................................. 7
- Defining the main() Function ........................... 8
- Displaying Text through the Standard Output ............ 8
- Terminating Statements ................................. 9
- Returning a Value from main() ......................... 10
- Working with the std Namespace .......................... 10
- Introducing the Game Over 2.0 Program .................. 10
- Employing a using Directive ........................... 11
- Introducing the Game Over 3.0 Program .................. 11
- Employing using Declarations .......................... 12
- Understanding When to Employ using .................... 12

![](img/34f09be0ed6217c465debc4490197d4f_6_0.png)

- Using Arithmetic Operators ................................... 13
- Introducing the Expensive Calculator Program .................. 13
- Adding, Subtracting, and Multiplying ........................... 14
- Understanding Integer and Floating Point Division ............. 14
- Using the Modulus Operator .................................... 15
- Understanding Order of Operations .............................. 15
- Declaring and Initializing Variables ............................. 16
- Introducing the Game Stats Program ............................. 16
- Understanding Fundamental Types ............................... 18
- Understanding Type Modifiers .................................. 18
- Declaring Variables ........................................... 19
- Naming Variables .............................................. 20
- Assigning Values to Variables ................................. 21
- Initializing Variables ........................................ 22
- Displaying Variable Values .................................... 22
- Getting User Input ............................................ 23
- Defining New Names for Types .................................. 23
- Understanding Which Types to Use ............................... 24
- Performing Arithmetic Operations with Variables ................. 24
- Introducing the Game Stats 2.0 Program ......................... 24
- Altering the Value of a Variable ............................... 26
- Using Combined Assignment Operators ............................ 26
- Using Increment and Decrement Operators ........................ 27
- Dealing with Integer Wrap Around ............................... 28
- Working with Constants .......................................... 29
- Introducing the Game Stats 3.0 Program ......................... 29
- Using Constants ................................................ 31
- Using Enumerations ............................................. 31
- Introducing Lost Fortune ........................................ 32
- Setting Up the Program ......................................... 32
- Getting Information from the Player ............................ 33
- Telling the Story .............................................. 34
- Summary .......................................................... 35
- Questions and Answers ........................................... 36
- Discussion Questions ............................................ 38
- Exercises ........................................................ 38
- Chapter 2  Truth, Branching, and the Game Loop:
- Guess My Number ................................................. 39
- Understanding Truth ............................................. 39
