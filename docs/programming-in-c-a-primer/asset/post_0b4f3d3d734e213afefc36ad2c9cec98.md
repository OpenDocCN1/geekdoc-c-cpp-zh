
- 16.2 Delegates 315
- 16.3 Delegate Declaration 316
- 16.4 Delegate Methods 316
- 16.5 Delegate Instantiation 317
- 16.6 Delegate Invocation 319
- 16.7 Using Delegates 319
- 16.8 Multicast Delegates 320
- 16.9 Events 322
- Case Study 329
- Review Questions 331
- Debugging Exercises 333
- 17. Managing Console I/O Operations 336
- 17.1 Introduction 336
- 17.2 The Console Class 336
- 17.3 Console Input 336
- 17.4 Console Output 337
- 17.5 Formatted Output 339
- 17.6 Numeric Formatting 340
- 17.7 Standard Numeric Format 340
- 17.8 Custom Numeric Format 342
- Case Study 345
- Review Questions 348
- Debugging Exercises 348
- Programming Exercises 350
- 18. Managing Errors and Exceptions 352
- 18.1 Introduction 352
- 18.2 What is Debugging? 352
- 18.3 Types of Errors 352
- 18.4 Exceptions 354
- 18.5 Syntax of Exception Handling Code 355
- 18.6 Multiple Catch Statements 357
- 18.7 The Exception Hierarchy 358
- 18.8 General Catch Handler 359
- 18.9 Using Finally Statement 360
- 18.10 Nested Try Blocks 361
- 18.11 Throwing Our Own Exceptions 363
- 18.12 Checked and Unchecked Operators 368
- 18.13 Using Exceptions for Debugging 368
- Case Study 368
- Common Programming Errors 371
- Review Questions 372
- Debugging Exercises 373
- Programming Exercises 376
- 19. Multithreading in C# 377
- 19.1 Introduction 377
- 19.2 Understanding the System.Threading Namespace 377
- 19.3 Creating and Starting a Thread 380
- 19.4 Scheduling a Thread 382
- 19.5 Synchronising Threads 384
- 19.6 Thread Pooling 386
- Case Study 388
- Common Programming Errors 390
- Review Questions 390
- Programming Exercises 390
- 20. Windows Forms and Web-based Application Development on .NET 392
- 20.1 Introduction 392
- 20.2 Creating Windows Forms 392
- 20.3 Customizing a Form 394
- 20.4 Understanding Microsoft Visual Studio 2005 398
- 20.5 Creating and Running a SampleWinApp Windows Application 402
- 20.6 Overview of Design Patterns 407
- 20.7 Creating and Running a SampleWinApp2 Windows Application 408
- 20.8 Web-based Application on .NET 418
- Case Study 433
- Common Programming Errors 437
- Review Questions 437
- Programming Exercises 438
- Appendix A: Minor Project 1: Project Planner 439
- Appendix B: Minor Project 2: Task Actions 455
- Appendix C: Major Project: Voting Control for ASP.NET 463
- Appendix D: The CLR and the .NET Framework 473
- Appendix E: Building C# Applications 488
- Bibliography 501
- Index 503

## Preface to the Third Edition

It gives me great pleasure to present the third edition of Programming in C#. During the years that the second edition has been in circulation, I have received a lot of favourable responses, comments and suggestions, and I have tried to keep them in mind while preparing the script of the third edition. The new edition has been updated and now contains enhanced topics and pedagogical features.

### Target Audience

As stated earlier, this book has not been written keeping any specific syllabus in mind, rather it can be used by any one who is desirous of developing C# programs and will be very useful for the first course in C# taken by undergraduate students in Computers and Information Technology.

### New to this Edition

The third edition has been enriched with inclusions of new topics and projects. These additions will provide more depth and wider coverage of topics and help the readers in developing new applications on their own. The revised edition maintains the lucid flow and continuity which has been the strength of the book. The topics and the script in itself are well-graded and it takes the student through a step-by-step process, starting from simple programming problems to more complex and difficult ones. The specific improvements in this edition are the following:

- New topics on
  - WinForms (in Chapter 20)
  - The CLR and .NET Framework (as Appendix)
  - Building C# Applications (as Appendix)
- Elaborated coverage on Debugging
- Three new projects: 2 minor (Project Planner, Task Actions) and 1 major (Voting Control for ASP.NET)
- Program codes written in C# version 2005
- Uses validated HTML coding (part of Web 2.0) used in the examples
- Two sample programs in each chapter using latest version of C#
- Stepwise solution provided for Case Study given in each chapter
- Strong pedagogy including
  - Over 100 Example programs
  - 20 Solved Case Studies
  - Over 350 Review Questions
- Over 150 Programming Exercises
- Over 40 Debugging Exercises

### Organization of the Book

The book has been divided into twenty chapters. Chapter 1 introduces the C# language, its development, characteristics and evolution. Chapter 2 details the .NET Framework, its benefits and the relationship between C# and .NET. Chapter 3 introduces the reader to the first steps of building a C# program.

Chapters 4 to 7 define literals, variables, data types, operators, expressions, decision making, branching and looping statements and how to use these in C# programs. Chapter 8 discusses declaring, invoking, nesting of methods and method overloading. Chapter 9 explains creation of arrays and the different types of arrays. Chapter 10 demonstrates string manipulation and Chapter 11 is on structures and enumerations.

The basic principles of object-oriented programming, classes, objects, constructors and destructors, are covered in Chapter 12. Chapter 13 lucidly explains the concepts of inheritance and polymorphism in C# and Chapter 14 goes a bit further to introduce interfaces and multiple inheritance. Operator overloading is covered in Chapter 15 while delegates and events are discussed in Chapter 16. Chapter 17 deals with managing console I/O operations and their standard numeric format and custom numeric format. Chapter 18 elucidates the various types of errors and exceptions occurring in C# and explains how to manage them. Chapter 19 extensively covers the concept of multithreading and finally, Chapter 20 discusses Windows Forms and Web-based applications, and their development in .NET. One major project (on Voting Control for ASP.NET) and two minor projects (on Project Planner and Task Actions) have been introduced as appendices A, B and C in this edition. The projects are elaborate case studies in themselves and offer ample hands-on practice to students at developing real-life C# applications.

The Common Language Runtime (CLR) is the virtual machine component of the .NET Framework. All .NET programs execute under the supervision of CLR, guaranteeing certain properties and behaviours in the areas of memory management, security and exception handling. Hence, a brief introduction to CLR and the .NET Framework is given in Appendix D. Appendix E explains how to create and write a C# application.

### Web Supplements

The online learning center can be accessed at http://www.mhhe.com/balagurusamy/csharp3e. It has exhaustive content which will be very useful for both instructors and students.

- Downloadable programs for students
- Exclusive 3 major projects (Employee Management System, Basic IO Example, Voting Control using ASP.NET) and 3 mini projects (Calculate Example, Random Number Application, Project Planner) for implementation with code, step-by-step description and user manual
- Chapterwise case studies
- Web links to more information on C#

### Acknowledgements

I would like to thank all those who provided me with valuable feedback and inputs during the preparation of this book, and especially those at Tata McGraw Hill Education, without whose help and cooperation, this book would not have had a timely release. The support, patience and inspiration that I got from my wife, Dr Sushila, is something which I cherish above all. A special thanks is also due to all my teacher friends and students for their encouragement. And finally, I would like to acknowledge all those reviewers whose feedback helped me in giving shape to this revised edition. Their names are given below.

- Khurram Mustafa
  Jamia Millia Islamia, New Delhi
- Rajiv Pandey
  Amity University, Lucknow, Uttar Pradesh
- Mirza Mohd. Sufyan Beg
  Jamia Millia Islamia, New Delhi
- Muhammad Abulaish
  Jamia Millia Islamia, New Delhi
- Sanjay Kumar Pandey
  United College of Engineering and Research, Allahabad, Uttar Pradesh
- Shashank Dwivedi
  United College of Engineering and Research, Allahabad, Uttar Pradesh
- Pranab Gayen
  Swami Vivekananda Institute of Science and Technology, Kolkata, West Bengal
- N Bhattacharya
  George College, Kolkata, West Bengal
- Bhagyashree Kulkarni
  Tilak College, Mumbai, Maharashtra
- Usha Sathyam
  Vaishnav College for Women, Chennai, Tamil Nadu
- B Kalavathy
  K S Rangaswamy College of Technology, Tiruchengode, Tamil Nadu
- Vanaja
  Sri Venkateswara College of Engineering, Sriperumbudur, Tamil Nadu
- S Murali
  People's Education Society (PES) College of Engineering, Mandya, Karnataka
