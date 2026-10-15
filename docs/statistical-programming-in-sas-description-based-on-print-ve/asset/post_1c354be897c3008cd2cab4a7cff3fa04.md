
11.9 Introducing SAS/IML Studio ......................................................... 411

11.10 Summary ......................................................... 422

11.11 References ......................................................... 422

11.12 Exercises ......................................................... 423

Index ......................................................... 427

## About This Book

## Purpose

Statistical programming is necessary where data-based analyses or simulation studies are conducted. For example, Monte Carlo methods are used to generate *p*-values for complex statistics. And, manipulating large data sets is becoming commonplace. Many people experience computing exclusively through a graphical user interface. Therefore, they might not be prepared to deal with the challenges of constructing specialized programs to address their research problems. They might not be familiar with basic programming concepts (e.g., looping or conditional execution) or programming styles to keep programs easier to read and maintain (e.g., modular code with sensible commenting). In this book, SAS 9.2 is used as a platform to introduce programming ideas for statistical analysis, data management, and simulation. Examples of statistical methods and concepts not always encountered in basic statistics courses (e.g., bootstrapping, randomization tests, and jittering) are used to illustrate these programming ideas.

## Intended Audience

Upper-level undergraduates, beginning graduate students, or professionals involved in data analysis, data management, or simulation studies. Some familiarity with basic statistical estimation and testing ideas is assumed.

Recently, a new section for statistical programmers and analysts was added to the American Statistical Association. Members of this new ASA section and members of the International Association for Statistical Computing, which is a section of the International Statistical Institute, might be interested in this book as well.

## Scope of This Book

This book has two parts. The first part addresses the nuts and bolts that are associated with good programming habits, getting external data sets into SAS to construct an analysis data set, generating basic descriptive statistical summaries, producing customized tables, generating more attractive output, and producing statistical graphics that lead to data insight. The second part emphasizes programming in the context of a DATA step, in macros, and in SAS/IML.

A good chunk of the topics included in the Base SAS Certification exam is included in this book, along with topics such as SQL and macros that are in the Advanced SAS Certification exam. Other topics are discussed such as high-quality graphical displays including one of the first descriptions of the new SAS 9.2 ODS Statistical Graphics procedures. Included in the book are extensive illustrations of the new ODS Statistical Graphics procedures in SAS, and a description of the new ODS Graphics Editor. Finally, an introduction to some of the capabilities of SAS/IML Studio, such as producing dynamically linked data displays and invoking R from SAS, is included in the last chapter.

## Use in a Statistical Programming Class

This book was developed as material for a semester-long class in statistical programming at Miami University (STA 402/502). Approximately 75% of a semester-long class is devoted to this material. Therefore, I believe this book could be used as a quarter-long introduction to statistical programming in SAS. This material has been successfully used by statistics students and by students from other disciplines including ecology, gerontology, marketing, microbiology, psychology, and economics.

## Belief and Style

You learn programming by doing it. And, you tend to learn a lot more from failing and fixing code than from getting it right the first time. So, you will get the most out of this book by trying the various code displays and the suggested exercises at the end of each chapter. The style of prose in this book is informal. I hope this makes the book a more entertaining read. This book is not written with a simple linear trajectory in which topics are not used until they are fully defined and developed. In programming, you might find that you need functions, procedures, etc., long before you learn about them in any formal way. Thus, I, unapologetically, brashly, and frustratingly (to some colleagues who prefer linear development and presentations) sometimes use ideas that are defined in later chapters if it helps tell a more interesting story earlier in the book. In addition, many of the exercises might require that you dig for additional programming information to successfully complete the exercise. When I teach this material, I assign the exercises early in class discussion, and then I serve as a consultant to the students throughout the following classes as they work on the exercises.

## Software Used for This Book

This book is based on SAS 9.2 software. Although every effort has been made to include the latest information available at the time of printing, new features will be made available in later releases. Be sure to check out the SAS Web site for current updates, and check the SAS OnlineDoc for enhancements and changes in new releases of SAS.

## Code Used in This Book

The code used in this book is available from the author page at http://support.sas.com/authors. From the John Bailer author page, select “Example Code and Data” to display the SAS programs that are included in the book.

For an alphabetical index listing of SAS books for which example code is available, see support.sas.com/bookcode. Select a title to display the book’s example code. If you are unable to access the code through this Web site, send e-mail to saspress@sas.com.

## SAS Author Page

You can access the author page for this book at support.sas.com/authors. This page includes several features that relate specifically to this book, including more information about the book and the author, book reviews, and book updates; book extras such as example code and data; and contact information for the author and SAS Press.

## Additional Resources

SAS offers you a wide variety of resources to help build your SAS skills and explore and apply the full power of SAS software. Whether you are in a professional or academic setting, there are learning products that can help you maximize your investment in SAS.

| Bookstore | http://support.sas.com/publishing/ |
| Training | http://support.sas.com/training/ |
| Certification | http://support.sas.com/certify/ |
| Higher Education Resources | http://support.sas.com/learn/ |
| SAS OnDemand for Academics | http://support.sas.com/ondemand/ |
| Knowledge Base | http://support.sas.com/resources/ |
| Support | http://support.sas.com/techsup/ |
| Learning Center | http://support.sas.com/learn/ |
| Community | http://support.sas.com/community/ |

## Comments or Questions?

If you have comments or questions about this book, you can contact the author through SAS as follows:

Mail:

SAS Institute Inc.
SAS Press
Attn: A. John Bailer
SAS Campus Drive
Cary, NC 27513

E-mail:

saspress@sas.com

Fax:

(919) 677-4444

Please include the title of the book in your correspondence.

For a complete list of books that are available through SAS Press, visit support.sas.com/publishing.

## SAS Publishing News

Receive up-to-date information about all new SAS publications via e-mail by subscribing to the SAS Publishing News monthly eNewsletter. Visit support.sas.com/subscribe.

## Acknowledgments

As with any book, there are many people who deserve recognition for their influence. These folks are usually too numerous to mention by name, and there is always the danger of leaving one out. Even though I recognize this danger, I’m attempting to recognize a subset of these people. My sense of good programming style evolved through formal courses and the informal influence of seasoned programmers. I hope that my former programming mentors and instructors who helped me navigate early encounters with Fortran, Ratfor, Pascal, Speakeasy, … will be pleased to read that I did pay attention to some of their advice.

Contributions to an external program review by Walter Piegorsch led to the introduction of the statistical programming course at Miami University and, consequently, to course notes and this book. Walter is an outstanding writer, and my experience working with him on two books was great background to have before writing this book. Maura Stokes encouraged me to pitch the idea of such a book to SAS Press, and, to my great surprise and delight, I was encouraged to work on this book.

This book was subjected to an extensive review by technical reviewers at SAS, as well as external reviewers recruited by SAS Press. I thank the reviewers for their careful work. This review process was incredibly rigorous and exhaustive, and the book improved as a direct result. Bob Rodriguez at SAS helped shape the presentation of SAS ODS Graphics and traditional graphics, while Kathy Roggenkamp of the University of North Carolina at Chapel Hill provided invaluable suggestions on complete drafts of this book.

My primary contact at SAS Press, John West, has been encouraging and supportive, and his help bringing this book to closure is much appreciated. Staff members from SAS Publications have done an outstanding job in translating a manuscript into a beautifully formatted final book. I appreciate the efforts of all including Amy Wolfe (copyediting), Candy Farrell (formatting the book and implementing corrections), Patrice Cherry (designing the front cover), Jennifer Dilley (designing the back cover), Mary Beth Steinbach (Managing Editor), Stacey Hamilton (Marketing), and Shelly Goodin (Marketing).

I owe a debt of gratitude to multiple cohorts of STA 402/502 students at Miami University. They helped shape my thinking about what a good course in statistical programming should include and how it should flow. My colleagues at Miami University have been patient with my countless intrusions into their offices to describe the latest cool thing that I discovered. (It is amazing what you learn when writing a book or teaching a book
