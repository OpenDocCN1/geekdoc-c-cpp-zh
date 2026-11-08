
### 14.6 Recovering Physical Location Information 468

- 14.6.1 Using the PATHNAME Function 468
- 14.6.2 SASHELP VIEWS and DICTIONARY Tables 468
- 14.6.3 Determining the Executing Program Name and Path 469
- 14.6.4 Retrieving the UNC (Universal Naming Convention) Path 470

## Chapter 15 Miscellaneous Topics 473

### 15.1 A Few Miscellaneous Tips 474

- 15.1.1 Customizing Your NOTEs, WARNINGs, and ERRORs 474
- 15.1.2 Enhancing Titles and Footnotes with the #BYVAL and #BYVAR Options 475
- 15.1.3 Executing OS Commands 477

### 15.2 Creating User-defined Functions Using PROC FCMP 479

- 15.2.1 Building Your Own Functions 479
- 15.2.2 Storing and Accessing Your Functions 481
- 15.2.3 Interaction with the Macro Language 482
- 15.2.4 Viewing Function Definitions 483
- 15.2.5 Removing Functions 484

### 15.3 Reading RTF as Data 485

- 15.3.1 RTF Diagram Completion 486
- 15.3.2 Template Preparation 486
- 15.3.3 RTF as Data 487

## Appendix A Topical Index 489

## Appendix B Usage Index 491

## Global Statements and Options 492

- Statements, Global 492
- Macro Language 493
- GOPTIONS, Graphics 493
- Options, System 493
- Options, Data Set 495

## Procedures: Steps, Statements, and Options 495

- Procedures 495

## DATA Step: Statements and Options 500

- Statements, DATA Step 500
- Format Modifiers 501
- Functions 501
- Hash Object 504

## Output Delivery System, ODS 504

- ODS Destinations and Targets 504
- ODS Attributes 505
- ODS Options 505
- ODS Statements 506

## SAS Display Manager 506

- Display Manager Commands 506

## References 507

- User Publications 507
- Generally Good Reading—Lots More to Learn 518
  - SAS Documentation 518
  - SAS Usage Notes 518
  - Discussion Forums 518
  - Newsletters, Corporate and Private Sites 519
  - User Communities 519
  - Publications 519
  - Learning SAS 520

## Index 521

## About This Book

### The Intent of this Book

The goal of this book is to broaden the usage of a number of SAS programming tools and techniques. This is a very eclectic collection of ideas and tips that have been advanced over the years by any number of users. Some are quite advanced; however, most require only an intermediate understanding of the general concepts surrounding the tip. For instance, if the technique involves the use of a double SET statement, you should have a decent understanding of the DATA step and how it is compiled and executed. Many of the techniques are even simple and are essentially suggestions along the lines of “Did you know that you can . . . ?”

### What this Book is NOT

As is the case with any book that deals with a very broad range of topics, no single topic can be covered with all possible detail. For example SAS Formats are discussed in this book in several places; however, if you want more information on SAS formats, a full book has been written on that subject alone (Bilenas, 2005); consequently the content of that book will not be repeated in this one.

Except for a few of the especially advanced topics (I get to decide which ones), for most topics, this book makes no attempt to explain the basics. There are several very good “getting started” books on various aspects of SAS, this book is NOT one of them. If you want the basic how-to for a procedure or technique consult one of these other books. Of course, the reality is that some of the readers of this book will have more, or less, experience than others. I have made some attempt at offering brief explanations on most topics. Hopefully the depth of this book will be enough to get you started in the right direction for any given topic, even if it does not cover that topic thoroughly.

By its very nature this book is not designed to be read linearly, front to back; instead, I anticipate that the reader will use it either as a reference for a specific technique, an exploration tool for learning random new 'tidbits', or perhaps most effectively as a sleeping aid. The MORE INFORMATION and SEE ALSO sections, as well as the topical index in Appendix A and the usage index in Appendix B, should help you find and navigate to related topics.

### What this Book is . . .

There are literally hundreds of techniques used on a daily basis by the users of SAS software as they perform analyses and generate reports. Although sometimes obscure, most of these techniques are relatively easy to learn and generally do not require any specialized training before they can be implemented. Unfortunately a majority of these techniques are used by only a very small minority of the analysts and programmers. They are not used more frequently, simply because a majority of SAS users have not been exposed to them. Left to ourselves, it is often very difficult to “discover” the intricacies of these techniques and then to sift through them for the nuggets that have immediate value. Certainly this is true for myself as I almost daily continue to learn new techniques. I regret that the nugget that I learn tomorrow will not make it into this book.

This book introduces and demystifies a series of such nuggets. It covers a very broad range of mostly Base SAS topics that have proven to be useful to the intermediate or advanced SAS programmer who is involved with the analysis and reporting of data. The intended audience is expected to have a firm grounding in Base SAS. For most of the covered topics, the book will introduce useful techniques and options, but will not “teach the procedure”.

I have purposefully avoided detailed treatment of advanced topics that are covered in other books. These include, but are not limited to: statistical graphics (Friendly, 1991), advanced ODS topics (Haworth et al., 2009), the macro language (Carpenter, 2004), PROC REPORT (Carpenter, 2007a), PROC TABULATE (Haworth, 1999), SAS/GRAPH (Carpenter and Shipp, 1995), and the annotate facility (Carpenter, 1999).

The more advanced users may find that they are already using some of these techniques, and I hope that this is the case for you. However, I believe that the range of topics is broad enough that there will be something for everyone. It may only take a single nugget to 'pay for the book'.

### Intended Audience

This book is intended to be used by intermediate and advanced SAS programmers and SAS users who are faced with large or complex reporting and analysis tasks. It is especially for those that have a desire to learn more about the sometimes obscure options and techniques used when writing code for the advanced analysis and reporting of data. SAS is complex enough that it can be very difficult, even for an advanced user, to have a knowledge base that is diverse enough to cover all the necessary topics. Covering, at least at a survey level, as many of these diverse topics as possible is the goal of this book.

This book has not been written for the user who is new to SAS. While this book contains a great deal that the new user will find valuable, unlike an introductory book that goes into great detail, most of the topics in this book are fairly brief and are intended more to spark the reader's interest rather than to provide a complete reference. The assumption is that most readers of this book will have sufficient background to 'dig deeper' for the details of the topics that most interest them.

### Overview of Chapters

#### Part 1 Data Preparation

Most tasks involving the use of SAS revolve around the data. The analyst is often responsible for bringing the data into the SAS world, manipulating it so that it can be analyzed, and for the analysis preparation itself. Although not all phases of data preparation are necessary for every project or task, the analyst must be prepared for a wide variety of *variations on the theme*.

##### Chapter 1: Moving, Copying, Importing and Exporting Data

The issues surrounding the movement of data into and out of the SAS environment are as diverse as the types and sources of data.

##### Chapter 2: Working with Your Data

Once the data is available to SAS, there are a number of ways that it can be manipulated and prepped for analysis. In addition to the DATA step, SAS contains a number of tools to assist in the process of data preparation.

##### Chapter 3: Just in the DATA Step

There are a number of tools and techniques that apply only to the DATA step.

##### Chapter 4: Sorting the Data

The order of the rows in a data table can affect not only how the data are analyzed, but also how it is presented.
