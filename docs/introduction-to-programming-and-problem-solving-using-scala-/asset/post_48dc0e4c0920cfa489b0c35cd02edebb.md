
# 17.3 Next Steps

You could redo lots of the things that you have done through this book in Eclipse, but what are your options for continuing to learn? If you want to continue work with Scala and gain a solid foundation in key concepts of computer science, we certainly recommend Object-Orientation, Abstraction, and Data Structures Using Scala[1]. In addition to the topics that are listed in the title, this book gives you an introduction to parallelism through multithreading and a coverage of networking.

Whatever route you take, you should really strive to learn more about computer science. These remarkable machines have become integrated in every aspect of our daily lives, often in ways that are remarkably non-obvious because they have so ubiquitous. Even when you do not see them, computers and the software that they run have a dramatic impact on your life. Learning how to tell these incredible devices how to do what you want is an increasingly essential skill for modern life.

# 17.4 End of Chapter Material

## 17.4.1 Exercises

- 1. Back in project 1.2 you were asked to compare programming to three other activities based on an extremely limited introduction. Now that you have significantly experience, revisit that same question.

- 2. Write one of the projects from chapter 16 in Eclipse.

# Appendix A

## Getting to Know the Tools

- A.1 Unix/Linux (includes Mac OS X) ................................................................. 530
  - A.1.1 Command Line ..................................................................................................... 530
    - A.1.1.1 Files and Directories ................................................................................ 530
    - Aside ................................................................................................................................... 532
    - A.1.1.2 Aside ........................................................................................................ 535
    - A.1.1.3 Helpful Tips ................................................................................ 535
    - A.1.1.4 Permissions ............................................................................... 536
    - Aside ................................................................................................................................... 538
    - A.1.1.5 Compression/Archiving .......................................................................... 538
    - A.1.1.6 Remote ....................................................................................................... 539
    - Aside ................................................................................................................................... 540
    - A.1.1.7 Other Commands ........................................................................................ 541
    - I/O Redirection ........................................................................................................ 542
  - A.1.3 Text Editors (vi/vim) ....................................................................... 543
    - vi Settings ............................................................................................................................ 545
  - A.2 Windows ........................................................................................................ 545
  - A.2.1 Command Line ................................................................................... 546
    - A.2.1.1 Files and Directories ................................................................... 547
    - Aside ................................................................................................................................... 547
  - A.2.2 Text Editors ................................................................................... 548
    - A.2.2.1 Edit ....................................................................................................... 548
    - A.2.2.2 Notepad ................................................................................... 548
    - A.2.2.3 Others ....................................................................................................... 549
  - A.2.3 Other Commands ............................................................................ 549
  - A.3 End of Appendix Material ................................................................................ 550
  - A.3.1 Summary of Concepts ................................................................................ 550
  - A.3.2 Exercises ....................................................................................... 551

Everything you do on a computer involves the running of software. At the most basic level, your computer has some operating system on it controls everything that happens, organizes data, and lets you execute other programs inside of it. What operating system and tool you choose to use has a significant impact on how you go doing things. This chapter walks you through some tools that you might use and might not be familiar. It moves on to look at some of the tools that are part of standard Scala distribution that we use through the rest of the book.

Your choice of tools begins with your choice of operating system. It is very likely that you are familiar with common graphical environments on a Windows PC or Macintosh environment. For that reason, we are not going to take time to introduce them. Instead, this appendix talks about how you interact with various operating systems using a text interface. There are a number of reasons why it is good to be able to use this type of interface. For our purposes, the most significant is that it is the way we will interact with some of the Scala tools that we will be using.

# A.1 Unix/Linux (includes Mac OS X)

This section covers the environment you will encounter in a Linux and Unix environment. Mac OS X is built on top of BSD Unix everything here applies to the Mac. If you are on a Mac you can open a terminal to get access to the command-line tools.

# A.1.1 Command Line

Most people these days are used to the point and click approach of a Graphical User Interface, GUI. This is not how people have always interacted with computers. Indeed, a GUI takes a significant amount of processing power to run. For many years, computers had to have a simpler interface. Even today, there are times when you will need to interact with a computer without a GUI. This can happen when something goes wrong with the computer or if you need to use a command that is located far away.

Even when a computer is running a GUI, you can choose to interact using a command interface. Using the command line provides you with abilities that are not easily accomplished with a GUI. The reason why many people choose not to use prompt is that it has a bit of a learning curve. You need to know some basics to be able to do anything. If you are going to spend much time working on computers it is worth putting in the small amount of effort to learn the basic commands for the command interface on your OS.

# A.1.1.1 Files and Directories

In a GUI you organize your files in folders. You have that represent different file types or folders you can place files/folders inside of folders to organize them. These concepts come from the systems already in place on the command line. The only change is terminology. The term folder works well from a graphical standpoint. On the command line they have long called directories.

The first set of commands we will learn about how to work with files and directories so that we can navigate around. Here is a list of commands with a brief description of each. You will notice that in general they are abbreviations for what they do.

- cat Display the contents of one or more files.

- cd Change directory.

- cp Copy one file to name or location.
