
Once you have the program decomposed with a top-down design, then you can begin to code it. To get started, this is a great point to take the pseudocode you've been generating and convert each step into a comment, generating comments for each section. Comments will help guide your code, and provide an explanation for the purpose of each part of the code, both during and after writing the code itself.

Considering the tree hierarchy, the root node becomes the overall comment for the program (2). The next level, the children of the root, each get their own comment. Because these are at the higher levels of the hierarchy and will be major sections, it can make sense to designate them in some way that makes them stand-out—for example, using asterisks (a).

Then, you can divide this into the next level down. Again, you convert each node into a new comment. In this case you can use a few asterisks to show that these are not the most basic levels of the hierarchy (b).

Then, you can go from there to even the next level down, converting nodes to comments (c).

Each of these is still pretty self-explanatory. Once you've done this for your whole program, it's time to start writing code.

```
1 // Program Fragment 11_1c
2 // Program to Predict Electricity Usage
3 #include <iostream>
4 #include <vector>
5 #include <fstream>
6 #include <string>
7 using namespace std;
8
9 int main() {
10 /** Read Past Data *****/
11 /** Read Electricity Data ***/
12 /* Open File */
13 /* Loop Through All Lines /
14 /* Store Data and Metering in Parallel Vectors */
15
16 /** Read Past Weather Data ***/
17
18 /** Read Past Individual Schedule ***/
19
20 ***** Get Detail To Predict *****/
22
23
24 ***** Calculate Predicted Usage *****/
25
26
27 ***** Present Prediction *****/
28
29 }
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_126_0.png)

## INCREMENTAL DEVELOPMENT

When you develop software, you want to construct the software piece by piece, and as each piece put into place, you want to ensure that you have a stable structure—something that is not complete but will operate just fine. You will be able to see that each piece works and is tested as you go along. And if you find that everything's not working, you can take one step back and return to a stable piece of software.

This is why you should use an incremental development approach, in which you code a little, until you are confident that everything up to that point is working, code a little more, and so on. Now you will be confident in what you have already.

Unfortunately when programmers—even experienced ones—construct a larger piece of software, they will write lots of code, and only at the end, they think they have all the pieces in place, do try to test it. If everything actually works, it's extremely rare to have it right. Instead, somewhere along the way, the made a mistake, and the entire program falls apart. Trying to find that one mistake is difficult, and sometimes even after fixing that, there's some other mistake, and you can't figure out if they fixed a problem or not.

In this case, it's OK to design your entire program top-down and write out the comments for each part ahead of. But when it comes to coding, you want to write code that you want to implement a small chunk and test what you've verified. Generally, this means you'll have to write code in a sequential order, once you start writing functions, and you'll have exactly to be the case.

In this example, the first section you encounter is part of reading past data, where you will read the past electricity data and where you went to open the file (d). That means you declare an ifstream (13) and then open it for input (14). Notice that you also write a line of code to close it (17).

| 1 // Program Fragment 11_1_d |
| 2 // Program to Predict Electricity Usage |
| 3 #include <iostream> |
| 4 #include <vector> |
| 5 #include <fstream> |
| 6 #include <string> |
| 7 using namespace std; |
| 8 |
| 9 int main() { |
| 10 /** Read Past Data *** |
| 11 /** Read Electricity Data ***/ |
| 12 /* Open File */ |
| 13 ifstream electricfile; |
| 14 electricfile.open("MeterReadings.dat", |
| 15 fstream::in); |
| 16 /* Loop Through All Lines */ |
| 17 /* Store Date and Meter Reading in Parallel |
| 18 Vectors */ |
| 19 electricfile.close(); |
| 20 /** Read Weather Data *** |
| 21 /** Read Past Individual Schedule *** |
| 22 |
| 23 |
| 24 ***** Get Detail To Predict *****/ |
| 25 |
| 26 |
| 27 |
| 28 |
| 29 |
| 30 ***** Calculate Predicted Usage *****/ |
| 31 |
| 32 ***** Present Prediction *****/ |
| 33 }

Incremental development is a critical part of developing large software. It's almost impossible to develop large programs without it.

After writing this, before going on to the next section, you want to stop and test what you have, making sure that you don't have a typo or some statement incorrectly formatted.

Once that's done, it's time to write and check your next section—looping through all the lines of the program (e).

In this case, you'll assume that the file consists of lines, each of which is a date given by a string and a meter reading given by an integer. So, to loop through all the lines in the file, you'll need to have 2 variables, labeled date (16) and meter (17). You'll try to read them in from the file (18) and loop until you've reached the end of the file (19). Inside the loop, you'll read the next line (22).

Also inside the loop, you'll have want to happen each time, which is to add the date and reading to vectors (20). But you're not going to write that yet; you'll test what you have so far.

To test that, you could put in some output statements to show what you read in each line. That's better than nothing, but another option that's available using the debugger.

```
// Program Fragment 11_1_e
// Program to Predict Electricity Usage
#include <iostream>
#include <vector>
#include <fstream>
#include <string>
using namespace std;

int main() {
    **** Read Past Data ****
    *** Read Past Electricity Data ***/
    /* Open File */
    fstream electricfile;
    electricfile.open("MeterReadings.dat", fstream::);
    /* Loop Through All Lines */
    string date;
    int meter;
    electricfile >> date >> meter;
    while (electricfile.get()) {
        /* Store Date and Meter Reading in Parallel Vectors */
        electricfile >> date >> meter;
    }
    electricfile.close();
}
*** Read Past Weather Data ***/
*** Read Past Individual Schedule ***/\n***** Get Detail To Predict *****/

***** Calculate Predicted Usage *****/

***** Present Prediction *****/
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_128_0.png)

## DEBUGGER TOOL

An IDE makes it easy to access and use the debugger tool. There are other debuggers, by far the easiest to use those included within an IDE. One in Visual Studio is used here.

As you work to develop larger programs, having the use of an IDE can be critical to helping examine the state of the program as it progresses, making sure that the program is working as intended.

Unfortunately, a debugger is not a tool that takes the bugs out of your program. In fact, a debugger that lets you step through a program's instructions one at a time and examine the state of everything in the program at that point.

A breakpoint is a point in the code where you want to stop the execution, so that you can examine the code more closely. When you run a program in the debugger, it'll just like expect until you hit a breakpoint. The execution will pause just before the line where the breakpoint is. a "break", not a line that gets executed. If you don't have a breakpoint set, the code will just run all the way through. That's what you've seen until now.

In Visual Studio, to set a breakpoint, you click on the area farthest to the left for the line where you want to set.

If you set a breakpoint at the first count statement, this puts a red circle at that line.(In Xcode, you just click on the vertical area of line code and a blue marker appears to show the breakpoint).

Debuggers have many tools within them that can help developers examine their code closely. But there just a few simple parts are enough to make a debugger really useful, and even if you need every feature of the debugger, these would still account for 90% of what you've ever done. These features are breakpoints, the Step Over and Step Into operations, and variable values.

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_129_0.png)

In order to use a debugger, the code must be compiled in what's called debugger mode, which adds some extra stuff in automatically that lets the debugger work. But this mode also makes the code less efficient than it will be when fully debugged and then compiled in more efficient release mode.

Because most development is done in debug mode, that's the default mode for compiling in both Visual Studio and Xcode.

Lecture 11 | Top-Down Design and Using a C++ Debugger
