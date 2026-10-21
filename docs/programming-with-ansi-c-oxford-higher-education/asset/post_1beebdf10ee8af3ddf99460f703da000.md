
# Case Study

# LEARNING OBJECTIVE

The single objective of this appendix is to apply the concepts studied so far in a real-world application.

# A.1 INTRODUCTION

C++ is an important player in designing compilers, operating systems, graphics applications, and networking and communication programs. If we choose a case study from any one of these domains, it would be difficult to understand. Hence, we will work on an example in a domain with which both teachers and students are familiar. The case study that is discussed here by no means gives a complete solution to the problem. A real commercial solution will contain many more features and, more importantly, a graphical user interface (GUI) component for the users to interact with.

One may wonder why C++ does not provide GUI as a built-in component, whereas VB and JAVA provide it. In this book, we have hardly used GUI features in any of the programs. Here are a few reasons:

- 1. C++ is traditionally considered good for generating dynamic link libraries (DLLs), network level programming (coding TCP/IP-like protocols), and building compilers, operating systems (Windows and Linux have significant parts written in C++), and other application development tools (VB is built using C++). GUI is not a necessary component for building these applications as there is no interaction with the user.
- 2. Unlike Java, which does not run directly on top of the operating system, or VB, which is confined to a single OS, C++ needs to work with many operating systems. For example, a TCP/IP protocol needs to run on top of multiple operating systems and must be designed in a way that the same program runs on top of any given operating system. GUI requirement hinders that possibility.
- 3. VC++ is the only exception that is designed to provide GUI, which is only in Windows environment. This design is not a part of the standard and, thus, is not useful elsewhere. The windows GUI model is fairly complex and is not easy for a normal user to work with.
- 4. Linux environment has a few solutions that provide GUI with C++. They too are complex and are not at all compatible with other solutions.
- 5. Some lightweight solutions such as conio in TC++ and curses in Linux are used to confine the output to a specific part of the text. Both conio and curses are text-based graphics and, therefore, have their own limitations. For example, they cannot have buttons and cannot provide event-driven programming. Even with these limitations, they are quite useful for generating different windows on the screen, and they make the program interface look better. Unfortunately, there are no standards for even these solutions, and hence, they are not recommended.

# A.2 MARKS ENTRY PROBLEM

Let us first have a briefing of the problem. Here, a teacher assigns his/her students two sessional examinations, two practical examinations, and a presentation in a given subject. The following points need to be noted:

- 1. In a given subject, five different types of marks are to be entered. Each type is known as a head. Thus, marks are to be entered under five different heads.
- 2. The teacher should be able to enter marks at any time. Sessional1 marks may be entered when Sessional1 theory answer sheets are checked. Similarly, Sessional2 marks are entered when Sessional2 answer sheets are checked. Practical1 and Practical2 marks are entered immediately after conducting the practical examination.
- 3. The teacher usually teaches more than one subject. He/she must be able to enter marks according to the subjects and also be able to enter the list of subjects once. He/ she should be able to choose from the subjects for marks entry every time the program is executed.
- 4. When the program is executed for the first time, it should read the subject and the year of entry. Next, it should read the marks for (usually) Sessional1 marks. Then, the entry is made for some other head; either Sessional2 or Practical1, etc.
- 5. It is important to get the Sessional1 marks entered earlier to be displayed with new marks. It is also important to tell the user that Sessional1 marks are already entered. Similarly, when the marks of the third head are being entered, the user should be informed that marks of two of the other heads are already entered.
- 6. The marks should be displayed in a formatted manner when needed.

This problem may look simple, but it is not. Some of the requirements are very challenging to meet.

- 1. Marks once entered should be available next time and every time. It demands that the marks are to be stored in some form of file.
- 2. The file that stores the information should be named such that it can be used without the user's intervention.
- 3. Two different types of files are required for entry of marks. The first file would store all the marks of different students. The second file would store information about the marks themselves (metadata). It stores information such as the subject and the year for which the marks are meant and under which of the five heads are they entered.

8. We need to use menus for the user to select from. Take the case of marks entry. We need to provide choices for the subject for which data is to be entered and also for the head. Both the requirements are different. The subjects are not known a priori. The list of subjects depends on the entry made by the user. We need to have some form of a dynamic menu. This menu is to be generated from the data entered by the user about subjects. The second menu is static and can be generated by simple cout statements.

9. The marks need to be entered for unknown number of students. Without the Standard Template Library (STL), we need either a large array or some form of dynamic memory manipulation. Fortunately, vectors are handy.

# Essential Components of the Project

Files and streams Why do we need files? Is our storage in a vector not enough? Unfortunately, it is not possible to use vectors in our case. We need to keep the status of the marks entered between multiple runs of our program. When we are entering Sessional2 marks, Sessional1 marks should be available and so on. The heads that are entered so far and those that are not entered should also be known. When the program is not executing, the values stored in the vector are just lost. It is important to reload the values in the vector when the program is rerun.

Menu-driven program The need for menus is not all that stringent. We can have a program without menus. Menus are used to improve the user interface so that users can easily choose from the given options. A GUI interface might have other types of user interfaces, but text-based interface is almost impossible without menus.

STL vector and student array We could have a normal array in the program instead of vectors. However, the problem is that we have no idea, while writing the program, about the number of students for which marks are to be entered. In such a case, we need to have a very large array or some form of dynamic memory mechanism. Fortunately, we do not need that if we use vectors because they can grow dynamically.

Classes and important functions We have two classes, Marks and Subject, and functions for data entry of marks of a subject and choosing a subject. Displaying the mark sheet is also done by a function. An important non-member function ChooseSubject() is provided for the user to choose subjects and related details.

# A.3 PROGRAM CONSTRUCT

Let us now analyse the following code. It is followed by one possible output, which consists of a total of 13 output screenshots.

//CaseStudy.cpp
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <list>
#include <algorithm>
#include <cstdlib>
#include <iomanip>

using namespace std;
// The following is an itoa function for Linux users
// from the website www.jb.man.ac.uk/~slowe/cpp/itoa.html
// The author is Robert Jan Schaper
char* itoa(int val, int base)
{
	static char buf[32] = {0};
	int i = 30;
	for(; val && i--; val /= base)
		buf[i] = "0123456789abcdef"[val % base];
	return &buf[i + 1];
}

enum
ReadingStatus {ReadingSessional1, ReadingSessional2, ReadingPractical1,
ReadingPractical2, ReadingPresentation};

class Marks
{
	// Metadata about Marks
	public:
	static ReadingStatus Status;
	static char Sessional1Entered;
	static char Sessional2Entered;
	static char Practical1Entered;
	static char Practical2Entered;
	static char PresentationEntered;
	static string FileName;
	static string Subject;
	static int Year;
	static void GetMetaData();
	// Normal Data
	private:
	int RollNo;
	int Sessional1;
	int Sessional2;
	int Practical1;
	int Practical2;
	int Presentation;
	static int CurrentRollNo;
	public:
	Marks() : RollNo(0)
	{ };
	friend istream & operator >>(istream &TempIn, Marks &TempMarks)
	{
		cout << "\n Enter marks for roll number" << TempMarks.RollNo << " ";
		if(Status == ReadingSessional1)
			TempIn >> TempMarks.Sessional1;
	}
