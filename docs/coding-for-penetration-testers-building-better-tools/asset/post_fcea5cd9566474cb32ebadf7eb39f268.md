
# CHAPTER 0

# Introduction

INFORMATION IN THIS CHAPTER

- Book Overview and Key Learning Points
- Book Audience
- How This Book Is Organized

## Book Overview and Key Learning Points

What sets a good penetration tester apart from an average one is the ability to adapt to the ever-changing landscape within which we live. One aspect of this adaptability is the skill to build, extend, and manipulate scripts and applications encountered in the field. Whether tools already exist to accomplish a task, or one needs to be built to take advantage of a new vulnerability, the ability to build and extend tools in a variety of scripting languages is important. Each of the first five chapters of this resource delves into a different scripting language that we may encounter while performing penetration tests.

Through investigating the core aspects of each language, either on Microsoft platforms, or on Linux platforms such as Kali 2.0, each chapter brings to light the power and strengths of each language. We will use these strengths to build a series of scripts to help us understand the intricacies of each language, and in most cases develop a basic tool that we can use and extend while penetration testing. Whether it is through shell scripting, Python, Perl, Ruby, or PHP, we will cover the basics of each language and discuss topics such as output handling, loops and control statements, networking, and command execution.

Once the core language concepts have been covered, Coding for Penetration Testers tackles the core tasks of penetration testing. While scanner scripting and information gathering, we will discuss tools such as Nmap and Nessus and use the scripting languages behind them to extend the capabilities of both tools. Information gathering is one of the first and most important steps of a penetration test. We don't know what we're attacking until the initial research. Chapter 8, Information gathering, investigates how to automate information gathering tasks to be more effective and have repeatable results.

Once we've gathered the information, we're ready to begin the offensive. Through looking at Python as an exploit delivery tool, we will discuss the basics of exploit development. Walking through building a working exploit, Chapter 9, Exploitation scripting, takes us through each step of the process, from creating a Proof of Concept to creating a repeatable and extendable exploit within the Metasploit Framework. Not to leave the Web applications out of the mix, Chapter 9, Exploitation scripting, covers a variety of Web attack methodologies and looks at how to how script these attacks to be more effective.

Although we’ve successfully penetrated a system, that doesn’t mean we’ve done. Chapter 10, Postexploitation scripting, brings in the testing we need to perform, with a discussion of postexploitation tasks under Windows, Linux, and Web applications. By understanding how to query systems, expand our access, and mine systems for data, we will be able to extend our reach from one system to the network or database. By the end of the book, we not only have covered the core languages encountered while penetration testing but also have built and investigated real-world scenarios for how to use these languages, tools, techniques, and concepts.

## Book Audience

This book will be a valuable resource to those involved in penetration testing activities, as well as security professionals and network and system administrators. The information provided on scripting languages and attacks can also be used to assist in engineering better and more efficient defenses.

Those in development positions will find this information useful as well, from the standpoint of developing better tools for their organizations. The concepts discussed in this book can be used to learn the basic concepts of several scripting languages, as well as working through the application of these languages in building practical tools.

In order to get the most out of this resource, some knowledge or experience is required. We will be going over networking, advanced Windows commands, and Web and application exploitation, so individuals need to have either a basic understanding of these tasks to get started, or a desire to learn those things alongside this text. In many cases, we point out resources to accompany the concepts that are being discussed, so don't be intimidated. The desire to learn and understand new and progressive concepts is essential for a good penetration tester.

## How This Book is Organized

Due to the content and organization of the topics in this book, it is not necessary to read it from front to back. Chapters 1–6 cover language concepts, while the final chapters cover applications of these languages. When we refer to information in other chapters in the book, we include references to point to the chapter where the information can be found. The following descriptions provide an overview of the contents of each chapter:

### Chapter 1: Introduction to Command Shell Scripting

In this chapter, we talk about shells, in the sense of the text-based interfaces we use to communicate with operating systems. UNIX, Linux, and OS X, as well as UNIX-like operating systems, tend to work on the same general principles for purposes of shell scripting, and make use of many common programming concepts such as data structures, variables, control statements, if-then clauses, and while loops. In Microsoft operating systems, we can find many shell scripting tools as well. In Windows, we can carry out commands and write scripts using the generic shells command.com and CMD.exe, the PowerShell shell, and add-on tools such as Cygwin to give access to bash on Windows, just to name a few.

### Chapter 2: Introduction to Python

In this chapter, we dig into the Python language and investigate different types of network scripts, subnetting, and file manipulation. These topics are investigated through practical examples that we will encounter while penetration testing. We look at how to build scripts to communicate with Web servers, determine what Web servers may be hiding, and even investigate how to send our data without being seen by network tools. These examples and more provide practical, real-world scenarios for when and how to use the Python language.

While we’re building tools that we can extend for our toolkit, we investigate all the Python basics from data structures, to control statements, to interacting with the shell, and manipulating strings and files.

### Chapter 3: Introduction to Perl

In this chapter, we examine the Perl language. We can use Perl to process data and merge data from disparate sources, a common function in the penetration testing world with its many tools. Scripting in Perl follows most of the standard conventions we can find in other scripting or programming languages and can make use of various data structures, such as variables and arrays to store data in our scripts, arguments, control statements as well as regular expressions, file I/O, and many of the other standard programming language features.

### Chapter 4: Introduction to Ruby

Ruby is a flexible programming language that has taken the better parts of Perl, Python, and many others to create a language that is both powerful and easy to read. In this chapter, we take a look at the powerful object-oriented approach to Ruby. Using Ruby to convert data between hex, binary, and plaintext data, this chapter looks at the details of network and file manipulation, building new classes, manipulating databases, and even building basic network servers. Through these examples, we explore the critical aspects of the Ruby language, and develop the skills to aid in real-world testing scenarios.

### Chapter 5: Introduction to Web Scripting With PHP

This chapter dives into the world of PHP and Web scripting. Through building basic Web applications with the HyperText Markup Language and PHP, we can build dynamic Web pages that take advantage of file manipulation, databases, and even issuing system
