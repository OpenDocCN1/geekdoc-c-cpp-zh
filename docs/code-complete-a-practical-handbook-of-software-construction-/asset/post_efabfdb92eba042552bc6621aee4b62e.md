
conceived this book as a full discussion of code construction—from one programmer to another.

## Author Note

I welcome your inquiries about the topics discussed in this book, your error reports, or other related subjects. Please contact me at stevemcc@construx.com, or visit my website at www.stevemcconnell.com.

Bellevue, Washington
Memorial Day, 2004

## Microsoft Learning Technical Support

Every effort has been made to ensure the accuracy of this book. Microsoft Press provides corrections for books through the World Wide Web at the following address:

http://www.microsoft.com/learning/support/

To connect directly to the Microsoft Knowledge Base and enter a query regarding a question or issue that you may have, go to:

http://www.microsoft.com/learning/support/search.asp

If you have comments, questions, or ideas regarding this book, please send them to Microsoft Press using either of the following methods:

Postal Mail:

Microsoft Press
Attn: Code Complete 2E Editor
One Microsoft Way
Redmond, WA 98052-6399

E-mail:

mspinput@microsoft.com

## Acknowledgments

A book is never really written by one person (at least none of my books are). A second edition is even more a collective undertaking.

I’d like to thank the people who contributed review comments on significant portions of the book: Håkon Agustsson, Scott Ambler, Will Barns, William D. Bartholomew, Lars Bergstrom, Ian Brockbank, Bruce Butler, Jay Cincotta, Alan Cooper, Bob Corrick, Al Corwin, Jerry Deville, Jon Eaves, Edward Estrada, Steve Gouldstone, Owain Griffiths, Matthew Harris, Michael Howard, Andy Hunt, Kevin Hutchison, Rob Jasper, Stephen Jenkins, Ralph Johnson and his Software Architecture Group at the University of Illinois, Marek Konopka, Jeff Langr, Andy Lester, Mitica Manu, Steve Mattingly, Gareth McCaughan, Robert McGovern, Scott Meyers, Gareth Morgan, Matt Peloquin, Bryan Pflug, Jeffrey Richter, Steve Rinn, Doug Rosenberg, Brian St. Pierre, Diomidis Spinellis, Matt Stephens, Dave Thomas, Andy Thomas-Cramer, John Vlissides, Pavel Vozenilek, Denny Williford, Jack Woolley, and Dee Zsombor.

Hundreds of readers sent comments about the first edition, and many more sent individual comments about the second edition. Thanks to everyone who took time to share their reactions to the book in its various forms.

Special thanks to the Construx Software reviewers who formally inspected the entire manuscript: Jason Hills, Bradley Honsinger, Abdul Nizar, Tom Reed, and Pamela Perrott. I was truly amazed at how thorough their review was, especially considering how many eyes had scrutinized the book before they began working on it. Thanks also to Bradley, Jason, and Pamela for their contributions to the **cc2e.com** website.

Working with Devon Musgrave, project editor for this book, has been a special treat. I’ve worked with numerous excellent editors on other projects, and Devon stands out as especially conscientious and easy to work with. Thanks, Devon! Thanks to Linda Engelman who championed the second edition; this book wouldn’t have happened without her. Thanks also to the rest of the Microsoft Press staff, including Robin Van Steenburgh, Elden Nelson, Carl Diltz, Joel Panchot, Patricia Masserman, Bill Myers, Sandi Resnick, Barbara Norfleet, James Kramer, and Prescott Klassen.

I’d like to remember the Microsoft Press staff that published the first edition: Alice Smith, Arlene Myers, Barbara Runyan, Carol Luke, Connie Little, Dean Holmes, Eric Stroo, Erin O'Connor, Jeannie McGivern, Jeff Carey, Jennifer Harris, Jennifer Vick, Judith Bloch, Katherine Erickson, Kim Eggleston, Lisa Sandburg, Lisa Theobald, Margarite Hargrave, Mike Halvorson, Pat Forgette, Peggy Herman, Ruth Pettis, Sally Brunsman, Shawn Peck, Steve Murray, Wallis Bolz, and Zaafar Hasnain.

## Acknowledgments

Thanks to the reviewers who contributed so significantly to the first edition: Al Corwin, Bill Kiestler, Brian Daugherty, Dave Moore, Greg Hitchcock, Hank Meuret, Jack Woolley, Joey Wyrick, Margot Page, Mike Klein, Mike Zevenbergen, Pat Forman, Peter Pathe, Robert L. Glass, Tammy Forman, Tony Pisculli, and Wayne Beardsley. Special thanks to Tony Garland for his exhaustive review: with 12 years’ hindsight, I appreciate more than ever how exceptional Tony’s several thousand review comments really were.

## Checklists

- Requirements 42
- Architecture 54
- Upstream Prerequisites 59
- Major Construction Practices 69
- Design in Construction 122
- Class Quality 157
- High-Quality Routines 185
- Defensive Programming 211
- The Pseudocode Programming Process 233
- General Considerations In Using Data 257
- Naming Variables 288
- Fundamental Data 316
- Considerations in Using Unusual Data Types 343
- Organizing Straight-Line Code 353
- Using Conditionals 365
- Loops 388
- Unusual Control Structures 410
- Table-Driven Methods 429
- Control-Structure Issues 459
- A Quality-Assurance Plan 476
- Effective Pair Programming 484
- Effective Inspections 491
- Test Cases 532
- Debugging Reminders 559
- Reasons to Refactor 570
- Summary of Refactorings 577
- Refactoring Safely 584
- Code-Tuning Strategies 607
- Code-Tuning Techniques 642

## Tables

- Table 3-1 Average Cost of Fixing Defects Based on When They’re Introduced and Detected 29
- Table 3-2 Typical Good Practices for Three Common Kinds of Software Projects 31
- Table 3-3 Effect of Skipping Prerequisites on Sequential and Iterative Projects 33
- Table 3-4 Effect of Focusing on Prerequisites on Sequential and Iterative Projects 34
- Table 4-1 Ratio of High-Level-Language Statements to Equivalent C Code 62
- Table 5-1 Popular Design Patterns 104
- Table 5-2 Design Formality and Level of Detail Needed 116
- Table 6-1 Variations on Inherited Routines 145
- Table 8-1 Popular-Language Support for Exceptions 198
- Table 11-1 Examples of Good and Bad Variable Names 261
- Table 11-2 Variable Names That Are Too Long, Too Short, or Just Right 262
- Table 11-3 Sample Naming Conventions for C++ and Java 277
- Table 11-4 Sample Naming Conventions for C 278
- Table 11-5 Sample Naming Conventions for Visual Basic 278
- Table 11-6 Sample of UDTs for a Word Processor 280
- Table 11-7 Semantic Prefixes 280
- Table 12-1 Ranges for Different Types of Integers 294
- Table 13-1 Accessing Global Data Directly and Through Access Routines 341
- Table 13-2 Parallel and Nonparallel Uses of Complex Data 342
- Table 16-1 The Kinds of Loops 368
- Table 19-1 Transformations of Logical Expressions Under DeMorgan’s Theorems 436
- Table 19-2 Techniques for Counting the Decision Points in a Routine 458
- Table 20-1 Team Ranking on Each Objective 469
- Table 20-2 Defect-Detection Rates 470
- Table 20-3 Extreme Programming’s Estimated Defect-Detection Rate 472
- Table 21-1 Comparison of Collaborative Construction Techniques 495
- Table 23-1 Examples of Psychological Distance Between Variable Names 556
- Table 25-1 Relative Execution Time of Programming Languages 600
- Table 25-2 Costs of Common Operations 601

## Tables

- Table 27-1 Project Size and Typical Error Density 652
- Table 27-2 Project Size and Productivity 653
- Table 28-1 Factors That Influence Software-Project Effort 674
- Table 28-2 Useful Software-Development Measurements 678
- Table 28-3 One View of How Programmers Spend Their Time 681

## Figures

Figure 1-1 Construction activities are shown inside the gray circle. Construction focuses on coding and debugging but also includes detailed design, unit testing, integration testing, and other activities. 4

Figure 1-2 This book focuses on coding and debugging, detailed design, construction planning, unit testing, integration, integration testing, and other activities in roughly these proportions. 5

Figure 2-1 The letter-writing metaphor suggests that the software process relies on expensive trial and error rather than careful planning and design. 14

Figure 2-2 It’s hard to extend the farming metaphor to software development appropriately. 15

Figure 2-3 The penalty for a mistake on a simple structure is only a little time and maybe some embarrassment. 17

Figure 2-4 More complicated structures require more careful planning. 18

Figure 3-1 The cost to fix a defect rises dramatically as the time from when it’s introduced to when it’s detected increases. This remains true whether the project is highly sequential (doing 100 percent of requirements and design up front) or highly iterative (doing 5 percent of requirements and design up front). 30

Figure 3-2 Activities will overlap to some degree on most projects, even those that are highly sequential. 35

Figure 3-3 On other projects, activities will overlap for the duration of the project. One key to successful construction is understanding the degree to which prerequisites have been completed and adjusting your approach accordingly. 35

Figure 3-4 The problem definition lays the foundation for the rest of the programming process. 37

Figure 3-5 Be sure you know what you’re aiming at before you shoot. 38

Figure 3-6 Without good requirements, you can have the right general problem but miss the mark on specific aspects of the problem. 39

Figure 3-7 Without good software architecture, you may have the right problem but the wrong solution. It may be impossible to have successful construction. 44

Figure 5-1 The Tacoma Narrows bridge—an example of a wicked problem. 75
