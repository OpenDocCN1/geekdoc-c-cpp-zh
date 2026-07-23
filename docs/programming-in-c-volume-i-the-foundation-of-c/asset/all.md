![](cover.jpeg)

Programming in C++

### Dontae M. Grose II

![](images/00001.jpeg)

Publishing Date: August 20th, 2017

Table of Contents

Chapter 1: Input, Output, and Information …………… Page 4

1.1)The Programming Environment …………………… Page 4

1.2)Program Structure and Layout …………………….. Page 8

1.3)Output and Input  ………………………………...... Page 11

1.4)Variables …………………..................................... Page 15

1.5)Mathematics and C++ ………………………...…. Page 20

1.6)Arrays …………...…………...…………………… Page 24

Chapter 2: Data and Structure ……………................. Page 30

2.1)Function Declaration …………………................... Page 30

2.2)Variable Scope and Prototyping ………………….. Page 36

2.3)Memory Addresses andPointers  ………………..... Page 42

2.4)Classes I …………………...................................... Page 44

2.5)Classes II (Classes with Functions) ………………. Page 46

Chapter 3: Algorithms and Logic …………………........ Page 49

3.1)The If and If-Else statements …………………….. Page 49

3.2)Switches …………………...................................... Page 53

3.3)Loops I (The While Loop and For Loop) ………… Page 56

Chapter 4: Files, Namespaces, and Libraries …...…...... Page 62

4.1)Namespace’s and Libraries …………………......... Page 62

4.2)File Reading and Manipulation ………………..…. Page 64

## Answer Key…………………....…………...…..………… Page 67

Chapter 1

Chapter 1.1

The Programming Environment

To begin programming in c++ we need to first download the graphical user interface (GUI) that we will be using to write our code in. The best programming environment for c++ is called Codeblocks and can be downloaded for free. While there are other programming environments you may also use, Codeblocks will be the easiest to learn at first and create for an easier transition to other GUI and software. One of the largest environments used to program is Microsoft Visual Studio which is for experienced users and once you learn the foundation of programming you should feel free to download this software and use that instead of CodeBlocks.

Graphical User interfaces serve as the main component in writing any computer code. Because GUI is the way data is represented to users, giving programmers a platform to code on as well as visually see projects. CodeBlocks is a free graphical user interface that we will be using throughout this book because everyone can download this software and because it is ‘in my opinion’ the best free graphical user interface. Ensuring that you know how to use this software because when issues arrive this knowledge will become primary in problem solving. As mentioned earlier you do not have to use Codeblocks but I would high recommend it to anyone who is completely new to programming. When downloading CodeBlocks we need to make sure that we are downloading the correct version for the correct operating system that you are currently running. This is huge as Codeblocks can be a very touchy piece of software, again, just take some time to familiarize with the software before entering the code of chapter 1\.

Another thing to note when downloading CodeBlocks is that we need to run over code and test it. We also need something that will do this for us and that is called the compiler. The compiler that CodeBlocks uses its built into the software which is a huge plus, but we should make sure that we click on the correct download link that includes this compiler. The download link will have the words “mingw” in the link somewhere and will include the GNU GCC Compiler that we need to run our code. Going through the installation of CodeBlocks make sure to read instructions carefully and you will be asked again what compiler you want to use during the installation process; In which you will of course choose the GNU GCC Compiler. Once you are done installing the program you will get the home screen of CodeBlocks where we can now begin to write our code.       

From the home screen of CodeBlocks click on the “create a new project” sub-link, next you will be presented with a dialog box that say’s “New from template” as the title of the window. From here click “Projects” on the left side of the dialog box and then “console application” on the windows to the right. You will then be asked if you are programming in C or C++ and while you know we are using C++, C isn’t that much different and if you want to learn that as well the transition from C++ to C will be very easy to do. Next, we simply need to name our project and pick that place for our project folder to be saved. Lastly, we choose our “GNU GCC Compiler”, make sure the “Create Dialog Configuration” box is checked and that the “Create release configuration”, is unchecked.

Once you click finish you are finally done setting up CodeBlocks and now have an environment to program and code as we wish. But we still should go over all the different buttons that are everywhere, which I will be glad to tell you that most of the features, most of which will not be used, but will later become apparent of their use. Later if you decide to continue to use CodeBlocks you will see that there are tons of plugins for different types of programming that can be done. For now, all we will use are the “management” tab on the left side of the software, if you do not see the management tab on the left side of the screen press “Shift+F2” and that will open that management tab, we will also need to be familiar with the file and build tabs on the top of the Codeblocks menu. File is where we will go to save, open, and close CodeBlocks and build is where will tell Codeblocks to compile and run our code. For example, Going to File > new > Project, will bring us back to the original screen of CodeBlocks where we can create a different project. You can have several projects open at once in CodeBlocks which is the reason for the management tab on the left side of the screen.

Navigating to the ‘build’ tab you will see the dropdown list that allows us to run and build or project using the compiler that we have previously installed. When we are running our programs, we will be using the “build and run” button (Shift F9) to build our program (resend it to the compiler) and run the program, which outs the program result. If you look down onto the code editor you will see a bit of code already inserted into it. Navigate to build and run, and run this program to see its result, and make sure you have everything installed correctly. You will get the console window that most of our code will appear in (until defined differently) saying “Hello World” by default. This is the first program that we have ran and the first program most programmers run when they are learning any programming language.

After you have navigated through CodeBlocks and are generally familiar with everything, navigate to the folder where your program was saved previously. If you cannot find this folder, save it again to a parent folder that will hold all your programs of somewhere that you can easily navigate. Open the folder that contains the program that you saved and you will notice that there are two folders within the program folder along with 3 other files. You should have a folder called ‘bin’ and a folder called ‘obj’ these folders are for the compiler and will be used later. You will also have the Project file used which is what you will click on when you are opening the project in CodeBlocks. You may see the CodeBlocks icon next to the project file and you can use this as a reference when you want to open a program that you have in a folder. Lastly there is the main source .cpp file which is a file that contains the c++ code. The reason of this file is to store the code if you want to use it somewhere else, are sending it to someone, and if you use a different software such as visual studio, down the road, you can easily transfer code back and forth from each platform. This brings us back into c++ being an object orientated programming language which allows for rearrangement and the reuse of functions that are previously created. Unlike some different languages which are proprietary to the program they are made for and must be highly modified to use in other programming environments.

Although I am using CodeBlocks as the software to program in; you are free to use any software that you want. There are tons of great software to download as well as amazing IDE’s out there and you are free to try other programs as they may suit you better. The reason that I primarily chose CodeBlocks is because it is a simple to use software that is only aimed towards writing c, c#, and c++ code while almost all other programs focus on the use of all programming languages. With this IDE, we do not have to worry too much about all the different buttons and settings that are for other programming languages, and rather we can focus just on c++ programming script and the functions of the language. This will make for a much easier transition as you go onto using other pieces of software that are more dynamic and have more options such as application creation, platform integration, as well as allow you to write in several different languages, create databases, and much more.

In the real world, different companies use tons and I do mean tons of different types of programming environments so I guess the versatility of being able to use multiple environments can be beneficial but that comes will time. But after you learn how to write the code the job of leaning the software and other programming languages will become easier because of the similarities between IDE and code implementation; the only real thing that changes when you are writing in a different programming language is the syntax of statements and functions. And the only thing that changes when you go from one IDE to another is the face that some allow for more versatility and options like Visual Studio and others IDE’s like CodeBlocks are used to create programs that usually do not display graphics but rather run and implement tasks in the background.

Chapter 1.2

Program Structure and Layout

Every programming language has a specific defined syntax that it uses to define its code. Syntax is just a way of structuring the code so that it has a clear outline and can be read by other programmers if needed. Most programs are built by teams of people so most of the traits that C++ offers over other programming languages is its ability to move the code from place to place with ease. Regarding to the syntax of the language almost every command in c++ will end with a semicolon (;) which tells the compiler that the command is defined and defines the end of the command.

The first two lines of code, #include <iostream> and ‘using namespace std’ are static throughout most of c++ programming, as well as the, int main () {}, function that will serve as the key to the program. Understanding this layout is important and when we build onto it you will understand why.

#include <iostream>, is what we call a header file and the file that we are calling is the iostream header file. The iostream header file is just telling our program that we are going to eventually want our program to output some result or overall goal to the console. Next, we have “using namespace std;”, which is just an easier medium that allows our code to be more structured when we are ready to publish it to whatever market its aimed towards.

After creating a program file, you will see this code written inside the console,

#include <iostream>

using namespace std;

int main (){

return 0; 

                            }

The command return 0;  can be discarded and we have,

#include <iostream>

using namespace std;

int main (){

}

This is what is called the “Main Function” and I say this with much emphasis because it is by far the most used block of code in all c++. Now, first we should understand what a function is in computer programming. A function is usually; besides in the case of the ‘main function’; used to hold a specific set of rules that complete a specific task for the program. The main function is a bit different because it not only can hold its own information but it also must know of every other function in the program. No matter what we are doing we will always end back to the main function to call that function which is something we will go over in chapter 2 when creating multiple functions other than the main function. But this is the reason that the main function is needed. You can think of the main function as the CPU on a PC’s motherboard, it handles the tasks that the computer needs but it uses the hard-drive (or in this case) other functions to hold the information until it needs to be accessed. The ‘int’ part of the code is known as the return value/type that the function which will be explained later again when we go over functions in chapter 2\.

After that we see two parentheses and body quotes closing with a semicolon, which if you remember, signifies the end to the main function. The set of parentheses after ‘main()’ are called parameters and are used to hold specific conditions that a function can take. The ‘main’ function does not need any parameters now. Lastly, we should body quotes {}; which are going to hold all the information for the main function. Any main function command will be written inside of these braces which are better known as the block of code that all functions by a semicolon. Now that there is a layout of the configuration that we will be using, we can begin to learn about how memory is stored on computers and how software and programs deal with the things that it has been programmed to remember.

With a blank screen with little to no code we have a long way to go until we reach the point where we can say we have developed a c++ program. In any source of computing storage is essential. Not only do you need it for music and games but it is also what holds the operating system and literally all other information that PC needs to run. We should consider that we have an empty programming environment and the only thing that it will be able to do are the things that we program it to do.

Chapter 1.3

Output and Input

When we ran our first program and we see the message “Hello World!” on the screen we should have realized two things. 1) The code with the writing in it should be able to be changed and 2) The cout << operator is since way of outputting messages to the user. If this was your assumption or you tried changing the text in the program then you are steps ahead. But what we need to output anything to the user is the cout command that is followed by the << symbol that signifies output.

In the line of code for output of text,

cout << “Hello World!” << endl;

We see that there are essentially 4 pieces of information. The command ‘cout’ means console output and is used to output all information that we are presenting to the user. This is how we will present data so that it is visible in the in the console and is used for sentences as well as numbers, expressions, formulas, and more. Next, we see two less than symbols <<, these are used to signify data going out to the user. Similarly, we can also see that if we had to greater than signs >> we would be signifying data entering the program from somewhere else. I may also refer to them as left and right logical operators.

Next, we have the text part of the code “Hello World!” which is called a string and strings are variable types or as you can see in this case they can be stated explicitly. This text again could be changed to anything else. Here is an example of a string output program using variables as we learned earlier.

#include <iostream>

Using namespace std;

int main(){

string mySentence = “Save this string of text”;

cout << mySentence << endl;

}

Here is another example of the same program without storing the string in a variable.

#include <iostream>

Using namespace std;

int main(){

cout << “Save this string of text” << endl;

}

These two ways of outputting text to the user. But which way should this be implemented? The key here is to remember that we will use variables all the time for several different functions if not in every single function. Get used to coding the first way and you will be better off as this will help you process how variables are called and how variables are used. While Strings are important for communicating data we also need to communicate or output numerical data to the user. An example would be if we were creating an arcade game that had health, life’s, and levels we would need to communicate the numbers associated with each of these variables. To output numbers to the user we remove the parentheses and we write the number as,

cout << 32 << endl;

We have the same output operator of course but we write a number, instead of a string of text. Although you could also write numbers inside a string if the syntax was correct, it’s just usually not good programming to do that. So now that we know how to call and use variables with system/console output; write a program to do the following,

Problem) 1) Write a program that remembers your name, address, city, State, and zip code.

   2) Have the program output that information to the screen.

By this time with the concepts that we have went over there are tons of different programs that we can make. I encourage you to try and create your own programs and save them in a folder, attempt all of them challenge problems and attempt to create your own programs along the way. Something that cannot be overlooked is that we are programming using a language and the only way to learn any language is the repeat, repeat, repeat. At the end of the day, the more effort that you put in the better results you will get, so make sure to go the extra mile and if you are not understanding something, search it on google and try to find the solution. If you cannot find the solution, write down the problem you are having, move on, and go back to the issue later.

In all computer programming, and extra amount of attention must be payed to syntax, spelling, capitalization, and ALL other problems. Something as simple as a letter being lowercase when it’s supposed to be uppercase will cause the whole program to fail and in some cases the program will not run at all with issues as small as this. I am not expressing this fact to try and scare you away from programming I am just expressing the fact that programming is very specific and must be very precise as well.

When someone opens your program, you want to have some way of greeting them into the program as well as ways to express what the program can do. They only way you can do this is to output text to the user and hope he/she reads this content and decide based on the options you have given them. But what happens when we want the user to enter some information or what happens when the user presses a button and expects that button to change or have some effect on the program. This is a situation in which we will need an operator that can be used to take in information. For inputting information to the user, we use the input operator which has the syntax,

cin >> variable;

The code ‘cin’ stands for console input and is the main operator in the line of code. Followed are the >> two greater than signs that show the flow of information into the PC. Lastly, we declare a variable which serves as a container for the information that is stored. Be careful as there are different variable types that are used to store different types of information which we will go over in the next section in full detail. For now, understand that we use variables to store information and these variables can be used along with input operators to store information that the users enter.

Knowing how to display output to the screen that the user can read and needing the user to enter information into your program are almost always going to play some role in your program. Going over and understanding how to do this is essential so practicing input and output is very important.

Chapter 1.4

Variables

In programming, we should store information and for that we use variables. That is the only job of a variable and when building any program in any language you will use variables to perform this same operation. Before we continue here is the list of the most common variables and their functions.

| Variable Type (Abbr.) | Example | Definition |
| Integer (int) | int x=5; | Used to hold numbers that are of integer value. |
| Float | Float u = 213.1234; | Stores decimal numbers |
| Double | Double c = 9.1234; | Stores decimal numbers |
| String | String  y= “NUMBERS”; | Stores words, letters, and phrases. |
| Character (char) | Char message = ‘a’; | Stores a single character |
| Boolean Variable (True/False) | Bool t = False; | Can only be true or false. |
| Constant (const) | Const int x = 10 | A variable that can never change. |

Those are the most common types of variables that are used in c++ and define what certain variables can hold. For example, in the table above you can see that if we want to store an integer we use int as our variable and if we want to define or store a number that is a decimal we use float or double. This is because we should use different types of variables depending on the information that is stored in the variable. Here is an example of how the float and integer variables are used,

int main (){

float x = 3.14;

int y = 4;

}

When we declare a variable, we need the data type which is (float, int, etc.…), and we also need to give our variable a name. The name can be anything string of text that you decide as you can see I used ‘x’ for the name of the float variable and ‘y’ for the name of the integer variable. And then we set the variable equal to the value that we are giving the variable using the equal sign (=). You can’t set the name of a variable to a number.

For example,

Float 3 = 5; , Would not work and would cause an error.

Now we have two variables that are assigned correct values, what can we do with these variables? The answer is that we can do several things with these values but we will start with how these variables can be used to perform several types of operations. The best thing to do so that you remember all the different variables is to write out the code using the different variable types and giving each variable a unique name.

Challenge Problem: Even though input can be pretty straight forward create a few programs that,

1) Create a program that asks the user to enter 3 integers and 3 decimals that are then stored in 6 variables.

2) Output those variables to the screen each on a different line.

Debugging

Having to debug your program is not only something that will inevitably happen it is also a skill and can only be learned through reading code and practicing the different uses of the code. But some problems are seen easily by the compiler and of almost all programming environments will have a built-in debugger that will detect syntax errors that are in the program upon running the program. You can see the debugger easily on the bottom of the CodeBlocks screen by clicking the “build log” tab. When you run your program the build log tab will show you what programs are being called and what is exactly executing when you are building and running your program. If also will detect errors as I said earlier that you have made within your code that are fundamentally wrong such as grammar, spelling, or syntax errors but it will not fix your program for you. It is important to read the build log and become familiar with what it says is wrong when you do have errors.

For example, If I make the mistake of calling a variable that doesn’t not exist such as writing something like this,

1)Float x = x + y;

2)Cin >> x;

3)Cin >> y;

4)Cout << r << endl;

Here you can see that the problem exists on line 4 where I accidentally tried to output the result of ‘r’ when I meant to type ‘x’. This program will not run because there is no variable named r and the build log will read something like,

Error: ‘r’ was not declared in this scope

This is probably the most important build log message that there is as you will get this message many times throughout your programming career. The message simple means that the variable was either never created or it’s not a public variable (in Public Scope) and therefore cannot be used because to the function that is was called in, it does not exist. This problem the main reason that most programmers declare their variables using this little trick.

Float newVariable;

As you can see the first word in the variable name is lower case and the second word in the name of the variable is upper case. This is something that you probably want to do when programming so that you do not have capitalization errors when you are creating variables, functions, classes, or anything else that need reference in c++. Anytime you have an error remember to first reference what the build log says and second look for flaws in the program. But the program may not notice some of the problems that you are having and that is just simply from programming wrong and the best way to handle that is to use comment where they are needed to reference different parts of your code. Even the best programmers use comments to mark off different parts of their code and again if your friend or someone want to use or buy a function that you have created you can always find it easier if you use comments to sections your code according to the task that is being done.

Understanding how the compiler is reading the program is also very important during this process as you need to understand the in c++ the compiler reads our code from line 1 down. In programming, we use a concept called variables to store information for the program, the programmer, and the users of the program. A variable can be thought of as a storage container for information and there are different types of variables depending on the information you are storing into the variable. Variables are a big part of all programs and they allow for some great programming as they allow programmers to store information for later use and serve as the keystone for any computer program. While the code may not be executed in this exact way depending on your program, the compiler starts at the top and reads downward, meaning if the information is not previously stated in the program, you will not get the correct results. For example, if I try to output a variable x and I use my output operator on line 4 to show to value of x, and the variable x isn’t created until line 6, the program will not know that the variable has not yet been created and therefor will not see the variable.

On the contrary if you move the output operator after line 6, you will be able to see the variable in the output put because the compiler has previous knowledge of the variable and its value. The compiler reads the code line for line and distinguishes what should happen and when it should happen.

Chapter 1.4 Practice Problems

1.4a) Create a program that asks the user to enter 3 integers and 3 decimals.

1.4b) Using the solution for 1.4a, Output variables to the user to enter 5 variables to the user each on its on line.

Chapter 1.5

Mathematics and C++

Math and programming go hand in hand. To be more specific Algebra and programming go hand in hand and are so much alike that I am sure you can see some similar traits already. With equations and formulas within algebra we fight to solve the equation (usually) for one variable, to do that we isolate the variable we want to answer to and set the other values on the other side of the equals sign. In programming, we are doing that same process when we create variables to solve problems and perform tasks within the program.             

Math Operators

Addition:  +

Subtraction: - 

Multiplication: *

Division: /

Modulus: %

Equal to: =

greater than: >

greater than or equal to: >=

less than: <

less than or equal to: <=

Most of these symbols are self-explanatory as I am sure that you are used to seeing them besides maybe the multiplication, division, and modulus symbols. For multiplication we use the as tricks symbol which is usually called by pressing “Shift+8”. The symbol used for division is the forward slash that is usually found below that backspace/delete button on your keyboard. Lastly, we have modulus which means to divide and take only the remainder value of the division. If there is no remainder during division in any case, modulus will be equal to 0\.

To perform a math operation, we need to have at least two different numerical values. To do this we will create two variables that hold two different numbers.

float firstNumber=67;

float secondNumber=34;

cout << firstNumber + secondNumber << endl;

cout << firstNumber % secondNumber << endl;

If you enter this to your program you will see that we get answers for these operations and they work to say the least. But as we start to use math formulas to solve things in our program we will program our variables to perform these calculations instead of stating them during the output process as,

float x = 3.5;

float y = 5.4;

float equationOne= x + y;

float equationTwo=x%y;

cout << “answer: ”<< equationOne << endl;

cout << “answer: ” << equationTwo << endl;

While this way of programming may technically take a few more lines of code. It creates a more efficient process because if I want to use the equation I can just reference to it later. Something else to consider is that we can change the value of a variable any time by writing the variable name and setting it equal to a new value. For example,

Int x = 3;

Cout << x << endl;

x= 6;

cout << x<< endl;

When we create a variable, and set it equal to a specific value such as 3, that variable then comes that value and the value also becomes that variable. When the first console output is running the program will output 3, because the value of ‘x’ is 3\. But in the next line of code you see that the value of the integer ‘x’ is changed to a value of 6\. And this is completely acceptable without re-stating the type of variable we are using because there is only one variable ‘x’. When we output the value of x for the second time, we will get 6\. Changing the value of a variable is useful but is something that you want to make sure is done right and that the value of the variable is known and accounted for at any given time. 

Now that we have went over almost every single aspect of basic programming and you are creating more advanced programs, you will also need more advanced ways to solve programming problems. For this I feel that using mathematics will help you understand more about what it means to create solutions for a computer. Creating solutions for a computer is very important as the solutions are algorithms that set rules for the goal that your program has. Even if you have several different tasks that are happening at one time you will have algorithms running to keep up with the program as the user makes changed.

For example, if we are keeping track of the ammunition that I have in a first-person shooter; I could create a variable that hold some specific number of bullets and then every time the user presses the mouse left-click I could tell that number to decrease by 1, simulating the use of a gun. But how would the algorithm for the ammunition decrease work and how do we know if the user has clicked their left-click on their mouse? These are problems that we need to understand how to handle as operations such as this one is used in every piece of software, every app, and every program. To solve this specific problem, you should understand loops and iterations which is something we will go over later to its full extent.

Using mathematics does not stop with one statement operations. We can use multiple variables and operations, making sure to follow the order of operations, to perform the task of taking in values for variables and then using them to solve algebraic expressions and formulas. For example, we can use the linear equation standard form or the equation for a straight-line y = mx+b , have the user enter their known values, and solve this equation for y.

To do this,

double m,x,b;

cout << “enter the value for m: ” << endl;

cin >> m;

cout << “enter the value for x: ” << endl;

cin >> x;

cout << “enter the value for b:” << endl;

cin >> b;

cout << “y = ” << (m*x) + b;

This would be a solution to the problem stated above saying the we want the user to enter the known value of the line and then we take those value, perform the correct operations, and output the answer to the user. In the last line of code, I used parentheses around the m*x because we want to perform this task first and from that result we add the variable b. In this case the user may also use decimals and because we are using the ‘double’ variable and the answer will be stored accordingly.

Chapter 1.5 Practice Problems

1.5a) Create a program that allows users to enter 5 variables. Take those values and perform addition, subtraction, multiplication, division to those 5 variables entered by the user. Make sure to account for both integer and quotient values. Output the value of each operation back to the user remembering to state each operation followed by the operations value.

1.5b) Create a program that divides 3 numbers by each other that the user enters.

Chapter 1.6

Arrays

In programming, there are so many different options and different categories of programs that all have different that they can be created. In fact, it’s almost impossible to line for line copy someone else in programming if you are writing because the combinations and ways that you can use the code are so abundant. And not only that there are also tons of different industries to program for. For example, do you want to create games? Software? Animations? Apps? Everything? Whatever you want to do you will need to understand the fundamentals of programming and well versed on the uses

Whether you want to create a game or an application for a phone you will be able to do so using c++ and when we are programming this giant piece of software we are going to have several different variables and all of those variables, whatever type they may be, are going to take up tons of memory. With every single variable, you create you are using memory and this means that overtime we will want to find a way to optimize this behavior and make the program run with less stress. The concept of optimization still an issue with computers today and although we have super computers such as D-wave, we have not yet hit an ultimatum in computer technology that appeals memory optimization and it may never happen.

Modern,2017, PC hard drives or hard disks are thick aluminum CD’s (Compact Disks) that are shoved into a metal case to make it look like a piece of hardware. If you didn’t know although they work and store a lot of memory in a small place they are subject to some capacity of gigabytes or terabytes which are still very small when it comes to the statement that we could possibly store an infinite amount of information in some material. If, and, what I believe, when this happens, we will be able to store the information of the universe into one piece of hardware. There will be one hard drive inside of every PC in America and big stocky Rosewill Thor, Prodigy, and corsair will become the equivalent to the Apple I created by Steve Wozniak (If I were to have it on my desk today) and therefor became antique/novelty items. Mind you I am talking about the physical structure of the Apple I and not anything inside of the outer shell. I am probably the biggest Wozniak fan there is, and in the late 1970’s Pc’s were far from being fully developed, thus the reason they didn’t spend much time with the case, as the hardware was the focus and at that point a goal as well.

Arrays are used to store multiple forms of the same data type in a single declaration to reduce not only complication that arises when we have multiple variables of the same type; but also, to make it easier to use these variables when they are needed in a program. The Syntax for an integer array is,

Int array[3] = {4,5,6};

This integer array holds 3 integer values that are 4,5, and 6\. We could also create a string array by simply changing the array memory type.

string x[3] = {“this”, “array”, “is a string ”};

Here we have a string array that holds three different values and each value is contained within double parentheses, separated by a comma, and held inside of braces. But now let’s say that we need to access one of these variables (as that is the point of storing a variable, to use it more than once); but in an array, we have to call our variable different than when we are calling a single stored variable. Since we have a single element ‘x’ that holds three different elements, we need a way to access a single element if need be and this is done by applying placement values to each element. Each element has its own number and this will be consistent for any array that you create. The first item in an array is referred to as element 0 and should be called as,

cout << “The first array element: ” << x[0] << endl;

This will output the first element of the array x, which is the string value “this”. The second value in an array is referred to as element 1, and the third element is called element 2\. So, no matter how many elements in the array, the elements will always be called (starting from 0), and counting upwards. In almost every concept in programming or computer science we will have a significance with the number 0 and it is almost always accounted for which is the opposite of modern mathematics which teaches us that the number 0 is obsolete for the most part, so keep this  in mind as we move on into other topics that we start counting at 0 and not 1\.

Now we should consider a topic known as the multidimensional array which are arrays that are often used to create tables of variables.

type Name[x][y] = { {Row 1’s values}, {Row 2’s values} };

This is  syntax for a multidimensional array and if you want to see this in a practical example,

int Multiarray[2][3] = { {23,3,6}, {56,23,80}};

So then when we need an element we call it using the multidimensional parameters. But the thing to understand is that position ‘x’ is the declaration of how many rows we want our array to hold and the position ‘y’ is how many elements are stored in each array.

To access each element in each row of the multidimensional array we need to use the first set of brackets after the name of the variable ( [x] ) to say what row we are using, but just as we learned earlier we should start at zero when counting, so when we want to call an element in row 1, we say,

cout << Multiarray[0][y];      // the first set of brackets implies we are accessing row 1

cout << Multiarray[1][y]; // the first set of brackets implies we are accessing row 2

The second set of brackets in the multidimensional array are used to specify which element in the array that we want to call, again starting at 0\. To print out every element in row 1 and 2 of  the multiarray variable we have,

#include <iostream>

using namespace std;

int main(){

int Multiarray[2][3] = {{23,3,6},{56,23,80}};

// Printing elements in row 1

cout << “Row 1, Element 1: ”<< Multiarray[0][0] << endl;

cout << “Row 1, Element 2: ”<< Multiarray[0][1] << endl;

cout << “Row 1, Element 3: ”<< Multiarray[0][2] << endl;

// Printing elements in row 2

cout << “Row 2, Element 1: ” << Multiarray[1][0] << endl;

cout << “Row 2, Element 2: ” << Multiarray[1][1] << endl;

cout << “Row 2, Element 3: ” << Multiarray[1][2] << endl;

}

Here is another example of a different multidimensional array.

#include <iostream>

using namespace std;

int main(){

int mul[2][3] = { {23,234,5},{768,965,3456} };

// Outputting the elements in row 1

cout <<  "Row 1, Element 1: " << mul[0][0] << endl;

cout <<  "Row 1, Element 2: " << mul[0][1] << endl;

cout <<  "Row 1, Element 3: " << mul[0][2] << endl << endl;

// Outputting the elements in row 2

cout << "Row 2, Element 1: " << mul[1][0] << endl;

cout << "Row 2, Element 2: " << mul[1][1] << endl;

cout << "Row 2, Element 3: " << mul[1][2] << endl;

}

We can also create multidimensional arrays of all other data types to store information in this way such as strings.

#include <iostream>

using namespace std;

int main(){

string SArray[2][5] = {

{"one","two","three","four", "five"},

{"six","seven","eight","nine","ten"}

};

// Elements in Row 1

cout << "Row 1, Element 1: " << SArray[0][0] << endl;

cout << "Row 1, Element 2: " << SArray[0][1] << endl;

cout << "Row 1, Element 3: " << SArray[0][2] << endl;

cout << "Row 1, Element 4: " << SArray[0][3] << endl;

cout << "Row 1, Element 5: " << SArray[0][4] << endl << endl;

// Elements in Row 1

cout << "Row 2, Element 1: " << SArray[1][0] << endl;

cout << "Row 2, Element 2: " << SArray[1][1] << endl;

cout << "Row 2, Element 3: " << SArray[1][2] << endl;

cout << "Row 2, Element 4: " << SArray[1][3] << endl;

cout << "Row 2, Element 5: " << SArray[1][4] << endl;

}

Chapter 1.6 Practice Problems

1.6a) Create three arrays each of a different data type. Output each variable one by one (Each on a separate line).

1.6b) Create a program that asks the user to enter three values and store each value that the user enters in an array. Output/print the values that the user has entered back to the program

1.6c) Create three arrays, each with a different variable type and output each value in all 3 arrays.

# Chapter 2: Functions

# Chapter 2.1: Function Declaration

When creating a program there are tons of different tasks and processes that are running at any point in time. For each of these tasks that our program has we should have a certain set of rules that the task follows to run properly. This is where functions come into programming and this is what also makes them so useful. We can take our different processes, break them into different groups, and define the solutions for each process while also having them separated to make them separate groups that make them easier to work on.

The main function is the only function that we have worked in so far but now we will be creating a new function that will be used to perform a specific task to the overall program. So before actually taking on the task of making a program we should create an outline of all the different tasks that will need to be performed. For example, if we are creating a function to create a program that can solve an equation, of the form  x -2(x+1)=0\. The first thing we must do is create an output/input system that is in place to ask the user to enter that data needed for this program. But what data is needed? We can see that for this specific equation we are only dealing with on variable. In solving for an equation of one variable, we need to isolate the variable to one side of the equation OR know that value of that variable and simply plug it into the equation to see if the result is true. Since we do not know the value of ‘x’ and we want to user to input this information, we need to create a variable that can be used to store the users inputted value for x. To do this we need to create a float or double variable that way if the user enters a fraction or decimal the program will answer the problem correctly. And we also need to prompt the user to enter the information.

We will start the creation of this program using a function that will perform the input/output tasks and returns the answer to the user. The syntax for a function is,

functionType  functionName(){}

The ‘Function Type’ that is used is defined by the return type of the function. The main function we use ‘int’ which defines that we are returning something to the user in this function. The other function return type that we will be using is the return type ‘void’ which indicates a blank return type meaning we are not returning anything directly to the user during this function. Next, we have the name of the function which is defined just as variable names are meaning that you can use any name for the function that you wish. We have empty parameters for now and an empty body block that we will writing the commands for this function in.

int equationFunction(){}

With this information create your own function giving it a personal name. Make sure that the function you create is above the main function for now. This is for a specific and rather important reason and that is the fact that when the compiler is reading C++ code (in all cases) it reads the code from top to bottom and if the function was created under the main function then we would have to do something call function prototyping which I feel is better explained directly after this section. After the function is created we must do one more thing which is tell the main function that we have created an additional function. If you remember from earlier I said that no matter what functions we create we will have to call them into the main function for them to run because the main function is the terminal for all other information in the program.

The thing that we must do Is to create something called a function declaration command within the main function. The function declaration will call the function into the program. We can create as many functions as we wish but if they are not prototyped the function will not be called for use in the program as it runs. The syntax for creating an object is,

FunctionName();

All we should write inside the main function for it to run the function that we have created recently is write the name of the function created and the parameters if there are any, if not leave them empty, and lastly a semicolon to signify the end of the object declaration. We should now have two functions 1) The main function and 2) the new function we just created and 3) the object for the function inside the main function. To make sure that you have the correct code and no errors have occurred, click the re-build button on CodeBlocks next to the ‘build and run’ button and the program will be check for errors. If there are no errors reported in the ‘build messages’ menu on the bottom of CodeBlocks then the program is built right. Here is an example,

#include <iostream>

int equationFunction(){

cout << “Is this function is working? ” << endl;

}

int main(){

equationFunction();

}

Note: You can create lines of code that are called comments and that does not affect the program in any way other than to server as comments for certain lines of code. To use a commend we type two forward slashed followed by the commend that you want to write.  For example,

int main(){

equationFunction(); // This is a comment

}

If you run this program you will see there are no errors and that this text is completely ignored by the program. We can also use /*   */  to create multi line comments.

Inside the function that we created earlier write a console output line of code that simply shows the user a message on the screen to see the function and function declaration work. When we call a function to the main() function we are simply saying that we have created a function in our program that we now want to use.                Functions will make it easier read your code and when other programmers read your code they will be able to define the elements of the program more efficiently. Also, when we create these huge programs with several different elements and multiple lines of code it will get harder and harder to manage your code and instead of cramming everything into the main function (while it would work), using functions is astronomically more efficient.

Now in the previous example we created a function that came before the main() function. What happens if we move the function below the main function and call it? You will get the compiler error that says to the compiler newFunction(); was not declared in the scope and will result in the program failing. To stop this from happening when you do create functions that are below your main(); function, is to do something called function prototyping.

In functions, we use parameters sometimes to specify certain variables that the class will be working with. This can be useful in tons of different ways when we are creating functions and allows us to further define a function and give it its own personal traits, as well as serve as a template for the function. Here is an example of a function with parameters,

#include <iostream>

using namespace std;

int function1(int x, int y){

cout << "x: " << x << endl;

cout << "y: " << y << endl;

}

int main(){

function1(3,2);

}

Here we have created an integer function with two parameters, integer x and integer y, and inside of this function we output each variables value. But the integer values are not given any values so we know that somehow these variables, to be printed to the screen, must be given a value. To do this, we call the function that we want to use into our main function and inside of the parameters set for that function we declare the values that we want to assign to each variable, each value separated by a comma.

Now we must talk about a topic in c++ called ‘recursion’ which happens when a function or loop calls itself. Recursion happens when you call a function inside of itself instead of calling the function inside of a different function. This looks like,

#include <iostream>

using namespace std;

int functionRecursion(){

cout << “recursion example ” << endl;

functionRecursion();

}

int main(){

functionRecursion();

}

Since we call the function ‘functionRecursion’ inside of itself the program and we called the function in main, when we run the program the ‘main’ function will call the ‘functionRecursion’ function, and the ‘functionRecursion’ function calls itself. This process will never stop if it happens so it’s important to remember not to call a function inside of itself. This process of recursion is known as creating a recursive function and while it can be useful to use it sometimes, most of the time this will create problems within your programs. Later, the thought of a recursive function will become more relevant and you will see why these functions can be useful in some special cases. We will go over what a loop is and how we can create loops the call functions a specific number of times which will tie into the thought of recursion and recursive functions.

Chapter 2.1 Practice Problems

2.1a) Create a function that has at least five lines of code, with at least one of which should be an output operator into the main function.

2.1b) Create a function, write any code in it that you want to, make sure it is under the main function, prototype the function, and call the function.

2.1c) Create three functions under the main function that work together to solve the calculation: x=7+(23/6)+(A+B), for the variable x. Allow the user to enter quotients if needed for variables A and B.

Chapter 2.2

Function Prototyping

If we create a function that is below the main() function we need to do something called function prototyping to remind the compiler that this function exists. Now what you are probably think why do I need to create functions below my main function in the first place? Can’t I just keep the main() function at the bottom of my code to avoid function prototyping? And the answer is that you may never need to create a function below the main function but know how to do it if you do need it always is a plus. To do this we write the function-type followed by the name of the function, but we write it under the ’ #using namespace std;’ but above any function or class in the program. This can be shown as,

#include <iostream>

Using namespace std;

void callingFunctions();

int main(){

callingFunctions();

}

void callingFunctions(){

cout << “hello” << endl;

}

Notice the prototype, on line 3, includes the type function as well as the name of the function, as this is a problem that occurs often and will create moments of despair when you are debugging your program to find out that you did not include the data type for a function prototype. Function prototyping is something that I think is the most redundant part of programming as it can be hard to remember sometimes so just make sure to practice this a lot to understand it to its full extent. What I do is I create the prototype for my functions as soon as the function is created and this way you don’t have to worry about the object later and you can also just make a specific list of the prototypes to make it even easier to manage.

Function prototyping is something that you want to get used to doing now. Later, almost all the functions that you use, both personally and in a workplace. When there are several functions it’s better to leave your main function on the top so that it can be easily referenced, but if you really wanted to you could just write every function above the main function.

Variables also have something that must considered which is called the variable scope. Variable scope is where the variable is used within the program and the different types of scope include global scope and private scope. When a variable has a global scope, it can be used in all the functions in a program. As you remember we are just using one function at this point (the main function) and we have been writing all our variables in the main function but we can also write our variables outside of the main function, these are called the global variables because they have global scope.

Global Scope, 

#include <iostream>

using namespace std;

int globalVariable = 5;

class VariableScope{

    public:

    int VS1(){

        int localVariable = 10;

    }

};

int main (){

    VariableScope VSobj;

    VSobj.VS1();

}

Here we can see how to use both a local variable and a global variable. Notice and understand the difference between creating these variables. The next type of scope that there is; is called private scope and is what we have been using when we declare the variables inside the main function. These types of variables with private scope can only be used within the main function and if you make another function that tries to use a variable with private scope that is not in that function, will cause an error. While we have not yet gone over how to make a function yet, understanding their use now is important so that as we move along and get into talking about functions, you will have the proper insight into how variables and variable scope work which will make learning to create functions easier.

Also note that you do not have the write the ‘<< endl’ part of the code if you are not writing out multiple lines of code but make sure to add the semicolon at the end the end the line of code. In most examples, I will use endl; as it makes the code easier to read when printing it to the console.

The main key to understanding how programming works and being able to store different formulas, words, and algorithms are a must. In any programming language or environment there will be variables used to store information that either the programmer will use during the process of programming or the user will need when using the program. When can also use variables to store information such as numbers and then we can create different variables that manipulate those variables such as,

float x=4;

float y=5;

float z=6;

float eQ = x+y;

cout << eQ/z << endl;

In the example above we created 3 variables that are used to store 3 different integers and then we use the variable eQ to add two of those numbers together, and finally we output the result of eQ divided by z. This is an example of how we can store variables and use them later in a program to perform operations such as math operations. This concept is something that will be highly utilized as we learn about loops and incrementation.

While creating a variable may seem like something that is constant, it is not. Variables can be changed from their original values by restating the name of the variable and giving the variable a new value. An example of this could be,

float damage = 20.23;

cout << “Current Damage: ” << damage << endl;

damage = damage + 3;

cout << “Current Damage: ” << damage << endl;

Here we create a variable used to store a float value called ‘damage’ and gave it the value 20.23 and simply outputted the value of damage to the user. Next, we restated the variable name of damage and said that we want to take the original value of damage and add 3 to it. So, on the first line of output we will get 20.23 but when we use the variable the second time we will get 23.23 or 20.23 + 3.00\. You can see that during this process we called the variable type, name, and value the first time it was declared but the second time we declared it we only used the variable name along with the new value that it was assigned. This is because we have already stated the variable type when we originally called the variable. The second time we use the variable, the compiler is already aware of the variable type and thus we do not need to state the variable type again. You can now see the inconvenience that would occur if we were to create two variables with the same name.

To understand the concept of variable scope to its full extent, create a function within your program ‘above’ the main function. This will allow us to talk about variable scope and why scope is important to remember when you are using multiple functions. There are two types of scope that we use when we are programming and both have drastic differences.

First, we have public scope, and when we are programming we often use variables that are within a public scope, meaning that the variable can be used within any function that we wish. To make a variable public we only do one thing, and that is put the variable declaration outside of the functions we have created. But remembering from earlier we see that we must put the variable declaration above all other functions because the compiler reads from top to bottom. If we create a variable and it is on top and not inside any other function, it is called a global variable and can be used in any function without causing any problems. To check this statement, simply create a variable and output it inside the main function as well as inside the function you just created. You will see that if the variable is on top of the functions, the variables value will print out without any issues.

But if we take that variable and put it inside one of the functions; then the other function will not notice it and for that reason the debugger will say that the variable that you are asking for is not in its scope. This is what we call a private variable and when private variables are only subject to being used in the function of which they are declared. This allows us to create functions with variables that must same names as well because if the variable is written inside of the function the variable will not be detected in other functions. When we are creating functions its always easier to create some specific set of tasks that the function should complete before ending that way you already know what variables you need and you will hopefully also know if the variables need to be global or private.

After you have created a function, we should also have to remember to call the function inside our ‘main’ function so that our functions run when we run the program. When calling functions, you again, should remember that the order in which the functions are called is the same order in which the functions will be ran. If you do not want to call a function or forget to call the function the program will still run properly, it will just run without that specific function. When we call our functions, we use the function name followed by parentheses or the parameters and a semi-colon to signify the end of the statement. This is called function prototyping which also may referred to as calling a function.

When compilers read your code the start on line 1 and work their way down the lines of code. This is the reason a task like changing the value of a variable can work. It is important to understand what the compiler is thinking to create efficient programs because the compiler is what is reading and checking your code not only for errors but it is also taking the code and trying to represent the program in sync with the user’s chain of command. In any program, you will have several operations and you don’t want these operations to flood the user, you want to allow the user to choose what operations should be called and define the order in which those operations are ran. Without this hierarchy way of programming we would lose all uniformity and our programs would run operations out of order.

Chapter 2.2 Practice Problems

2.2a) Create two global variables and two local variables, that are in a function and output all four variables.

2.2b) Create at least 3 separate functions. Each function should have at least one local variable. Find a unique way to tie these functions together into a single program.

Chapter 2.3

Memory Addresses and Pointers

Memory and Variables

When we need to we can use the ampersand ‘&’ to give us the memory address of a variable. Because as we know variables are held in storage of the program and in certain situations we may want to need to know the memory address which serves as the mail box for each variable. Each mailbox ‘variable’ has an address on it and we can access that address if we use an ampersand pre-variable.

int x = 5;

cout << “memory address: ” << &x << endl;

This code outputs the memory address of the variable x and we can use this technique to output any address to any variable that is within the program.

Challenge Problem:

- Print the memory address of 5 different variables.

Pointers

When we are specifically creating a variable that we want to access the memory address of we use something called a pointer which is accessed by the * sign. So, when we are creating a pointer to point to a memory address we would write something like,

int PointFunction1(){

int *x = &5;

cout << “the memory address of x: ” << *x << endl;

}

int main(){

PointFunction1();

}

Here we have an integer pointer that is named ‘x’ and has the value of the memory address of the number 5\. We can now use our pointer to extract the information stored is the ‘x’ memory storage spot. And we can use multiple pointers in the same section by,

int main(){

int *pointer1, *pointer2;

cout << “Memory Address 1: ” << &pointer1 << endl;

cout << “Memory Address 2: ” << &pointer2 << endl;                            

}

We create pointers to refer to the actual variable and instead of using the physical memory address. When we use certain data types we are asking the computer to set aside a specific amount of memory for that variables to hold. That way we, the programmers, know which data type to use in all the different

Chapter 2.3 Practice Problems

2.3a) Print the memory addresses of five different variables.

2.3b) Create five pointers to five different memory addresses and the value of each pointer. Output each memory address, numbering them one through five. 

2.3c) Create a loop that involves a pointer. Try to change the value of a memory address by using a math operator. What happens?

Chapter 2.4

Classes and Objects

We create classes to group together our functions that are similar when we are programming and are used as containers to group functions for readability and manipulation. Usually when only use classes when we are using several different functions and again we use them to group together tasks that have a goal or that work together. The syntax for a class is,

class className{

int newFunction (){

}

};

int main(){

className classObject;

classObject.functionName();

}

To declare a class, we type ‘class’ in lowercase letters and then we type the name of the class after which is  followed by {} braces and an ending semicolon. So, we have a class, a class name, and a function that is inside the class named newFunction(). The first thing you should notice is the fact that we are not using parentheses or parameters when we declare a class, that is because there are no statements that are ran through a class, the only reason or purpose that a class serves is to serve as a container for functions. After the ending brace and semi-colon, we enter the main function and inside the main function we have a new topic called a class object.

Class objects are used to call functions that are within the class specified the object is made for. Every class should have a corresponding object and if the class does not have an object then the functions that are written inside of the class cannot be called. The syntax is stated above but to go into further detail the first line,             

className classObject;

Is where we are creating the object for the class. First, we state the name of the class that we are creating the object for and then we single-space and write the name of the object, which can be anything, followed by a semi-colon to end the statement, which I will assume from now on you understand the semi-colon and need no further explanation. Now that you have the object for the class you are using, you should specify a way to access the functions in that class as well as call the function in main(). We can do this will one string of code written in line 2 as,

classObject.functionName();

Here is the part where we take the object we created to call the function that we want to use in our program. We write the name of the class object separated by a period ‘.’ , followed by the name of the function that we want to call and the parameters.

When we call functions we always need to add parameters, even if the function does not take in any parameters. Also remember not to add parameters after stating the name of a class because classes do not take parameters. We can now use classes to structure our code which if you have made it this far I am sure you are realizing that keeping track of things can be difficult. As we continue, you will find yourself using more and more classes as a tool to manage your code.

Chapter 2.4 Practice Problems

2.4a) Use a global variable to perform the calculation we used in section 2.1, x =7+(23/6)+(A/B),  solve this equation for ‘x’ inside of a class.

2.4b) Create two classes, each with at least one function nested inside of it, and each function with an output operator. Call the functions.

2.4c) Create a class with two functions. One function that solves 1yt =x for ‘x’ given whatever value the user enters for ‘y’ and ‘t’. Use the second function to solve y=23+mx for whatever values the user enters for ‘m’ and ‘x’.

Chapter 2.5

Classes II

Classes as we know them are used to group functions that are similar so that we have an easier time calling and finding these functions when we need them. In some cases, we may need to access a classes function for a different class, in these cases we use inheritance to allow a class to access the functions in another class. Inheritance allows us to use information that may be stored in one class be used in another class as well without moving any of the information between the classes. Although we usually create classes to keep certain specific related content; we may have a class that specifically needs some information from another class and without having to recode principles that are already outlined, we can use the idea of inheritance to inherit this code if needed.

To inherit the information from another class we write he name of the class that we are inheriting from we write the name of the class we want to inherit from after the class that we are using the information in by setting a colon and then the word “public” and lastly the name of the class. 

#include <iostream>

using namespace std;

class Team2{

public:

int Function2(){

        int x = 10;

        cout << x << endl;

    }

};

class Team : public Team2 {

public:

    int function1(){

        Function2();

    }

};

int main()

{

    Team TeamObj;

    TeamObj.function1();

    return 0;

}

With this form of inheritance, we took the information in the Team 2 class and  we are using that information the in-Team class. We took the inheritance of Team2 and then we can use the functions that are stored inside this class.

When we are specifying public, private, and protected at the beginning of programs we are given our class what is called an access specifier. Access specifiers tell the program what classes may access each other’s data. For instance, when create a class and have everything inside of the class set to public, we are saying that any class or function in that class can be used outside of that class. But when we set out access specifier to private we are saying that we do not want other classes or functions to be able to access the data stored in that class. But there is also the protected access specifier which is used when we have classes nested inside one of another. The protected access operator is only used when nesting class and this again ONLY allows for the parent class of the nested class the access the data in the child class.

| Access Specifier Type | Definition |
| public: | Allows all classes and functions to access the classes data. |
| private: | Does not allow other classes or functions to access the classes data. |
| protected: | Child Classes nested inside parent classes will be able to share data. |

Chapter 2.5 Practice Problems

2.5a) Create two classes each with its own function and connect these classes using inheritance.

Chapter 3: Algorithms and Logic

Chapter 3.1 The If and If-else Statement

The if-statement is a very important logical process that we use in programming to take two or more conditions and test them against each other. The syntax for an if statement is,

if(test == true){

cout << “This Statement is True” << endl;

}

This says; if the test inside the parameters is true then the code that is in the body of the program is running and if not then the code inside the if statement body is not executed. For this test inside the parentheses we will again be using variables or statements that are tested against each other and for that test we will have to use conditional operators.

Conditional Operators

- == ,Equal to

- > ,Greater than

- >=,Greater than or equal to

- < ,Less than

- <=,Less than or equal to

- !=,Not equal to

An example of a true if statement is,

float a = 10;

float b = 15;

if(a<b) {

cout << “a is less than b” << endl;

}

In this if statement we are testing two variables ‘a’ and ‘b’ against one another to see if the value of ‘a’ is less than the value of ‘b’. Since this test evaluates as true, the code inside the if statement is ran and outputted to the screen. If the test evaluated to false there would be no action that would be taken.

We can also use two more operators that can be used when testing if statements that when implemented are game changing to the natural way that if statements are thought of. These two operators are,

- &&, Means AND

- ||, Means OR

The && operator is used to test two different statements against each other and will only evaluate to true if both statements in the test are true. And the || operator which means OR is used to test two different statements and if at least one of the two statements are true then the test will run as true. For the example of this I will use several different operations so follow along carefully.

float team1Health = 100;

float team1Damage=20;

string usersChoice;

float team2Health = 100;

float team2Damage =15;

cout << “Choose a team:  a) Team 1” << endl << “b) Team 2” << endl;

cin >> usersChoice;

if(usersChoice == ‘a’){

cout << “You have chosen team 1! ” << endl;

cout << “Your damage is : ” << team1Damage << endl;

cout << “Your Health is: ” << team1Health << endl;

}

if(usersChoice == ‘b’ ){

cout << “You have chosen team 2! ”<< endl;

cout << “Your damage is : ” << team2Damage << endl;

cout << “Your Health is: ” << team2Health << endl;

}

In this program, you can see that are two separate teams each with a specific health and a specific damage. You are given the choice of which team you want to play on by typing ‘a’ for team 1 and ‘b’ for team 2\. Upon the input, you are given the team that you picked by being presented with an output specifying that team and you are also told the amount of health your team has and the amount of damage that each attack will give to your opponent.

Note: Something else we see while using the if-statement is the use of the == operator. We only use the == operator when we are testing two statements/variables against each other. When we use a single equals sign we are declaring a statement/variable a value.

Remember , there could also be any other set of conditions and that we could use different comparison operators. For example, we could add another if-statement at the end of this code that says, if we get any other user input other than ‘a’ or ‘b’ then the program will tell the user that their input is invalid.

If(usersChoice != ‘a’ || ‘b’){

cout << “INVALID!” << endl; }

Which says that if the usersChoice variable is not ‘a’ or ‘b’, meaning if the user does not enter ‘a’ or ‘b’; they will get a message outputted to their screen that says Invalid.

Expanding on this same topic is the if-else statement which is just the if statement with another body of code at the end of it.

The syntax of the if-else statement is,

int main(){

if(test == True){

// Run these Commands if the test is true.

} else {

// Run these commands if test is false.

}

}

We test something inside the parameters of the if statement and if the statement is true than the body of code in the if-statement will be ran. But if the test happens to be false then to program will run the code inside the else block of code. The else declaration does not require any parameters as no test needs to be ran. These purpose of the if else statement is to provide a way for a program to test true and false and output and outcome for each no matter what the answer to the test yields. When we are closing blocks of code we also do not need a semi-colon because the compiler already knows that the forward brace ‘{’ signifies the start of a blocks of code and that the backwards brace ‘}’ signifies the end of the code block. 

Challenge Problem:

3.1a) Nest an if-else statement inside of a function.

Chapter 3.2

Switches

When we are programming and we have tons of different if statement that are running different tests and outputting answers depending on the results of each test, we can quickly become overwhelmed with all the code that must be written to perform a task life this and this is not to mention all the different blocks of code that will accrue over time. This is where the use of switches comes into play as they serve as a medium for these tests to occur without having to restate the whole conditional statement and with only one block of code. Using switches is very lucrative as we can use them in almost any situation that we need to perform multiple tests.  

We can think of a switch as a function and inside this function we use sub-cases called cases that are the tests that are ran on the switch. Lastly, we use something called a ‘break’ that will separate the results that occur upon the truth of one of the tests.

The syntax of the switch statement is,

switch(variableTested){

case TEST1:

// if the test is true run this code

break;

case TEST2:

// if the test is true run this code

break;

}

An example of the use of a switch is,

    int x;

    cout << "enter x: " << endl;

    cin >> x;

switch(x){

case 1:

    cout << "1! " << endl;

    break;

case 2:

    cout << "2!" << endl;

    break;

}

Here we can see that we have an integer ‘x’ that we are lettering the user store into a variable x, simple enough, Next, we have the switch that take sin the variable x as a test. Inside the body of the switch we have ‘case 1:’ which says that ‘incase the user enters 1’, then we will run the code after the colon that signifies the start of the block of code for ‘case 1’. This is important to remember that when we are using switches, the case command that tests the variable inside the switch, must have a colon after it to signify that start of the code for that specific case. Next, we simply write some code inside of the switch that we want to run if that case is true and you have all the code written you write the ‘break;’ command to signify that you are don’t with the code for that case.

We then repeat this process and create as many cases that we need for the process to be complete. While the process of it may seem a little more involved the process is actually very simple and can be useful when you are using multiple if-statements. Being able to test many different situations is something that will become easier and easier the farther that we move along as you will see that that are much faster ways of performing a task like this when we need them to perform a multiple test.

Think about programs that we see running everyday such as video games we can pick apart the fact that in a video game we have several things that are happening at once. If we think of how shooting games are running we can think of the guns that we use in the video game and how the bullets come out upon clicking a button and how-to person walks through the environment of the video game. When you press a button, the gun performs a specific set of tasks that are pre-programmed and can be used whenever they are called but the tasks also know that they may never be called. We call these type of functions static functions, meaning that they contain code that may never be used but should be implemented upon the user requested its use. Next, we have something like the environment that the user runs through and we can see that the environment can never go away, this means that the code for this environment and everything that belongs specifically to the environment must be programmed in a way that loops over and over and never disappears or stops while the use is in a game. This type of function and use of programming is called looped programming and that is what we will be using next and that will greatly expand on the use of conditional statements like the if statement.

Take the code that we have used in the last few sections about if-statements, if-else statements, and the use of switches and create functions that use one or two or each of these to create a program. This will sharpen your use of the functions and the syntax that is used for each command which will allow you to create more intuitive programs and deal with program problems when they come up. While programming is one of the best tools that we have on earth is not 100% full-proof and problems will occur within your programs as the get more and more complex and perform more and more tasks. This is something that you should be ready for and understand how to deal with.

Challenge Problem(s):

3.2a) Create a switch with 5 cases. Put the switch inside of a function and the function inside of a class.

3.2b) Create a function that performs the same exact task as 3.2a, but this time use if statements. Notice the difference between these two functions.

Chapter 3.3

Loops

Sometimes we have code that we will want to run more than one time and this is where we should introduce a new concept called looping. Looping allows us to reiterate code and run it more than one time which can create a new avenue of concepts that allows for tons of new programming ideas. The concept of a loop can be explained as a function that tests a certain set of parameters and if the test inside of the set of parameters is true, the code inside of the loop will run.

The first loop that we will go over is called a ‘while’ loop which has the syntax of

while(test){

// run this code

}

The while loop takes parameters that are the ‘test’ of the loop and if the test of the loop is true then the body of code while run, until the loop becomes is false. The test of the loop is written inside parentheses which are referred to as the loops parameters.

This is better to see in an example,

int main(){

int x =4;

int y =5;

while(x>y){

cout << x << endl;

}

In the main function, we can see that we have two integer variables, one of which is 4 and one is 5\. Next, we have our while loop which says that if ‘x’ is greater than ‘y’, we output the value of ‘x’. If we run this code we will see that we get a never-ending program that will forever outputting the value of x. And while in some cases we will see that this is a useful technique to use when we are programming but not much. And what I mean by this is that we need to terminate this code somehow. Maybe we want the loop to run 10 times or 100 times, but it will be very rare for us to have a loop that never stops.

To stop our loops, we need to change the value of x or change the value of y (while the program is running) that will eventually cause the test to be false. For this we use an incrementer to change the value of one of the variables. But what is an incrementer? An incrementer changes the value of a specific variable by taking that variable and adding, subtracting, multiplying, or dividing the value while the program is running the test within the while loop. In c++, the most common incrementer is ‘x++’ which means x = x+1, which takes the value of ‘x’ (which is just the name of the variable), and adds ‘1’ to that number every time. So, if we put x++ in the body of the while loop than the value of x will change by +1 every time the loop is ran, and the test will become false.

int main (){

int x = 4;

int y = 5;

while(x>y) {

cout << x << endl;

x++;

}

When we run this code, we will get the value of x, just a single time. This is because when the program runs this loop the second time the value of x will be equal to the value of y, and there for not greater than y. If we wanted this loop to run twice we could say,             

while(x>=y)

Which would run twice because the second time the loop runs ‘x’ will be equal to ‘y’ which still true given the test inside of the parameters. We can use whatever values that we want to use for the variables as well as the incrementer. The incrementer could be set to,

#include <iostream>

using namespace std;

int main(){

int x = 0;

int y = 10;

while(x<=10){}

cout << x << endl;

x = x+5;

}

This loop increments by 5 by taking the value of x and adding 5 each time to it which will allows this loop to run twice before it terminates.

There is also a slightly modified version of the while loop that we can use in some cases called the ‘do-while’ loop.

do{

}while(test)

The ‘do-while’ loop guarantees that the code inside of it runs at least one time before terminating. We get the ‘do’ block which will be ran before the test of the while loop is even ran, the test can be true or false and we will still get the loop ran at least one time.

Challenge Problem:

3.3a) Create a loop that re-iterates 100 times. The loop should ask the user to enter values and perform a mathematical calculation given the values entered by the user.

The For Loop

The for loop, is a different type of loop that we will use at times to give the loop a little more information. If the for loop we usually initialize a specific variable that is used only during the test and loop process, to serve as the primary testing subject for the loop. This way the change in value only effects the loop and doesn’t affect any other part of the program. The syntax for the for loop is,

for(variable declaration; test; incrementer) {

// run this code

}

We first declare our variable inside of the parameters of the function, next we write the test that we want to run, and lastly, we include the incrementer inside of our loop. This condenses the different parts of a loop into a single line of code which can then make the loop simpler to read and if you need to move the loop somewhere in the future; like a different place in your code; you will be able to do that because the variable and incrementer as intact with the loop in one block of code. Now let’s create a for loop on the contrary when we use a while loop we cannot move the loop without also moving the variable and incrementer. In some special cases, we will not use the for loop we will use the while loop and vice versa, so understand how each of these are used are when it would be more beneficial to write one and not the other.

To create an example, we can see how the value of a variable changes as the loop runs by creating a simple for loop. This loop with contain an integer variable and will run until ‘x’ that is set equal to 1, is greater than 10, or while x is less than 10.  It will also iterate by 1 by using the ‘++’ operator on the variable on the variable ‘x’. Each time the loop runs it will print out the value of ‘x’ which will increase by 1 each time the loops runs.

#include <iostream>

using namespace std;

class CreatingLoops{

public:

void Loops() {

    // 1 -

    for(int x=1; x < 10; x++){

        cout << "value for x: " << x << endl;

    }

}

};

int main(){

CreatingLoops Object1;

Object1.Loops();

return 0;

}

While this loop can serve some presence, it is very simple in use and loops like this are rarely used for that reason. We usually create a loop to do some task, obviously, something that needs run more than once, but we usually don’t know how many times the loop with need to be ran, usually the user of the program will state this factor and for that we will need to create a loop that allows for a user-controlled variable to state the starting and stopping of the loop. This way the user is in specific control of this and the loop and the conditions that call the loop as well as the conditions that stop the loop.

Chapter 3.3 Practice Problems

3.3a) Create a loop that reiterates 100 times and continuously asks the user to enter values and perform a mathematical calculation.

3.3b) Use a while and a for loop in the same function.

Chapter 4: Files, Namespaces, Libraries, and Polymorphism

Chapter 4.1

Namespaces and Libraries

C++ Libraries are a compilation of functions and classes that denoted by the hash-tag or number sign (#). As you can see we have a library that we are currently using called the '#include <iostream>' library. This is a library that is pre-configured and consists of general purpose functions that allow us to perform certain special operations. These are also known as header files and they are used to hold the logic for functions that are being used as well as implement these tasks. Header files are also known as preprocessor directives because they are files that the processor loads before compiling the code written inside of the .cpp file. This is important for the structure of c++ because before the compiler can read the code, it takes in the preprocessor directives and takes in the logic of what functions can be used inside the program. This allows for our programs to run more efficiently as the preprocessor directives are loaded up before the program runs and while it may create a bigger startup impact, the program will already have done this in startup so the program does not slow down, freeze, or try to run this process while its running.

The c++ standard library (#include <cstdlib>) is used to perform several different tasks and can be added to the top of your c++ code under or above the existing header file. A popular function in the c standard library is the random function which allows us to get a random number.

#include <iostream>

#include <cstdlib>

#include <ctime>

using namespace std;

int main(){

    float num;

srand(time(NULL)) ;

cout << rand();

cin.get();

}

We have added two different header files to this program, both of which are necessary to access the information used. When we use '#include <cstdlib>' we are saying that we are including the c standard library which again allows us to access the srand(); function, which stands for seed random and inside the parameters we use the time function which has the parameter of 'NULL'. To use this time function, we also should introduce a new header file '#include <ctime>' which will allow the program to access the time. But we are not accessing the time directly. The value returned by,

srand(time(NULL));

Passing time(NULL) into the srand function starts a counter that counts how many seconds have passed since 00:00 hours, January 1, 1970 which is what we know in programming as the date of the 'Unix timestamp'. Which in turn allows us to always get a different value every single time we ask for this number.

We can use namespaces and header files we can call all types of interesting functions and commands. When we need a special case like this in the future we know that we can look at different header files that offer different functions such as the ‘srand()’ function that can help further expand on our programs.

Chapter 4.2

File Reading & Manipulation

When we are opening a file in c++, we to create a file stream, that then allows us to manipulate the file in various ways. We then can create or open an existing file and manipulate the contents of this file. To do this we use a new command that takes multiple parameters.

open(“filename”, mode);

We use the ‘open’ command followed by a set of parameters. Inside of the parameters we put the name of the file, surrounded by quotations, a comma, and then we can set something called the ‘mode’. The ‘mode’ represents the different types of functions that may be used when opening a file.

| ios::in | Opens the file and allows the programmer to write something to the file. |
| ios::out | Opens the file and allows output of the content inside of the file. Makes the files ‘readable’. |
| ios::binary | This operator opens the contents of the file in binary mode. |
| ios::app | Writes all new file content to the end of the file, allowing us to append information to the file. |
| ios::ate | When the file is opened the streams position indicator is moved to the end of the file. |
| ios::trunc | Takes the content written to the file and deletes it. The old content of the file will be gone and the new content will be written to the same file. |

These operators can be combined using a bitwise operator ( | ), which is used to separate each command.

Ofstream textFile;

textFile.open(“textExample.txt”, ios::out | ios::app | ios::binary);

Each of the member functions of classes ifstream, ofstream, and fstream have a default mode that is called whenever the file is opened without a second argument. After we are done using a file we should remember that we need to close the file for the information to be saved to the file.

#include <iostream>

#include <fstream>

using namespace std;

int main(){

ofstream textFile(“textExample.txt”);

if(textExample.is_open() ){

textExample << “This is on line 1  << endl;

textExample << “This is on line 2” << endl;

textExample.close();

}else {

cout << “unable to open file”;

}

}

Challenge Problem Answer Key

Variables Problem 1

Problem: Create a Program that asks the use to enter 3 integers and 3 decimals.

#include <iostream>

int main(){

int a,b,c;

cout << “ enter three integers” << endl;

cin >> a;

cin >> b;

cin >> c;

float x,y,z;

cout << “enter 3 decimals: ” << endl;

cin >> x;

cin  >> y;

cin >> z;

}

Variables Problem 2

Problem: Output those variables to the user to enter 5 variables to the user. Each answer should be displayed at the end of the program to the user on a separate line.

#include <iostream>

using namespace std;

int main(){

float x,y,z;

int a,b,c;

cout << “enter three decimals “ << endl;

cin >> x;

cin >> y;

cin >> z;

cout << “enter three integers “ << endl;

cin >> a;

cin >> b;

cin >> c;

cout << “Integers Entered” << endl;

cout << “Integer 1: “ << a << endl;

cout << “Integer 2: “ << b << endl;

cout << “Integer 3: ” << c << endl;

cout << “Decimals Entered” << endl;

cout << “decimal 1: “ << x <<  endl;

cout << “decimal 2: ” << y << endl;

cout << “decimal 3: ” << z << endl;

}

Math Operations Problem 1

Problem: Create a program that allows users to enter 5 variables. Take those values and perform multiplication/division/addition/subtraction to the 5 variables that the user has entered. Output the value of each math operation back to the user remembering to state each operation followed by the operations value.

#include <iostream>

using namespace std;

int main(){

float a,b,c,d,e;

cout << “Enter 5 real numbers” << endl;

cin >> a;

cin >> b;

cin >> c;

cin >> d;

cin >> e;

cout << “addition: “ << a+b << endl;

cout << “subtraction” << a-c << endl;

cout << “multiplication ” << a*d << endl;

cout << “division: ” << a/e << endl;

cout << “all” << (a+b)+(c+d)+e << endl;

}

Math Operations Problem 2

Question: Create a program that divides 3 numbers by each other that the user enters.

#include <iostream>

using namespace std;

int main(){

float a,b,c;

cout << “enter 3 numbers” << endl;

cin >> a;

cin >> b;

cin >> c;

cout << “division 1” << a/b << endl;

cout << “division 2” << a/c << endl;

cout << “division 3” << b/c << endl;

}

Array Problem 1

Questions: Create three arrays each of a different data type. Output each variable one by one (each on a separate line).

#include <iostream>
using namespace std;

int main(){

string a[3] = {“Array 1”,”Array 2”,”Array 3”};

float b[3] = {“bArray1”,”bArray2”,”bArray3”};

int c[3] = {“cArray1”,”cArray2”,”cArray3”};

cout << a[0] << endl;

cout << a[1] << endl;

cout << a[2] << endl;

cout << “------------------------------“ << endl;

cout << b[0] << endl;

cout << b[1]  << endl;

cout << b[2] << endl;

cout << “------------------------------” << endl;

cout << c[0] << endl;

cout << c[1] << endl;

cout << c[2] << endl;

cout << “-------------------------------” << endl;

}

Array Problem 2

Question: Create a program that asks the user to enter three values and store each in a specific spot in an array. Output the values they user entered back to them.

#include <iostream>

using namespace std;

int main(){

float a[3];

cout << “enter three real numbers ” << endl;

cin >> a[0];

cin >> a[1];

cin >> a[2];

cout << “Values Entered” << endl;

cout << a[0] << endl;

cout << a[1] << endl;

cout << a[2] << endl;

}

Arrays Problem 3

Question: Create three arrays, each  with a different variable type and output each variable within all 3 arrays.

#include <iostream>

using namespace std;

int main(){

float Array1[4] = {6.19, 7.2, 8.0, 10.8};

cout << “Multiplication: ” << Array1[0] * Array1[1] << endl;

cout << “Division: ” << Array1[2] /Array1[1] << endl;

cout << “Addition: “ << Array1[3] + Array1[0] << endl;

cout << “Subtraction:  ” << Array1[3] –  Array1[2]  << endl;

}

Function Prototype Problem 1

Question: Create a function that has at least five lines of code. Call the function through the main function.

#include <iostream>

using namespace std;

int Function1(){

float a,b,c;

cout << “enter a value for a: ” << endl;

cin >> a;

cout << “Enter a value for b” << endl;

cin >> b;

cout << “Enter a value for c” << endl;

cin >> c;

}

int main(){

Function1();

}

Function prototype Problem 2

Question: Create a function, write any code in it that you want to, make sure it is under the main function, create the function prototype, and call the function to use.

#include <iostream>

using namespace std;

int  Function1();

int main(){

function1();

}

int Function1(){

float a,b,c;

cout << “a: “ << endl;

cin >>  a;

cout << “b: “ << endl;

cin >> b;

cout << “c: ” << endl;

cin >> c;

cout << “Value Entered for A: “ << a << endl;

cout << “Value Entered For B: “ << b << endl;

cout << “Value Entered For C: ” << c << endl;

}

Function Prototyping Problem 3

Question: Create three functions under the main function that perform x=7+(23/6)+(A+B). The user will enter the values for ‘A’ and ‘B’ and if the user enters real numbers the program will find the answer to the equation.

- Note: Remember that the user should be able to enter integers, decimals, and fractions.

#include <iostream>

using namespace std;

// x = 7 + (23/A) + (A*B)

float A,B;

int function1();

int function2();

int function3();

int main(){

function1();

function2();

function3();

float answer1 = 23/A;

float answer2 = A*B;

cout << "The answer: " << 7 + answer1 + answer2 << endl;

}

int function1(){

    cout << "Welcome to this equation solving program! " << endl;

    cout << "Enter A and B to solve the equation x=7+(23/A)+(A*B) " << endl;

}

int function2(){

    cout << "Enter the value for A" << endl;

    cin >> A;

}

int function3(){

cout << "enter the value for B" << endl;

cin >> B;

}

Variable Scope Problem 1

Question: Write two global variables and write two local variables, that are in a function and output all four variables.

#include <iostream>

using namespace std;

float GlobalVariable1, GlobalVariable2;

int MyFunction1(){

float LocalVariable1, LocalVariable2;

cout << "Enter a Value AS LocalVariable1: ";

cin >> LocalVariable1;

cout << "Local Variable 1: " << LocalVariable1;

cout << endl;

cout << "Enter a Value as Local Variable2: ";

cin >> LocalVariable2;

cout << "Local Variable 2: " << LocalVariable2;

cout << endl;

cout << "Enter a value as the global variable 1: " << endl;

cin >> GlobalVariable1;

cout << "Global Variable 1: " << GlobalVariable1 << endl;

cout << endl;

cout << "Enter a value to save to global variable 2: " << endl;

cin >> GlobalVariable2;

cout << "Global Variable 2: " << GlobalVariable2 << endl;

cout << endl;

}

int main()

{

MyFunction1();

}

Variable Scope Problem 2

Question: Create at least 3 separate functions. Each function should have local variables. Find a unique way to tie these three functions together into a single program.

#include <iostream>

using namespace std;

void welcome();

void player();

void health();

void damage();

int main()

{

welcome();

player();

health();

damage();

}

void welcome(){

string welcome = "Welcome to The Best Video Game Ever";

cout << welcome << endl;

}

void player(){

string name;

cout << "Enter the Name of Your Character: " << endl;

cin >> name;

cout << "You have chosen the name: " << name << endl;

}

void health(){

float Health1;

cout << "How much Health Do You Want Your Character to Have? From 0 - 100" << endl;

cin >> Health1;

cout << "You have chosen to have " << Health1 << " % armor" << endl;

}

void damage(){

float damage1;

cout << "How much Damage Do You Want Your Character to Have? From 0 - 100" << endl;

cin >> damage1;

cout << "You have chosen to have " << damage1 << " Points of Damage Per Hit" << endl;

}

Classes Problem 1

Question: Use a global variable to perform a calculation in a class.

#include <iostream>

using namespace std;

class calculation{

public:

    float a,b,c;

    int calc(){

        cout << "Enter three variables" << endl;

        cin >> a;

        cin >> b;

        cin >> c;

        cout << "Answer:  " << a+b+c << endl;

    }

};

int main(){

calculation cObj;

cObj.calc();                  }

Classes Problem 2

Question: Create two classes, each with a function inside, and a string output operator. Call both functions to the main function.

#include <iostream>

using namespace std;

class HELLO{

public:

int welcome(){

cout << "welcome to the How Much Money program!" << endl;

}

};

class calculations{

public:

float moneyMade;

int moneyFunction(){

cout << "Enter the amount of money you want to make" <<endl;

cin >> moneyMade;

cout << "Next Year You Will Make: " << "$" << moneyMade << endl;

}

};

int main(){

HELLO Hobj;

Hobj.welcome();

calculations cObj;

cObj.moneyFunction();

}

Classes Problem 3

Question: Create a class with two functions. One function that solves 1yz = x  for x given whatever value the user enters for ‘m’. Use the second function to solve y = 23+ (m*x) for whatever values the user enters.

#include <iostream>

using namespace std;

float x,y,z,m;

const float u = 23;

class expert{

public:

    //  1yz = x

    int function1(){

        cout << "Enter a value for y " << endl;

        cin >> y;

        cout << "Enter a value for z " << endl;

        cin >> z;

        float calc1 =(y*z*1);

        cout << "x = " << calc1 << endl;

    }

    // y=23+mx

    int function2(){

        cout << "Enter the value for m " << endl;

        cin >> m;

        cout << "Enter the value for x " << endl;

        cin >> x;

         float calc2 = (m*x);

        cout << "y = " << calc2 + u << endl;

    }

};

int main(){

expert eObj;

eObj.function1();

eObj.function2();

}

Classes II Problem 1

Question: Write two classes each with its own function connect these classes using inheritance.

#include <iostream>

using namespace std;

class zed{

public:

    string language = "C++";

};

class app: public zed{

    public:

    int F2(){

    cout << language << endl;

    }

};

int main(){

    zed zObj;

app aObj;

aObj.F2();

}

If and If-Else Statements Problem 1

Question: Create an if-else statement nested inside a function.

#include <iostream>

using namespace std;

int Control();

int main(){

Control();

}

int Control(){

float x = 10;

float y = 23;

if(x<y){

    cout << "Yes, x is greater than y" << endl;

}else {

cout << "No, x is not greater than y" << endl;

}

}

Switches Problem 1

Question: Create a switch with 5 cases. Put the switch inside of a function and the function inside of a class.

#include <iostream>

using namespace std;

int x;

class Inside{

public:

void Function1(){

    cout << "Enter Your Age " << endl;

    cin >> x;

switch(x){

case 13:

    cout << "You can now watch pg-13 movies" << endl;

    break;

case 18:

    cout << "You can get your drivers license!" << endl;

case 21:

    cout << "You can now buy alcohol!" << endl;

break;

default:

        cout << "Please enter another value" << endl;

}

  }

};

int main(){

Inside iObj;

iObj.Function1();

}

Switches Problem 2

Question: Create a function that achieves the same look as the function in the first problem, but this time use if statements. Notice the difference between these two functions.

#include <iostream>

using namespace std;

int age;

int experiment(){

if(age==13){

cout << "You can watch a pg-13 movie" << endl;

}

if(age==18){

    cout << "You can now purchase a lottery ticket" << endl;

}

if(age==21){

    cout << "You are now allowed to buy alcohol!" << endl;

}else {

    cout << "The value you entered is not valid" << endl;

}

}

int main(){

cout << "What is your age" << endl;

cin >> age;

experiment();

}

Loops Problem 1

Question: Create a loop that reiterates 100 times and continuously asks the user to enter values and perform a mathematical calculation. Given the values entered by the user.

#include <iostream>

using namespace std;

int main(){

for(int x=0;x<=99;x++){

    float a;

    cout << "Guess 100 Numbers between 1 and 10,000" << endl;

    cin >> a;

    if(a==837){

            for(int y=0;y<=99999999;y++){

        cout << "YOU GUESSED THE CORRECT NUMBER" << endl;

    }

    }

}

}

Loops Problem 2

Question: Use a while and a for loop in the same program.

#include <iostream>

using namespace std;

float z;

int main(){

for(int y=0;y<=99;y++){

while(z != -1){

cout << "enter an integer" << endl;

cin >> z;

} } }

Memory and Variables Problem 1

Question: Print the memory addresses of 5 different variables inside of their own dedicated class and function.

#include <iostream>

using namespace std;

int main(){

float a,b,c,d,e;

cout << "Memory address 1: " << &a << endl;

cout << "Memory address 2: " << &b << endl;

cout << "Memory address 3: " << &c << endl;

cout << "Memory address 4: " << &d << endl;

cout << "Memory address 5: " << &e << endl;

}

Memory and Variables Problem 2

Question: Create five pointers to five different memory addresses and the value of each pointer. Output them numbering them one through five.

#include <iostream>

using namespace std;

int main(){

    int *a,*b,*c,*d,*e;

    cout << "Memory Address For 'a' : " << &a << endl;

     cout << "Memory Address For 'b' : " << &b << endl;

      cout << "Memory Address For 'c' : " << &c << endl;

       cout << "Memory Address For 'd' : " << &d << endl;

        cout << "Memory Address For 'e' : " << &e <<endl;

}

Memory and Variables Problem 3

Question: Create a loop that involves a pointer. Try to change the value of a memory address by using a math operator. What happens?

#include <iostream>

using namespace std;

int main(){

int *pointer;

  cout << "Regular Memory Address: " << &pointer << endl;

  cout << "Memory Address + 5: " << &pointer + 5 << endl;

}