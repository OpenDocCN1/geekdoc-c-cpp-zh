
### LESSON 30: PRINTING

- Try It 418
  - Lesson Requirements 418
  - Hints 418
  - Step-by-Step 418
- Exercises 419
- Windows Forms Printing 421
  - Getting Started 422
  - Starting a Printout 422
  - Drawing Shapes 423
  - Drawing Text 424
- WPF Printing 425
- Printing Visuals 426
- Try It 431
  - Lesson Requirements 431
  - Hints 431
  - Step-by-Step 432
- Exercises 434

## PART VI: WINDOWS APPS

### LESSON 31: WINDOWS STORE APPS

- Navigation Style 439
- App Styles 440
- App Images 440
- Deployment 444
  - Deploying Locally 444
  - Deploying to the Windows Store 445
- WPF Techniques 446
  - Using Styles 446
  - Setting Dependency Properties 447
- Try It 448
  - Lesson Requirements 448
  - Hints 449
  - Step-by-Step 449
- Exercises 452

### LESSON 32: WINDOWS PHONE APPS 455

- Building Apps 455
- Navigation Style 458
- App Styles 458
- App Images 459
- Try It 461
  - Lesson Requirements 461
  - Step-by-Step 462
- Exercises 462

## PART VII: SPECIALIZED TOPICS

### LESSON 33: LOCALIZING PROGRAMS 467

- Understanding Localization 468
- Building Localized Interfaces 469
- Testing Localizations 469
- Processing Locale-Specific Values 470
- Try It 472
  - Lesson Requirements 472
  - Hints 472
  - Step-by-Step 472
- Exercises 474

### LESSON 34: PROGRAMMING DATABASES, PART 1 479

- Connecting to a Database 479
- Displaying Data in a Grid 483
- Displaying Data One Record at a Time 486
- Try It 488
  - Lesson Requirements 488
  - Hints 488
  - Step-by-Step 488
- Exercises 489

### LESSON 35: PROGRAMMING DATABASES, PART 2 493

- Searching 493
- Filtering 494
- Sorting 495
- Try It 495
  - Lesson Requirements 495
  - Hints 496
  - Step-by-Step 496
- Exercises 496

### LESSON 36: LINQ TO OBJECTS 499

- LINQ Basics 499
- where Clauses 501
- order by Clauses 504
- select Clauses 504
- Try It 507
  - Lesson Requirements 508
  - Hints 508
  - Step-by-Step 508
- Exercises 509

### LESSON 37: LINQ TO SQL 511

- Connecting to the Database 511
- Making LINQ to SQL Classes 515
- Writing Code 517
- Using LINQ Queries 518
- Understanding Nullable Fields 519
- Understanding Query Execution 520
- Using LINQ to SQL with Access 522
- Try It 524
  - Lesson Requirements 524
  - Hints 524
  - Step-by-Step 524
- Exercises 525

## AFTERWORD: WHAT'S NEXT? 527

## INDEX 529

(I don't want to receive a bunch of flaming e-mails complaining that the material in this book is too basic, so I'm warning you right now. If you've been programming in C++ or Visual Basic for 16 years, don't blame me if a lot of this material seems pretty simple to you. Instead of wasting your time complaining, go find a more advanced book.)

## WHAT THIS BOOK COVERS (AND WHAT IT DOESN'T)

This book explains C# programming. It explains how to write, debug, and run applications that interact with the user and the computer. It shows how to understand object-oriented concepts, perform calculations, manipulate files and strings, produce printouts, and interact with simple databases. It explains how to run programs on your desktop, from the Windows Start menu, with a Windows tablet-style interface, and on a Windows Phone.

Programming in any language is an enormous topic, however, so this book doesn't cover everything. It doesn't explain how to design databases, build cryptographically secure web applications, create multithreaded programs that run on multiple CPUs, or build Xbox games, all tasks that are possible using C#. When you're finished reading this book, however, you'll be ready to move on to more advanced books that cover those topics.

## THE WROX 24-HOUR TRAINER APPROACH

Educators have known for many years that different people use different learning styles most effectively. Different students may learn best by:

- Reading a textbook
- Looking at nonwritten material such as pictures and graphs
- Listening to an instructor lecture
- Watching someone demonstrate techniques
- Doing exercises and examples

(Personally, I learn best by watching and doing.)

Good instructors try to incorporate material that helps students with all of these learning styles. Combining text, lecture, demonstration, discussion, and exercises lets every student pick up as much as possible using whichever methods work best.

Like a good instructor, this book uses materials that address each learning style. It uses text and figures to help visual learners, screencasts that provide visual demonstrations and auditory instruction, step-by-step instructions to help you do it yourself, and exercises for further study.

The book is divided into small, bite-sized lessons that begin with a discussion of a particular concept or technique, complete with figures, notes, tips, and other standard fare for instructional books. The lessons are short and tightly focused on a single task so you can finish each one in a single sitting. You shouldn't need to stop in the middle of a lesson and leave concepts half-learned (at least if you turn off your phone).

> NOTE The “24-Hour” in the title means the book is available to train you 24 hours per day, not that you should be able to read the entire book in 24 hours. Unless you just skim the text and skip all of the Try Its and exercises, I’d be surprised if anyone could work through the whole thing in 24 hours.

After describing the main concept, the lesson includes a Try It section that invites you to perform a programming exercise to solidify the lesson's ideas.

The Try It has several subsections. Lesson Requirements describes the exercise so you know what should happen. Hints gives pointers about possible confusing aspects of the problem, if they're needed. Step-by-Step provides a numbered series of steps that show how to solve the problem.

A screencast on the accompanying DVD shows me working through the Try It problem. Additional commentary at the end of the screencast highlights extensions of the lesson's main concepts.

After the Try It's Step-by-Step section, the lesson concludes with extra exercises that you can solve for further practice and to expand the lesson's main ideas. Some of the exercises extend the material in the main lesson, so I recommend that you at least skim the exercises and ask yourself if you think you could do them. Solutions to the Try Its and all of the exercises are available for download on the book's website. Additional screencasts show how to work through many of the exercises.

## WEBSITES

To find the book's web page, go to www.wrox.com/go/csharp24hourtrainer2e. There you can find solutions to all of the Try Its and exercises, plus some additional resources. You can view the screencasts at www.wrox.com/go/csharp24hourtrainer2evideos.

The one thing that a good classroom experience has that this book doesn't is direct interaction. You can't shout questions at the instructor, work in a team with fellow students, and discuss exercises with other students in the campus coffee house.

Although the book itself can't help here, you can do at least three things to get this kind of interaction. First, join the Wrox P2P (peer-to-peer) discussion forum for this book. As the section “P2P.WROX.COM” later in this lesson says, you can join the discussion forum to post questions, provide answers, see what other readers are doing with the book's material, and generally keep tabs on book-related topics. You can also sign up for other discussion groups on the Internet, too. You can post questions on those discussions, but it's also very interesting to see what other people are asking. Book discussion groups often don't have as much traffic, so the topics tend to be more limited than those in these other groups. (Although I watch my P2P groups closely, so go there if you want me to answer.)

Finally, if you get stuck on an exercise or some other program you're working on, e-mail me at RodStephens@CSharpHelper.com. I won't solve the exercises for you but I'll try to clarify problems or give you the hints you need to solve them yourself.

## GETTING THE MOST OUT OF THE BOOK

This book provides a lot of tools that you can use to best match your learning style, but you have to use them. If you learn best by reading text, spend more time on the text. If you like step-by-step instructions, focus on the Try Its and their step-by-step instructions. If you learn best by watching and listening, focus on the screencasts.

Then, after you've finished a lesson, use the exercises to verify that you've mastered the material. Most of the lessons are fairly easy to just read through quickly. Unless you practice what you've learned, you can't be sure it's sticking, so plan to spend some time on the exercises. It would not be strange to spend half an hour reading the lesson and then several hours working through the Try It and exercises.

And don't be afraid to invent programs of your own. Just because an idea isn't in the book doesn't mean it wouldn't make good practice. Modify the programs you build for the exercises to find out what you can accomplish.

## HOW THIS BOOK IS STRUCTURED

This book is divided into seven sections, each containing a series of short lessons. The lessons are generally arranged in order, with later lessons depending on earlier ones, so you should study the lessons more or less in order, at least through the first four sections. The lessons in sections V, VI, and VII cover slightly more specialized topics and you can study them in any order.

Many of the exercises are tagged with a topic as in [Games] or [WPF]. Those indicate a theme that you may find interesting. For example, the [Games] exercises involve techniques that you may find useful if you want to build game programs. The topics include:

- [WPF]—These ask you to use WPF. They are often harder than corresponding Windows Forms programs, but they sometimes produce better-looking results. (You also need to use WPF to build tablet-style and Windows Phone apps.)
- [Games]—These are generally amusing or demonstrate techniques that may be useful in building game programs.
- [SimpleEdit]—This is a simple word processing application that is built and enhanced over a sequence of exercises in several lessons.
