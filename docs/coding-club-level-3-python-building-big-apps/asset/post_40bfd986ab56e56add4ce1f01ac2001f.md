
## Coding Club

## Python: Building BIG Apps

Level 3

Chris Roffey

![](img/c4403822ba1e00f0a2ce532b3f9d5054_0_0.png)

## Python: Building BIG Apps

![](img/c4403822ba1e00f0a2ce532b3f9d5054_2_0.png)

Level 3

Chris Roffey

CAMBRIDGE UNIVERSITY PRESS
Cambridge, New York, Melbourne, Madrid, Cape Town, Singapore, São Paulo, Delhi, Mexico City

Cambridge University Press
The Edinburgh Building, Cambridge CB2 8RU, UK

www.cambridge.org
Information on this title: www.cambridge.org/9781107666870

© Cambridge University Press 2013

This publication is in copyright. Subject to statutory exception and to the provisions of relevant collective licensing agreements, no reproduction of any part may take place without the written permission of Cambridge University Press.

First published 2013

Printed in Poland by Opolgraf

*A catalogue record for this publication is available from the British Library*

ISBN 978-1-107-66687-0 Paperback

Cambridge University Press has no responsibility for the persistence or accuracy of URLs for external or third-party internet websites referred to in this publication, and does not guarantee that any content on such websites is, or will remain, accurate or appropriate.

## Contents

- Introduction ................................ 4
- Chapter 1: Can you guess my password? ................................ 7
- Chapter 2: Objects, classes and factories ................................ 17
- The MyPong Project ................................ 32
- Chapter 3: Creating the Table ................................ 34
- Chapter 4: Making the Ball ................................ 51
- Chapter 5: Building the Bats ................................ 69
- Chapter 6: The rules and scoring ................................ 91
- Bonus Chapter: Two more games ................................ 106
- Taking things further ................................ 120
- Appendix: Some key bits of information ................................ 123
- Glossary and index ................................ 126
- Quick Quiz answers ................................ 131
- Acknowledgements ................................ 132

## Introduction

### Who is this book for?

This book is the Level 3 core book in the Coding Club series. Before reading this, you should have either read *Coding Club, Python: Next Steps* or have become familiar with Python 3 and learned about variables, while loops, lists and tuples. This book is aimed at coders with a little bit of previous programming experience.

### Why should you choose this book?

Building larger programs and applications can seem daunting. As well as sorting out the normal details and algorithms, the big picture has to be maintained. This book helps you to see your way through the big picture – it shows you how to break your applications up into manageable chunks that are logical, and even better, reusable. To do this you are given an introduction to a style of programming called object oriented programming (OOP). This is a great way to program but might seem a little more complicated at first than the way you have learned to code in the level 1 and 2 books.

![](img/c4403822ba1e00f0a2ce532b3f9d5054_5_0.png)

At this stage in your coding it is important that you are introduced to classes and objects. This is because you will certainly want to use other people's classes, and to do this effectively a little understanding goes a long way. What is special about this book is how the explanations are rooted in the real world and use analogies that you will understand. The code is also built so that it mirrors real objects whenever possible. This is so that when you go on to write your own applications you will be able to imagine how to convert real objects into coded objects.

### What you will need

Any type of computer can run Python 3. If yours does not already have it installed, there is a section on the companion website (www.codingclub.co.uk) that guides you through installing IDLE and Python 3. This only takes about 5 minutes, and is all you require to get started.

So that you do not have to do too much typing and do not get lost in the bigger projects, there are start files and, if you need them, finished files for all the projects in the book in one easily downloadable zip file. The website also has answers to the puzzles and challenges to help you if you get stuck.

### How to use this book

The ideal way to use this book is to read everything carefully and build all the main projects in order. At the end of each chapter there are further ideas, and challenges that you can think of as ‘mini quests’. Some readers will want to work through them all so that they understand everything all the time. Some of you will probably prefer to rush through and get to the end. Which approach is best? The one you are most comfortable with. However, if you are being guided by a teacher, you should trust their judgement so that they can help you in the best possible way.

There are four ways in which this book tries to help you to learn:

- 1. Typing out the code – this is important as it encourages you to work through the code a line at a time (like computers do) and will help you to remember the details in the future.
- 2. Finding and fixing errors – error messages in Python give you some clues as to what has gone wrong. Solving these problems yourself will help you to become a better programmer. To avoid feeling bored and frustrated though, the code can be downloaded from the companion website www.codingclub.co.uk
- 3. Experimenting – feel free to experiment with the code you write. See what else you can make it do. If you try all of the challenges, puzzles and ideas, and generally play with the code, this will help you learn how to write code like a pro.
- 4. Finally, this book will not only provide the code to build some pretty cool, short projects – it will also teach you how the programs were designed. You can then use the same methods to design your own applications.

### A word of warning

You may be tempted to simply get the code off the website instead of typing it yourself. If you do, you will probably find that you cannot remember how to write code so easily later. In this book you will only be asked to type small chunks of code at a time – remember that this will help you understand every detail of each of your programs.

## Chapter 1: Can you guess my password?

This book assumes that you have read *Coding Club: Python Basics*. If you have not, you should at least understand what variables and functions are and know how to use IDLE in both interactive mode and script mode. In this first chapter you will recall some of this by making a very simple application called ‘Guess My Password’. You will then have revised:

- variables
- if, elif and else
- functions
- while loops
- modules
- using IDLE’s script mode.

![](img/c4403822ba1e00f0a2ce532b3f9d5054_8_0.png)

### Guess My Password

The game is going to start by asking the player to guess my password. The app then waits for the player’s input, which is stored in a variable. Finally, the player’s input will be compared with the computer’s own secret password. If the guess is correct the player is congratulated, if not, a random message is supplied and then the player is asked to try again.

As in the previous Coding Club books, you will use IDLE, an example of an IDE. You can start by opening IDLE and then choosing New Window from the File menu. This gets you into IDLE’s script mode. It is a good idea to now re-arrange the windows so that the interactive mode console and new window are next to each other and both can be seen at the same time (Figure 1.1).

![](img/c4403822ba1e00f0a2ce532b3f9d5054_9_0.png)

Figure 1.1 A simple IDLE arrangement.

Copy the code from Code Box 1.1 and save the file to your Python Code folder as `GuessMyPassword.py`. You may not have a Python Code folder so you might need to create one first. Choose a sensible place to save this, such as your Documents folder.

### Code Box 1.1

```python
# GuessMyPassword.py is a quick revision application.

import random

# Initialise variables:
response1 = "I am afraid not. Please try again."
response2 = "That is a good password but not my password. Keep guessing."
response3 = "That is not my password. It really is easy to guess my password."
response4 = "Well done! You must work for MI6. Give my regards to James Bond."
MY_PASSWORD = "my password"
```

### Analysis of Code Box 1.1

### Comments

Comments appear in red in IDLE; these are aimed at humans only and begin with the hash symbol `#`.
