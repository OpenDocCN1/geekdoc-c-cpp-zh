![](OPS/images/cover.jpg)

![cover](OPS/images/cover.jpg)![Cover](OPS/images/cover.jpg)

First Edition 2024

Copyright © BPB Publications, India

ISBN: 978-93-55519-115

All Rights Reserved. No part of this publication may be reproduced, distributed or transmitted in any form or by any means or stored in a database or retrieval system, without the prior written permission of the publisher with the exception to the program listings which may be entered, stored and executed in a computer system, but they can not be reproduced by the means of publication, photocopy, recording, or by any electronic and mechanical means.

LIMITS OF LIABILITY AND DISCLAIMER OF WARRANTY

The information contained in this book is true to correct and the best of author’s and publisher’s knowledge. The author has made every effort to ensure the accuracy of these publications, but publisher cannot be held responsible for any loss or damage arising from any information in this book.

All trademarks referred to in the book are acknowledged as properties of their respective owners but BPB Publications cannot guarantee the accuracy of this information.

![](OPS/images/BPB_Catalogue_QR.png)

[www.bpbonline.com](https://www.bpbonline.com)

**Dedicated to**

*My son, Vidit, for igniting the idea behind this book*

*My husband, parents, and siblings for their endless support and blessings*

*—Shikha Jain*

*My dearest daughter, Sachi, your love fuels every word in this book*

*My husband and the Almighty God, for their guidance and inspiration, without whom this book would not have been possible*

*—*Kavita Pandey

# About the Authors

*   Shikha Jain is an Assistant Professor at Jaypee Institute of Information Technology (JIIT), NOIDA, INDIA. She has more than twenty years of research and academic experience. She has received her PhD in computer science from Jaypee Institute of Information Technology, Noida, India. She has contributed significantly to the field, publishing numerous research papers in prestigious journals and conferences.

    She was a guest editor for the notable Advances in Computational Intelligence and its Applications issue in the International Journal of Information Retrieval Research. She is an active reviewer of many International Journals and a technical program committee member of various International Conferences. Her research area includes Affective Computing, Emotion Modelling, Cognitive Affective Architectures, Machine Learning, and Soft Computing. She also takes on the editor role for the book Artificial Intelligence, Machine Learning, and Mental Health in Pandemics: A Computational Approach.

*   Kavita Pandey is an Assistant Professor (Senior Grade) at Jaypee Institute of Information Technology (JIIT), Noida. She has more than 20 years of academic experience. She received her B.Tech. in Computer Science and Engineering from M.D. University in 2002 and M.Tech. (CS) from Banasthali Vidyapeeth University in 2003\. She obtained her Ph.D. (CS) from JIIT, Noida, India, in January 2017\. Presently, she is guiding two Ph.D. students. She has mentored 16 M.Tech. thesis/industrial projects and 57 + undergraduate projects.

    She is an editor of a book named Artificial Intelligence, Machine Learning, and Mental Health in Pandemics: A Computational Approach. She has published one patent. She also contributed to IGNOU study material titled Data Communications and Computer Network. Her research interests include Soft Computing, Machine Learning, Vehicular Ad hoc Networks, the Internet of Things, and Optimization Techniques. She has published 60+ articles in International journals and conferences, including Wiley, IEEE, Springer, Inderscience, etc. She was a guest editor of the special issue Advances in Computational Intelligence and Applications in the International Journal of Information Retrieval Research (IJIRR), IGI Global, ESCI, and Web of Science. She is working as an Academic Editor on the Editorial Board of the International Journal of Distributed Sensor Networks, Hindawi. She was a reviewer in many international journals of renowned publishers, including Elsevier, Inderscience, and IEEE Access, among others. She is an active TPC member of many conferences, such as FSDM, REDSET, IC3, UPCON, TEAMC, ICTCS, and many more. She is also a senior member of the IEEE Society.

# About the Reviewer

Sachin Jain, a seasoned professional with over two decades of experience in the IT industry, stands as a testament to the fusion of passion and expertise. Born with a natural inclination towards technology, he embarked on a journey that has defined him as a master in his field. He pursued his academic aspirations with a Master’s in Computer Applications, laying the foundation for an illustrious career.

With an impressive 20-plus years of experience, Sachin has become a stalwart in the IT industry, contributing significantly to developing and designing large-scale enterprise applications. His coding prowess and innovative approach have set him apart, making him a go-to technology expert.

Beyond the world of coding and algorithms, Sachin finds solace in his passion for travel and cinema. Exploring new landscapes and immersing himself in diverse cultures fuels his creativity and broadens his perspective. Amid intricate lines of code, Sachin discovers balance through the magic of storytelling, whether on the screen or in the pages of a good book.

Sachin Jain’s journey is a testament to the harmonious blend of technical understanding and a rich, multifaceted life. As he continues to push the boundaries of what is possible in the IT landscape, Sachin remains a true connoisseur of the digital age.

# Acknowledgement

Alone we can do so little; together we can do so much.

—Helen Keller   

We humbly acknowledge the divine presence that has guided and inspired the creation of this book. We sincerely thank Almighty God for providing wisdom, strength, and inspiration throughout this journey.

A heartfelt thanks go to the entire team of BPB Publishers for their unwavering support in bringing our dream to fruition.

We are grateful to known and unknown individuals whose contributions have enriched our pool of knowledge, enabling us to author this book.

We sincerely appreciate the reviewers whose insightful suggestions and feedback significantly enhanced the quality of this book.

Lastly, we express our gratitude to all the readers for their interest in our book. Your encouragement is invaluable.

# Preface

Welcome to Code Factory. This is specially designed for new entrants in the programming world. The main objective of the book is to trigger and nurture logic-building skills among students. It provides a comprehensive introduction to the fundamental programming concepts through the lens of two powerful languages—C and Python. The book will help the reader develop problem-solving and logic-building abilities with the help of algorithms and flowcharts. It will also teach how to transform the flowchart/algorithm into a program. Simultaneously, engaging with flowcharts, algorithms, and programming enhances the reader’s ability to comprehend the translation of a given problem into logical solutions and subsequently into executable programs. By working in parallel with these components, readers gain a holistic perspective on the problem-solving process. It reinforces the connection between the problem statement, the logical constructs devised in algorithms, and their representation in a programming language.

The book is structured to introduce concepts gradually, ensuring a smooth learning curve. Each chapter presents challenges of increasing difficulty, allowing students to build on their skills progressively. One book chapter is designed to expose real-world examples of applying learned concepts to solve coding problems, enhancing their ability to tackle programming challenges in various domains.

This book will help the readers develop a well-rounded skill set covering flowcharts, algorithmic thinking, and practical implementation in both C and Python languages. It will provide a holistic foundation for anyone aspiring to become fearless in coding. I hope this guide will empower you to embark on a fulfilling journey into coding.

[Chapter 1: Simple Input Output Program](#ch01.xhtml) – It provides a comprehensive understanding of the fundamental concepts and techniques involved in handling input and output operations in programming. It aims to offer a thorough comprehension of fundamental algorithms flowcharts and Python and C code implementations. These programs help users grasp crucial concepts, including user input, data manipulation, and result display. Consider this chapter a foundational step for constructing more intricate applications in subsequent book sections.

[Chapter 2: Conditional Statements](#ch02.xhtml) – It covers the concept of decision statements( if-else), elucidating them through flowcharts, algorithms, and coding. Using numerous examples, it has effectively illustrated the various facets of conditional statements such as simple if, if-else, if-else if-else, and so on. Decision statements enable the execution of specific code blocks based on certain conditions. They provide the logic for making choices within a program, making them a fundamental building block.

[Chapter 3: Simple Loops](#ch03.xhtml) – It discusses the basic loop statements such as while-loop and for-loop. In programming, a loop is a fundamental control structure that allows you to execute a block of code repeatedly as long as a specific condition is met. Loops are essential for automating repetitive tasks, iterating over certain statements, and performing various computational tasks efficiently. It optimizes the code as well. Overall, the chapter underscores the significance of loops as essential tools for improving code automation and computational efficiency in programming

[Chapter 4: Complex Loops](#ch04.xhtml) – It delves into the intricate applications of loops, showcasing their capacity to address complex problems. Loops are not confined to essential repetition; they can be seamlessly integrated with multiple conditional statements to devise sophisticated solutions. Furthermore, the chapter elevates their significance in handling certain challenges that demand the utilization of multiple loops, either sequentially or in the form of nested loops.

[Chapter 5: Complex Problem Solving](#ch05_split_000.xhtml) – It presents the complex logic building using various programming constructs (as discussed in previous chapters). The main focus of the chapter is on solving challenging problems by thinking of some logic. The chapter presents the problems or challenges that require creative and intricate solutions. These problems often go beyond simple algorithmic steps and may involve multiple steps, conditional logic, loops, lists, and matrices. The chapter discusses creating a logical flow for solving complex problems, including algorithms and flowcharts, to plan solutions before writing executable code.

[Chapter 6: Real World Problems](#ch06.xhtml) – It guides readers to navigate the intersection of real-world problems and programming constructs. The primary emphasis lies in strategically mapping these tangible challenges to previously studied concepts. By aligning real-world problems with established programming principles, the chapter seeks to demystify complex issues and demonstrate how simple programming constructs can be ingeniously applied.

# Code Bundle and Coloured Images

Please follow the link to download the

***Code Bundle*** and the ***Coloured Images*** of the book:

[https://rebrand.ly/eaal7hm](https://rebrand.ly/eaal7hm)

The code bundle for the book is also hosted on GitHub at [https://github.com/bpbpublications/Code-Factory](https://github.com/bpbpublications/Code-Factory) In case there’s an update to the code, it will be updated on the existing GitHub repository.

We have code bundles from our rich catalogue of books and videos available at [**https://github.com/bpbpublications**](https://github.com/bpbpublications). Check them out!

Errata

We take immense pride in our work at BPB Publications and follow best practices to ensure the accuracy of our content to provide with an indulging reading experience to our subscribers. Our readers are our mirrors, and we use their inputs to reflect and improve upon human errors, if any, that may have occurred during the publishing processes involved. To let us maintain the quality and help us reach out to any readers who might be having difficulties due to any unforeseen errors, please write to us at :

**[errata@bpbonline.com](mailto:errata@bpbonline.com)**

Your support, suggestions and feedbacks are highly appreciated by the BPB Publications’ Family.

**Join our book’s Discord space**

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](OPS/images/fm1.png)

# [CHAPTER 1Simple Input Output Program](#contents.xhtml_ch01a)

[Introduction](#contents.xhtml_sc2_1a)

The ability to process input and generate output is a fundamental aspect of programming. In this chapter, we delve into the world of simple input-output programs. It comprehensively explains basic algorithms, flowcharts, Python, and C code implementations. These programs allow users to grasp essential concepts such as user input, data manipulation, and result display. This chapter will be a building block for developing more complex applications in further book chapters.

Whether you are a novice programmer seeking to strengthen your fundamental abilities or an experienced developer looking for practical examples, this chapter offers a diverse range of simple programs to explore. A basic understanding of the program would be built by studying the algorithms and visualizing the flowcharts. In addition, the Python and C code will give you valuable insights into the core principles of input-output operations in these languages. Overall, the skills necessary to solve real-world programming challenges would be gained. The basic building blocks of a flowchart are shown in [Figure 1.1](#ch01.xhtml_fig1-1):

![](OPS/images/Figure_1.1.png)

Figure 1.1: The basic building blocks of a flowchart

Let us embark on this journey through simple input-output programs and discover the power of these fundamental building blocks.

[Structure](#contents.xhtml_sc2_2a)

In this chapter, there are a total of 21 programs, and four sub-topics complement each program. The following topics will be covered with each program:

*   Understand the program objective with sample input and outputs. It will give the user an understanding of what kind of user input is expected and what result will be projected for a particular program.
*   Understand the program with an algorithm. This will help the user to understand the methodology behind writing the sequence of steps required to solve a program.
*   Visualize the program flow with flowcharts. Program objectives can be understood easily with the flowchart representation. Users will understand which symbols to use in which context throughout different program’s flowchart representations.
*   Python source code of each program. Each program’s source code in Python programming language is provided to the user so the user can understand the basic operations of the language. An explanation of each code is also provided.
*   C implementation of each program. Users can learn the basic concepts of C language with the provided C language code and its explanation for every program.

[Objectives](#contents.xhtml_sc2_3a)

In this chapter, the reader will learn the fundamentals of input-output operations and their significance in program development. We will discuss designing algorithms to perform basic input and output operations. We will acquire the skills to create visual representations of program flow using flowcharts and the ability to implement simple input-output programs using Python and C programming languages. With the sample codes, users can gain hands-on experience. We will also gain problem-solving skills related to simple basic problems, such as accepting user input, performing calculations, and displaying results.

[Program 1.1: Print your name](#contents.xhtml_sc2_4a)

Take your name as input and print Hello name.

[Sample input output](#contents.xhtml_sc3_5a)

Test case #1:

Input: Neo

Output: Hello Neo

Test case #2:

Input: Sam

Output: Hello Sam

Test case #3:

Input: John Will

Output: Hello John Will

[Algorithm](#contents.xhtml_sc3_6a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2.  Enter your name in name

Step 3. Print "Hello" name

Step 4\. Stop

[Flowchart](#contents.xhtml_sc3_7a)

[Figure 1.2](#ch01.xhtml_fig1-2) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_1.2.jpg)

Figure 1.2: Flowchart illustrating program 1.1

[Python code](#contents.xhtml_sc3_8a)

Python code for the program 1.1 is as follows:

1.  # read a input from the user
2.  name= input("Enter your name: ")
3.  # print the name on the screen
4.  print("Hello ", name)

[Python code explanation](#contents.xhtml_sc4_9a)

The program prompts the user to enter the name and then prints a greeting message containing the name.

name = input("Enter your name: "): This line prompts the user to enter the name by printing the string Enter your name:. The input() function is used to read the user’s input as a string and assign it to the variable name.

print("Hello", name): This line uses the print() function to print the string Hello followed by the value of the name variable.

Python is an indentation-sensitive language. Indentation is used to mark the block of code.

Any statement preceded by # is a comment which does not execute. These comments are ignored by the compiler and used only for the user to understand the code.

[C code](#contents.xhtml_sc3_10a)

The C code of program 1.1 is specified below:

1.  #include <stdio.h>

3.  int  main() //The execution of C program starts with main function
4.  {
5.  char name[100]; //declared a variable of character type of size 10
6.  printf("Enter your name: ");
7.  gets(name);  // read a input from the user
8.  printf("Hello %s", name); // print the name on the screen
9.  return  0; // The main() function returns an integer value 0
10.  }

[C code explanation](#contents.xhtml_sc4_11a)

stdio.h is a header file that should be included in the program to use various input-output functions. Main() function serves as the starting point for program execution. It is mandatory to write a main function in every C program. Here, int is written before main(). This means that the function main() will return an integer value after completing the program’s execution. The last statement return 0 returns a value 0 on successful execution of the program.

A variable name is declared as an array of 100 characters. gets() is an input function used to read a string. Referring to test case #3, gets() function also allows the space between words. Also, C uses %s as the format specifier for strings. Finally, we use printf() function to output the greeting message with the user’s name.

Unlike Python, indentation is not important in C language. Each block of code is enclosed between parentheses.

[Program 1.2: Print your lucky number](#contents.xhtml_sc2_12a)

Take a number as input and print the number as Number entered by you is: number.

[Sample input output](#contents.xhtml_sc3_13a)

Test case #1:

Input: 10

Output: Number entered by you is: 10

Test case #2:

Input: 55

Output: Number entered by you is: 55

[Algorithm](#contents.xhtml_sc3_14a)

The below steps illustrate the working of program 1.2:

Step 1\. Start

Step 2\. Enter a number in n

Step 3\. Print "Number entered by you is : " n

Step 4\. Stop

[Flowchart](#contents.xhtml_sc3_15a)

[Figure 1.3](#ch01.xhtml_fig1-3) depicts the program in the form of a flowchart as follows:

![](OPS/images/Figure_1.3.jpg)

Figure 1.3: Flowchart for program 1.2

[Python code](#contents.xhtml_sc3_16a)

Python code for the program1.2 is as follows:

1.  # read an integer input from the user
2.  n=int(input("Enter a number "))
3.  #print the output on the screen
4.  print("Number entered by you is: ", n)

[Python code explanation](#contents.xhtml_sc4_17a)

The first line of this code uses the input() function to prompt the user to enter a number. The input() function reads the user input as a string, so int() function is used to convert the input to an integer. The resulting integer is then assigned to the variable n.

The second line of the code uses the print() function to output a message to the user. The message includes the string Number entered by you is: and the value of the variable n. The print() function automatically adds a new line character at the end of the output, so the message is printed on a new line.

[C code](#contents.xhtml_sc3_18a)

C code for the program 1.2 is as follows:

1.  #include <stdio.h>
2.  int  main() {
3.  int n; //declared a variable of integer type
4.  printf("Enter a number: ");
5.  scanf("%d", &n); // read a input from the user
6.  printf("Number entered by you is: %d\n", n); // print the output on the screen
7.  return  0; // The main() function returns an integer value 0
8.  }

[C code explanation](#contents.xhtml_sc4_19a)

This code prompts the user to enter a number, reads the user’s input in a variable n, and then prints out the entered number. C uses %d as the format specifier for integers.

[Program 1.3: Print your details](#contents.xhtml_sc2_20a)

Take the name, age, address, and class 12th marks as input and print its name is age years old, lives in address, and scored marks in 12th.

[Sample input output](#contents.xhtml_sc3_21a)

Test case #1:

Input:

Enter your name: Shikha

Enter your age: 42

Enter your address: Delhi

Enter your marks: 40

Output:

Shikha is 42 years old, lives in Delhi, and scored 40 marks in 12th.

Test case #2:

Input:

Enter your name: John Gill

Enter your age: 10

Enter your address: Noida, UP

Enter your marks: 30

Output:

John Gill is 10 years old, lives in Noida, UP, and scored 30 marks in 12th.

[Algorithm](#contents.xhtml_sc3_22a)

Steps to execute the program 1.3 are mentioned as follows:

Step 1\. Start

Step 2. Enter your name, age, address, and marks as n, age, address, m

Step 3\. Print n, " is ", age, " years old, lives in ", address, " and scored ", m, " marks in 12th."

Step 4\. Stop

[Flowchart](#contents.xhtml_sc3_23a)

The flowchart of the algorithm is illustrated in [Figure 1.4](#ch01.xhtml_fig1-4):

![](OPS/images/Figure_1.4.jpg)

Figure 1.4: Flowchart illustrating program 1.3

[Python code](#contents.xhtml_sc3_24a)

The following describes the Python code for program 1.3:

1.  #read name and address as string input
2.  n=input("Enter your name: ")
3.  address=input("Enter your address: ")
4.  #read age as integer input
5.  age=int(input("Enter your age: "))
6.  m=int(input("Enter your marks: "))
7.  # print the output
8.  print( n, "is", age, "years old, lives in ", address, " and scored ", m, " marks in 12th.")

[Python code explanation](#contents.xhtml_sc4_25a)

The first four lines of this code use the input() function to prompt a message and take input from the user in variables n, age, address, and m.

Then, the print() function is used to output a message to the user. The message includes the variables n, age, address, and m along with some strings that provide context for the values.

[C code](#contents.xhtml_sc3_26a)

The following describes the C code for program1.3:

1.  /* Take the name, age, address, and class 12th marks as input
2.  and print as name is age years old, lives in address, and
3.  scored marks in 12th. */

5.  #include <stdio.h>

7.  int  main() {
8.  //declared two variable of character type of each of size 100
9.  char n[100], address[100];
10.  int age, m; //declared two variable of integer type

12.  printf("Enter your name: ");
13.  gets(n); // read a string as input from the user

15.  printf("Enter your age: ");
16.  scanf("%d", &age); // read an integer input from the user

18.  fflush(stdin); //function to clear input buffer
19.  printf("Enter your address: ");
20.  gets(address); // read a string as input from the user

22.  printf("Enter your marks: ");
23.  scanf("%d", &m); // read an integer input from the user

25.  // print the output on the screen
26.  printf("%s is %d years old, lives in %s, and scored %d marks in 12th.\n", n, age, address, m);

28.  return  0;
29.  }

[C code explanation](#contents.xhtml_sc4_27a)

In this C code, the variables n, age, address, and m are first declared. Since n and address are strings; we declare them as character arrays with a fixed size 100\. The age and m variables are declared as integers.

Next, printf() function prompts the user to enter their name, age, address, and marks. For string-type variables, we have used the gets() function so that it can take multiple words together. Before the second use of the gets() function, the fflush() function is used as it clears the buffer and helps in the smooth handling of the gets() function. For integer-type input, the scanf() function reads the user’s input and stores it in the appropriate variable.

Finally, the printf() function prints an output message to the user, including their name, age, address, and marks. We use placeholders like %s (for string) and %d (for integer) to substitute the values of the variables in the message.

[Program 1.4: Find sum of two numbers](#contents.xhtml_sc2_28a)

Take two numbers as input and print their sum.

[Sample input output](#contents.xhtml_sc4_29a)

Test case #1:

Input:

Enter first number: 56

Enter second number: 34

Output:

Sum = 90

Test case #2:

Input:

Enter first number: -23

Enter second number: 45

Output:

Sum = 22

Test case #3:

Input:

Enter first number: -198

Enter second number: -23

Output:

Sum = -221

[Algorithm](#contents.xhtml_sc3_30a)

To run the program 1.4, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Enter two numbers as n and m

Step 3\. sum = n+m

Step 4\. Print "Sum=" sum

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_31a)

The flowchart of the algorithm is illustrated in [Figure 1.5](#ch01.xhtml_fig1-5):

![](OPS/images/Figure_1.5.jpg)

Figure 1.5: Flowchart for summation of two numbers

[Python code](#contents.xhtml_sc3_32a)

Here is the Python source code for program1.4:

1.  #read two integer inputs from the user
2.  n=int(input("Enter first number: "))
3.  m=int(input("Enter second number: "))
4.  #performed addition of two numbers
5.  sum= n+m
6.  #print the output on the screen
7.  print("Sum =", sum)

[Python code explanation](#contents.xhtml_sc4_33a)

This code prompts the user to enter two numbers, n, and m using the input() function preceded by the int() function. It calculates their sum and prints it to the console using print() function.

[C code](#contents.xhtml_sc3_34a)

Here is the C source code for program 1.4:

1.  #include <stdio.h>

3.  int  main() {
4.  int n, m, sum; //declared three variable of integer type

7.  printf("Enter first number: ");
8.  scanf("%d", &n); // read an integer input from the user

10.  printf("Enter second number: ");
11.  scanf("%d", &m); // read another integer input from the user

13.  sum = n + m; //performed addition of two numbers

15.  printf("Sum = %d\n", sum); // print the output on the screen

17.  return  0;
18.  }

[C code explanation](#contents.xhtml_sc4_35a)

In this C code, we first declare n, m, and sum as integers. Printf() and scanf() functions prompt a message and take the input from the user.

The sum of n and m is calculated and stored in the variable sum. Finally, the output is printed using printf() function.

[Program 1.5: Find product of two numbers](#contents.xhtml_sc2_36a)

Take two numbers as input and print their product.

[Sample input output](#contents.xhtml_sc3_37a)

Test case #1:

Input:

Enter first number: 20

Enter second number: 56

Output:

Product = 1120

Test case #2:

Input:

Enter first number: -34

Enter second number: 67

Output:

Product = -2278

Test case #3:

Input:

Enter first number: -12

Enter second number: -32

Output:

Product = 384

[Algorithm](#contents.xhtml_sc3_38a)

The stages for running program 1.5 are shown below:

Step 1\. Start

Step 2\. Enter two numbers as n and m

Step 3\. p = n * m

Step 4\. Print "Product =", p

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_39a)

The flowchart of program 1.5 is shown in [Figure 1.6](#ch01.xhtml_fig1-6):

![](OPS/images/Figure_1.6.jpg)

Figure 1.6: Flowchart for product of two numbers

[Python code](#contents.xhtml_sc3_40a)

The Python source code for program 1.5 is available here:

1.  #read two integer inputs from the user
2.  n=int(input("Enter first number: "))
3.  m=int(input("Enter second number: "))
4.  #performed multiplication of two numbers
5.  p= n * m
6.  #print the output on the screen
7.  print("Product =", p)

[Python code explanation](#contents.xhtml_sc4_41a)

This code prompts the user to enter two numbers, n, and m using the input() function preceded by the int() function. It calculates their product and prints it to the console.

[C code](#contents.xhtml_sc3_42a)

The C source code for program 1.5 is available here:

1.  #include <stdio.h>

3.  int  main() {
4.  int n, m, p;

6.  printf("Enter first number: ");
7.  scanf("%d", &n); // read an integer input from the user

9.  printf("Enter second number: ");
10.  scanf("%d", &m); // read an integer input from the user

12.  p = n * m; //performed multiplication of two numbers

14.  printf("Product = %d\n", p); // print the output on the screen

16.  return  0;
17.  }

[C code explanation](#contents.xhtml_sc4_43a)

This C code prompts the user to enter two numbers, n, and m then calculates their product and prints it to the console.

It declares three integer variables (n, m, and p). Then, use the scanf() function to read the values of n and m from the console.

It then calculates its product, stores it in the variable p, and finally prints out the p value using the printf() function.

[Program 1.6: Perform division](#contents.xhtml_sc2_44a)

Take two numbers (dividend and divisor) as input and print the quotient and remainder.

[Sample input output](#contents.xhtml_sc3_45a)

Test case #1:

Input:

Enter first number: 98

Enter second number: 3

Output:

Quotient = 32 Remainder = 2

Test case #2:

Input:

Enter first number: 936

Enter second number: 6

Output:

Quotient = 156 Remainder = 0

Test case #3:

Input:

Enter first number: 56

Enter second number: 76

Output:

Quotient = 0 Remainder = 56

[Algorithm](#contents.xhtml_sc3_46a)

The following are the steps for running program 1.6:

Step 1\. Start

Step 2\. Enter two numbers as n and m

Step 3\. p = n/m

Step 4\. r = n%m

Step 5\. Print "Quotient =", p, " Remainder = ", r

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_47a)

[Figure 1.7](#ch01.xhtml_fig1-7) shows an illustration of the program 1.6 flowchart:

![](OPS/images/Figure_1.7.jpg)

Figure 1.7: Flowchart illustrating program 1.6

[Python code](#contents.xhtml_sc3_48a)

The program 1.6 source code in Python is available here:

1.  #read two integer inputs from the user
2.  n=int(input("Enter first number: "))
3.  m=int(input("Enter second number: "))
4.  #performed division to obtain quotient
5.  p= n// m
6.  #obtained remainder using % operator
7.  r=n%m
8.  #print the output on the screen
9.  print("Quotient =", p, "Remainder = ", r)

[Python code explanation](#contents.xhtml_sc4_49a)

This code prompts the user to enter two numbers, n, and m using the input() function preceded by the int() function. It calculates their quotient and the remainder and prints it to the console.

In line three, the// operator is used for integer division to generate a quotient. In line four, the % operator is used to find the remainder.

[C code](#contents.xhtml_sc3_50a)

The program 1.6 source code in C is available here:

1.  #include <stdio.h>

3.  int  main() {
4.  int n, m, p, r;

6.  printf("Enter first number: ");
7.  scanf("%d", &n); // read an integer input from the user

9.  printf("Enter second number: ");
10.  scanf("%d", &m); // read an integer input from the user

12.  p = n / m;  //performed division to obtain quotient
13.  r = n % m;  // obtained remainder using % operator

15.  printf("Quotient = %d Remainder = %d\n", p, r); // print the output on the screen

17.  return  0;
18.  }

[C code explanation](#contents.xhtml_sc4_51a)

This C code prompts the user to enter two numbers, n, and m, then calculates their quotient and remainder and prints them to the console. It does this by declaring four integer variables (n, m, p, and r) and then using the scanf() function to read the values of n and m from the console.

It then calculates their quotient and remainder using the / and % operators and stores them in the variables p and r. Finally, it prints out the values of p and r using the printf() function.

[Program 1.7: Print equivalent rational numbers](#contents.xhtml_sc2_52a)

Print three equivalent rational numbers of a given rational number.

[Sample input output](#contents.xhtml_sc3_53a)

Test case #1:

Input:

Enter numerator: 3

Enter denominator: 6

Output:

Equivalent fractions are: 6 / 12, 9 / 18, 12 / 24

Test case #2:

Input:

Enter numerator: 9

Enter denominator: 4

Output:

Equivalent fractions are: 18 / 8, 27 / 12, 36 / 16

[Algorithm](#contents.xhtml_sc3_54a)

The following steps are provided for running program 1.7:

Step 1\. Start

Step 2\. Enter numerator and denominator as n and m

Step 3\. Print "Equivalent fractions are: ", n*2, /, m*2, ,,n*3, /,
m*3, ,, n*4, /,m*4

Step 4\. Stop

[Flowchart](#contents.xhtml_sc3_55a)

[Figure 1.8](#ch01.xhtml_fig1-8) illustrates the algorithm flowchart:

![](OPS/images/Figure_1.8.jpg)

Figure 1.8: Flowchart to obtain the equivalent rational numbers

[Python code](#contents.xhtml_sc3_56a)

The source code for program 1.7 in Python is provided below:

1.  #read two integer inputs from the user
2.  n=int(input(" Enter numerator: "))
3.  m=int(input(" Enter denominator: "))

5.  #print the output on the screen
6.  #it is obtained by multiplying numerator & #denominator by 2, the 3 and then 4
7.  print(" Equivalent fractions are : ", n*2, "/", m*2, ", ", n*3, "/", m*3, ", ", n*4, "/", m*4)

[Python code explanation](#contents.xhtml_sc4_57a)

This code prompts the user to enter two numbers, n and m, representing the numerator and denominator of a fraction using the input() function preceded by the int() function.

It then calculates three equivalent fractions by multiplying the numerator and denominator by 2, 3, and 4, respectively, and prints them using the print() function.

[C code](#contents.xhtml_sc3_58a)

The source code for program 1.7 in C is provided below:

1.  #include <stdio.h>

3.  int  main() {
4.  int n, m;

6.  printf("Enter numerator: ");
7.  scanf("%d", &n); // read an integer input from the user

9.  printf("Enter denominator: ");
10.  scanf("%d", &m); // read an integer input from the user

12.  // print the output on the screen
13.  //it is obtained by multiplying numerator & denominator by 2, the 3 and then 4
14.  printf("Equivalent fractions are: %d/%d, %d/%d, %d/%d\n", n*2, m*2, n*3, m*3, n*4, m*4);

16.  return  0;
17.  }

[C code explanation](#contents.xhtml_sc4_59a)

This C code prompts the user to enter two numbers, n and m, representing the numerator and denominator of a fraction, respectively.

It then calculates three equivalent fractions by multiplying the numerator and denominator by 2, 3, and 4, respectively, and prints them to the console using the printf() function.

[Program 1.8: Swapping using temporary variable](#contents.xhtml_sc2_60a)

Swap two variables provided by the user using a temporary variable.

[Sample input output](#contents.xhtml_sc3_61a)

Test case #1:

Input:

Enter first number: 65

Enter second number: 92

Output:

Numbers after swapping are 92 65

Test case #2:

Input:

Enter first number: 34

Enter second number: 98

Output:

Numbers after swapping are 98 34

[Algorithm](#contents.xhtml_sc3_62a)

Follow these steps to run the program1.8:

Step 1. Start

Step 2\. Enter two numbers as n and m

Step 3\. temp = n

Step 4\. n=m

Step 5\. m= temp

Step 6\. Print "Numbers after swapping are ", n, m

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_63a)

The flowchart of the algorithm is illustrated in [Figure 1.9](#ch01.xhtml_fig1-9):

![](OPS/images/Figure_1.9.jpg)

Figure 1.9: Flowchart for swapping two numbers using temporary variable

[Python code](#contents.xhtml_sc3_64a)

The Python source code for program 1.8 is provided here:

1.  #read two integer inputs from the user
2.  n=int(input("Enter first number: "))
3.  m=int(input("Enter second number: "))
4.  temp = n #store the value of n in a temporary variable
5.  n=m #copy second variable to first one
6.  m = temp #copy the value of first variable form temporary variable to second variable

8.  #print the output on the screen
9.  print("Numbers after swapping are ", n, m)

[Python code explanation](#contents.xhtml_sc4_65a)

The code takes two numbers as input from the user in n and m variables. It then stores the value of n in temp, assigns the value of m to n, and finally assigns the value of temp to m.

Finally, the interchanged values are displayed in the console.

[C code](#contents.xhtml_sc3_66a)

The C source code for program 1.8 is provided here:

1.  #include <stdio.h>

3.  int  main() {
4.  int n, m, temp;

6.  printf("Enter first number: ");
7.  scanf("%d", &n); // read an integer input from the user

9.  printf("Enter second number: ");
10.  scanf("%d", &m); // read an integer input from the user

12.  temp = n; //store the value of n in a temporary variable
13.  n = m; //copy second variable to first one
14.  m = temp; // copy the value of first variable form temporary variable to second variable.

16.  // print the output on the screen
17.  printf("Numbers after swapping are : n = %d, m = %d\n", n, m);

19.  return  0;
20.  }

[C code explanation](#contents.xhtml_sc4_67a)

This C code prompts the user to enter two numbers, n, and m, then swaps their values using a temporary variable temp. It does this by declaring three integer variables (n, m, and temp) and then using scanf() to read the values of n and m from the console. It then stores the value of n in temp, assigns the value of m to n, and finally assigns the value of temp to m.

This has the effect of swapping the values of n and m. Finally, the code prints out the new values of n and m using print().

[Program 1.9: Swapping without temporary variable](#contents.xhtml_sc2_68a)

Swap two variables provided by the user without using a temporary variable.

[Sample input output](#contents.xhtml_sc3_69a)

Test case #1:

Input:

Enter first number: 66

Enter second number: 99

Output:

Numbers after swapping are 99 66

Test case #2:

Input:

Enter first number: 34

Enter second number: 123

Output:

Numbers after swapping are 123 34

[Algorithm](#contents.xhtml_sc3_70a)

The following steps are provided for running program1.9:

Step 1\. Start

Step 2\. Enter two numbers as n and m

Step 3\. n= n+m

Step 4\. m= n-m

Step 5\. n= n-m

Step 6\. Print "Numbers after swapping are ", n, m

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_71a)

[Figure 1.10](#ch01.xhtml_fig1-10) depicts the program1.9 flowchart:

![](OPS/images/Figure_1.10.jpg)

Figure 1.10: Flowchart illustrating program 1.9

[Python code](#contents.xhtml_sc3_72a)

The following describes the Python code for program 1.9:

1.  #read two integer inputs from the user
2.  n=int(input("Enter first number: "))
3.  m=int(input("Enter second number: "))

5.  #to swap to numbers without temporary variable
6.  #some simple arithmetic is applied

8.  n = n+m
9.  m = n-m
10.  n = n-m

12.  #print the output on the screen
13.  print("Numbers after swapping are ", n, m)

This code takes two integers as input from the user and stores them in variables n and m respectively. It then swaps the values of these variables without using a temporary variable.

It asks the user to enter two numbers. First, it adds the values of n and m and assigns the result to n. Then, it assigns the difference of n and m to m. Since n now contains the sum of the original n and m, m now contains the original value of n.

Finally, it assigns the difference of n and m to n. Since m now contains the original value of n, n now contains the original value of m, the values are swapped. Then, it prints the swapped values.

[C code](#contents.xhtml_sc3_73a)

The following describes the C code for program 1.9:

1.  #include <stdio.h>

3.  int  main() {
4.  int n, m, temp;

6.  printf("Enter first number: ");
7.  scanf("%d", &n); // read an integer input from the user

9.  printf("Enter second number: ");
10.  scanf("%d", &m); // read an integer input from the user

12.  //to swap to numbers without temporary variable
13.  // some simple arithmetic is applied

15.  n = n + m;
16.  m = n - m;
17.  n = n - m;

19.  // print the output on the screen
20.  printf("Numbers after swapping are %d %d\n", n, m);

22.  return  0;
23.  }

[C code explanation](#contents.xhtml_sc4_74a)

This C code prompts the user to enter two numbers, n, and m, and then swaps their values without using a temporary variable. It does this by declaring two integer variables (n and m) and then using scanf() to read the values of n and m from the console.

It then performs the swap using arithmetic operations: First, it adds n and m together and stores the result in n. Then, it subtracts the original value of m from the new value of n and assigns the result to m.

Finally, it subtracts the new value of m from the new value of n and assigns the result to n. This has the effect of swapping the values of n and m. Finally, the code prints out the new values of n and m using printf().

[Program 1.10: Find square of a number](#contents.xhtml_sc2_75a)

Take a number as input and print the square of the number as Square of the number is number.

[Sample input output](#contents.xhtml_sc3_76a)

Test case #1:

Input:

Enter a number 8

Output:

Square of 8 is 64

Test case #2:

Input:

Enter a number: 34

Output:

Square of 34 is 1156

[Algorithm](#contents.xhtml_sc3_77a)

The following are the steps for running program 1.10:

Step 1\. Start

Step 2\. Enter a number in n

Step 3\. Print "Square of ", n, " is ", n*n

Step 4\. Stop

[Flowchart](#contents.xhtml_sc3_78a)

The flowchart for program1.10 is shown in [Figure 1.11](#ch01.xhtml_fig1-11):

![](OPS/images/Figure_1.11.jpg)

Figure 1.11: Flowchart for finding the square of a number

[Python code](#contents.xhtml_sc3_79a)

The Python code for program 1.10 is as follows:

1.  #read an integer input from the user
2.  n=int(input("Enter a number "))

4.  #print the square of the number on the screen
5.  print("Square of ", n, " is ", n*n)

[Python code explanation](#contents.xhtml_sc4_80a)

This code takes an integer input from the user using the input() function and stores it in the variable n. It then calculates the square of the input number by multiplying n with itself and prints the result using the print() function.

[C code](#contents.xhtml_sc3_81a)

The C code for program 1.10 is as follows:

1.  #include <stdio.h>

3.  int  main() {
4.  int n;

6.  printf("Enter a number ");
7.  scanf("%d", &n); // read an integer input from the user

9.  // print the square of the number on the screen
10.  printf("Square of %d is %d\n", n, n*n);

12.  return  0;
13.  }

[C code explanation](#contents.xhtml_sc4_82a)

This C code prompts the user to enter a number, n, and then calculates and prints its square. It does this by declaring an integer variable n and then using scanf() to read the value ofn from the console. It then calculates the square of n using the * operator.

Finally, the code prints out the result using printf() function  using format specifiers %d.

[Program 1.11: Find cube of a number](#contents.xhtml_sc2_83a)

Take a number as input and print the cube of the number as the Cube of the number is number.

[Sample input output](#contents.xhtml_sc3_84a)

Test case #1:

Input:

Enter a number 7

Output:

Cube of 7 is 343

Test case #2:

Input:

Enter a number 21

Output:

Cube of 21 is 9261

[Algorithm](#contents.xhtml_sc3_85a)

To run the program 1.11, the following steps are formulated as an algorithm:

Step 1\. Start

Step 2\. Enter a number in n

Step 3\. Print "Cube of ", n, " is ", n*n*n

Step 4\. Stop

[Flowchart](#contents.xhtml_sc3_86a)

[Figure 1.12](#ch01.xhtml_fig1-12) depicts the flowchart of program 1.11:

![](OPS/images/Figure_1.12.jpg)

Figure 1.12: Flowchart to find the cube of a number

[Python code](#contents.xhtml_sc3_87a)

The program 1.11 source code in Python is specified as follows:

1.  #read an integer input from the user
2.  n=int(input("Enter a number "))
3.  #print the cube of the number on the screen
4.  print("Cube of ", n, " is ", n*n*n)

[Python code explanation](#contents.xhtml_sc4_88a)

This code takes an integer input from the user using the input() function and stores it in the variable n. It then calculates the cube of the input number by multiplying n with itself three times (n*n*n) and prints the result using the print()function.

[C code](#contents.xhtml_sc3_89a)

The program 1.11 source code in C is specified as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int n;
5.  printf("Enter a number ");
6.  scanf("%d", &n); // read an integer input from the user

8.  // print the cube of the number on the screen
9.  printf("Cube of %d is %d", n, n*n*n);
10.  }

[C code explanation](#contents.xhtml_sc4_90a)

This C code takes an integer input from the user and calculates the cube of the input number using the formula n*n*n. The output is then printed to the console using the printf() function.

[Program 1.12: Find average](#contents.xhtml_sc2_91a)

Take three numbers as input and print their average.

[Sample input output](#contents.xhtml_sc3_92a)

Test case #1:

Input:

Enter first number 23

Enter second number 33

Enter third number 65

Output:

Average = 40.333333333333336

Test case #2:

Input:

Enter first number 7

Enter second number 3

Enter third number 4

Output:

Average = 4.6666666667

[Algorithm](#contents.xhtml_sc3_93a)

To run the program 1.12, the algorithm is as follows:

Step 1\. Start

Step 2\. Enter three numbers as n, m, and p

Step 3\. a = (n+m+p)/3

Step 4\. Print "Average = ", a

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_94a)

The flowchart of the program 1.12 is illustrated in [Figure 1.13](#ch01.xhtml_fig1-13):

![](OPS/images/Figure_1.13.jpg)

Figure 1.13: Flowchart illustrating program 1.12

[Python code](#contents.xhtml_sc3_95a)

Here is the Python source code for program 1.12:

1.  #read three integer inputs from the user
2.  n=int(input("Enter first number "))
3.  m=int(input("Enter second number "))
4.  p=int(input("Enter third number "))

6.  #find average
7.  a = (n+m+p)/3

9.  #print the output on the screen
10.  print("Average = ", a)

[Python code explanation](#contents.xhtml_sc4_96a)

This code takes three integer inputs from the user using the input()and int()functions and calculates their average. The average is then printed to the console using the print()function.

It calculates the average of the three input numbers by adding n, m, and p and dividing the sum by 3. The result is assigned to the variable a.

[C code](#contents.xhtml_sc3_97a)

Here is the C source code for program 1.12:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int n,m, p;
5.  float a;
6.  printf("Enter three numbers");
7.  scanf("%d%d%d",& n,&m, &p); // read three integer inputs from the user
8.  //find the sum of three numbers and divide it by 3
9.  a = (n+m+p)/3.0;
10.  // print the output on the screen
11.  printf("Average =%f", a);
12.  }

[C code explanation](#contents.xhtml_sc4_98a)

This code takes three integer inputs from the user using the scanf() function and calculates their average. The average is then printed to the console using the printf() function.

Here, the sum of three numbers is divided by 3.0. In C, dividing an integer value by an integer value gives an integer result. However, an average of three numbers can be a real number. Hence, the sum is divided by a float number (3.0).

[Program 1.13: Find percentage marks](#contents.xhtml_sc2_99a)

Take your marks in 5 subjects as input and print the percentage marks.

[Sample input output](#contents.xhtml_sc3_100a)

Test case #1:

Input:

Enter marks in first subject 20

Enter marks in 2nd subject 21

Enter marks in 3rd subject 21

Enter marks in 4th subject 21

Enter marks in 5th subject 21

Output:

Percentage = 20.8

Test case #2:

Input:

Enter marks in first subject 70

Enter marks in 2nd subject 80

Enter marks in 3rd subject 90

Enter marks in 4th subject 85

Enter marks in 5th subject 75

Output:

Percentage = 80

[Algorithm](#contents.xhtml_sc3_101a)

The following steps are expressed as an algorithm to execute program 1.13:

Step 1\. Start

Step 2\. Enter marks in 5 subjects as s1, s2, s3, s4 and s5

Step 3\. a= (s1+s2+s3+s4+s5)*100/500

Step 4\. Print "Percentage = ", a

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_102a)

[Figure 1.14](#ch01.xhtml_fig1-14) shows the flowchart of program 1.13:

![](OPS/images/Figure_1.14.jpg)

Figure 1.14: Flowchart illustrating program 1.13

[Python code](#contents.xhtml_sc3_103a)

The following describes the Python source code for program 1.13:

1.  #read marks in five subjects as inputs from the user

3.  s1=int(input(" Enter marks in first subject "))
4.  s2=int(input("Enter marks in 2nd subject "))
5.  s3=int(input("Enter marks in 3rd subject "))
6.  s4=int(input("Enter marks in 4th subject "))
7.  s5=int(input("Enter marks in 5th subject "))

9.  #find percentage marks
10.  a = (s1+s2+s3+s4+s5)*100/500

12.  #print the output on the screen
13.  print ("Percentage =", a)

[Python code explanation](#contents.xhtml_sc4_104a)

This code prompts the user to enter marks in five different subjects and calculates the percentage of marks obtained by the student. The percentage marks is calculated by dividing the sum of all the marks by 500 and multiplying the result by 100\. The result is stored in the variable a. Finally, the output is printed on the console.

[C code](#contents.xhtml_sc3_105a)

The following describes the Python source code for program 1.13:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int s1, s2, s3, s4, s5;
5.  float a;
6.  printf("Enter marks in 5 subjects ");
7.  scanf("%d%d%d%d%d",&s1,&s2, &s3, &s4, &s5); // read five integer inputs from the user
8.  //calculate the percentage of marks in 5 subjects
9.  a = (s1+s2+s3+s4+s5)*100/500.0;
10.  // print the output on the screen
11.  printf ("Percentage = %f ", a);
12.  }

[C code explanation](#contents.xhtml_sc4_106a)

This code prompts the user to enter marks in five different subjects, and entered values are stored in five different variables. The next line calculates the total marks obtained by adding marks in all five subjects and then multiplying the sum by 100/500.0 to get the percentage of marks. The result is stored in the variable a and displayed using the printf()function. It should be noted that the sum is divided by 500.0 to obtain the real value as result of the division.

[Program 1.14: Convert meter to centimeter](#contents.xhtml_sc2_107a)

Take length (in meters) as input and print it in centimeters.

[Sample input output](#contents.xhtml_sc3_108a)

Test case #1:

Input:

Enter length in meters 3.4567

Output:

Length in cm is 345.67

Test case #2:

Input:

Enter length in meters 10.5

Output:

Length in cm is 1050

[Algorithm](#contents.xhtml_sc3_109a)

The steps listed below are formed as an algorithm to run program 1.14:

Step 1\. Start

Step 2\. Enter length in meters as m

Step 3\. cm= m*100

Step 4\. Print "Length in cm is ", cm

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_110a)

The flowchart of program 1.14 is shown in [Figure 1.15](#ch01.xhtml_fig1-15):

![](OPS/images/Figure_1.15.jpg)

Figure 1.15: Flowchart of program 1.14

[Python code](#contents.xhtml_sc3_111a)

The Python source code for program 1.14 is as follows:

1.  #read float type input from the user
2.  m=float(input("Enter length in meters "))
3.  #convert cm to m by multiplying by 100
4.  cm = m*100
5.  #print the output on the screen
6.  print("Length in cm is ", cm)

[Python code explanation](#contents.xhtml_sc4_112a)

This code prompts the user to enter a length in meters, then calculates and prints the equivalent length in centimeters. This program converts this by multiplying the m value by 100, which is the conversion factor from meters to centimeters.

[C code](#contents.xhtml_sc3_113a)

The C source code for program 1.14 looks as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  float m, cm;
5.  printf("Enter length in meters");
6.  scanf("%f",&m); // read a float input from the user
7.  //to convert meter in cm, multiply it by 100
8.  cm = m*100;
9.  // print the output on the screen
10.  printf("Length in cm is %f", cm);
11.  }

[C code explanation](#contents.xhtml_sc4_114a)

This C language code is a simple example of converting a length measurement from one unit (meters) to another (centimeters) by multiplying the value of m by 100, using input and output functions to interact with the user.

[Program 1.15: Convert degree F to degree C](#contents.xhtml_sc2_115a)

Take temperature (in degree F) as input and print it in degree C.

[Sample input output](#contents.xhtml_sc3_116a)

Test case #1:

Input:

Enter temperature in degree F: 98.4

Output:

Temperature in degree Celsius is 36.888888888888886

Test case #2:

Input:

Enter temperature in degree F: 32

Output:

Temperature in degree Celsius is 0.0

[Algorithm](#contents.xhtml_sc3_117a)

The steps to run program 1.15 are listed below:

Step 1\. Start

Step 2\. Read temperature in degree F as F1

Step 1\. C1=(F1-32)*5/9

Step 2\. Print "Temperature in degree Celsius is ", C1

Step 3\. Stop

[Flowchart](#contents.xhtml_sc3_118a)

[Figure 1.16](#ch01.xhtml_fig1-16) shows an illustration of the program 1.15 in a flowchart:

![](OPS/images/Figure_1.16.jpg)

Figure 1.16: Flowchart of program 1.15

[Python code](#contents.xhtml_sc3_119a)

The Python source code for program 1.15 is described below:

1.  #read float type input from the user
2.  F1 = float(input("Enter temperature in degree F: "))
3.  #convert temp in F to C
4.  C1 = (F1 - 32) * 5 / 9
5.  #print the output on the screen
6.  print("Temperature in degree Celsius is ", C1)

[Python code explanation](#contents.xhtml_sc4_120a)

This code prompts the user to enter a temperature in Fahrenheit and reads the input value as an integer, which is stored in the variable F1. Then, it converts the temperature in Fahrenheit to Celsius using the formula (F1 - 32) * 5/9, where F1 is the temperature in Fahrenheit.

The result is stored in the variable C1. Finally, it prints the converted temperature in Celsius to the console.

[C code](#contents.xhtml_sc3_121a)

The C source code for program 1.15 is described below:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  float F1, C1;
5.  printf("Enter temperature in degree F ");
6.  scanf("%f",&F1); // read a float input from the user
7.  //convert temp on F to C
8.  C1= (F1-32)*5/9.0;
9.  // print the output on the screen
10.  printf("Temperature in degree Celsius is %f", C1);
11.  }

[C code explanation](#contents.xhtml_sc4_122a)

This C program takes an input temperature in Fahrenheit and converts it to Celsius using the formula (F1-32)*5/9. Since temperature can be a real number, F1 and C1 are declared float, and the %f format specifier is used. Again, to obtain a real number as a result of division, 9.0 (a real number) is used in the denominator.

[Program 1.16: Convert inch to feet](#contents.xhtml_sc2_123a)

Take height (in inches) as input. Convert it into feet and display it as Your height is 5 feet 2 in.

[Sample input output](#contents.xhtml_sc3_124a)

Test case #1:

Input:

Enter height in inches 63.5

Output:

Your height is 5.0 feet 3.5 in

Test case #2:

Input:

Enter height in inches 55.0

Output:

Your height is 4.0 feet 7.0 in

[Algorithm](#contents.xhtml_sc3_125a)

The following steps are provided for running program 1.16:

Step 1\. Start

Step 2\. Read height in inches as i

Step 3\. f = i/12

Step 4\. in = i%12

Step 5\. Display "Your height is ", f, " feet ",in, " inch. "

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_126a)

Here, the flowchart ofprogram 1.16 is shown in [Figure 1.17](#ch01.xhtml_fig1-17):

![](OPS/images/Figure_1.17.jpg)

Figure 1.17: Flowchart illustrating program 1.16

[Python code](#contents.xhtml_sc3_127a)

The Python source code of program 1.16 is described as follows:

1.  #read float type input from the user
2.  i=float(input("Enter height in inches "))
3.  #convert inch to feet-inch
4.  f=i//12
5.  inch = i%12
6.  #print the output on the screen
7.  print("Your height is ", f, " feet", inch, "in")

[Python code explanation](#contents.xhtml_sc4_128a)

This Python program takes an input height in inches in variable i and converts it to feet and inches. It calculates the number of whole feet in height by dividing i by 12 using the integer division operator // and stores the result in the variable f.

Then, it calculates the number of remaining inches by dividing the remainder of i by 12 using the modulus operator % and stores the result (remainder) in the variable inch. Also, note that the conversion to feet and inches is not rounded, so the output may include a fractional part for the inches.

[C code](#contents.xhtml_sc3_129a)

The C source code of program 1.16 is described as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, in, f;

6.  printf("Enter height in inches ");
7.  scanf("%d",&i); // read a float input from the user
8.  //convert height given in inches to feet, inches
9.  f=i/12;
10.  in = i%12;
11.  // print the output on the screen
12.  printf("Your height is %d feet %d in", f, in);
13.  }

[C code explanation](#contents.xhtml_sc4_130a)

This program takes an input height in inches in variable i and converts it to feet and inches. It declares two float variables, in and i, to hold the height in inches and remaining inches, respectively, and an integer variable f, to hold the number of feet in the height.

First, it calculates the number of whole feet in height by dividing i by 12. Then, it calculates the remaining inches by taking the remainder of dividing i by 12 using % operater  and then stores the result in the variable in. It finally prints the result to the console.

[Program 1.17: Find area of a rectangle](#contents.xhtml_sc2_131a)

Read two sides of a rectangle (in meters) as input and calculate its area.

[Sample input output](#contents.xhtml_sc3_132a)

Test case #1:

Input:

Enter length of the rectangle (in meters) 3.5

Enter breadth of the rectangle (in meters) 5

Output:

Area of (3.5 X 5.0) is 17.5 sq meter

Test case #2:

Input:

Enter length of the rectangle (in meters) 4

Enter breadth of the rectangle (in meters) 5

Output:

Area of (4.0X 5.0) is 20 sq meter

Algorithm

The action listed below is an algorithm to execute program 1.17:

Step 1\. Start

Step 2\. Read two sides (in meters) of a rectangle as l and b

Step 3\. area=l*b

Step 4\. Display "Area of (", l, " X ", b, ") is “, area

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_133a)

Program 1.17 flowchart is depicted in [Figure 1.18](#ch01.xhtml_fig1-18):

![](OPS/images/Figure_1.18.jpg)

Figure 1.18: The flowchart of program 1.17

[Python code](#contents.xhtml_sc3_134a)

The Python source code for program 1.17 is as follows:

1.  #read float type inputs from the user
2.  l=float(input("Enter length of the rectangle "))
3.  b=float(input("Enter breadth of the rectangle "))
4.  #obtain area
5.  area=l*b
6.  #print the output on the screen
7.  print("Area of (", l, " X ", b, ") is ", area)

[Python code explanation](#contents.xhtml_sc4_135a)

The code reads the length and breadth of a rectangle, calculates its area by multiplying length and breadth, and then prints the area to the console.

[C code](#contents.xhtml_sc3_136a)

The C source code for program 1.17 is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  float l,b, area;
5.  printf("Enter two sides of a rectangle (in meters)");
6.  scanf("%f%f",&l, &b); // read two float inputs from the user
7.  //obtain area by multiplying length and breath
8.  area = l*b;
9.  // print the output on the screen
10.  printf("Area of ( %f X %f) is %f sq meter",l,b, area);
11.  }

[C code explanation](#contents.xhtml_sc4_137a)

This program takes the sides of a rectangle as input. The area of the rectangle is calculated by multiplying the length (l) and breadth (b) of the rectangle, and the result is stored in the area variable.

Finally, the printf() function is used to display the area of the rectangle on the screen, along with the values of l and b.

[Program 1.18: Find area of a circle](#contents.xhtml_sc2_138a)

Read the radius of a circle as input and calculate its area.

[Sample input output](#contents.xhtml_sc3_139a)

Test case #1:

Input:

Enter the radius of circle 4.5

Output:

Area of circle is 63.585

Test case #2:

Input:

Enter the radius of circle 2.4

Output:

Area of circle is 18.09

[Algorithm](#contents.xhtml_sc3_140a)

Program 1.18 can be executed using the algorithm listed below:

Step 1\. Start

Step 2\. Read the radius of circle as r

Step 3\. pie=3.14

Step 4\. area=pie*r*r

Step 5\. Display "Area of circle is ", area

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_141a)

[Figure 1.19](#ch01.xhtml_fig1-19) depicts the flowchart of program 1.18:

![](OPS/images/Figure_1.19.jpg)

Figure 1.19: Flowchart for computing the area of a circle

[Python code](#contents.xhtml_sc3_142a)

Here is the Python source code for program 1.18:

1.  #read float type input from the user
2.  r=float(input("Enter the radius of circle "))
3.  #define constant value of Pie
4.  pie=3.14
5.  #obtain area
6.  area=pie*r*r
7.  #print the output on the screen
8.  print("Area of circle is ", area)

[Python code explanation](#contents.xhtml_sc4_143a)

This code reads the radius of a circle from the user and calculates its area. The program starts with the user entering the circle’s radius value using the input() function. The input value is read as a string and converted to float using the float() function.

The area of the circle is calculated using the formula A = πr², where r is the radius of the circle. The result is displayed on the screen using the print() function, along with a message that says Area of circle is.

[C code](#contents.xhtml_sc3_144a)

Here is the C source code for program 1.18:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  float r, pie,area;
5.  printf("Enter the radius of circle");
6.  scanf("%f", &r); // read a float input from the user
7.  //define value of pie
8.  pie=3.14;
9.  //find area of circle
10.  area=pie*r*r;
11.  // print the output on the screen
12.  printf("Area of circle is %f", area);
13.  }

[C code explanation](#contents.xhtml_sc4_145a)

The program calculates the area of a circle. The program starts with including the standard input-output header file using the #include directive. Three variables are declared in the main function: r, pie, and area. These variables are of type float. The value of the mathematical constant pi is assigned to a variable called pie.

The area of the circle is calculated using the formula A = πr², where r is the radius of the circle. Finally, the printf() function is used to display the area of the circle on the screen, along with a message that says Area of circle is.

[Program 1.19: Find area of parallelogram](#contents.xhtml_sc2_146a)

Read the base and height of a parallelogram as area and compute its area.

[Sample input output](#contents.xhtml_sc3_147a)

Test case #1:

Input:

Enter base of a parallelogram 6.5

Enter height of a parallelogram 3.5

Output:

Area of (6.5 X 3.5) is 22.75

Test case #2:

Input:

Enter base of a parallelogram 3.5

Enter height of a parallelogram 4.5

Output:

Area of (3.500000 X 4.500000) is 15.750000

[Algorithm](#contents.xhtml_sc3_148a)

Program 1.19 can be executed using the steps listed below:

Step 1\. Start

Step 2\. Read base and height of a parallelogram as b and h

Step 3\. area=b*h

Step 4\. Display "Area of (", b, " X ", h, ") is ", area

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_149a)

[Figure 1.20](#ch01.xhtml_fig1-20) illustrates the flowchart of program 1.19:

![](OPS/images/Figure_1.20.jpg)

Figure 1.20: Flowchart illustrating program 1.19

[Python code](#contents.xhtml_sc3_150a)

The source code in Python of program 1.19 is available here:

1.  #read float type inputs from the user
2.  b=float(input("Enter base of a parallelogram"))
3.  h=float(input("Enter height of a parallelogram"))
4.  #obtain area
5.  area=b*h
6.  #print the output on the screen
7.  print("Area of (", b, " X ", h, ") is ", area)

[Python code explanation](#contents.xhtml_sc4_151a)

The given Python code reads the base and height of a parallelogram from the user, calculates its area using the formula area = base * height, and then prints the area on the console.

[C code](#contents.xhtml_sc3_152a)

The source code in C of program1.19 is available here:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  float b, h, area;
5.  printf("Enter base of a parallelogram ");
6.  scanf("%f",&b); // read a float input from the user
7.  printf("Enter height of a parallelogram ");
8.  scanf("%f",&h); // read a float input from the user
9.  //obtain area
10.  area = b*h;
11.  // print the output on the screen
12.  printf("Area of ( %f X %f) is %f",b,h, area);
13.  }

[C code explanation](#contents.xhtml_sc4_153a)

The code takes the base and height of a parallelogram from the user, calculates its area using the formula area = base * height, and then prints the area to the console. Format specifier %f is used to handle real numbers.

[Program 1.20: Find distance between two points](#contents.xhtml_sc2_154a)

Find the distance between two points P1 = (x1, y1) and P2 = (x2, y2) using the Manhattan distance and Euclidean distance formula.

[Sample input output](#contents.xhtml_sc3_155a)

Test case #1:

Input:

Enter x-point 1 3

Enter y-point 1 6

Enter x-point 2 4

Enter y-point 2 5

Output:

Manhattan distance is 2

Euclidean distance is 1.4142135623730951

Test case #2:

Input:

Enter x-point 1 4

Enter y-point 1 5

Enter x-point 2 10

Enter y-point 2 20

Output:

Manhattan distance is 21

Euclidean distance is 16.155

[Algorithm](#contents.xhtml_sc3_156a)

The following steps execute program 1.20:

Step 1\. Start

Step 2\. Enter point 1 as x1, y1

Step 3\. Enter point 2 as x2, y2

Step 4\. man_dis = abs(x1-x2) + abs (y1-y2)

Step 5\. eucl_dis = sqrt((x1-x2)* (x1-x2) + (y1-y2)* (y1-y2))

Step 6\. Display "Manhattan distance is ", man_dis

Step 7\. Display "Euclidean distance is ", eucl_dis

Step 8\. Stop

[Flowchart](#contents.xhtml_sc3_157a)

The program 1.20 flowchart is shown in [Figure 1.21](#ch01.xhtml_fig1-21):

![](OPS/images/Figure_1.21.jpg)

Figure 1.21: Flowchart depicting program 1.20

[Python code](#contents.xhtml_sc3_158a)

The Python source code for program 1.20 is provided below:

1.  import math

3.  #read coordinates (x, y) as input from the user
4.  x1=int(input("Enter x-point 1 "))
5.  y1=int(input("Enter y-point 1 "))
6.  x2=int(input("Enter x-point 2 "))
7.  y2=int(input("Enter y-point 2 "))
8.  #obtain Manhattan distance
9.  man_dis = abs(x1-x2) + abs (y1-y2)
10.  #obtain Euclidean distance
11.  eucl_dis = math.sqrt((x1-x2)* (x1-x2) + (y1-y2)* (y1-y2))
12.  #print the output on the screen
13.  print("Manhattan distance is ",man_dis)
14.  print("Euclidean distance is ", eucl_dis)

[Python code explanation](#contents.xhtml_sc4_159a)

This code reads in the x and y coordinates of two points and then calculates the Manhattan and Euclidean distances between them. The Manhattan distance is the sum of the absolute differences between the x and y coordinates, while the Euclidean distance is the square root of the sum of the squared differences of the x and y coordinates. Finally, the code prints out the calculated distances. Here, the math library is imported at the beginning to calculate the square root.

[C code](#contents.xhtml_sc3_160a)

The C source code for program 1.20 is provided below:

1.  #include<stdio.h>
2.  #include<math.h>
3.  void  main()
4.  {
5.  float x1,y1,x2,y2,man_dis, eucl_dis;
6.  printf("Enter x1, y1, x2, y2");
7.  scanf("%f%f%f%f", &x1, &y1, &x2, &y2); // read four float inputs from the user
8.  //calculate Manhattan distance
9.  man_dis = abs(x1-x2) + abs (y1-y2);
10.  //calculate Euclidean distance
11.  eucl_dis = sqrt((x1-x2)* (x1-x2) + (y1-y2)* (y1-y2));
12.  // print the output on the screen
13.  printf("Manhattan distance is %f",man_dis);
14.  printf("\nEuclidean distance is %f",eucl_dis);
15.  }

[C code explanation](#contents.xhtml_sc4_161a)

<math.h> is a library of C where sqrt() function is defined. Thus, it is used in this program. The user is asked to read the x and y coordinates of two points and then it calculates the Manhattan distance and Euclidean distance between them. The Manhattan distance is the sum of the absolute differences between the x and y coordinates, while the Euclidean distance is the square root of the sum of the squared differences of the x and y coordinates. Finally, the code prints out the calculated distances.

[Program 1.21: Obtain logical truth table](#contents.xhtml_sc2_162a)

Print the truth table of logical operators AND, OR, and NOT.

[Sample input output](#contents.xhtml_sc3_163a)

| x | y | x and y | x or y | Not x |
| 0 | 0 | 0 | 0 | True |
| 0 | 1 | 0 | 1 | True |
| 1 | 0 | 0 | 1 | False |
| 1 | 1 | 1 | 1 | False |

[Algorithm](#contents.xhtml_sc3_164a)

The algorithm listed below is used to execute program 1.21:

Step 1\. Start

Step 2\. Print("x y (x and y) (x or y) (not x)")

Step 3\. x=0, y=0

Step 4\. Print (x, y, x&&y, x||y, !x)

Step 5\. x=0, y=1

Step 6\. Print (x, y, x&&y, x||y, !x)

Step 7\. x=1, y=0

Step 8\. Print (x, y, x&&y, x||y, !x)

Step 9\. x=1, y=1

Step 10\. Print (x, y, x&&y, x||y, !x)

Step 11\. Stop

[Flowchart](#contents.xhtml_sc3_165a)

The flowchart of the algorithm is illustrated in [Figure 1.22](#ch01.xhtml_fig1-22):

![](OPS/images/Figure_1.22.jpg)

Figure 1.22: Flowchart depicting program 1.21

[Python code](#contents.xhtml_sc3_166a)

The Python source code for program 1.21 is written as follows:

1.  print("x y x and y x or y not x")
2.  #first time value of x & y is 0
3.  x=0
4.  y=0
5.  # and is to perform bitwise ANd operation, or #performs OR operation, not perform NOT operation
6.  print (x, y, x and y, x or y, not x)

8.  #then, values of x & y are set to 0 & 1
9.  x=0
10.  y=1
11.  print (x, y, x and y, x or y, not x)

13.  #then, values of x & y are set to 1 & 0
14.  x=1
15.  y=0
16.  print (x, y, x and y, x or y, not x)

18.  #then, values of x & y are set to 1 & 1
19.  x=1
20.  y=1
21.  print (x, y, x  and y, x or y, not x)

[Python code explanation](#contents.xhtml_sc4_167a)

This code is a series of logical operations on two binary variables x and y. First, it prints the header for the table that will show the output of the logical operations.

Then, it sets the different possible logical combination of values to x and y and prints the values of x and y, followed by the result of the AND operation (x and y), followed by the result of the OR operation (x or y), and finally the result of the NOT operation (not x).

[C code](#contents.xhtml_sc3_168a)

The C source code for program 1.21 is written as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int x,y;
5.  printf("x y x and y x or y not x");
6.  //first time value of x & y is 0
7.  x=0;
8.  y=0;
9.  // && is to perform bitwise ANd operation, || performs OR operation, ! perform NOT operation
10.  printf ("\n%d %d %d %d %d",x, y, x&&y, x||y, !(x));
11.  //then, values of x & y are set to 0 & 1
12.  x=0; y=1;
13.  printf ("\n%d %d %d %d %d",x, y, x&&y, x||y, !(x));
14.  //then, values of x & y are set to 1 & 0
15.  x=1; y=0;
16.  printf ("\n%d %d %d %d %d",x, y, x&&y, x||y, !(x));
17.  //then, values of x & y are set to 1 & 1
18.  x=1; y=1;
19.  printf ("\n%d %d %d %d %d",x, y, x&&y, x||y, !(x));
20.  }

[C code explanation](#contents.xhtml_sc4_169a)

This code is a series of logical operations on two binary variables x and y. First, it prints the header for the table that will show the output of the logical operations.

Then, it sets the different possible logical combination of values to x and y and prints the values of x and y, followed by the result of the AND operation (x and y), followed by the result of the OR operation (x or y), and finally the result of the NOT operation (not x).

In C language, && is used for AND operation, || is used for OR operation, and! is a unary not operation.

[Conclusion](#contents.xhtml_sc2_170a)

This chapter has provided a comprehensive understanding of the fundamental programming concepts and techniques for handling input and output operations. Readers have learned how to break down given problems into manageable steps and visualize the program flow using the presented algorithms and flowcharts as visual aids. Python and C programming languages have allowed for hands-on experience in implementing input-output programs, reinforcing concepts such as user input handling, data processing, and result display.

The next chapter on programs with conditional statements will discuss the interesting realm of conditional statements, exploring how programming languages use decision-making constructs to control the execution flow.

[Points to remember](#contents.xhtml_sc2_171a)

*   Use clear and precise language while writing the steps of the algorithm. To check the correctness of the algorithm, test it with different input combinations.
*   While drawing the flowchart, use standard symbols such as oval for mentioning start and end points, parallelogram for input/output, rectangle for process steps, and arrows for flow direction.
*   Import the required modules using import in Python.
*   Every C program begins with a main function, and every line in a C program ends with a semicolon.
*   All variables to be used in a C program are to be declared at the beginning of the program, whereas explicit variable declaration is not required in Python language.
*   Include relevant header files using #include in a C program.
*   Use scanf() and printf() functions to accept user input from the standard input stream and display the output to the standard output stream in C language.
*   In Python, utilize the input() function to accept user input from the standard input stream and print() function to display the output to the standard output stream.

[Questions](#contents.xhtml_sc2_172a)

1. Write a Python and C codes for the program, which takes two numbers as input and prints the subtracted value.

2. Draw a flowchart and write the algorithm, which takes four numbers as input and prints their product.

3. Write an algorithm and Python code for the program that takes temperature (in degree Celsius) as input and prints it in degree Fahrenheit.

4. Draw a flowchart and write the C code for the program that takes length (in km) as input and print it in meters.

5. Write the code in Python and C for the program, which takes the base and height of a triangle (in cm) as input and computes its area.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](OPS/images/fm1.png)

# [CHAPTER 2Conditional Statements](#contents.xhtml_ch02a)

[Introduction](#contents.xhtml_sc2_173a)

Certain variations of conditional statements, such as the first type, involve taking action only if the condition is true. The second type deals with taking action 1 if the condition is true; otherwise, it proceeds to take action 2\. The third type takes action 1 if condition 1 is true. If condition 1 is false, it checks condition 2\. If condition 2 is true, then action 2 is executed; otherwise, it resorts to taking action 3\. The fourth type requires both condition 1 and condition 2 to be true for action 1 to be executed. If any of the conditions is false, it leads to executing action 2\. The fifth type calls for taking action 1 if either condition 1 or condition 2 or both are true. However, if both conditions are false, action 2 is carried out. The final type involves checking condition 1 first. If condition 1 is true, it proceeds to check condition 2\. If both conditions are true, action 1 is taken.

In programming, the combinations of if-else statements are used to make decisions based on certain conditions. It allows the program to execute code blocks depending on whether a given condition is true or false. Here if, else-if, else, elif are the keywords.

Here is a breakdown of how the if-else statement works:

*   The condition is a logical expression that evaluates to either true or false.
*   If the condition is true, the code within the if block is executed.
*   If the condition is false, the code within the else block is executed (if present).
*   The else block is optional. If it is not included, the program will simply skip the code within the else block if the condition is false.
*   The code within the if and else blocks can consist of a single statement or multiple statements enclosed within curly braces {} (in C program) or indented towards the right side (in Python program).
*   Multiple if-else statements can be nested to handle more complex conditions. The else-if (elif, in Python) construct can also specify additional conditions to check if the initial condition is false.

[Structure](#contents.xhtml_sc2_174a)

In this chapter, there are a total of 18 programs, and five sub-sections complement each program:

*   Understand the program objective with sample test cases consisting of inputs and outputs. It will give the user an understanding of what kind of user input is expected and what result will be projected for a particular program.
*   Understand the program with an algorithm. This will help the user to understand the logic and methodology behind writing the sequence of steps required to solve a program.
*   Visualize the program flow with flowcharts. Program objectives can be understood easily with the flowchart representation. User will understand which symbols to use in which context throughout different program’s flowchart representations.
*   Python source code of each program. Each program’s source code in Python programming language is provided to the user so the user can understand the basic operations of the language. An explanation of each code is also provided.
*   C implementation of each program. Users can learn the basic concepts of C language with the provided C language code and its explanation for every program.

[Objectives](#contents.xhtml_sc2_175a)

This chapter provides readers with a comprehensive understanding of conditional statements and their importance in the development of programs. It covers the fundamental concepts behind conditional statements and how they enable decision-making within algorithms through if-else constructs. Additionally, the chapter imparts the skills necessary for visual representations of conditional statements in program flow using flowcharts, facilitating a clearer and more intuitive grasp of their functionality.

Moreover, the chapter focuses on practical application by demonstrating how to implement conditional statements in Python and C programming languages. Sample codes are provided to offer hands-on experience, allowing readers to practice and gain confidence in effectively utilizing conditional statements in real-world coding scenarios. By the end of this chapter, readers will have acquired the knowledge and skills to leverage conditional statements in their programming.

[Program 2.1: Find absolute value of a number](#contents.xhtml_sc2_176a)

Print the absolute value of a number entered by the user.

[Sample input output](#contents.xhtml_sc3_177a)

Test case #1:

Input: Enter the value of n: -23

Output: 23

Test case #2:

Input: Enter the value of n: 56

Output: 56

Test case #3:

Input:  Enter the value of n: 0

Output: 0

[Algorithm](#contents.xhtml_sc3_178a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Declare variable n

Step 3\. Read n

Step 4\. if n >= 0

i. print n

Step 5\. else

i. print n*(-1)

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_179a)

[Figure 2.1](#ch02.xhtml_fig2-1) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_2.1.jpg)

Figure 2.1: Flowchart illustrating the program 2.1

[Python code](#contents.xhtml_sc3_180a)

Python code for the program 2.1 is as follows:

1.  n=int(input("Enter n: "))
2.  if n >= 0:
3.  print( n)
4.  else:
5.  print(-1*n)

[Python code explanation](#contents.xhtml_sc4_181a)

The given code asks the user to enter a number, which is taken as the input using the input() function, and then the value is converted to an integer using the int()function. In Python, the block of if and else statements are indented towards the right. if and else are the keywords. Here, if-else statement is used to check if n is greater than 0. If the number is greater than 0, it is called a positive number. Otherwise, it is called a negative number. if keyword is followed by the condition (n >= 0). If the condition is true, the next statement in the program print(n) will execute and print the value of n. Otherwise, this statement will be skipped, and a block of else will execute. It will multiply the value of n after multiplying it with –1.

[C code](#contents.xhtml_sc3_182a)

C code for the program 2.1 is as follows:

1.  #include<stdio.h>
2.  #include<math.h>
3.  int  main()
4.  {
5.  int n;
6.  printf("Enter the value of n: ");
7.  scanf("%d", &n);
8.  if(n >= 0) //check if n is a positive number
9.  printf("%d", n);
10.  else //Else block will execute only if n is a negative number
11.  printf("%d",-1*n);
12.  return 0;
13.  }

[C code explanation](#contents.xhtml_sc4_183a)

The given code prompts the user to enter a value for n, reads the input, and then checks whether the value of n is positive. If the number is greater than 0, it is called a positive number. Otherwise, it is called a negative. An if-else statement is used to check whether n is greater than 0. If it is greater than or equal to zero, the value of n is displayed as it is. If the value of n is less than zero, it is multiplied by -1 to make it positive, and then the resultant value is displayed.

The if and else are the keywords used for the if-else statement. The condition is enclosed in parentheses (). It is a logical expression that evaluates to either true or false. If the condition is true, the code block follows the if statement and is executed. If the condition is false, the code block immediately following the else statement is executed (if present).

Unlike Python, the code block associated with the if statement is enclosed in curly braces {}. It contains one or more statements executed if the condition is true. The else part is optional. If it is present, it is followed by a code block enclosed in curly braces {}. This code block contains one or more statements executed if the condition is false.

[Program 2.2: Check if you are an adult?](#contents.xhtml_sc2_184a)

Ask the user to enter the name and the age. Check if the age is >=18, then print the message Abc is an adult.

[Sample input output](#contents.xhtml_sc3_185a)

Test case #1:

Input:

Enter your name: Neo

Enter your age: 98

Output:

Neo is an adult

Test case #2:

Input:

Enter your name: John

Enter your age: 10

Output:

[Algorithm](#contents.xhtml_sc3_186a)

The steps to be followed to write the program are:

Step 1\. Start

Step 2\. Enter your name and age as n, a

Step 3\. if a>=18:

Step 4\. print(n, " is an adult")

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_187a)

[Figure 2.2](#ch02.xhtml_fig2-2) illustrates the flowchart of the program:

![](OPS/images/Figure_2.2.jpg)

Figure 2.2: Flowchart illustrating the program 2.2

[Python code](#contents.xhtml_sc3_188a)

Python code for the program is as follows:

1.  n=input("Enter your name: ")
2.  a=int(input("Enter your age: "))
3.  if a>=18:
4.  print(n, " is an adult")

[Python code explanation](#contents.xhtml_sc4_189a)

This code prompts the user to enter their name and age as n and a. By default, Python reads the input as a string. So, age, a, is converted to a number using the int() function. Using the if condition, it checks if the entered age is greater than or equal to 18. If the condition is true, it prints the entered name followed by the message is an adult. It should be noticed that else block is not mentioned in the code. Hence, if the condition fails (as in test case#2), the program will terminate without generating any output.

[C code](#contents.xhtml_sc3_190a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  char n[100];
5.  int a;
6.  printf("Enter your name: ");
7.  gets(n);
8.  fflush(stdin);
9.  printf("Enter your age: ");
10.  scanf("%d", &a);
11.  if (a>=18)
12.  printf("%s is an adult", n);
13.  }

[C code explanation](#contents.xhtml_sc4_191a)

This C code starts with the necessary header files. It includes the header file stdio.h, which provides input and output functionality. Within the main() function, it declares a character array n of size 100 to store the user’s name and an integer variable a to store the user’s age. It asks the user to enter their name and age. It reads the user’s input as a string using the gets() function and stores it in the n variable. In C code, sometimes, string input creates problems with the scanf() or gets() function. To avoid these issues, fflush() is used to clear the input stream. Then, it takes age as the input. It checks if the value of a is greater than or equal to 18. If the condition is true, it prints the value of n followed by the message is an adult. Since the else part is optional, it is not used. Hence, if the condition fails (as in test case number 2), the program will terminate without generating any output.

[Program 2.3: Check if number is even or odd](#contents.xhtml_sc2_192a)

Ask the user for a number (3-digit integer). Print out an appropriate message to the user, depending on whether the number is even or odd.

[Sample input output](#contents.xhtml_sc3_193a)

Test case #1:

Input: Enter a number: 45

Output: Number is ODD

Test case #2:

Input: Enter a number: 68

Output: Number is EVEN

[Algorithm](#contents.xhtml_sc3_194a)

The steps to be followed to write the program are:

Step 1\. Start

Step 2\. Enter a number as n

Step 3\. if n%2 ==0:

print("number is EVEN")

Step 4\. else:

print("number is ODD")

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_195a)

[Figure 2.3](#ch02.xhtml_fig2-3) illustrates the flowchart of the program:

![](OPS/images/Figure_2.3.jpg)

Figure 2.3: Flowchart illustrating the program 2.3

[Python code](#contents.xhtml_sc3_196a)

Python code for the program is as follows:

1.  n=int(input("Enter a number : "))
2.  if n%2 ==0:
3.  print("number is EVEN")
4.  else:
5.  print("number is ODD")

[Python code explanation](#contents.xhtml_sc4_197a)

The Python code prompts the user to enter a number and reads the input as an integer, storing it in the variable n. It checks if the value of n is divisible by 2 or not. For that, the modulo operator (%) is used, which calculates the remainder when n is divided by 2. If the remainder is 0, it means the number is even and prints the message number is EVEN. Otherwise, it executes the else block and prints the message number is ODD.

[C code](#contents.xhtml_sc3_198a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int n;
5.  printf("Enter a number : ");
6.  scanf("%d",&n);
7.  if (n%2 ==0)
8.  printf("Number is EVEN");
9.  else
10.  printf("Number is ODD");
11.  }

[C code explanation](#contents.xhtml_sc4_199a)

This C code includes the header file stdio.h, and the remaining code is written within curly brackets {} of the main() function. It declares an integer variable n to store the user’s number, reads the user’s input as an integer using the scanf() function, and stores it in the n variable.

It checks if the value of n is divisible by 2 or not. The modulo operator (%) calculates the remainder when n is divided by 2. If the remainder is 0, it means the number is even and prints the message Number is EVEN. Otherwise, it executes the else block and prints the message Number is ODD. Since, here, if and else blocks contain only one statement, there is no need to enclose the block within {} brackets. However, if the number of statements in the if-else block is more than one, they must be placed within {} brackets.

[Program 2.4: Check type of integer](#contents.xhtml_sc2_200a)

Check if the input number is positive, negative, or zero.

[Sample input output](#contents.xhtml_sc3_201a)

Test case #1:

Input: Enter a number 56

Output: Number is positive

Test case #2:

Input: Enter a number -98

Output: Number is negative

[Algorithm](#contents.xhtml_sc3_202a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable x

Step 3\. Read x

Step 4\. If (x<0)

print "Number is negative"

Step 5\. else if (x ==0)

print "Number is zero"

Step 6\. else

print "Number is positive"

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_203a)

[Figure 2.4](#ch02.xhtml_fig2-4) illustrates the flowchart of the program:

![](OPS/images/Figure_2.4.png)

Figure 2.4: Flowchart illustrating the program 2.4

[Python code](#contents.xhtml_sc3_204a)

Python code for the program is as follows:

1.  x=int(input("Enter a number: "))
2.  if x < 0:
3.  print("Number is negative")
4.  elif x == 0:
5.  print("Number is zero")
6.  else:
7.  print("Number is positive")

[Python code explanation](#contents.xhtml_sc4_205a)

The code prompts the user to enter a number and stores the input as an integer in the variable x. It checks if the value of x is less than 0. If the condition in line 2 is true (x is negative), it prints the message Number is negative. If the condition in line 2 is false, it checks the next condition. It checks if the value of x is equal to 0. If the condition in line 4 is true (x is zero), it prints the message Number is zero. If both the conditions in line 2 and line 4 are false, it executes the else block and prints the message Number is positive.

[C code](#contents.xhtml_sc3_206a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int x;
5.  printf("Enter a number ");
6.  scanf("%d", &x);
7.  if (x < 0)
8.  printf("Number is negative");
9.  else  if (x == 0)
10.  printf("Number is zero");
11.  else
12.  printf("Number is positive");
13.  }

[C code explanation](#contents.xhtml_sc4_207a)

The code prompts the user to enter a number and stores the input in an integer variable x. It checks if the value of x is less than 0. If the condition in line 2 is true (x is negative), it prints the message Number is negative. If the condition in line 2 is false, it checks the next condition. It checks if the value of x is equal to 0. If the condition in line 4 is true (x is zero), it prints the message Number is zero. If both the conditions in line 2 and line 4 are false, it executes the else block and prints the message Number is positive.

[Program 2.5: Validate a triangle](#contents.xhtml_sc2_208a)

Take the sides of a triangle as input and check whether a triangle can be formed or not using if else.

Hint: For a valid triangle, the sum of the two sides should be greater than the third side of the triangle.

[Sample input output](#contents.xhtml_sc3_209a)

Test case #1:

Input: Enter the three sides of a triangle: 6

7

8

Output: It is a valid triangle

Test case #2:

Input: Enter the three sides of a triangle: 1

1

3

Output: It is not a valid triangle

[Algorithm](#contents.xhtml_sc3_210a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable x1,x2,x3

Step 3\. Read x1,x2,x3

Step 4\. if (x1+x2) > x3 and (x1+x3) > x2 and (x2+x3) > x1

print "It is a valid triangle"

Step 5\. else

print "It is not a valid triangle"

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_211a)

[Figure 2.5](#ch02.xhtml_fig2-5) illustrates the flowchart of the program:

![](OPS/images/Figure_2.5.jpg)

Figure 2.5: Flowchart illustrating the program 2.5

[Python code](#contents.xhtml_sc3_212a)

Python code for the program is as follows:

1.  x1=int(input("Enter first side of triangle: "))
2.  x2=int(input("Enter second side of triangle: "))
3.  x3=int(input("Enter third side of triangle: "))
4.  if((x1+x2) > x3 and (x1+x3) > x2 and (x2+x3) > x1):
5.  print ("It is a valid triangle")
6.  else:
7.  print ("It is not a valid triangle")

[Python code explanation](#contents.xhtml_sc4_213a)

This Python code takes 3 sides of a triangle as input from the user and converts them into an integer using the int() function. For a triangle to be valid, the sum of two sides should be greater than the third side of the triangle based on the triangle inequality theorem. So, there are three such conditions, and if all three conditions are true, then only the triangle can be considered valid. Hence, in step 4, three conditions are combined using and operator. The if statement is true only if all the three conditions are individually true and step 5 executes. If any one of them is false, else block executes and prints the message It is not a valid triangle.

Note: The block of if-else is indented towards the right side.

[C code](#contents.xhtml_sc3_214a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int x1, x2, x3;
5.  printf("Enter the three sides of a triangle: ");
6.  scanf("%d%d%d", &x1,&x2,&x3);
7.  if((x1+x2) > x3 && (x1+x3) > x2 && (x2+x3) > x1)
8.  printf("It is a valid triangle");
9.  else
10.  printf("It is not a valid triangle");
11.  }

[C code explanation](#contents.xhtml_sc4_215a)

This C code takes three sides of a triangle as input from the user in variables x1, x2, x3. For a triangle to be valid, the sum of two sides should be greater than the third side of the triangle based on the triangle inequality theorem. So, there are three such conditions, and if all three conditions are true, then only the triangle can be considered valid. Hence, in step 8, three conditions are combined using the && operator. In C, && is the logical AND operator. The if statement is true only if all three conditions are individually true and step 9 executes. It prints the message It is a valid triangle. If any one of them is false, else block executes and prints the message It is not a valid triangle.

[Program 2.6: Check divisibility by 7 and 5](#contents.xhtml_sc2_216a)

Read a number from the user and check if the number is divisible by 7 and 5.

Hint: A number is divisible by 7 and 5 if the remainder is zero on dividing the number by 7 and 5.

[Sample input output](#contents.xhtml_sc3_217a)

Test case #1:

Input: Enter a number 35

Output: Number is divisible by 7 and 5

Test case #2:

Input: Enter a number 63

Output: It is not divisible by 7 and 5

[Algorithm](#contents.xhtml_sc3_218a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable x

Step 3\. Read x

Step 4\. if (x%7 ==0) && (x%5==0)

i. Print "Number is divisible by 7 and 5 both"

Step 5\. else

i. Print "It is not divisible by 7 and 5 both"

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_219a)

[Figure 2.6](#ch02.xhtml_fig2-6) illustrates the flowchart of the program:

![](OPS/images/Figure_2.6.jpg)

Figure 2.6: Flowchart illustrating the program 2.6

[Python code](#contents.xhtml_sc3_220a)

Python code for the program is as follows:

1.  x= int(input("Enter a number: "))
2.  if (x%7 ==0) and (x%5==0):
3.  print("Number is divisible by 7 and 5 both")
4.  else:
5.  print("It is not divisible by 7 and 5 both ")

[Python code explanation](#contents.xhtml_sc4_221a)

The code takes a number as input using input() and int() functions. Since a number is divisible by 7 and 5, if the remainder is zero on dividing the number by 7 and 5, there are 2 conditions to be true. So, in step 2, both the conditions are checked and combined using and operator. If statement is true only if both the conditions are individually true and step 3 executes. It prints the message Number is divisible by 7 and 5 both. If any of them is false, else block executes and prints the message: It is not divisible by 7 and 5 both.

[C code](#contents.xhtml_sc3_222a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int x;
5.  printf("Enter a number: ");
6.  scanf("%d", &x);
7.  if ((x%7 ==0) && (x%5==0))
8.  printf("Number is divisible by 7 and 5 both");
9.  else
10.  printf("It is not divisible by 7 and 5 both ");
11.  }

[C code explanation](#contents.xhtml_sc4_223a)

The C code takes an integer number as input using scanf() function. Since a number is divisible by 7 and 5, if the remainder is zero on dividing the number by 7 and 5, there are two conditions to be true. So, in step 7, both the conditions are checked and combined using the && operator. It checks if the value of x is divisible by 7 (x%7 == 0) and divisible by 5 (x%5 == 0). if statement is true only if both the conditions are individually true and step 8 executes. It prints the message Number is divisible by 7 and 5 both. If any of them is false, else block executes and prints the message It is not divisible by 7 and 5 both.

[Program 2.7: Check if character is a vowel or consonant](#contents.xhtml_sc2_224a)

Check whether an entered letter is a vowel or consonant.

Hint: In English, out of 26 alphabets, 5 (a, e, i, o, u) are vowels, and the rest are consonants.

[Sample input output](#contents.xhtml_sc3_225a)

Test case #1:

Input: Enter a character a

Output: a is a vowel

Test case #2:

Input: Enter a character p

Output: p is a consonant

[Algorithm](#contents.xhtml_sc3_226a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Read input as c

Step 3\. If c== 'a' or c== 'e' or c== 'i' or c== 'o' or c== 'u' then

print "entered character is a vowel"

Step 4\. else

print "entered character is a consonant"

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_227a)

[Figure 2.7](#ch02.xhtml_fig2-7) illustrates the flowchart of the program:

![](OPS/images/Figure_2.7.jpg)

Figure 2.7: Flowchart illustrating the program 2.7

[Python code](#contents.xhtml_sc3_228a)

Python code for the program is as follows:

1.  c=input("Enter a character: ")
2.  if c== 'a'  or c== 'e'  or c== 'i'  or c== 'o'  or c== 'u':
3.  print( "Entered character is a vowel")
4.  else:
5.  print( "The character is a consonant")

[Python code explanation](#contents.xhtml_sc4_229a)

The code prompts the user to enter a character in variable c using the input() function. Here, if the entered character is any one of the characters (a, e, i, o, or u), then if condition should be true. Since, in this program, at least one condition should be true, the or operator is used. So, in step 2, out of 5 conditions, if anyone is true, the if-block executes. It prints the message it is a vowel. If all the conditions are false, it executes the else block. In the else block, it prints the message it is a consonant.

[C code](#contents.xhtml_sc3_230a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  char c;
5.  printf("Enter a character ");
6.  scanf("%c", &c);
7.  if(c== 'a' || c== 'e' || c== 'i' || c== 'o' || c== 'u')
8.  printf("%c is a vowel", c);
9.  else
10.  printf("%c is a consonant", c);
11.  }

[C code explanation](#contents.xhtml_sc4_231a)

The C code asks the user to enter a character in variable c using the %c format specifier in the scanf() function. Here, if the entered character is any of the characters (a, e, i, o, or u), then the if-condition should be true. Since, in this program, at least one condition should be true, the || operator is used. II is or operator in the C program. So, in step 7, out of five conditions, if anyone is true, the if-block executes. It prints the message it is a vowel. If all the conditions are false, it executes the else block. In the else block, it prints the message it is a consonant.

[Program 2.8: Check if you can sit in exam?](#contents.xhtml_sc2_232a)

A student will not be allowed to sit in the end-term exam if the attendance is less than 80%. Take the input: number of classes held and number of classes attended. Print the percentage of classes attended. Then, decide whether a student is allowed to sit in the exam or not.

[Sample input output](#contents.xhtml_sc3_233a)

Test case #1:

Input:

Enter total number of classes held 42

Enter total number of classes attended 20

Output:

You are debarred. Attendance is 47.619049

Test case #2:

Input:

Enter total number of classes held 10

Enter total number of classes attended 9

Output:

Not debarred. Attendance is 90

[Algorithm](#contents.xhtml_sc3_234a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable class_held, class_att, Percent_att

Step 3\. Read class_held, class_att

Step 4\. Percent_att = (class_att / class_held) *100

Step 5\. if Percent_att>=80

print "Not Debarred"

Step 6\. else

print "You are debarred"

Step 7\. print "attendance is " +Percent_att

Step 8\. Stop

[Flowchart](#contents.xhtml_sc3_235a)

[Figure 2.8](#ch02.xhtml_fig2-8) illustrates the flowchart of the program:

![](OPS/images/Figure_2.8.png)

Figure 2.8: Flowchart illustrating the program 2.8

[Python code](#contents.xhtml_sc3_236a)

Python code for the program is as follows:

1.  class_held = int(input("Total number of classes held: "))
2.  class_att= int(input("Total number of classes attended: "))
3.  Percent_att = (class_att / class_held) *100
4.  if(Percent_att>=80):
5.  print( "Not Debarred")
6.  else:
7.  print( "You are debarred")

9.  print("Attendance is ",round(Percent_att,2), "%")

[Python code explanation](#contents.xhtml_sc4_237a)

The Python program reads the number of classes held and the total number of classes attended values from the user. Step 3 calculates the attendance percentage by dividing the number of classes attended by the total classes held, multiplied by 100\. If attendance percentage is greater than or equal to 80, it prints the message Not Debarred. Otherwise, it executes the else block and prints the message You are debarred. In step 9, it prints the attendance percentage. The decimal number is rounded up to 2 places after decimal.

Note: The indentation of the statement 9\. It is left indented, which means it is outside the if and else block and will execute irrespective of the condition.

[C code](#contents.xhtml_sc3_238a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int class_held, class_att;
5.  float Percent_att;
6.  printf("Enter total number of classes held ");
7.  scanf("%d", &class_held);
8.  printf("Enter total number of classes attended ");
9.  scanf("%d", &class_att);
10.  Percent_att = (class_att / (float)(class_held)) *100.0;

12.  if(Percent_att>=80)
13.  printf( "Not Debarred");
14.  else
15.  printf( "You are debarred. ");

17.  printf("Attendance is %f", Percent_att);
18.  }

[C code explanation](#contents.xhtml_sc4_239a)

The C code calculates the percentage of attendance based on the total number of classes held and attended and determines if the student is debarred or not based on a threshold of 80%. It provides the appropriate output message indicating the result and displays the attendance percentage. The Python program reads the number of classes held and the total number of classes attended values from the user. In step 10, it calculates the attendance percentage by dividing the number of classes attended by the total classes held, multiplied by 100\. Here, float is written before class_held to convert the nature of the variable from integer to floating point. If attendance percentage is greater than or equal to 80, it prints the message Not Debarred. Otherwise, it executes the else block and prints the message You are debarred. In step 17, it prints the attendance percentage. Note that this statement is outside the if and else block and will execute irrespective of the condition.

[Program 2.9: Check if you can sit in exam (extended)?](#contents.xhtml_sc2_240a)

Modify the program 2.8 to allow students to sit if they have a medical case. Ask the user if they have a medical case or not (Y or N) and print accordingly.

[Sample input output](#contents.xhtml_sc3_241a)

Test case #1:

Input:

Enter total number of classes held 42

Enter total number of classes attended 39

If there is some medical case enter y n

Output:

Not Debarred

Attendance is 92.857140

Test case #2:

Input:

Enter total number of classes held 42

Enter total number of classes attended 20

If there is some medical case enter y n

Output:

You are debarred

Attendance is 47.619049

Test case #3:

Input:

Enter total number of classes held 42

Enter total number of classes attended 20

If there is some medical case enter y y

Output:

Not Debarred

Attendance is 47.619049

[Algorithm](#contents.xhtml_sc3_242a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable class_held, class_att, Percent_att, medical_case

Step 3\. Read class_held, class_att, medical_case

Step 4\. Percent_att = (class_att / class_held) *100

Step 5\. if Percent_att>=80

print "Not Debarred"

Step 6\. Else if medical_case== 'Y'

print "Not Debarred"

Step 7\. else

print "You are debarred"

Step 8\. print "attendance is " +Percent_att

Step 9\. Stop

[Flowchart](#contents.xhtml_sc3_243a)

[Figure 2.9](#ch02.xhtml_fig2-9) illustrates the flowchart of the program:

![](OPS/images/Figure_2.9.png)

Figure 2.9: Flowchart illustrating the program 2.9

[Python code](#contents.xhtml_sc3_244a)

Python code for the program is as follows:

1.  class_held = int(input("Total number of classes held "))
2.  class_att= int(input("Total number of classes attended "))
3.  medical_case = input("if there is some medical case enter y ")

5.  Percent_att = (class_att / class_held) *100
6.  if Percent_att>=80 :
7.  print("Not Debarred")
8.  elif medical_case== 'y':
9.  print("Not Debarred")
10.  else:
11.  print("Debarred")
12.  print("Attendance is ", round(Percent_att,2))

[Python code explanation](#contents.xhtml_sc4_245a)

This program is an extension of the previous program with an extra condition of medical case. So, if the attendance percentage is less than 80%, the student is checked for medical cases. If the student has some medical case, the condition in step 8 becomes true, and the corresponding block is executed. Otherwise, it prints the message You are debarred as the attendance percentage is below 80, and there is no medical case. Finally, it displays the attendance percentage irrespective of condition (note the indentation of the statement).

[C code](#contents.xhtml_sc3_246a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int class_held, class_att;
5.  float Percent_att;
6.  char medical_case;
7.  printf("Enter total number of classes held ");
8.  scanf("%d", &class_held);
9.  printf("Enter total number of classes attended ");
10.  scanf("%d", &class_att);
11.  fflush(stdin);
12.  printf("If there is some medical case enter y ");
13.  scanf("%c", &medical_case);
14.  Percent_att = (class_att / (float)class_held) *100.0;

16.  if(Percent_att>=80)
17.  printf( "Not Debarred");
18.  else  if (medical_case== 'y')
19.  printf( "Not Debarred");
20.  else
21.  printf( "You are debarred");

23.  printf("\nAttendance is %f", Percent_att);
24.  }

[C code explanation](#contents.xhtml_sc4_247a)

This program is an extension of the previous program with an extra condition of medical case. So, if the attendance percentage is less than 80%, the student is checked for medical cases. If the student has some medical case, the condition in step 18 becomes true, and the corresponding block is executed. Otherwise, it prints the message You are debarred as the attendance percentage is below 80, and there is no medical case. Finally, it displays the attendance percentage irrespective of condition as this statement in outside if-else if–else blocks.

[Program 2.10: Who spent more money?](#contents.xhtml_sc2_248a)

You purchased some toffees, each costing $2\. Your sister purchased some chocolates, each costing $10\. Check that who spent more money. Take the number of toffees and chocolates as input from the user.

[Sample input output](#contents.xhtml_sc3_249a)

Test case #1:

Input:

Enter no of your toffees 25

Enter no of sister toffee 2

Output:

I spent more money

Test case #2:

Input:

Enter no of your toffees 10

Enter no of sister toffee 3

Output:

She spent more money

Test case #3:

Input:

Enter no of your toffees 10

Enter no of sister toffee 2

Output:

We spent equal money

[Algorithm](#contents.xhtml_sc3_250a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable no_my_toffee, no_sis_choco, my_rs, sis_rs

Step 3\. Read no_my_toffee, no_sis_choco

Step 4\. my_rs = 2 *no_my_toffee

Step 5\. sis_rs = 10 * no_sis_choco

Step 6\. if my_rs>sis_rs

print "I spent more money"

Step 7\. elseifmy_rs==sis_rs

print "We spent equal money"

Step 8\. else

print "She spent more money"

Step 9\. Stop

[Flowchart](#contents.xhtml_sc3_251a)

[Figure 2.10](#ch02.xhtml_fig2-10) illustrates the flowchart of the program:

![](OPS/images/Figure_2.10.jpg)

Figure 2.10: Flowchart illustrating the program 2.10

[Python code](#contents.xhtml_sc3_252a)

Python code for the program is as follows:

1.  no_my_toffee = int(input("Enter number of your toffees "))
2.  no_sis_choco = int(input("Enter number of sister's chocolates "))
3.  my_rs = 2 *no_my_toffee
4.  sis_rs = 10 * no_sis_choco
5.  if my_rs>sis_rs:
6.  print("I spent more money")
7.  elif my_rs==sis_rs:
8.  print("We spent equal money")
9.  else:
10.  print("She spent more money")

[Python code explanation](#contents.xhtml_sc4_253a)

This program is similar to the previous one, checking two levels of conditions using if-else if- else statement. It takes the number of toffees and chocolates as input and then calculates the cost of both (Steps 3 and 4). It first calculates the amount of money you spent by multiplying the number of your toffees (no_my_toffee) by 2 and stores the result in the my_rs variable. Similarly, it calculates the amount of money your sister spent by multiplying the number of your sister’s toffees (no_sis_choco) by 10 and stores the result in the sis_rs variable. If the amount of money you spent (my_rs) is greater than the amount of money your sister spent (sis_rs), it prints the message I spent more money. Else if the amount of money you spent (my_rs) is equal to the amount your sister spent (sis_rs), it prints the message We spent equal money. Else (the amount of money your sister spent sis_rs, is greater than the amount of money you spent my_rs), it prints the message: She spent more money.

[C code](#contents.xhtml_sc3_254a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int no_my_toffee, no_sis_choco, my_rs, sis_rs;
5.  printf("Enter no of your toffees ");
6.  scanf("%d", &no_my_toffee);
7.  printf("Enter no of sister toffee ");
8.  scanf("%d", &no_sis_choco);
9.  my_rs = 2 *no_my_toffee;
10.  sis_rs = 10 * no_sis_choco;

12.  if(my_rs>sis_rs)
13.  printf("I spent more money");
14.  else  if (my_rs==sis_rs)
15.  printf("We spent equal money");
16.  else
17.  printf("She spent more money");
18.  }

[C code explanation](#contents.xhtml_sc4_255a)

This program is similar to the previous one, checking two levels of conditions using if-else if- else statement. It takes the number of toffees and chocolates as input and then calculates the cost of both (Step 9 and 10). It calculates the money you spend by multiplying the number of your toffees (no_my_toffee) by 2 and stores the result in the my_rs variable. Similarly, it calculates the amount of money your sister spent by multiplying the number of your sister’s toffees (no_sis_choco) by 10 and stores the result in the sis_rs variable. If the amount of money you spent (my_rs) is greater than the amount of money your sister spent (sis_rs), it prints the message I spent more money. Else if the amount of money you spent (my_rs) is equal to the amount your sister spent (sis_rs), it prints the message We spent equal money. Else (the amount of money your sister spent, sis_rs, is greater than the amount you spent my_rs), it prints the message: She spent more money.

[Program 2.11: Find type of triangle](#contents.xhtml_sc2_256a)

Lengths of three sides of a triangle, a, b, c, are given as input. Check if the triangle is isosceles, equilateral, or scalene.

Hint: In an equilateral triangle, three sides are equal. In an isosceles triangle, two sides are equal. In a scalene triangle, three sides are not equal.

[Sample input output](#contents.xhtml_sc3_257a)

Test case #1:

Input: Enter 3 sides of a triangle: 12 12 4

Output: It is an isosceles triangle

Test case #2:

Input: Enter 3 sides of a triangle: 10 4 9

Output: It is a scalene triangle

Test case #3:

Input: Enter 3 sides of a triangle: 5 5 5

Output: It is an equilateral triangle

[Algorithm](#contents.xhtml_sc3_258a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Enter three sides of a triangle as a,b,c

Step 3\. If a==b==c:

Print("It is an equilateral triangle")

Step 4\. else if a==b or b==c or c==a :

Print("It is an isosceles triangle")

Step 5\. Else:

Print("It is a scalene triangle")

[Flowchart](#contents.xhtml_sc3_259a)

[Figure 2.11](#ch02.xhtml_fig2-11) illustrates the flowchart of the program:

![](OPS/images/Figure_2.11.jpg)

Figure 2.11: Flowchart illustrating the program 2.11

[Python code](#contents.xhtml_sc3_260a)

Python code for the program is as follows:

1.  a=int(input("Enter side 1 of a triangle "))
2.  b=int(input("Enter side 1 of a triangle "))
3.  c=int(input("Enter side 1 of a triangle "))
4.  if a==b and b==c:
5.  print("It is an equilateral triangle")
6.  elif a==b or b==c or c==a :
7.  print("It is an isosceles triangle")
8.  else:
9.  print("It is a scalene triangle")

[Python code explanation](#contents.xhtml_sc4_261a)

The code prompts the user to enter the lengths of the sides of a triangle, and then it determines the type of triangle (equilateral, isosceles, or scalene). The first condition checks if the first side is equal to the second and the second is equal to the third. Here, both the conditions must be true. Hence, and operator is used. If both the conditions are true, it prints the message It is an equilateral triangle. Else if at least two sides of the triangle are equal, it prints the message: It is an isosceles triangle. Here, only one condition is sufficient to make the statement true, and hence, or operator is used. If none of the sides are equal, it prints the message: It is a scalene triangle.

Note: Check the order of conditions. If the condition of the isosceles triangle is checked before the equilateral triangle, it will never give the correct output for the equilateral triangle.

[C code](#contents.xhtml_sc3_262a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int a,b,c;
5.  printf("Enter 3 sides of a triangle: ");
6.  scanf("%d%d%d",&a,&b,&c);
7.  if (a==b && b==c)
8.  printf("It is an equilateral triangle: ");
9.  else  if (a==b || b==c || c==a)
10.  printf("It is an isosceles triangle");
11.  else
12.  printf("It is a scalene triangle");
13.  }

[C code explanation](#contents.xhtml_sc4_263a)

The code prompts the user to enter the lengths of the sides of a triangle and determines the type of triangle (equilateral, isosceles, or scalene). The first condition checks if the first side is equal to the second and the second is equal to the third. Here, both conditions must be true. Hence, the && (and) operator is used. If both the conditions are true, it prints the message It is an equilateral triangle. Else if at least two sides of the triangle are equal, it prints the message: It is an isosceles triangle. Here, only one condition is sufficient to make the statement true; hence, the || (or) operator is used. If none of the sides are equal, it prints the message: It is a scalene triangle.

Note: Check the order of conditions. If the condition of an isosceles triangle is checked before the equilateral triangle, it will never give the correct output for the equilateral triangle.

[Program 2.12: Check if year is a leap year](#contents.xhtml_sc2_264a)

Check if the year entered is a leap year or not.

Hint: To be a leap year, the year should be divisible by either 400 or 4 but not with 100.

[Sample input output](#contents.xhtml_sc3_265a)

Test case #1:

Input: Enter year 2024

Output: It is a leap year

Test case #2:

Input: Enter year 2300

Output: It is not a leap year

Test case #3:

Input: Enter year 2000

Output: It is a leap year

[Algorithm](#contents.xhtml_sc3_266a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. input year

Step 3\. if year%400 ==0 then

Print "it is a leap year"

Step 4\. else if year %100 != 0 and year%4 ==0 then

Print "it is a leap year"

Step 5\. Else

Print "it is not a leap year"

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_267a)

[Figure 2.12](#ch02.xhtml_fig2-12) illustrates the flowchart of the program:

![](OPS/images/Figure_2.12.jpg)

Figure 2.12: Flowchart illustrating the program 2.12

[Python code](#contents.xhtml_sc3_268a)

Python code for the program is as follows:

1.  year = int(input("Enter year "))
2.  if year%400 ==0:
3.  print("it is a leap year")
4.  elif year %100 != 0  and year%4 ==0:
5.  print("it is a leap year")
6.  else:
7.  print("it is not a leap year")

[Python code explanation](#contents.xhtml_sc4_269a)

The code prompts the user to enter a year and determines if it is a leap year based on the given conditions: If the year is divisible by 400 (year%400 == 0), it prints the message it is a leap year. Otherwise, it checks the second condition. If the year is not divisible by 100 (year%100 != 0) and divisible by 4 (year%4 == 0), it prints the message it is a leap year. Else (neither of the above conditions is true), it prints the message it is not a leap year.

[C code](#contents.xhtml_sc3_270a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int year;
5.  printf("Enter year ");
6.  scanf("%d", &year);
7.  if (year%400 ==0)
8.  printf("it is a leap year");
9.  else  if (year %100 != 0 && year%4 ==0)
10.  printf("it is a leap year");
11.  else
12.  printf("it is not a leap year");
13.  }

[C code explanation](#contents.xhtml_sc4_271a)

The code prompts the user to enter a year and determines if it is a leap year based on the given conditions: If the year is divisible by 400 (year%400 == 0), it prints the message it is a leap year. Otherwise, it checks the second condition. That is, if the year is not divisible by 100 (year%100 != 0) and divisible by 4 (year%4 == 0), it prints the message it is a leap year. Else (neither of the above conditions is true), it prints the message it is not a leap year.

[Program 2.13: Find largest number](#contents.xhtml_sc2_272a)

Take three numbers as input from the user and print the largest number.

[Sample input output](#contents.xhtml_sc3_273a)

Test case #1:

Input: Enter 3 numbers: 23 54 87

Output: 87 is largest

Test case #2:

Input: Enter 3  numbers: 12 54 7

Output: 54 is largest

[Algorithm](#contents.xhtml_sc3_274a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Declare a,b,c

Step 3\. Input a,b,c

Step 4\. If a>b:

If b>c

Print a is largest

Else if a>c

Pint a is largest

Else

Print c is largest

Step 5\. Else

If a>c

Print b is largest

Else if b>c

Print b is largest

Else

Print c is largest

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_275a)

[Figure 2.13](#ch02.xhtml_fig2-13) illustrates the flowchart of the program:

![](OPS/images/Figure_2.13.jpg)

Figure 2.13: Flowchart illustrating the program 2.13

[Python code](#contents.xhtml_sc3_276a)

Python code for the program is as follows:

1.  a=int(input("Enter first number"))
2.  b=int(input("Enter first number"))
3.  c=int(input("Enter first number"))
4.  if a>b:
5.  if b>c:
6.  print("a is largest")
7.  elif a>c:
8.  print("a is largest")
9.  else:
10.  print("c is largest")
11.  else:
12.  if a>c:
13.  print("b is largest")
14.  elif b>c:
15.  print("b is largest")
16.  else:
17.  print("c is largest")

[Python code explanation](#contents.xhtml_sc4_277a)

The code prompts the user to enter three numbers and determines the largest number using nested if-else statements.

Note: Steps 5-10 are indented towards the right and hence considered part of if - if-block (step 4). Similarly, steps 12-17 are part of the else - block. Based on the conditions, the appropriate message is displayed.

[C code](#contents.xhtml_sc3_278a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int a, b,c;
5.  printf("Enter 3 numbers: ");
6.  scanf("%d%d%d", &a, &b, &c);
7.  if (a>b)
8.  {
9.  if (b>c)
10.  printf( "%d is largest", a);
11.  else  if (a>c)
12.  printf( "%d is largest", a);
13.  else
14.  printf( "%d is largest", c);
15.  }
16.  else
17.  {
18.  if (a>c)
19.  printf( "%d is largest", b);
20.  else  if ( b>c)
21.  printf( "%d is largest", b);
22.  else
23.  printf( "%d is largest", c);
24.  }
25.  }

[C code explanation](#contents.xhtml_sc4_279a)

The code prompts the user to enter three numbers and determines the largest number using nested if-else statements.

Note: The steps 9-14 are enclosed within {} brackets. Hence, they are part of the if-block (step 7). Similarly, steps 18-23 are part of the else - block. Based on the conditions, the appropriate message is displayed.

[Program 2.14: Design arithmetic calculator](#contents.xhtml_sc2_280a)

Design a simple arithmetic calculator.

[Sample input output](#contents.xhtml_sc3_281a)

Test case #1:

Input:

Enter two numbers: 23 65

Enter operator: a for addition, s for subtraction, m for multiplication and d for division a

Output: 88

Test case #2:

Input:

Enter two numbers: 12 4

Enter operator: a for addition, s for subtraction, m for multiplication and d for division: d

Output: 3.000000

[Algorithm](#contents.xhtml_sc3_282a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Read two number as x, y

Step 3\. Read operator op as a for addition, s for subtraction,

m for multiplication and d for division

Step 4\. if op== 'a' then

Print x+y

Step 5\. Else if op== 's' then

Print x-y

Step 6\. Else if op== 'm' then

Print x*y

Step 7\. Else if op== 'd' then

Print x/y

Step 8\. Else

Print "entered invalid operator"

Step 9\. Stop

[Flowchart](#contents.xhtml_sc3_283a)

[Figure 2.14](#ch02.xhtml_fig2-14) illustrates the flowchart of the program:

![](OPS/images/Figure_2.14.jpg)

Figure 2.14: Flowchart illustrating the program 2.14

[Python code](#contents.xhtml_sc3_284a)

Python code for the program is as follows:

1.  x=int(input("Enter first number "))
2.  y= int(input("Enter second number "))
3.  op=input("Enter operator: a for addition, s for subtraction, m for multiplication and d for division ")
4.  if op== 'a':
5.  print( x+y)
6.  elif op== 's':
7.  print( x-y)
8.  elif op== 'm':
9.  print( x*y)
10.  elif op== 'd':
11.  print( x/y)
12.  else:
13.  print("Entered invalid operator")

[Python code explanation](#contents.xhtml_sc4_285a)

The code prompts the user to enter two numbers and an operator. It performs the corresponding arithmetic operation based on the operator entered and provides the appropriate output message or result. It should be noted that using multiple elif statements, many conditions are checked. If none of the conditions match, the else-block is executed.

[C code](#contents.xhtml_sc3_286a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int x,y;
5.  char op;
6.  printf("Enter two numbers: ");
7.  scanf("%d%d",&x, &y);
8.  fflush(stdin);
9.  printf("Enter operator: a for addition, s for subtraction, m for multiplication and d for division: ");
10.  scanf("%c", &op);
11.  if (op== 'a')
12.  printf("%d",x+y);
13.  else  if (op== 's')
14.  printf("%d", x-y);
15.  else  if (op== 'm')
16.  printf("%d", x*y);
17.  else  if (op== 'd')
18.  printf("%f", x/(float)y);
19.  else
20.  printf( "Entered invalid operator");
21.  }

[C code explanation](#contents.xhtml_sc4_287a)

The code prompts the user to enter two numbers and an operator. It performs the corresponding arithmetic operation based on the operator entered and provides the appropriate output message or result. It should be noted that many conditions are checked by using multiple else if statements. If none of the conditions match, the else-block is executed.

[Program 2.15: Calculate the grade of a student](#contents.xhtml_sc2_288a)

Write a program that will take the marks of a student in five subjects: Computer, Social Science, Math, English, and Hindi. It will calculate the percentage and print the grade sheet according to given conditions:

*   If percentage >= 90% : Grade A
*   If percentage >= 80% : Grade B
*   If percentage >= 60% : Grade C
*   If percentage >= 40% : Grade D
*   If percentage <40%: Grade F

[Sample input output](#contents.xhtml_sc3_289a)

Test case #1:

Input: Enter marks in 5 subjects 87 89 86 90 92

Output: Grade is B

Test case #2:

Input: Enter marks in 5 subjects 43 56 73 34 66

Output: Grade is D

[Algorithm](#contents.xhtml_sc3_290a)

The steps needed to be followed to write the program are:

Step 1\. Start

Step 2\. Enter marks in 5 subjects as a,b,c,d,e

Step 3\. p=((a+b+c+d+e)/500)*100

Step 4\. if p>=90

print("grade is A")

Step 5\. else if p>=80

print("grade is B")

Step 6\. else if p >=60

print("grade is C")

Step 7\. else if p >=40

print("grade is D")

Step 8\. else

print("grade is F")

Step 9\. STOP

[Flowchart](#contents.xhtml_sc3_291a)

[Figure 2.15](#ch02.xhtml_fig2-15) illustrates the flowchart of the program:

![](OPS/images/Figure_2.15.jpg)

Figure 2.15: Flowchart illustrating the program 2.15

[Python code](#contents.xhtml_sc3_292a)

Python code for the program is as follows:

1.  a=int(input("Enter marks in subject 1: "))
2.  b=int(input("Enter marks in subject 2: "))
3.  c=int(input("Enter marks in subject 3: "))
4.  d=int(input("Enter marks in subject 4: "))
5.  e=int(input("Enter marks in subject 5: "))

7.  p=((a+b+c+d+e)/500)*100
8.  if p >=90:
9.  print("Grade is A")
10.  elif p >=80:
11.  print("Grade is B")
12.  elif p >=60:
13.  print("Grade is C")
14.  elif p >=40:
15.  print("Grade is D")
16.  else:
17.  print("Grade is F")

[Python code explanation](#contents.xhtml_sc4_293a)

The code prompts the user to enter marks in five subjects, calculates the percentage, determines the grade based on the percentage, and provides the appropriate output based on the following conditions:

*   If the percentage (p) is greater than or equal to 90, it prints the message Grade is A.
*   Else if the percentage (p) is greater than or equal to 80, it prints the message Grade is B.
*   Else if the percentage (p) is greater than or equal to 60, it prints the message Grade is C.
*   Else if the percentage (p) is greater than or equal to 40, it prints the message Grade is D. Else (the percentage is less than 40), it prints the message Grade is F.

Note: Check the order of the conditions. Try to check the conditions in some other order and observe the difference in the output.

[C code](#contents.xhtml_sc3_294a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int a,b,c,d,e;
5.  float p;
6.  printf("Enter marks in 5 subjects ");
7.  scanf("%d%d%d%d%d", &a,&b,&c,&d,&e);
8.  p=((a+b+c+d+e)/(float)500)*100;
9.  if (p >=90)
10.  printf("Grade is A");
11.  else  if (p >=80)
12.  printf("Grade is B");
13.  else  if ( p >=60)
14.  printf("Grade is C");
15.  else  if (p >=40)
16.  printf("Grade is D");
17.  else
18.  printf("Grade is F");
19.  }

[C code explanation](#contents.xhtml_sc4_295a)

The code prompts the user to enter marks in five subjects, calculates the percentage, determines the grade based on the percentage, and provides the appropriate output based on the following conditions:

*   If the percentage (p) is greater than or equal to 90, it prints the message Grade is A.
*   Else if the percentage (p) is greater than or equal to 80, it prints the message Grade is B.
*   Else if the percentage (p) is greater than or equal to 60, it prints the message Grade is C.
*   Else if the percentage (p) is greater than or equal to 40, it prints the message Grade is D.
*   Else (the percentage is less than 40), it prints the message Grade is F.

Note: The order of conditions. Try to check the conditions in some other order and observe the difference in the output.

[Program 2.16: Find gross salary](#contents.xhtml_sc2_296a)

The gross salary of an employee in a firm is calculated based on the following:

Formula: Gross = Basic + DA+HRA

Take the basic salary of an employee as input and calculate gross salary according to given conditions:

*   Basic salary <= 10000 : HRA = 20%, DA = 80%
*   Basic salary is between 10001 to 20000 : HRA = 25%, DA = 90%
*   Basic salary >= 20001 : HRA = 30%, DA = 95%

[Sample input output](#contents.xhtml_sc3_297a)

Test case #1:

Input: Enter your basic salary 3000

Output: Gross Salary is 6000.000000

Test case #2:

Input: Enter your basic salary 25000

Output: Gross Salary is 56250.000000

[Algorithm](#contents.xhtml_sc3_298a)

The steps to be followed to write the program are:

Step 1\. Start

Step 2\. Enter your basic salary as sal

Step 3\. if sal<= 10000 :

HRA = 0.2 * sal

DA = 0.8*sal

Step 4\. else if sal<= 20000 :

HRA = 0.25*sal

DA =0.9*sal

Step 5\. else:

HRA = 0.3*sal

DA =0.95*sal

Step 6\. print(" Gross Salary is", sal+HRA+DA)

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_299a)

[Figure 2.16](#ch02.xhtml_fig2-16) illustrates the flowchart of the program:

![](OPS/images/Figure_2.16.jpg)

Figure 2.16: Flowchart illustrating the program 2.16

[Python code](#contents.xhtml_sc3_300a)

Python code for the program is as follows:

1.  sal=int(input("Enter your basic salary "))
2.  if sal <= 10000 :
3.  HRA = 0.2 * sal
4.  DA = 0.8*sal
5.  elif sal <= 20000 :
6.  HRA = 0.25*sal
7.  DA =0.9*sal
8.  else:
9.  HRA = 0.3*sal
10.  DA =0.95*sal
11.  print("Gross Salary is ", sal+HRA+DA)

[Python code explanation](#contents.xhtml_sc4_301a)

The code prompts the user to enter their basic salary, calculates the House Rent Allowance (HRA) and Dearness Allowance (DA) based on the salary range, and calculates the gross salary by adding the basic salary, HRA, and DA. It then provides the appropriate output message indicating the gross salary. Note the indentation in the code.

[C code](#contents.xhtml_sc3_302a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int sal;
5.  float HRA, DA;
6.  printf("Enter your basic salary ");
7.  scanf("%d", &sal);
8.  if (sal <= 10000)
9.  {
10.  HRA = 0.2 * sal;
11.  DA = 0.8*sal;
12.  }
13.  else  if (sal <= 20000)
14.  {
15.  HRA = 0.25*sal;
16.  DA =0.9*sal;
17.  }
18.  else
19.  {
20.  HRA = 0.3*sal;
21.  DA =0.95*sal;
22.  }
23.  printf("Gross Salary is %f", sal+HRA+DA);
24.  }

[C code explanation](#contents.xhtml_sc4_303a)

The code prompts the user to enter their basic salary, calculates the HRA and DA based on the salary range, and calculates the gross salary by adding the basic salary, HRA, and DA. It then provides the appropriate output message indicating the gross salary. Note the indentation in the code.

[Program 2.17: Generate shopping bill](#contents.xhtml_sc2_304a)

During the sale hours, a shop prints the following offer:

If you will purchase for more than $1000, you will get a 20% discount. If you purchase for more than $5000, you will get a 50% discount.

Assume that each product costs $120.Take quantity as input and calculate the amount to be paid.

[Sample input output](#contents.xhtml_sc3_305a)

Test case #1:

Input: Enter no of products you purchased: 3000

Output: Please pay 180000.000000

Test case #2:

Input: Enter no of products you purchased: 350

Output: Please pay 21000.000000

[Algorithm](#contents.xhtml_sc3_306a)

The steps to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable quantity, amt, x

Step 3\. Read quantity

Step 4\. amt=quantity * 120

Step 5\. if amt>5000

x= amt – 0.5*amt

print "Pls pay" + x

Step 6\. Else if amt> 1000

x= amt – 0.2*amt

print "Pls pay" + x

Step 7\. else

print "Pls pay" + amt

Step 8\. Stop

[Flowchart](#contents.xhtml_sc3_307a)

[Figure 2.17](#ch02.xhtml_fig2-17) illustrates the flowchart of the program:

![](OPS/images/Figure_2.17.jpg)

Figure 2.17: Flowchart illustrating the program 2.17

[Python code](#contents.xhtml_sc3_308a)

Python code for the program is as follows:

1.  quantity=int(input("Enter no of products you purchased "))
2.  amt=quantity * 120
3.  if amt>5000:
4.  x= amt-0.5*amt
5.  print("Pls pay ", x)
6.  elif amt> 1000:
7.  x= amt-0.2*amt
8.  print("Pls pay ", x)
9.  else:
10.  print("Pls pay ", amt)

[Python code explanation](#contents.xhtml_sc4_309a)

The code prompts the user to enter the quantity of products purchased and calculates the total amount by multiplying the quantity by 120\. It applies a discount based on the total amount range and provides the appropriate output message indicating the final amount to be paid.

[C code](#contents.xhtml_sc3_310a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int quantity, amt;
5.  float x;
6.  printf("Enter no of products you purchased: ");
7.  scanf("%d", &quantity);
8.  amt=quantity * 120;
9.  if(amt>5000)
10.  {
11.  x= amt-0.5*amt;
12.  printf("Pls pay %f", x);
13.  }
14.  else  if (amt> 1000)
15.  {
16.  x= amt-0.2*amt;
17.  printf("Pls pay %f", x);
18.  }
19.  else
20.  {
21.  printf("Pls pay %d", amt);
22.  }
23.  }

[C code explanation](#contents.xhtml_sc4_311a)

The code prompts the user to enter the quantity of products purchased and calculates the total amount by multiplying the quantity by 120\. It applies a discount based on the total amount range and provides the appropriate output message indicating the final amount to be paid.

[Program 2.18: Generate shopping bill during sale](#contents.xhtml_sc2_312a)

A bookshop prints the following discount:

Buy 2, get 3

Two higher MRP book prices would be used to calculate the amount to be paid. For example, you purchased 3 books for $500, $900, and $700. Then, your bill amount will be $1600\. Write an algorithm to compute the bill amount.

[Sample input output](#contents.xhtml_sc3_313a)

Test case #1:

Input: Enter price of 3 books: 300 400 500

Output: Please pay 900.000000

Test case #2:

Input: Enter price of 3 books: 800 400 1000

Output: Please pay 1800.000000

[Algorithm](#contents.xhtml_sc3_314a)

The steps to be followed to write the program are:

Step 1\. Start

Step 2\. Declare variable price1, price2, price3

Step 3\. Read price1, price2, price3

Step 4\. If (price1 < price2 and price 1< price3)

amt_paid = price2 + price3

Step 5\. else if (price2 < price 1 and price 2< price 3)

amt_paid = price1 + price3

Step 6\. else

amt_paid = price2 + price1

Step 7\. Print" Pls pay" + amt_paid

Step 8\. Stop

[Flowchart](#contents.xhtml_sc3_315a)

[Figure 2.18](#ch02.xhtml_fig2-18) illustrates the flowchart of the program:

![](OPS/images/Figure_2.18.jpg)

Figure 2.18: Flowchart illustrating the program 2.18

[Python code](#contents.xhtml_sc3_316a)

Python code for the program is as follows:

1.  price1=int(input("enter price of book 1 "))
2.  price2=int(input("enter price of book 2 "))
3.  price3=int(input("enter price of book 3 "))

5.  if (price1 < price2 and price1< price3):
6.  amt_paid = price2 + price3
7.  elif (price2 < price1 and price2< price3):
8.  amt_paid = price1 + price3
9.  else:
10.  amt_paid = price2 + price1
11.  print("Pls pay",amt_paid)

[Python code explanation](#contents.xhtml_sc4_317a)

The code prompts the user to enter the prices of three books and compare them. The conditions are combined using and operator. It picks the price of two books with higher MRP than the third one and calculates the amount to be paid based on those two books. It then provides the appropriate output message indicating the amount to be paid.

[C code](#contents.xhtml_sc3_318a)

C code for the program is as follows:

1.  void  main()
2.  {
3.  float price1, price2, price3;
4.  float amt_paid;
5.  printf("Enter price of 3 books: ");
6.  scanf("%f%f%f",&price1, &price2, &price3);
7.  if ((price1 < price2) && (price1< price3))
8.  amt_paid = price2 + price3;
9.  else  if ((price2 < price1) && (price2 < price3))
10.  amt_paid = price1 + price3;
11.  else
12.  amt_paid = price2 + price1;
13.  printf("Pls pay %f",amt_paid);
14.  }

[C code explanation](#contents.xhtml_sc4_319a)

The code prompts the user to enter the prices of three books and compare them. The conditions are combined using and operator. It picks the price of two books with higher MRP than the third one and calculates the amount to be paid based on those two books. It then provides the appropriate output message indicating the amount to be paid.

[Conclusion](#contents.xhtml_sc2_320a)

The chapter has discussed decision statements through flowcharts, algorithms, and coding. With the help of several examples, the different flavors of condition statements are presented.

In the next chapter, control flow statements (loops) will be discussed with the help of a good number of solved programs.

[Points to remember](#contents.xhtml_sc2_321a)

*   For comparing the values, double equal to sign (==) is used.
*   In Python, indentation plays an important role in deciding the code block.
*   In C, a single line block can be written without special care.
*   Multiple line blocks in C should be enclosed within curly {} brackets.
*   An if statement within the if block is known as a nested if else statement.
*   It is possible to check many options one after the other using the if- else if - else statement.
*   Logical operators and (&&) / or (||) allow us to combine multiple conditions in a single if- statement.
*   While writing the code, the order of checking the conditions should be decided carefully.

[Questions](#contents.xhtml_sc2_322a)

1. Write a program to check if the number entered by the user is divisible by 4 using the if statement.

2. Extend question 1 to print the appropriate message using the else statement.

3. Extend question 1\. If the number is not divisible by 4, then check whether it is an even number.

4. Further to question 2, if the number is divisible by 4, check if it is divisible by 9.

5. Write a program to check whether the user is an adult male.

# [CHAPTER 3Simple Loops](#contents.xhtml_ch03a)

[Introduction](#contents.xhtml_sc2_323a)

In this chapter, the basic loop statements, while-loop and for-loop, are discussed. In programming, a loop is a fundamental control structure that allows you to execute a block of code repeatedly as long as a certain condition is met. Loops are essential for automating repetitive tasks, iterating over certain statements, and performing various computational tasks efficiently. It optimizes the code as well. There are different types of loops in most programming languages, but the two main types are while-loops and for-loops:

*   While-loop: A while loop repeatedly executes a block of code as long as a specified condition is evaluated to be true. The loop continues to run until the condition becomes false. The loop counter is initialibefore the beginning of the while-loop. It is incremented inside the loop.
*   For-loop: A for loop is used when you know the number of iterations. It allows you to iterate over a sequence (list, tuple, string) or a range of values. All three operations, initialization, increment, and condition check, are performed using a single statement.

The flowchart presents loops by pointing the edge backward until the loop condition becomes false.

[Structure](#contents.xhtml_sc2_324a)

In this chapter, there are a total of 16 programs, and five sub-sections complement each program:

*   Understand the program objective with sample test cases consisting of inputs and outputs. It will give the user an understanding of what kind of user input is expected and what result will be projected for a particular program.
*   Understand the program with an algorithm. This will help the user to understand the logic and methodology behind writing the sequence of steps required to solve a program.
*   Visualize the program flow with flowcharts. Program objectives can be understood easily with the flowchart representation. Users will understand which symbols to use in which context throughout different program’s flowchart representations.
*   Python source code of each program. Each program’s source code in Python is provided to the user so the user can understand the basic operations of the language. An explanation of each code is also provided.
*   C implementation of each program. Users can learn the basic concepts of C language with the provided C language code and its explanation for every program.

[Objectives](#contents.xhtml_sc2_325a)

This chapter provides readers with a comprehensive understanding of control statements and their importance in the development of programs. It covers the fundamental concepts behind control statements and how they can execute the instruction repeatedly using a loop. Additionally, the chapter imparts the skills necessary for visual representations of control statements in program flow using flowcharts, facilitating a clearer and more intuitive grasp of their functionality.

Moreover, the chapter focuses on practical application by demonstrating how to implement control statements (for-loop and while-loop) in Python and C programming languages. Sample codes are provided to offer hands-on experience, allowing readers to practice and gain confidence in effectively utilizing loops in real-world coding scenarios. By the end of this chapter, readers will have acquired the knowledge and skills to leverage control statements in their programming.

[Program 3.1: Display '*'](#contents.xhtml_sc2_326a)

Display *for n times.

[Sample input output](#contents.xhtml_sc3_327a)

Test case #1:

Input: Enter a number: 3

Output: * * *

Test case #2:

Input: Enter a number: 6

Output: * * * * * *

[Algorithm](#contents.xhtml_sc3_328a)

To run the above program, the following steps are needed:

Step 1\. Start

Step 2\. Input n

Step 3\. i=1

Step 4\. Repeat if i< = n:

print "*"

i=i+1

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_329a)

[Figure 3.1](#ch03.xhtml_fig3-1) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.1.jpg)

Figure 3.1: Flowchart illustrating the program 3.1

[Python code](#contents.xhtml_sc3_330a)

Python code for the program is as follows:

n=int(input("Enter a number: "))

1.  i=1
2.  while(i<=n):
3.  print("*", end=" ")
4.  i=i+1

[Python code explanation](#contents.xhtml_sc4_331a)

This Python code prompts the user to enter a number, and the input function is used to read the input from the user. The input is initially treated as a string, so we use int() to convert it to an integer and store it in the variable n. The variable i is initialized to 1. The variable i is used to keep track of the current iteration. To repeat statements 4 and 5, while loop is used. The loop will continue executing if the value of i is less than or equal to n.

Inside the while loop, this line prints an asterisk (*) to the console using the print function. The end=" " argument is used to specify that after printing the asterisk, a space should be added instead of the default newline character. This means that each asterisk will be printed side by side on the same line instead of each one on a new line.

After each execution of the while block, the counter i is increased by 1. This is essential because it ensures that the loop will eventually reach a point where the condition (i<= n) becomes false, and the loop will terminate.

So, it should be noted that instead of writing the statement 4 again and again, it is written once, while loop helps repeat the statement n times.

Also, note the indentation in the code. Since steps 4and5 are indented towards the right, both belong to the block of while loop.

[C code](#contents.xhtml_sc3_332a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  printf("Enter a number: " );
6.  scanf("%d", &n);
7.  i=1;
8.  while(i<=n)
9.  {
10.  printf ("*");
11.  i=i+1;
12.  }
13.  }

[C code explanation](#contents.xhtml_sc4_333a)

This C code prompts the user to enter a number n and reads the input from the user using the scanf() function. The variable i is an integer-type variable that is initialized toequal1\. The variable i is used to keep track of the current iteration. Steps 10 and 11 are enclosed within the curly brackets, indicating that it is a block of while-loop. These statements will continue repeating if the value of i is less than or equal to n.

Inside the while loop, this line prints an asterisk (*) to the console using the printf() function. After each execution of the while block, the counter i is increased by 1\. This is essential because it ensures that the loop will eventually reach a point where the condition (i<= n) becomes false, and the loop will terminate.

[Program 3.2: Display natural numbers](#contents.xhtml_sc2_334a)

Display first n natural numbers.

[Sample input output](#contents.xhtml_sc3_335a)

Test case #1:

Input: Enter a number: 4

Output: 1 2 3 4

Test case #2:

Input: Enter a number: 7

Output: 1 2 3 4 5 6 7

[Algorithm](#contents.xhtml_sc3_336a)

To run the above program, the following steps are needed:

Step 1\. Start

Step 2\. Input n

Step 3\. i=1

Step 4\. Repeat if i< = n:

print i

i=i+1

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_337a)

[Figure 3.2](#ch03.xhtml_fig3-2) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.2.jpg)

Figure 3.2: Flowchart illustrating the program 3.2

[Python code](#contents.xhtml_sc3_338a)

Python code for the program is as follows:

1.  n=int(input("Enter a number: "))
2.  i=1
3.  while(i<=n):
4.  print(i, end=" ")
5.  i=i+1

[Python code explanation](#contents.xhtml_sc4_339a)

The Python code is to print first n natural numbers (starting from 1). It takes an integer input n from the user. The variable i is initialized to 1 to keep track of the count of iterations of the loop. Then, it uses a while loop to print numbers from 1 to n, separated by spaces in ascending order. The loop stops when the value of i becomes more than n. Note the indentation of the while-block.

[C code](#contents.xhtml_sc3_340a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  printf("Enter a number: " );
6.  scanf("%d", &n);
7.  i=1;
8.  while(i<=n)
9.  {
10.  printf (" %d", i);
11.  i=i+1;
12.  }
13.  }

[C code explanation](#contents.xhtml_sc4_341a)

The C code prints first n natural numbers (starting from 1). It takes an integer input n from the user. The variable i is initialized to 1 to keep track of the count of iterations of the loop. Then, it uses a while loop to print numbers from 1 to n, separated by spaces in ascending order. The loop stops when the value of i becomes more than n. Note the curly {} brackets of the while-block.

[Program 3.3: Display square of natural numbers](#contents.xhtml_sc2_342a)

Display the square of the first n natural numbers.

[Sample input output](#contents.xhtml_sc3_343a)

Test case #1:

Input: Enter a number: 3

Output: 149

Test case #2:

Input: Enter a number: 5

Output: 1491625

[Algorithm](#contents.xhtml_sc3_344a)

To run the above program, the following steps are needed:

Step 1\. Start

Step 2\. Input n

Step 3\. i=1

Step 4\. Repeat if i< = n:

print i*i

i=i+1

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_345a)

[Figure 3.3](#ch03.xhtml_fig3-3) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.3.jpg)

Figure 3.3: Flowchart illustrating the program 3.3

[Python code](#contents.xhtml_sc3_346a)

Python code for the program is as follows:

1.  n=int(input("Enter a number: "))
2.  i=1
3.  while(i<=n):
4.  print(i*i)
5.  i=i+1

[Python code explanation](#contents.xhtml_sc4_347a)

This code takes an integer input from the user, stores it in the variable n, and then uses a while loop to calculate and print the square of each number from 1 to n. Each square is printed on a new line. The loop iterates from 1 to n, inclusive, and i is incremented by 1 after each iteration.

[C code](#contents.xhtml_sc3_348a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  printf("Enter a number: " );
6.  scanf("%d", &n);
7.  i=1;
8.  while(i<=n)
9.  {
10.  printf (" %d", i*i);
11.  i=i+1;
12.  }
13.  }

[C code explanation](#contents.xhtml_sc4_349a)

This C code takes an integer input from the user, stores it in the variable n, and then uses a while loop to calculate and print the square of each number from 1 to n. Each square is printed on a new line. The loop iterates from 1to n, inclusive, and i is incremented by 1 after each iteration. Note the placement of curly brackets. Everything inside the curly brackets of the while-loop is repeated till the condition i<=n becomes false.

[Program 3.4: Display cube of numbers](#contents.xhtml_sc2_350a)

Display the cube of numbers between the range n and m where n and m are inclusive.

[Sample input output](#contents.xhtml_sc3_351a)

Test case #1:

Input:

Enter number1: 5

Enter number2: 9

Output: 125216343512729

Test case #2:

Input:

Enter number1: 2

Enter number2: 5

Output: 82764125

[Algorithm](#contents.xhtml_sc3_352a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Input n,m

Step 3\. i=n

Step 4\. Repeat if i< = m:

print i*i*i

i=i+1

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_353a)

[Figure 3.4](#ch03.xhtml_fig3-4) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.4.jpg)

Figure 3.4: Flowchart illustrating the program 3.4

[Python code](#contents.xhtml_sc3_354a)

Python code for the program is as follows:

1.  n=int(input("Enter number1: "))
2.  m=int(input("Enter number2: "))
3.  i=n
4.  while(i<=m):
5.  print(i*i*i)
6.  i=i+1

[Python code explanation](#contents.xhtml_sc4_355a)

This Python code prompts the user to enter two integer numbers, n, and m, and then uses a while loop to calculate and print the cube of each number from n to m. The variable i is initialized with the value of n. The loop starts with i=n and stops when i becomes greater than m. The loop variable i is incremented by 1 after each iteration to ensure the progress of the while-loop. Inside the loop, the cube of the current value i is calculated and printed on the console.

[C code](#contents.xhtml_sc3_356a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n, m;
5.  printf("Enter two numbers: " );
6.  scanf("%d%d", &n, &m);
7.  i=n;
8.  while(i<=m)
9.  {
10.  printf (" %d", i*i*i);
11.  i=i+1;
12.  }
13.  }

[C code explanation](#contents.xhtml_sc4_357a)

This C code asks the user to enter two integer numbers, n, and m, and then uses a while-loop to calculate and print the cube of each number from n to m. The variable i is initialized with the value of n. The loop starts with i=n and stops when i becomes greater than m. The loop variable i is incremented by 1 after each iteration to ensure the progress of the while-loop. Inside the loop, the cube of the current value of i is calculated and printed on the console.

[Program 3.5: Display multiples](#contents.xhtml_sc2_358a)

Display first n multiples of 5.

[Sample input output](#contents.xhtml_sc3_359a)

Test case #1:

Input: Enter number: 4

Output: 5101520

Test case #2:

Input: Enter number: 6

Output:51015202530

[Algorithm](#contents.xhtml_sc3_360a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Input n

Step 3\. i=1

Step 4\. Repeat if i< = n:

print 5*i

i=i+1

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_361a)

[Figure 3.5](#ch03.xhtml_fig3-5) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.5.jpg)

Figure 3.5: Flowchart illustrating the program 3.5

[Python code](#contents.xhtml_sc3_362a)

Python code for the program is as follows:

1.  n=int(input("Enter number: "))
2.  i=1
3.  while(i<=n):
4.  print(5*i)
5.  i=i+1

[Python code explanation](#contents.xhtml_sc4_363a)

This Python code prompts the user to enter an integer number, n, and then uses a while loop to calculate and print the n multiples of 5, such as 5, 10, 15, and so on. The loop iterates from 1 to n, inclusive, and the loop variable i is incremented by 1 after each iteration. The while-loop continues as long as the value of i is less than or equal to n. Inside the loop, it calculates the multiple of 5 by multiplying the current value of i with 5 and printing the result on the console. The block of the while-loop is presented with indentation.

[C code](#contents.xhtml_sc3_364a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  printf("Enter a numbers: " );
6.  scanf("%d", &n);
7.  i=1;
8.  while(i<=n)
9.  {
10.  printf (" %d", 5*i);
11.  i=i+1;
12.  }
13.  }

[C code explanation](#contents.xhtml_sc4_365a)

This code prompts the user to enter an integer number, n, and then uses a while loop to calculate and print the n multiples of 5, such as 5, 10, 15, and so on. The loop iterates from 1 to n, inclusive, and the loop variable i is incremented by 1 after each iteration. The while-loop continues as long as the value of i is less than or equal to n. Inside the loop, it calculates the multiple of 5 by multiplying the current value of i with 5 and printing the result on the console. The block of the while-loop is presented within curly brackets.

[Program 3.6: Find sum and average](#contents.xhtml_sc2_366a)

Display the sum and average of the first 10 natural numbers.

[Sample input output](#contents.xhtml_sc3_367a)

Test case #1:

Output: Sum and Average are 55, 5.5

[Algorithm](#contents.xhtml_sc3_368a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Declare the variables as i,n,s,avg

Step 3\. i=0, s=0, avg=0

Step 4\. if i<n

i=i+1

s = s + i

Step 5\. Repeat step 4

Step 6\. Display s

Step 7\. avg=s/10

Step 8\. Display avg

Step 9\. Stop

[Flowchart](#contents.xhtml_sc3_369a)

[Figure 3.6](#ch03.xhtml_fig3-6) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.6.jpg)

Figure 3.6: Flowchart illustrating the program 3.6

[Python code](#contents.xhtml_sc3_370a)

Python code for the program is as follows:

1.  i=0
2.  s=0
3.  avg=0
4.  while ( i<10):
5.  i=i+1
6.  s = s + i
7.  avg=s/10

9.  print("Sum and Average are ", s, avg)

[Python code explanation](#contents.xhtml_sc4_371a)

This code calculates the sum and average of the first 10 natural numbers and then prints the result. Here, a variable i is initialized with the value 0. This variable will be used as a loop counter. The variables s and avg are used to store the sum and average of the numbers, respectively. Both are initialized with a value of 0, indicating that the initial sum and average are zero. Inside the loop, increment the value of i by 1 to count the loop iterations from 1 to 10. Also, the current value of i is added to s to continuously accumulate the sum of the numbers from 1 to 10. Once the sum of 10 numbers is calculated in the while-loop, the sum, s, is divided by 10 to get the average and stored in avg.

Note: The same problem statement can also be solved without using loops. Use the formula s=n(n+1)/2 and avg=s/n.

[C code](#contents.xhtml_sc3_372a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, s=0;
5.  float avg=0.0;
6.  i=0;
7.  while(i<10)
8.  {
9.  i=i+1;
10.  s=s+i;
11.  }
12.  avg=s/10.0;
13.  printf("The sum and average of first 10 natural numbers are : %d and %f", s, avg);
14.  }

[C code explanation](#contents.xhtml_sc4_373a)

This code calculates the sum and average of the first 10 natural numbers and then prints the result. Here, a variable i is initialized with the value 0. This variable will be used as a loop counter. The variables s and avg are used to store the sum and average of the numbers, respectively. Since the sum of numbers can be an integer value, and the average can be a decimal value, s is declared int type and avg as float type. Both are initialized with a value of 0, indicating that the initial sum and average are zero. Inside the loop, increment the value of i by 1 to count the loop iterations from 1 to 10. Also, the current value of i is added to s to continuously accumulate the sum of the numbers from 1 to 10. Once the sum of 10 numbers is calculated in the while-loop, the sum, s, is divided by 10.0 to get the average and stored in avg.

Note: The same problem statement can also be solved without using loops. Use the formula s=n(n+1)/2 and avg=s/n.

[Program 3.7: Find sum of sqaure](#contents.xhtml_sc2_374a)

Display the sum of the square of the first n natural numbers.

[Sample input output](#contents.xhtml_sc3_375a)

Test case #1:

Input: Enter a number: 10

Output: Sum is 385

Test case #2:

Input: Enter a number: 18

Output: Sum is 2109

[Algorithm](#contents.xhtml_sc3_376a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Input n

Step 3\. i=0, s=0

Step 4\. Repeat if i< n:

i=i+1

s = s+i*i

Step 5\. Display s

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_377a)

[Figure 3.7](#ch03.xhtml_fig3-7) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.7.jpg)

Figure 3.7: Flowchart illustrating the program 3.7

[Python code](#contents.xhtml_sc3_378a)

Python code for the program 3.7 is as follows:

1.  n=int(input("Enter a number: "))
2.  i=0
3.  s=0
4.  while ( i<n):
5.  i=i+1
6.  s = s + i*i
7.  print("Sum is ",s)

[Python code explanation](#contents.xhtml_sc4_379a)

This code calculates the sum of squares of the first n natural numbers and then prints the result. First, it prompts the user to enter a number and reads the input as an integer. Store it in the variable n. Then, it initializes a variable i with the value 0. This variable will be used as a loop counter. Variable sis initialized with the value 0. This variable will be used to store the sum of squares. While-loop starts with the condition (i< n). The loop will continue if the value of i is less than n. Inside the loop, the value of i is incremented by 1. Also, the square of the current value of i (i*i) is calculated and added to the variable s. This will continuously accumulate the sum of squares of the numbers from 1 to n.

[C code](#contents.xhtml_sc3_380a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  int s=0;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);
8.  i=0;
9.  while(i<n)
10.  {
11.  i=i+1;
12.  s=s+i*i;
13.  }
14.  printf("The sum of square of first %d natural numbers is %d", n, s);
15.  }

[C code explanation](#contents.xhtml_sc4_381a)

This code calculates the sum of squares of the first n natural numbers and then prints the result. First, it prompts the user to enter a number and reads the input as an integer. Store it in the variable n. Then, it initializes a variable i with the value 0. This variable will be used as a loop counter. Variable s is declared as an integer and initialized with the value 0. This variable will be used to store the sum of squares. While-loop starts with the condition (i< n). The loop will continue as long as the value of i is less than n. Inside the loop, the value of i is incremented by 1. Also, the square of the current value of i(i*i) is calculated and added to the variable s. This will continuously accumulate the sum of squares of the numbers from 1 to n.

[Program 3.8: Find factorial](#contents.xhtml_sc2_382a)

Display the product of the first n natural numbers (factorial of n).

[Sample input output](#contents.xhtml_sc3_383a)

Test case #1:

Input: Enter a number: 5

Output: Product is 120

Test case #2:

Input: Enter a number: 10

Output: Product is 3628800

[Algorithm](#contents.xhtml_sc3_384a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Input n

Step 3\. i=0, p=1

Step 4\. Repeat if i< = n:

i=i+1

p = p*i

Step 5\. Display p

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_385a)

[Figure 3.8](#ch03.xhtml_fig3-8) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.8.jpg)

Figure 3.8: Flowchart illustrating the program 3.8

[Python code](#contents.xhtml_sc3_386a)

Python code for the program is as follows:

1.  n=int(input("Enter a number: "))
2.  i=0
3.  p=1
4.  while ( i<n):
5.  i=i+1
6.  p = p * i
7.  print("Product is ",p)

[Python code explanation](#contents.xhtml_sc4_387a)

The code prints the product of first n natural numbers. It is also called the factorial of a number. Here, i is used to count the loop repetition. Variable p is used to store the accumulated product of n numbers. It is initialized with a value of 1 as something multiplied by a number results in that number itself. While-loop starts with 0 and goes till the value of i is less than n. Finally, the value of p is displayed.

[C code](#contents.xhtml_sc3_388a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  int p=1;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);
8.  i=0;
9.  while(i<n)
10.  {
11.  i=i+1;
12.  p=p*i;
13.  }
14.  printf("The factorial of %d is %d", n, p);
15.  }

[C code explanation](#contents.xhtml_sc4_389a)

The code prints the product of first n natural numbers. It is also called the factorial of a number. Here, i is used to count the loop repetition. Variable p is used to store the accumulated product of n numbers. It is initialized with a value of 1 as something multiplied by a number results in that number itself. While-loop starts with 0 and goes till the value of i is less than n. Finally, the value of p is displayed.

[Program 3.9: Find 2 raise to the power n](#contents.xhtml_sc2_390a)

Take n as input and compute 2^n (2 raised to the power n).

[Sample input output](#contents.xhtml_sc3_391a)

Test case #1:

Input: Enter n:3

Output: 2^3 =8

Test case #2:

Input: Enter n:6

Output:2^6 = 64

[Algorithm](#contents.xhtml_sc3_392a)

To run the above program, the following steps are needed to be:

Step 1\. Start

Step 2\. Read n

Step 3\. p=1, i=1

Step 4\. Repeat if i<=n

p=p*2

i=i+1

Step 5\. Print("2^",n," = ",p)

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_393a)

[Figure 3.9](#ch03.xhtml_fig3-9) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.9.jpg)

Figure 3.9: Flowchart illustrating the program 3.9

[Python code](#contents.xhtml_sc3_394a)

Python code for the program is as follows:

1.  n=int(input("Enter n: "))
2.  p=1
3.  for i in range(1,n+1):
4.  p=p*2
5.  print("2^",n," = ",p)

[Python code explanation](#contents.xhtml_sc4_395a)

To calculate 2 raised to the power n, we need to multiply 2 to itself n times. The same logic is implemented using Python code. In this program, instead of while-loop, for-loop is used, although while-loop can also be used. After taking input from the user, variable p is initialized to 1. This variable calculates and stores the result of 2 raised to the power n. In the for-loop, it starts with a keyword for that iterates over the values in the range from 1 ton (inclusive). The variable i takes the values 1, 2, 3, ..., n during each iteration represented using range(1,n+1). The range function includes the first parameter, 1, and excludes the last parameter. Hence, it will generate the values from 1 to n. Then, the current value of p is multiplied by 2 (2 is the base for the exponentiation). This step is performed for each value of i in the loop, effectively calculating 2^1, 2^2, 2^3, ..., 2^n. Finally, the calculated value of p, representing 2 raised to the power n, is displayed.

[C code](#contents.xhtml_sc3_396a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  int p=1;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);
8.  i=1;
9.  while(i<=n)
10.  {
11.  p=p*2;
12.  i=i+1;
13.  }
14.  printf("The 2^%d is %d", n, p);
15.  }

[C code explanation](#contents.xhtml_sc4_397a)

To calculate 2 raised to the power n, we need to multiply 2 to itself n times. The same logic is implemented using this C code. Here, after taking input from the user, variable p is initialized to 1. This variable calculates and stores the result of 2 raised to the power n. The while-loop iterates from 1 to n. Then, the current value of p is multiplied by 2 (2 is the base for the exponentiation). This step is performed for each value of i in the loop, effectively calculating 2^1, 2^2, 2^3, ..., 2^n. The value of i is incremented after every iteration. Finally, the calculated value of p, representing 2 raised to the power n, is displayed.

[Program 3.10: Find x raise to the power n](#contents.xhtml_sc2_398a)

Take x and n as input and compute x^n (x raised to the power n).

[Sample input output](#contents.xhtml_sc3_399a)

Test case #1:

Input:

Enter n: 3

Enter x: 4

Output: 4 ^ 3 = 64

Test case #2:

Input:

Enter n: 2

Enter x: 6

Output: 6 ^ 2 = 36

[Algorithm](#contents.xhtml_sc3_400a)

To run the above program, the following steps are needed:

Step 1\. Start

Step 2\. Read n

Step 3\. Read x

Step 4\. p=1, i=1

Step 5\. Repeat if i<=n

p=p*x

i=i+1

Step 6\. Print(x, "^",n," = ",p)

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_401a)

[Figure 3.10](#ch03.xhtml_fig3-10) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.10.jpg)

Figure 3.10: Flowchart illustrating the program 3.10

[Python code](#contents.xhtml_sc3_402a)

Python code for the program 3.10 is as follows:

1.  n=int(input("Enter n: "))
2.  x=int(input("Enter x: "))
3.  p=1
4.  for i in range(1,n+1):
5.  p=p*x
6.  print(x,"^",n," = ",p)

[Python code explanation](#contents.xhtml_sc4_403a)

To calculate x raised to the power n, we need to multiply x by itself n times. The same logic is implemented using Python code. The remaining part is the same as program 3.9.

[C code](#contents.xhtml_sc3_404a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n, x;
5.  int p=1;
6.  printf("Enter two numbers: " );
7.  scanf("%d%d", &n, &x);
8.  i=1;
9.  while(i<=n)
10.  {
11.  p=p*x;
12.  i=i+1;
13.  }
14.  printf("The %d^%d is %d",x, n, p);
15.  }

[C code explanation](#contents.xhtml_sc4_405a)

To calculate x raised to the power n, we need to multiply x by itself n times. The same logic is implemented using this code. The remaining part is the same as program 3.9.

[Program 3.11: Display the multiplication table](#contents.xhtml_sc2_406a)

Display the multiplication table of a number taken as input from the user.

[Sample input output](#contents.xhtml_sc3_407a)

Test case #1:

Input: Enter a number: 11

Output:

11 x 1 = 11

11 x 2 = 22

11 x 3 = 33

11 x 4 = 44

11 x 5 = 55

11 x 6 = 66

11 x 7 = 77

11 x 8 = 88

11x 9 = 99

11 x 10 = 110

Test case #2:

Input: Enter a number: 4

Output:

4 x 1 = 4

4 x 2 = 8

4 x 3 = 12

4 x 4 = 16

4 x 5 = 20

4 x 6 = 24

4 x 7 = 28

4 x 8 = 32

4 x 9 = 36

4 x 10 = 40

[Algorithm](#contents.xhtml_sc3_408a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Accept a number as input from the user and store it in a
variable 'num'.

Step 3\. Loop from 1 to 10:

Multiply 'num' with the loop variable and store it in a
variable 'result'.

Print 'num', '*', loop variable, '=', 'result'.

Step 4\. End of loop.

Step 5\. Stop

[Flowchart](#contents.xhtml_sc3_409a)

[Figure 3.11](#ch03.xhtml_fig3-11) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.11.jpg)

Figure 3.11: Flowchart illustrating the program 3.11

[Python code](#contents.xhtml_sc3_410a)

Python code for the program 3.11 is as follows:

1.  num = int(input("Enter a number: "))

3.  for i in range(1, 11):
4.  print(num, "x", i, "=", num*i)

[Python code explanation](#contents.xhtml_sc4_411a)

The code prompts the user to enter a number and then prints the multiplication table for that number from 1 to 10 using for-loop. Since the range() function includes the first parameter and excludes the second parameter, range(1,11) is written to iterate the for-loop from 1 to 10. It displays the multiplication equation with the number and multiples on each line.

[C code](#contents.xhtml_sc3_412a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int  main() {
3.  int num;

5.  printf("Enter a number: ");
6.  scanf("%d", &num);
7.  for (int i = 1; i <= 10; i++) {
8.  printf("%d * %d = %d\n", num, i, num*i);
9.  }
10.  return  0;
11.  }

[C code explanation](#contents.xhtml_sc4_413a)

The code prompts the user to enter a number, num, and then prints the multiplication table for that number from 1 to 10 using for-loop. In C, the for-loop contains three sub-statements separated by a semi-colon: initialization (i=1), then condition (i<10), and finally increment (i++). According to the for-loop statement, the variable i is used to count the loop iterations. It starts with a value of 1. The value of i is incremented by 1 after every iteration. The loop stops when the value of i becomes greater than 10. It displays the multiplication equation with the number and multiples on each line.

[Program 3.12: Find sum of series 1](#contents.xhtml_sc2_414a)

Find the sum of the series: 1+ 3 + 5+........+ (2*n-1).

[Sample input output](#contents.xhtml_sc3_415a)

Test case #1:

Input: Enter n: 4

Output: 16

Test case #2:

Input: Enter n: 7

Output: 49

[Algorithm](#contents.xhtml_sc3_416a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Read n

Step 3\. i=1

Step 4\. s=0

Step 5\. Repeat if i<=n

s=s+2*i-1

Step 6\. Print s

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_417a)

[Figure 3.12](#ch03.xhtml_fig3-12) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.12.jpg)

Figure 3.12: Flowchart illustrating the program 3.12

[Python code](#contents.xhtml_sc3_418a)

Python code for the program 3.12 is as follows:

1.  n=int(input("Enter n: "))
2.  s=0

4.  for i in range(1, n+1):
5.  s=s+2*i-1
6.  print(s)

[Python code explanation](#contents.xhtml_sc4_419a)

To print the sum of series: 1+ 3 + 5+........+ (2*n-1), any nth number can be generated by substituting the value of n in (2*n-1). The same concept is used in the code. After taking input from the user, the variable s is initialized with a value of 0 and is used to store the sum of the series. Inside the for loop, the current value of i is used to calculate the i-th odd number (2*i-1), which is added to the variable s. This step is performed for each value of i in the loop, effectively calculating the sum of the first n odd numbers. After the loop, the code prints the calculated sum of the first n odd numbers.

[C code](#contents.xhtml_sc3_420a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n;
5.  int s=0;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);

9.  for(i =1; i<=n; i++)
10.  {
11.  s=s+2*i-1;
12.  }
13.  printf("The sum of the series is %d", s);
14.  }

[C code explanation](#contents.xhtml_sc4_421a)

To print the sum of series: 1+ 3 + 5+........+ (2*n-1), any nth number can be generated by substituting the value of n in (2*n-1). The same concept is used in the code. After taking input from the user, the variable s is initialized with a value of 0 and is used to store the sum of the series. Inside the for loop, the current value of i is used to calculate the i-th odd number (2*i-1), which is added to the variable s. This step is performed for each value of i in the loop, effectively calculating the sum of the first n odd numbers. After the loop, the code prints the calculated sum of the first n odd numbers.

[Program 3.13: Find sum of series 2](#contents.xhtml_sc2_422a)

Find the sum of series: 1/2!+2/3!+3/4!..........

[Sample input output](#contents.xhtml_sc3_423a)

Test case #1:

Input: Enter the number of terms: 4

Output: Sum of the series is: 1.4833333333333332

Test case #2:

Input: Enter the number of terms: 8

Output: Sum of the series is: 1.4999944885361551

[Algorithm](#contents.xhtml_sc3_424a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Initialize a variable n to the number of terms to be added
in the series.

Step 3\. Initialize two variables, sum and fact, to 0 and 1 respectively.

Step 4\. Using a loop ranging from 1 to n, perform the following
steps:

update fact as fact * (i+1).

sum=sum+i/f

Step 5\. Print the final value of sum.

Step 6\. Stop

[Flowchart](#contents.xhtml_sc3_425a)

[Figure 3.13](#ch03.xhtml_fig3-13) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.13.jpg)

Figure 3.13: Flowchart illustrating the program 3.13

[Python code](#contents.xhtml_sc3_426a)

Python code for the program 3.13 is as follows:

1.  n = int(input("Enter the number of terms: "))
2.  sum = 0
3.  f=1

5.  for i in range(1, n+1):
6.  if i == 1:
7.  sum += 1/2
8.  else:
9.  f = f*(i+1)
10.  sum =sum + i/f

12.  print("Sum of the series is:", sum)

[Python code explanation](#contents.xhtml_sc4_427a)

The code prompts the user to enter the number of terms (n) and then calculates the sum of a series using a for-loop. It considers a special case for the first term (1/2) and computes subsequent terms based on the factorial. Finally, it prints the sum of the series. The series formula is 1/2 + 1/2! + 2/3! + 3/4! + ... + (n-1)/n!.

[C code](#contents.xhtml_sc3_428a)

C code for the program is as follows:

1.  #include <stdio.h>

3.  int  main() {
4.  int n;
5.  double sum = 0, factorial = 1;
6.  printf("Enter the value of n: ");
7.  scanf("%d", &n);

9.  for(int i = 1; i <= n; i++) {
10.  factorial *= i+1;
11.  sum += i / factorial;
12.  }
13.  printf("Sum of the series is: %lf", sum);
14.  return  0;
15.  }

[C code explanation](#contents.xhtml_sc4_429a)

The code prompts the user to enter the number of terms (n) and then calculates the sum of a series using a for-loop. Here, the variables, sum and factorial, are declared of type double as the value of these variables will be very high for the high value of i. The code considers a special case for the first term (1/2) and computes subsequent terms based on the factorial. Finally, it prints the sum of the series. The series formula is 1/2 + 1/2! + 2/3! + 3/4! + ... + (n-1)/n!.

[Program 3.14: Find sum of series 3](#contents.xhtml_sc2_430a)

Find the sum of the series [ 9 + 99 + 999 + 9999 ...]

[Sample input output](#contents.xhtml_sc3_431a)

Test case #1:

Input: Enter n: 4

Output:11106

Test case #2:

Input: Enter n: 8

Output:111111102

[Algorithm](#contents.xhtml_sc3_432a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Declare the var as i,n,sum,t

Step 3\. Read value of n

Step 4\. i=1,s=0,t=9

Step 5\. Repeat if i<=n

s =s+t

t=t*10+9

i=i+1

Step 6\. Display sum

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_433a)

[Figure 3.14](#ch03.xhtml_fig3-14) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.14.jpg)

Figure 3.14: Flowchart illustrating the program 3.14

[Python code](#contents.xhtml_sc3_434a)

Python code for the program 3.14 is as follows:

1.  n=int(input("Enter n: "))

3.  s=0
4.  t=9
5.  for i in range(1, n+1):
6.  s=s+t
7.  t=t*10+9

9.  print(s)

[Python code explanation](#contents.xhtml_sc4_435a)

This code prompts the user to enter a number (n) and then calculates and prints the sum of a series based on the pattern of repeating digit 9. To generate the next value of the series, the current value of t is updated by multiplying it by 10 and then adding 9. This step generates the next term of the series based on the pattern of repeating digit 9. After the loop, the variable s will contain the sum of the series.

[C code](#contents.xhtml_sc3_436a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i, n, t=9;
5.  float s=0;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);

9.  for(i =1; i<=n; i++)
10.  {
11.  s=s+t;
12.  t=t*10+9;
13.  }

15.  printf("The sum of the series is %f", s);

17.  }

[C code explanation](#contents.xhtml_sc4_437a)

This code prompts the user to enter a number (n) and then calculates and prints the sum of a series based on the pattern of repeating digit 9. To generate the next value of the series, the current value of tis updated by multiplying it by 10 and then adding 9. This step generates the next term of the series based on the pattern of repeating digit 9. After the loop, the variable s will contain the sum of the series.

[Program 3.15: Find sum of n elements](#contents.xhtml_sc2_438a)

Find the sum of n elements entered by the user.

[Sample input output](#contents.xhtml_sc3_439a)

Test case #1:

Input:

Enter n: 5

Enter x: 2

Enter x: 1

Enter x: 6

Enter x: 5

Enter x: 3

Output: The sum is 17

Test case #2:

Input:

Enter n: 3

Enter x: 8

Enter x: 7

Enter x: 9

Output: The sum is 24

[Algorithm](#contents.xhtml_sc3_440a)

To run the above program, the following steps are needed to be followed:

Step 1\. Start

Step 2\. Declare the variables as x

Step 3\. Read value of n

Step 4\. i=1, s=0

Step 5\. Repeat if i<=n

x=read("Enter number", i)

s=s+ x

i=i+1

Step 6\. Print("The sum is ", s)

Step 7\. Stop

[Flowchart](#contents.xhtml_sc3_441a)

[Figure 3.15](#ch03.xhtml_fig3-15) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.15.jpg)

Figure 3.15: Flowchart illustrating the program 3.15

[Python code](#contents.xhtml_sc3_442a)

Python code for the program3.15 is as follows:

1.  s=0
2.  n=int(input("Enter n: "))
3.  for i in range(1, n+1):
4.  x=int(input("Enter x: "))
5.  s =s+ x
6.  print("The sum is ", s)

[Python code explanation](#contents.xhtml_sc4_443a)

This code prompts the user to enter a number n, then it iteratively asks the user to enter n values (x) inside the loop and calculates the sum of those values. Finally, it prints the calculated sum.

[C code](#contents.xhtml_sc3_444a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int i;
5.  int s=0;
6.  int x,n;

8.  printf("Enter a numbers: " );
9.  scanf("%d", &n);
10.  printf("Enter %d numbers: ",n );
11.  for(i =1; i<=n; i++)
12.  {
13.  scanf("%d", &x);
14.  s=s+x;
15.  }

17.  printf("The sum is %d", s);

19.  }

[C code explanation](#contents.xhtml_sc4_445a)

This code prompts the user to enter a number n, then it iteratively asks the user to enter n values (x) inside the loop and calculates the sum of those values. Finally, it prints the calculated sum.

[Program 3.16: Display Fibonacci series](#contents.xhtml_sc2_446a)

Display the n terms of the Fibonacci series. For example, if n=6, the output should be 1 1 2 3 5 8.

[Sample input output](#contents.xhtml_sc3_447a)

Test case #1:

Input: Enter n: 5

Output: 1 1 2 3 5

Test case #2:

Input: Enter n: 10

Output: 1 1 2 3 5 8 13 21 34 55

[Algorithm](#contents.xhtml_sc3_448a)

To run the above program, the following steps are needed:

Step 1\. Start

Step 2\. Declare variables n,x,y,z

Step 3\. Read n

Step 4\. x=1

Step 5\. y=1

Step 6\. print(x)

Step 7\. print(y)

Step 8\. Repeat for i=(3, n+1):

z=x+y

print(z)

x=y

y=z

Step 1\. Stop

[Flowchart](#contents.xhtml_sc3_449a)

[Figure 3.16](#ch03.xhtml_fig3-16) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_3.16.jpg)

Figure 3.16: Flowchart illustrating the program 3.16

[Python code](#contents.xhtml_sc3_450a)

Python code for the program 3.16 is as follows:

1.  n=int(input("Enter n: "))
2.  x=1
3.  y=1
4.  print(x, end=" ")
5.  print(y, end=" ")
6.  for i in range(3, n+1):
7.  z=x+y
8.  print(z, end=" ")
9.  x=y
10.  y=z

[Python code explanation](#contents.xhtml_sc4_451a)

The Fibonacci sequence is where the next number is found by adding up the two numbers before it. The first two numbers are fixed as 1, 1\. This code prompts the user to enter a number n, then generates and prints the first n numbers of the Fibonacci sequence using a for loop. Here, the x and y variables store the previous two numbers. In the loop, the next number, z, in the Fibonacci sequence is calculated by adding the current values of x and y. Then, the value of x is replaced by y, and the value of y is replaced by the value of z for the next iteration. The loop stops after printing n terms.

[C code](#contents.xhtml_sc3_452a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int n,x,y,z;
5.  printf("Enter n:");
6.  scanf("%d", &n);
7.  x=1;
8.  y=1;
9.  printf("%d", x);
10.  printf(" %d", y);
11.  for (int i=3; i<=n; i++)
12.  {
13.  z=x+y;
14.  printf(" %d", z);
15.  x=y;
16.  y=z;
17.  }}

[C code explanation](#contents.xhtml_sc4_453a)

The Fibonacci sequence is where the next number is found by adding up the two numbers before it. The first two numbers are fixed as 1, 1\. This code prompts the user to enter a number n, then generates and prints the first n numbers of the Fibonacci sequence using a for loop. Here, the x and y variables store the previous two numbers. In the loop, the next number, z, in the Fibonacci sequence is calculated by adding the current values of x and y. Then, the value of x is replaced by y, and the value of y is replaced by the value of z for the next iteration. The loop stops after printing n terms.

[Conclusion](#contents.xhtml_sc2_454a)

The chapter has discussed simple control statements (while-loop and for-loop) in the form of flowcharts, algorithms, and coding. With the help of several examples, the different flavors of loop statements are presented.

In the next chapter, complex control flow statements (loops) will be discussed with the help of a good number of solved programs.

[Points to remember](#contents.xhtml_sc2_455a)

*   If some statements are supposed to be repeated in a code, write them once inside a loop statement instead of writing the same statements repeatedly. It makes the code more efficient.
*   For the while-loop, the loop counter, generally i, is initialized before the loop and is incremented inside the loop.
*   In the for-loop, initialization, condition check, and increment, all three operations are mentioned in one statement at the beginning.
*   In Python code, the loop block should be indented toward the right side.
*   In C code, the loop block should be enclosed within curly brackets {}.
*   Loop counter value should be assigned carefully. For instance, we want to execute a loop 5 times. Then either assign i=0 and check the condition as i<n or assign i=1 and check the condition as i<=n.

[Questions](#contents.xhtml_sc2_456a)

1. Display first n whole numbers. For example:0,1,2,3,4…

2. Find the sum of every fifth number in the range 0-500

3. Display all the numbers between 1 to 10, incrementing each time by 2.

4. Accept a number as input from the user. If the number is less than 0, change it to zero, print Negative change to zero,  and ask the user to enter again until the number is ≥ 0, and print the number.

5. Display a cube of first n natural numbers.

6. Display the sum of the first n natural numbers.

7. Display the sum of the cube of the first n natural numbers.

8. Find the sum of the series: 2+ 5 + 8+........+ (3*n-1).

9. Find the sum of the series: 5+ 9 + 13+........+ (4*n + 1).

10. Find the sum of the series: 1/2 + 1/5 + 1/8+….....+ 1/(3*n-1).

11. Find the sum of the series:1+1/1!+1/2!+....+ 1/n!

# [CHAPTER 4Complex Loops](#contents.xhtml_ch04a)

[Introduction](#contents.xhtml_sc2_457a)

In this chapter, the complex usage of loop statements, while-loop and for-loop are discussed. In programming, a loop is a fundamental control structure that allows you to execute a block of code repeatedly as long as a certain condition is met. The loops can be used along with multiple conditional statements to solve complex problems. Moreover, some of the problems require the use of multiple loops, one after the other, or nested loops. All these variants of problems are discussed in this chapter.

[Structure](#contents.xhtml_sc2_458a)

In this chapter, there are a total of 20 programs, and five sub-sections complement each program:

*   Understand the program objective with sample test cases consisting of inputs and outputs. It will give the user an understanding of what kind of user input is expected and what result will be projected for a particular program.
*   Understand the program with an algorithm. This will help the user to understand the logic and methodology behind writing the sequence of steps required to solve a program.
*   Visualize the program flow with flowcharts. Program objectives can be understood easily with the flowchart representation. Users will get an understanding of which symbols to be used in which context throughout different program’s flowchart representations.
*   Python source code of each program. Each program’s source code in Python programming language is provided to the user so the user can understand the basic operations of the language. An explanation of each code is also provided.
*   C implementation of each program. Users can learn the basic concepts of C language with the provided C language code and its explanation for every program.

[Objectives](#contents.xhtml_sc2_459a)

In this chapter, the reader will learn the complex control statements and their significance in program development. Additionally, the chapter imparts knowledge required for designing algorithms to perform decisions using while-loop and for-loop in combination with nested loops or conditional statements. Further, it focuses on the skills of creating visual representations of complex control statements in program flow using flowcharts. Moreover, it will develop the ability to use complex control statements while writing code in Python and C programming languages. With the sample codes, users can gain hands-on experience.

[Program 4.1: Find sum and check if even](#contents.xhtml_sc2_460a)

Display EVEN if the sum of the first n natural numbers is even; otherwise, display ODD.

[Sample input output](#contents.xhtml_sc3_461a)

Test case #1:

Input: Enter a number: 7

Output: EVEN

Test case #2:

Input: Enter a number: 5

Output: ODD

[Algorithm](#contents.xhtml_sc3_462a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read n
3.  i=1
4.  s=0
5.  Repeat if i<=n
6.  s=s+i
7.  i=i+1
8.  if s%2==0
9.  print "EVEN"
10.  else
11.  print "ODD"
12.  Stop

[Flowchart](#contents.xhtml_sc3_463a)

[Figure 4.1](#ch04.xhtml_fig4-1) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.1.jpg)

Figure 4.1: Flowchart illustrating the program 4.1

[Python code](#contents.xhtml_sc3_464a)

Python code for the program is as follows:

1.  n=int(input("Enter a number "))
2.  i=1
3.  s=0
4.  while(i<=n):
5.  s=s+i
6.  i=i+1
7.  #end of while loop
8.  print("The sum is ",s)
9.  if(s%2==0):
10.  print("EVEN");
11.  else:
12.  print("ODD");

[Python code explanation](#contents.xhtml_sc4_465a)

The Python code takes an input number n, calculates the sum of numbers from 1 to n, and then determines whether the sum is even or odd.

After inputting a number, variable i is initialized with the value 0 to control the loop iterations. Then, variable s is initialized with the value 0. This variable will be used to keep track of the sum of the numbers.

The while-loop will run until i reaches the value of n. The value of i is incremented by 1 in each iteration. The current value of i is added to the variable s, accumulating the sum of the numbers. After completing the loop, it prints out the calculated sum and checks if the sum s is even or odd using the modulus operator (%). If the remainder when s is divided by 2 is 0, then the sum is even otherwise odd.

[C code](#contents.xhtml_sc3_466a)

The C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, n;
5.  int s=0;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);
8.  i=1;
9.  while(i<=n)
10.  {
11.  s=s+i;
12.  i=i+1;
13.  }
14.  if (s%2==0)
15.  {printf("EVEN");}
16.  else
17.  {printf("ODD");}
18.  }

[C code explanation](#contents.xhtml_sc4_467a)

The C code takes an input number n, calculates the sum of numbers from 1 to n, and then determines whether the sum is even or odd.

Inside the main function, the local variables are declared and initialized. The variable i is initialized with 0 to control the loop iterations. Then, variable s is initialized with the value 0. This variable will be used to keep track of the sum of numbers. Then, it reads an integer input from the user and stores it in the variable n.

The while-loop will run until i reaches the value of n. The value of i is incremented by 1 in each iteration. The current value of i is added to the variable s, accumulating the sum of the numbers. This calculates the sum of numbers from 1 to n. After the loop completes, it prints out the calculated sum. And check if the sum s is even or odd using the modulus operator (%). If the remainder when s is divided by 2 is 0, then the sum is even otherwise odd.

[Program 4.2: Display odd numbers](#contents.xhtml_sc2_468a)

Display odd numbers between the range n and m where n and m are inclusive.

[Sample input output](#contents.xhtml_sc3_469a)

Test case #1:

Input: Enter two numbers: 2 6

Output: 3 5

Test case #2:

Input: Enter two numbers: 2 19

Output: 3 5 7 9 11 13 15 17 19

[Algorithm](#contents.xhtml_sc3_470a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read n,m
3.  i=n
4.  Repeat if i<=m
5.  if i%2 !=0
6.  print i
7.  i=i+1
8.  Stop

[Flowchart](#contents.xhtml_sc3_471a)

[Figure 4.2](#ch04.xhtml_fig4-2) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.2.jpg)

Figure 4.2: Flowchart illustrating the program 4.2

[Python code](#contents.xhtml_sc3_472a)

Python code for the program is as follows:

1.  n=int(input("Enter n: "))
2.  m=int(input("Enter m: "))
3.  for i in range(n,m+1):
4.  if(i%2 !=0):
5.  print(i)

[Python code explanation](#contents.xhtml_sc4_473a)

This Python code takes two input integers, n and m, then iterates through the range of numbers from n to m, printing each odd number in that range. Here is what each part of the code does:

First, it takes two numbers, n and m, as input to set the range. In the for-loop, it iterates through the range of numbers from n to m (inclusive of m). The range() function returns a sequence of numbers starting from n till m, incrementing by 1. The variable i takes each value in this range during each iteration and is checked if the current value of i is not divisible by 2 (odd) using the modulus operator %. If the remainder is not 0, that means i is odd, and it prints the value of i if odd. The loop continues until the range is exhausted, and the program displays all odd numbers between n and m.

[C code](#contents.xhtml_sc3_474a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, n, m;
5.  printf("Enter two numbers: " );
6.  scanf("%d%d", &n, &m);
7.  i=n;
8.  while(i<=m)
9.  {
10.  if (i%2 !=0)
11.  { printf("%d ", i); }
12.  i=i+1;
13.  }
14.  }

[C code explanation](#contents.xhtml_sc3_475a)

This C code prompts the user for two input numbers, n and m. Variable I is the loop invariant, which is initialized with n. It then uses a while loop to iterate through the range of numbers from n to m. Within the loop, it checks if each number is odd using the condition i% 2 != 0. If the number is odd, it is printed. The loop continues until the range is exhausted, and the program displays all odd numbers between n and m.

[Program 4.3: Count number of even numbers](#contents.xhtml_sc2_476a)

Ask the user to enter n numbers and count how many are even.

[Sample input output](#contents.xhtml_sc3_477a)

Test case #1:

Input: Enter a number: 6

Enter six numbers: 3 4 8 7 6 5

Output: There are 3 even numbers

Test case #2:

Input: Enter a number: 5

Enter five numbers:2 2 2 2 2

Output: There are 5 even numbers

[Algorithm](#contents.xhtml_sc3_478a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  declare the variables as n, x
3.  read value of n
4.  c=0,i=1
5.  if i<=n
6.  x=read("Enter number")
7.  if (x%2==0)
8.  c=c+1
9.  i=i+1
10.  repeat step 5
11.  print("There are ", c , " even numbers")
12.  Stop

[Flowchart](#contents.xhtml_sc3_479a)

[Figure 4.3](#ch04.xhtml_fig4-3) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.3.jpg)

Figure 4.3: Flowchart illustrating the program 4.3

[Python code](#contents.xhtml_sc3_480a)

Python code for the program is as follows:

1.  n=int(input("Enter n: "))
2.  c=0
3.  for i in range(1, n+1):
4.  x=int(input("Enter x:"))
5.  if(x%2 == 0):
6.  c=c+1
7.  print("There are ", c , " even numbers") 

[Python code explanation](#contents.xhtml_sc4_481a)

The Python code takes an input integer n. Then, it prompts the user to enter n numbers one by one. For each entered number, if it is even, the code increments the count c. Finally, it prints the total count of even numbers entered.

It prompts the user to input an integer n and stores it in the variable n. The variable cis initialized to 0 to count the number of even numbers entered. The for loop iterates through the range of numbers from 1 to n (inclusive of n). The user is prompted to input the number x for n times. After each input, the current value of x is checked to see if it is even by evaluating the condition x % 2 == 0. If the entered value is even, the count c is incremented by 1. After the loop completes, it prints the count of even numbers.

[C code](#contents.xhtml_sc3_482a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, n, x;
5.  int c=0;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);
8.  printf("Enter %d numbers:", n);
9.  for(i =1; i<=n; i++)
10.  {
11.  scanf("%d", &x);
12.  if(x%2==0)
13.  c=c+1;
14.  }

16.  printf("There are %d even numbers", c);

18.  }

[C code explanation](#contents.xhtml_sc4_483a)

The C code takes an input integer n, then it prompts the user to enter n numbers one by one. For each entered number, if it is even, the code increments the count c. Finally, it prints the total count of even numbers entered.

The variable c is initialized to 0 to count the number of even numbers entered. It prompts the user to input an integer n and stores it in the variable n. The for loop iterates through the range of numbers from 1 to n (inclusive of n). The user is prompted to input the number x for n times. After each input, the current value of x is checked to see if it is even by evaluating the condition x % 2 == 0. If the entered value is even, the count c is incremented by 1. After the loop completes, it prints the count of even numbers.

[Program 4.4: Find sum of even numbers](#contents.xhtml_sc2_484a)

Display the sum of the first ten even terms of natural numbers.

[Sample input output](#contents.xhtml_sc3_485a)

Test case #1:

Output: The sum is 110

[Algorithm](#contents.xhtml_sc3_486a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare the variable as i,n,s
3.  i=1,s=0,n=20
4.  Repeat if i<=n
5.  If i%2==0
6.  s = s + i
7.  i=i+1
8.  Display s
9.  Stop

[Flowchart](#contents.xhtml_sc3_487a)

[Figure 4.4](#ch04.xhtml_fig4-4) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.4.jpg)

Figure 4.4: Flowchart illustrating the program 4.4

[Python code](#contents.xhtml_sc3_488a)

Python code for the program is as follows:

1.  s=0
2.  for i in range(1,21):
3.  if(i%2==0):
4.  s = s+ i
5.  print("sum is ",s)

[Python code explanation](#contents.xhtml_sc4_489a)

The Python code calculates the sum of even numbers from 1 to 20 and then prints the sum. The loop iterates through the numbers and the condition i % 2 == 0 is used to select even numbers for summation.

[C code](#contents.xhtml_sc3_490a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, n;
5.  int s=0;
6.  n=20;
7.  i=1;
8.  while(i<=n)
9.  {
10.  if (i%2==0)
11.  { s=s+i; }
12.  i=i+1;
13.  }
14.  printf("The sum is %d", s);
15.  }

[C code explanation](#contents.xhtml_sc4_491a)

The C code calculates the sum of even numbers from 1 to 20 using a while loop and then prints the sum. The loop iterates through the numbers and the condition i % 2 == 0 is used to select even numbers for summation.

[Program 4.5: Find sum of numbers divisble by 9](#contents.xhtml_sc2_492a)

Display the sum of all integers between 100 and 200,divisible by 9.

[Sample input output](#contents.xhtml_sc3_493a)

Test case #1:

Output: Sum is 1683

[Algorithm](#contents.xhtml_sc3_494a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare the variable as i,n,s
3.  i=100,s=0,n=200
4.  Repeat if i<=n
5.  If i%9==0
6.  s = s + i
7.  i=i+1
8.  Display s
9.  Stop

[Flowchart](#contents.xhtml_sc3_495a)

[Figure 4.5](#ch04.xhtml_fig4-5) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.5.jpg)

Figure 4.5: Flowchart illustrating the program 4.5

[Python code](#contents.xhtml_sc3_496a)

Python code for the program is as follows:

1.  s=0
2.  for i in range(100,201):
3.  if(i%9==0):
4.  s = s+ i
5.  print("sum is ",s)

[Python code explanation](#contents.xhtml_sc4_497a)

The Python code calculates the sum of numbers between 100 and 200 divisible by 9 and then prints the sum. The loop iterates through the range and the condition i % 9 == 0 is used to select numbers for summation. The variable s is used to accumulate the sum of numbers. Inside the loop, in every iteration, if the number i is divisible by 9, the value of s is updated by adding the value of i to it. After the loop completes, it prints the accumulated sum of numbers.

[C code](#contents.xhtml_sc3_498a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i=100;
5.  int s=0;
6.  while(i <=200)
7.  {
8.  if (i%9 ==0)
9.  {s=s+i;}
10.  i=i+1;
11.  }
12.  printf("Sum is %d", s);
13.  }

[C code explanation](#contents.xhtml_sc4_499a)

The C code calculates the sum of numbers between 100 and 200 divisible by 9 and then prints the sum. The loop iterates through the range, and the condition i % 9 == 0 is used to select numbers for summation. The variable s is used to accumulate the sum of numbers. Inside the loop, in every iteration, if the number i is divisible by 9, the value of s is updated by adding the value of i to it. After the loop completes, it prints the accumulated sum of numbers.

[Program 4.6: Difference of sum of even and odd numbers](#contents.xhtml_sc2_500a)

Find the difference between the sum of all even and odd numbers in the first 50 natural numbers.

[Sample input output](#contents.xhtml_sc3_501a)

Test case #1:

Output: Difference is 25

[Algorithm](#contents.xhtml_sc3_502a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  n=50
3.  i=1
4.  sumE=0, sumO=0
5.  repeat if i<=n
6.  if i%2==0
7.  sumE=sumE+i
8.  else
9.  sumO=sumO+i
10.  i=i+1
11.  d = sumE-sumO
12.  Display d
13.  Stop

[Flowchart](#contents.xhtml_sc3_503a)

[Figure 4.6](#ch04.xhtml_fig4-6) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.6.jpg)

Figure 4.6: Flowchart illustrating the program 4.6

[Python code](#contents.xhtml_sc3_504a)

Python code for the program is as follows:

1.  sumE=0
2.  sumO=0
3.  n=50
4.  for i in range(1,n+1):
5.  if(i%2==0):
6.  sumE = sumE + i
7.  else:
8.  sumO = sumO + i
9.  print("Difference is ",sumE-sumO)

[Python code explanation](#contents.xhtml_sc4_505a)

The Python code calculates the sum of all even numbers from 1 to 50 and stores it in the variable sumE. Similarly, it calculates the sum of all odd numbers from 1 to 50 and stores it in the variable sumO. Finally, it displays the difference between the sum of even numbers and the sum of odd numbers.

[C code](#contents.xhtml_sc3_506a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, n=50;
5.  int sumE=0;
6.  int sumO=0;
7.  i=1;
8.  while(i<=n)
9.  {
10.  if (i%2==0)
11.  { sumE=sumE+i; }
12.  else
13.  { sumO=sumO+i; }
14.  i=i+1;
15.  }
16.  printf("Difference is %d ", sumE-sumO);
17.  }

[C code explanation](#contents.xhtml_sc4_507a)

The C code calculates the sum of all even numbers from 1 to 50 and stores it in the variable sumE. Similarly, it calculates the sum of all odd numbers from 1 to 50 and stores it in the variable sumO. Finally, it displays the difference between the sum of even numbers and the sum of odd numbers.

[Program 4.7: Display list of divisor](#contents.xhtml_sc2_508a)

Ask the user for a number and then display a list of all the factors of that number in increasing order.

Hint: Factor means the number that can divide another number completely.

[Sample input output](#contents.xhtml_sc3_509a)

Test case #1:

Input: Enter a number 10

Output: 1 2 5 10

Test case #2:

Input: Enter a number 254

Output: 1 2 127 254

[Algorithm](#contents.xhtml_sc3_510a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare variables i, n
3.  Read n
4.  i=1
5.  while i<=n:
6.  if n%i==0
7.  print i
8.  Stop

[Flowchart](#contents.xhtml_sc3_511a)

[Figure 4.7](#ch04.xhtml_fig4-7) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.7.jpg)

Figure 4.7: Flowchart illustrating the program 4.7

[Python code](#contents.xhtml_sc3_512a)

Python code for the program is as follows:

1.  n=int(input("Enter a number "))
2.  for i in range(1,n+1):
3.  if n%i==0:
4.  print(i) 

[Python code explanation](#contents.xhtml_sc4_513a)

The Python code takes an input number n, then prints all the positive divisors (factors) of n by iterating through the numbers from 1 to n and checking if they divide n.

First, it prompts the user to input a number and stores it in the variable n. Then, it checks if the current value of n is divisible by the value of i, by evaluating the condition n % i == 0. If the condition is true (meaning n is divisible by i and i is a factor of n), it prints the value i.

[C code](#contents.xhtml_sc3_514a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  int n, i;
5.  printf("Enter a number ");
6.  scanf("%d", &n);
7.  for (i=1; i<=n;i++)
8.  {
9.  if( n%i==0)
10.  printf("%d ", i) ;
11.  }}

[C code explanation](#contents.xhtml_sc4_515a)

The C code takes an input number n, then prints all the positive divisors (factors) of n by iterating through the numbers from 1 to n and checking if they divide n.

First, it prompts the user to input a number and stores it in the variable n. Then, it checks if the current value of n is divisible by the value of i, by evaluating the condition n % i == 0. If the condition is true (meaning n is divisible by i and i is a factor of n), it prints the value i.

[Program 4.8: Find max 1](#contents.xhtml_sc2_516a)

Find the max of the given five numbers.

[Sample input output](#contents.xhtml_sc3_517a)

Test case #1:

Input: Enter 5 numbers: 98 78 990 65 32

Output: The maximum number is 990

Test case #2:

Input: Enter 5 numbers: 23 34 45 56 78

Output: The maximum number is 78

[Algorithm](#contents.xhtml_sc3_518a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  declare the variables as x
3.  n =5
4.  i=1, max_no=0
5.  if i<=n
    1.  x=read("Enter number", i)
    2.  if (x >max_no)
    3.  max_no = x
    4.  i=i+1
    5.  repeat step 5
6.  print("The maximum number is ", max_no)
7.  Stop

[Flowchart](#contents.xhtml_sc3_519a)

[Figure 4.8](#ch04.xhtml_fig4-8) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.8.jpg)

Figure 4.8: Flowchart illustrating the program 4.8

[Python code](#contents.xhtml_sc3_520a)

Python code for the program is as follows:

1.  max_no=0
2.  n=5
3.  for i in range(1, n+1):
4.  x=int(input("Enter x:"))
5.  if (x > max_no):
6.  max_no = x
7.  print("The maximum number is ", max_no) 

[Python code explanation](#contents.xhtml_sc4_521a)

The Python code prompts the user to input 5 numbers one by one. Initially, a variable max_no is initialized to 0. This variable will keep track of the maximum number entered.

For each entered number, if it is greater than the current maximum (max_no), the code updates the maximum number. Finally, it prints the maximum number among the input numbers.

[C code](#contents.xhtml_sc3_522a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, x;
5.  int max_no=0;
6.  int n=5;
7.  printf("Enter 5 numbers: ");
8.  for(i =1; i<=n; i++)
9.  {
10.  scanf("%d", &x);
11.  if (x > max_no)
12.  max_no = x;
13.  }
14.  printf("The maximum number is %d", max_no );
15.  }

[C code explanation](#contents.xhtml_sc4_523a)

The C code prompts the user to input 5 numbers one by one. Initially, a variable max_no is initialized to 0. This variable will keep track of the maximum number entered.

For each entered number, if it is greater than the current maximum (max_no), the code updates the maximum number. Finally, it prints the maximum number among the input numbers.

[Program 4.9: Find max 2](#contents.xhtml_sc2_524a)

Find the max of n numbers as entered by the user.

[Sample input output](#contents.xhtml_sc3_525a)

Test case #1:

Input: Enter a number: 8

Enter 8 numbers: 3 2 1 7 6 5 4 3

Output: The maximum number is 7

[Algorithm](#contents.xhtml_sc3_526a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  declare the variables as x
3.  read value of n
4.  i=1, max_no=0
5.  if i<=n
    1.  x=read("Enter number", i)
    2.  if (x >max_no)
    3.  max_no = x
    4.  i=i+1
    5.  repeat step 5
6.  print("The maximum number is ", max_no)
7.  Stop

[Flowchart](#contents.xhtml_sc3_527a)

[Figure 4.9](#ch04.xhtml_fig4-9) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.9.jpg)

Figure 4.9: Flowchart illustrating the program 4.9

[Python code](#contents.xhtml_sc3_528a)

Python code for the program is as follows:

1.  max_no=0
2.  n=int(input("Enter n:"))
3.  for i in range(1, n+1):
4.  x=int(input("Enter x:"))
5.  if (x > max_no):
6.  max_no = x
7.  print("The maximum number is ", max_no) 

[Python code explanation](#contents.xhtml_sc4_529a)

This program is an extended version of the previous one. Here, it prompts the user to input n numbers one by one. Initially, a variable max_no is initialized to 0. This variable will keep track of the maximum number entered.

For each entered number, if it is greater than the current maximum (max_no), the code updates the maximum number. Finally, it prints the maximum number among the input numbers.

[C code](#contents.xhtml_sc3_530a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, n, x;
5.  int max_no=0;
6.  printf("Enter a numbers: " );
7.  scanf("%d", &n);
8.  printf("Enter %d numbers: ", n );
9.  for(i =1; i<=n; i++)
10.  {
11.  scanf("%d", &x);
12.  if (x > max_no)
13.  max_no = x;
14.  }
15.  printf("The maximum number is %d", max_no );

17.  }

[C code explanation](#contents.xhtml_sc4_531a)

This program is an extended version of the previous one. Here, it prompts the user to input n numbers one by one. Initially, a variable max_no is initialized to 0. This variable will keep track of the maximum number entered.

For each entered number, if it is greater than the current maximum (max_no), the code updates the maximum number. Finally, it prints the maximum number among the input numbers.

[Program 4.10: Count number of consonants](#contents.xhtml_sc2_532a)

Count the number of consonants in a string. If the consonant appears twice, the count is 2.

Hint: In the English alphabet, there are five vowels: a, e, i, o, u, and all others are consonants.

[Sample input output](#contents.xhtml_sc3_533a)

Test case #1:

Input: Enter a string: codefactory

Output: There are 7 consonants in the string.

Test case #2:

Input: Enter a string: programming

Output: There are 8 consonants in the string.

[Algorithm](#contents.xhtml_sc3_534a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare the variables as s, i, v
3.  Read a string as s
4.  i=0, v=0
5.  if s[i] != "\0" and (ord(s[i]) in range(65,91) or ord(s[i]) in range(97, 123))
    1.  if s[i] != ‘a’ AND s[i] != ‘e’ AND s[i] != ‘i’ AND s[i] != ‘o’ AND s[i] != ‘u’
        1.  v=v+1
    2.  i=i+1
    3.  repeat Step 5
6.  Print ("There are ", v, " consonants in the string.")
7.  Stop

[Flowchart](#contents.xhtml_sc3_535a)

[Figure 4.10](#ch04.xhtml_fig4-10) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.10.jpg)

Figure 4.10: Flowchart illustrating the program 4.10

[Python code](#contents.xhtml_sc3_536a)

Python code for the program is as follows:

1.  s= input("Enter a string: ")
2.  v=0
3.  for i in s:
4.  if ord(i) in range(65,91) or ord(i) in range(97,123):
5.  if(i != ‘a’ and i != ‘e’ and i != ‘i’ and i != ‘o’ and i != ‘u’):
6.  v=v+1
7.  else:
8.  print("Special character encountered. ")
9.  break
10.  print ("There are ", v, "consonants in the string.")

[Python code explanation](#contents.xhtml_sc4_537a)

The main logic behind counting the number of consonants is to count the number of characters that are not vowels. First, it prompts the user to input a string and stores the input in the variable s. It initializes a variable v to 0. This variable will count the number of consonants in the input string. The for-loop iterates through each character in the string s. First, it checks if the entered characters are valid English characters using the ASCII value of each character using the ord() function. The ACSII value of uppercase characters lies between [65 and 90] and [97 and 122] for lowercase characters. Then, it checks if the current character i is not equal to any vowels a, e, i, o, and u. If the condition is true (i is a consonant), the count v is incremented by 1. After the loop completes, this line prints the count of consonants in the input string.

[C code](#contents.xhtml_sc3_538a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int i, v=0;
5.  char s[30];
6.  printf("Enter a string: ");
7.  gets(s);
8.  i=0;
9.  while(s[i] != ‘\0’){
10.  if ((((int)(s[i]) >=65) && ((int)(s[i]) <=90)) || (((int)(s[i]) >=97) && ((int)(s[i]) <=122)))
11.  {
12.  if (s[i] != ‘a’ && s[i] != ‘e’ && s[i] != ‘i’ && s[i] != ‘o’ && s[i] != ‘u’)
13.  {v=v+1;}
14.  i=i+1;
15.  }
16.  }
17.  else{
18.  printf("Special character encountered.\n");
19.  break;
20.  }
21.  printf("There are %d consonants in the string.", v);
22.  }

[C code explanation](#contents.xhtml_sc4_539a)

This code is a simple C program that counts the number of consonants in a given input string.

An array, s[30] of character type, is declared to store the input string provided by the user. Then, it reads the text (string) from the user using the gets() function and stores it in the s array. It initializes a variable v to 0. This variable will count the number of consonants in the input string. The while-loop iterates through each character in the string s. The loop will continue if the current character in the string s is not the null character (\0), which marks the end of a C-style string. First, it checks if the entered characters are valid English characters using the ASCII value of each character. The ACSII value of uppercase characters lies between [65 and 90] and [97 and 122] for lowercase characters. Then, it checks if the current character, s[i], at index i is not equal to any vowels a, e, i, o, and u. If the condition is true (s[i] is a consonant), the count v is incremented by 1. After the loop completes, this line prints the count of consonants in the input string.

[Program 4.11: Check if a number is prime](#contents.xhtml_sc2_540a)

Check whether a given number is a prime number or not.

Hint: A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself.

[Sample input output](#contents.xhtml_sc3_541a)

Test case #1:

Input: Enter a number: 6

Output: 6 is not a prime number

Test case #2:

Input: Enter a number: 127

Output: 127 is a prime number

[Algorithm](#contents.xhtml_sc3_542a)

To run the above program, the following are s are needed to be followed:

1.  Start
2.  Declare the variable n, i, flag
3.  Read n
4.  flag =0
5.  i=2
6.  if n==1
    1.  print("it is neither prime or composite.")
    2.  exit
7.  Repeat till i<n
    1.  if(n%i==0):
        1.  flag =1
        2.  print(n, "is not a prime number")
        3.  break
    2.  i=i+1
8.  if flag==0:
    1.  print(n, "is a prime number")
9.  Stop

[Flowchart](#contents.xhtml_sc3_543a)

[Figure 4.11](#ch04.xhtml_fig4-11) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.11.jpg)

Figure 4.11: Flowchart illustrating the program 4.11

[Python code](#contents.xhtml_sc3_544a)

Python code for the program is as follows:

1.  n=int(input("Enter a number: "))
2.  if n==1:
3.  print("it is neither prime or composite")
4.  exit(1)
5.  flag =0
6.  for i in range(2,n):
7.  if(n%i==0):
8.  flag =1
9.  break
10.  if flag==0:
11.  print(n, "is a prime number")
12.  else:
13.  print(n, "is not a prime number")

[Python code explanation](#contents.xhtml_sc4_545a)

This code is a Python program that checks whether a given input number is prime. It prompts the user to input a number and stores it as an integer in the variable n. The variable flag is initialized to 0. This variable indicates whether the input number is prime or not. The for-loop iterates through the numbers from 2 to n-1. The loop variable i takes on values from 2 to the input number n. Then, it checks if the input number n is divisible evenly by the current value of i. If the condition is satisfied (n is divisible by i and has a factor), the flag variable is set to 1, indicating that the number is not prime. break statement is used to terminate the loop if n is found to be divisible by any value of i, then it is already not a prime number. There is no need to continue checking further. If, after the loop, the value of the flag is still 0, it means the loop is completed without finding any divisors for n, indicating that the number is prime. So, it prints that n is a prime number. If the flag value is 1,n is divisible by at least one number other than 1 and the number itself. Hence, it prints that n is not a prime number).

[C code](#contents.xhtml_sc3_546a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int n, flag,i;
5.  printf("Enter a number: ");
6.  scanf("%d", &n);
7.  if (n==1)
8.  {
9.  printf("it is neither prime or composite");
10.  exit(1);
11.  }
12.  flag =0;
13.  for (i=2; i<n;i++)
14.  {
15.  if(n%i==0)
16.  {
17.  flag =1;
18.  break;
19.  }
20.  }
21.  if (flag==0)
22.  printf( "%d is a prime number", n);
23.  else
24.  printf("%d is not a prime number", n);
25.  }

[C code explanation](#contents.xhtml_sc4_547a)

This code is a Python program that checks whether a given input number is prime. It prompts the user to input a number and stores it as an integer in the variable n. The variable flag is initialized to 0. This variable indicates whether the input number is prime or not. The for-loop iterates through the numbers from 2 to n-1. The loop variable i takes on values from 2 to the input number n. Then, it checks if the input number n is divisible evenly by the current value of i. If the condition is satisfied (n is divisible by i and has a factor), the flag variable is set to 1, indicating that the number is not prime. break statement is used to terminate the loop if n is found to be divisible by any value of i, then it is already not a prime number. There is no need to continue checking further. If, after the loop, the value of flag is still 0, it means the loop is completed without finding any divisors for n, indicating that the number is prime. So, it prints that n is a prime number. If the flag value is 1 that means n is divisible by at least one number other than 1 and the number itself. Hence, it prints that n is not a prime number).

[Program 4.12: Find LCM](#contents.xhtml_sc2_548a)

Find the LCM of given numbers X and Y.

[Sample input output](#contents.xhtml_sc3_549a)

Test case #1:

Input: Enter 2 numbers: 45 100

Output: LCM is 900

Test case #2:

Input: Enter 2 numbers: 76 33

Output: LCM is 2508

[Algorithm](#contents.xhtml_sc3_550a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare variables as n,m, lcm,i
3.  Read n, m
4.  lcm=1
5.  for i = min(n,m) to 1:
    1.  if n>=i and m >=i:
        1.  if n%i ==0 and m%i == 0:
            1.  n=n/i
            2.  m=m/i
            3.  lcm=lcm*i
    2.  else:
        1.  break
6.  if n!=0:
    1.  lcm = lcm*n
7.  if m!=0:
    1.  lcm = lcm*m
8.  print(lcm)
9.  Stop

[Flowchart](#contents.xhtml_sc3_551a)

[Figure 4.12](#ch04.xhtml_fig4-12) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.12.jpg)

Figure 4.12: Flowchart illustrating the program 4.12

[Python code](#contents.xhtml_sc3_552a)

Python code for the program is as follows:

1.  n=int(input("Enter 1st number: "))
2.  m=int(input("Enter 2nd number: "))
3.  lcm=1
4.  for i in range(min(n,m),1, -1):
5.  if n>=i and m >=i:
6.  if n%i ==0 and m%i == 0:
7.  n=n/i
8.  m=m/i
9.  lcm=lcm*i
10.  else:
11.  break
12.  if n!=0:
13.  lcm = lcm*n
14.  if m!=0:
15.  lcm = lcm*m
16.  print(lcm)

[Python code explanation](#contents.xhtml_sc4_553a)

The logic behind finding LCM is to find the common factors of both the numbers: n, m. Divide n and m by the common factor and then multiply the common factor with the remaining values of n and m to obtain LCM.

It prompts the user to input two numbers and store them in the variables n and m. It initializes a variable lcm to 1 to store the least common multiple (LCM) of the two input numbers. The for-loop iterates backward from the minimum of n and m down to 1.min() if a function in Python returns a minimum of two. Keyword and is used to ensure the true value for both conditions. It checks if both n and m are greater than or equal to i. If yes, it checks if the current i is a common factor of n and m. If this condition is also true, then update the value of n by n/i and m by m/i. It updates the lcm by multiplying it with i, which is a common factor. As i becomes greater than n or m, it indicates that no more common factors can be obtained, so a break statement is used to come out of the loop. Then, it multiplies lcm by the remaining value of n and m. Finally, it prints the calculated least common multiple (lcm) of the two.

[C code](#contents.xhtml_sc3_554a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  #include<math.h>
3.  #define min(n,m) n<m?n:m
4.  void main()
5.  {
6.  int n,m,lcm,i;
7.  printf("Enter 2 numbers: ");
8.  scanf("%d%d", &n, &m);
9.  lcm=1;
10.  for (i=min(n,m); i>1; i--)
11.  {
12.  if (n>=i  && m >=i)
13.  {
14.  if (n%i ==0 && m%i == 0)
15.  {n=n/i;
16.  m=m/i;
17.  lcm=lcm*i;
18.  }
19.  }
20.  else
21.  break;
22.  }
23.  if (n!=0)
24.  lcm = lcm*n;
25.  if (m!=0)
26.  lcm = lcm*m;
27.  printf("LCM is %d", lcm);
28.  }

[C code explanation](#contents.xhtml_sc4_555a)

The logic behind finding LCM is to find the common factors of both the numbers: n, m. Divide n and m by the common factor and then multiply the common factor with the remaining values of n and m to obtain LCM.

It prompts the user to input two numbers and store them in the variables n and m. It initializes a variable lcm to 1 to store the LCM of the two input numbers. The for-loop iterates backward from the minimum of n and m down to 1. In C, min is not a predefined function. So, a preprocessor directive, #define, is used to define the function. #define min(n,m) n<m?n:m: This line defines a macro named min that takes two arguments: n and m. It uses the ternary conditional operator (? :)to create a shorthand if-else statement. The purpose of this macro is to find the minimum of the two values n and m. The ternary conditional expression (n<m?n:m)checks if the condition n < m is true. If it is true, the expression evaluates to n. Otherwise, it evaluates to m.

Further, && is used to ensure the true value for both conditions. It checks if both n and m are greater than or equal to i. If yes, it checks if the current i is a common factor of n and m. If this condition is also true, then update the value of n by n/i and m by m/i. It updates the lcm by multiplying it with i, which is a common factor. As i becomes greater than n or m, it indicates that no more common factors can be obtained, so a break statement is used to come out of the loop. Then, it multiplies lcm by the remaining value of n and m. Finally, it prints the calculated least common multiple (lcm) of the two.

[Program 4.13: Find HCF](#contents.xhtml_sc2_556a)

Find the HCF of given numbers X and Y.

[Sample input output](#contents.xhtml_sc3_557a)

Test case #1:

Input: Enter 2 numbers: 15 3

Output: HCF is 3

Test case #2:

Input: Enter 2 numbers: 65 52

Output: HCF is 13

[Algorithm](#contents.xhtml_sc3_558a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare variables as n, m, hcf,i
3.  Read n, m
4.  hcf=1
5.  for i = min(n,m) to 2:
    1.  if n>=i and m >=i:
        1.  if n%i ==0 and m%i == 0:
            1.  n=n/i
            2.  m=m/i
            3.  hcf=hcf*i
    2.  else:
        1.  break
6.  Print(hcf)
7.  Stop

[Flowchart](#contents.xhtml_sc3_559a)

[Figure 4.13](#ch04.xhtml_fig4-13) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.13.jpg)

Figure 4.13: Flowchart illustrating the program 4.13

[Python code](#contents.xhtml_sc3_560a)

Python code for the program is as follows:

1.  n=int(input("Enter 1st number: "))
2.  m=int(input("Enter 2nd number: "))
3.  hcf=1
4.  for i in range(min(n,m), 1, -1):
5.  if n>=i and m >=i:
6.  if n%i ==0 and m%i == 0:
7.  n=n/i
8.  m=m/i
9.  hcf=hcf*i
10.  else:
11.  break
12.  print(hcf)

[Python code explanation](#contents.xhtml_sc4_561a)

The Python program calculates the highest common factor (HCF), also known as the greatest common divisor (GCD), of two given input numbers n and m. The logic and program are the same as those used in the previous program for finding LCM.

[C code](#contents.xhtml_sc3_562a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  #define min(n,m) n<m?n:m

4.  void main()
5.  {
6.  int n,m,hcf,i;
7.  printf("Enter 2 numbers: ");
8.  scanf("%d%d", &n, &m);
9.  hcf=1;
10.  for (i=min(n,m); i>1; i--)
11.  {
12.  if (n>=i  && m >=i)
13.  {
14.  if (n%i ==0 && m%i == 0)
15.  {
16.  n=n/i;
17.  m=m/i;
18.  hcf=hcf*i;
19.  }
20.  }
21.  else
22.  break;
23.  }
24.  printf("HCF is %d", hcf);
25.  }

[C code explanation](#contents.xhtml_sc4_563a)

The C program calculates the HCF, also known as GCD, of two given input numbers n and m. The logic and program are the same as those used in the previous program for finding LCM.

[Program 4.14: Search a number](#contents.xhtml_sc2_564a)

Search for an element in a list.

[Sample input output](#contents.xhtml_sc3_565a)

Test case #1:

Input: Enter the size of the list: 10

Enter the elements of the list:1 2 3 4 5 6 7 8 9 8

Enter the element to be searched: 10

Output: 10 is not present in the list.

Test case #2:

Input: Enter the size of the list: 5

Enter the elements of the list:

23 45 21 87 44

Enter the element to be searched: 87

Output: 87 is present at position 4 in the list.

[Algorithm](#contents.xhtml_sc3_566a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare n, a, flag, x, el
3.  Read the size of the list as n
4.  Initialize a as empty, a=[]
5.  flag=0
6.  for i =0 to n-1
    1.  Read element as el
    2.  Append el to a
7.  Read the element to be searched as x
8.  for i = 0 to n-1
    1.  if (a[i] == x)
        1.  flag = 1
        2.  break
9.  if (flag == 1)
    1.  Display number to be searched is present
10.  else
    1.  Display number to be searched is not present
11.  Stop

[Flowchart](#contents.xhtml_sc3_567a)

[Figure 4.14](#ch04.xhtml_fig4-14) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.14.jpg)

Figure 4.14: Flowchart illustrating the program 4.14

[Python code](#contents.xhtml_sc3_568a)

Python code for the program is as follows:

1.  n=int(input("Enter the size of the list: "))
2.  print("Enter the elements of the list:\n");
3.  a=[]
4.  flag=0
5.  for i in range(0, n):
6.  el=int(input("Enter :"))
7.  a.append(el)

9.  x=int(input("Enter the element to be searched: "))

11.  for i in range(0, n):
12.  if (a[i] == x):
13.  flag = 1
14.  break
15.  if (flag == 1):
16.  print(a[i]," is present at position ",i+1, " in the list")
17.  else:
18.  print(a[i]," is not present in the list")

[Python code explanation](#contents.xhtml_sc4_569a)

The Python code takes the size and elements of a list as input from the user. Here, a is a list that can store n number of elements in it. Initially, an empty list is created (a=[]).append() function is used to add elements to the list. It then prompts the user to input an element to search for. It initializes a flag variable flag to 0 to indicate whether the searched element is found or not. The code iterates through the list to determine if the searched element is present. Inside the loop, it checks if the current element in the list a at index i is equal to the element being searched for (x). If the condition is true, it sets the flag variable to 1, indicating that the element is found and breaks out of the loop since there is no need to continue searching. Outside the loop, if a flag is equal to 1, it prints the found element a[i] and its position in the list i+1. Otherwise, it indicates that it is not present in the list.

[C code](#contents.xhtml_sc3_570a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n, i, x, flag = 0;
4.  printf("Enter the size of the list: ");
5.  scanf("%d", &n);
6.  int a[n];
7.  printf("Enter the elements of the list:\n");
8.  for (i = 0; i < n; i++) {
9.  scanf("%d", &a[i]);
10.  }
11.  printf("Enter the element to be searched: ");
12.  scanf("%d", &x);
13.  for (i = 0; i < n; i++) {
14.  if (a[i] == x) {
15.  flag = 1;
16.  break;
17.  }
18.  }
19.  if (flag == 1) {
20.  printf("%d is present at position %d in the list.\n", x, i+1);
21.  }
22.  else {
23.  printf("%d is not present in the list.\n", x);
24.  }
25.  return 0;
26.  }

[C code explanation](#contents.xhtml_sc4_571a)

In this program, the user first inputs the size of the list and then enters the elements of the list. Here, a is an integer-type array used to store n elements. The user also inputs the element to be searched. The program then uses a for-loop to search for the element in the list. If the element is found, the program sets a flag variable to 1 and breaks out of the loop. If the element is not found, the flag variable remains 0. Finally, the program checks the value of the flag variable and prints the appropriate message.

[Program 4.15: Handling list/ arrays](#contents.xhtml_sc2_572a)

Given two integer lists, create a third list such that it has only odd numbers from the first list and even numbers from the second list.

[Sample input output](#contents.xhtml_sc3_573a)

Test case #1:

Input: List 1: 1 2 3 5 70 11 13

List 2: 21 42 63 82 10

Output: List 3: 1 3 5 11 13 42 82 10

Test Case #1:

Input: List 1: 11 12 13 14 15

List2 = 16 17 18 19 20

Output: List 3 = 11 13 15 16 18 20

[Algorithm](#contents.xhtml_sc3_574a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Initialize list1 = [1, 3, 5, 7, 9]
3.  Initialize list2 = [2, 4, 6, 8, 10]
4.  Create empty list, result_list = []
5.  for each element (num) of the list1:
    1.  if num % 2 != 0:
    2.  append to result_list
6.  for each element (num) of the list2:
    1.  if num % 2 == 0:
    2.  append to result_list
7.  Display result_list
8.  Stop

[Flowchart](#contents.xhtml_sc3_575a)

[Figure 4.15](#ch04.xhtml_fig4-15) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.15.jpg)

Figure 4.15: Flowchart illustrating the program 4.15

[Python code](#contents.xhtml_sc3_576a)

Python code for the program is as follows:

1.  list1 = [1, 3, 5, 7, 9]
2.  list2 = [2, 4, 6, 8, 10]
3.  result_list = []
4.  for num in list1:
5.  if num % 2 != 0:
6.  result_list.append(num)

8.  for num in list2:
9.  if num % 2 == 0:
10.  result_list.append(num)
11.  print(result_list)

[Python code explanation](#contents.xhtml_sc4_577a)

The Python code creates two lists list1 and list2, containing some numbers. It then initializes an empty list result_list and uses loops to iterate through both list1 and list2, appending odd numbers from list1 and even numbers from list2 to the result_list. Finally, it prints the combined result list.

[C code](#contents.xhtml_sc3_578a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main()
3.  {
4.  int list1[] = {1, 2, 3, 5, 70,11,13};
5.  int list2[] = {21, 42, 63, 82, 10};
6.  int size1 = sizeof(list1) / sizeof(list1[0]);
7.  int size2 = sizeof(list2) / sizeof(list2[0]);
8.  int list3[size1 + size2];
9.  int index = 0;

11.  for(int i = 0; i < size1; i++)
12.  {
13.  if(list1[i] % 2 != 0)
14.  {
15.  list3[index] = list1[i];
16.  index++;
17.  }
18.  }

20.  for(int j = 0; j < size2; j++)
21.  {
22.  if(list2[j] % 2 == 0)
23.  {
24.  list3[index] = list2[j];
25.  index++;
26.  }
27.  }
28.  printf("List 1: ");
29.  for(int i = 0; i < size1; i++)
30.  {
31.  printf("%d ", list1[i]);
32.  }
33.  printf("\nList 2: ");
34.  for(int i = 0; i < size2; i++)
35.  {
36.  printf("%d ", list2[i]);
37.  }
38.  printf("\nList 3: ");
39.  for(int i = 0; i < index; i++)
40.  {
41.  printf("%d ", list3[i]);
42.  }

44.  return 0;
45.  }

[C code explanation](#contents.xhtml_sc4_579a)

The C code creates and initializes two arrays list1 and list2, containing some numbers. It then initializes an empty array, list3, and uses loops to iterate through both list1 and list2, appending odd numbers from list1 and even numbers from list2 to list3. Finally, it prints the combined result array. Here, the sizeof() function is used to find the arrays list1andlist2.

[Program 4.16: Frequency of occurrence of elements](#contents.xhtml_sc2_580a)

Count the frequency of occurrence of each element entered by the user.

[Sample input output](#contents.xhtml_sc3_581a)

Test case #1:

Input: Enter the size of list: 6

7 8 7 3 1 8

Output: Frequency of 7 is 2

Frequency of 8 is 2

Frequency of 3 is 1

Frequency of 1 is 1

Test case #2:

Input: Enter the size of list: 5

1 2 1 2 1

Output: Frequency of 1 is 3

Frequency of 2 is 2

[Algorithm](#contents.xhtml_sc3_582a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare variables n, x, a, f, count, i, j
3.  Read the size of list as n
4.  a=[]
5.  f=[]
6.  for i =0 to n-1
    1.  read a number as x
    2.  append x to a
    3.  append -1 to f
7.  for i = 0 to n-1
    1.  count=0
    2.  if f[i] == 1:
        1.  continue
    3.  for j =0 to n-1
        1.  if a[i]==a[j]:
            1.  f[j]=1
            2.  count=count+1
    4.  print("Frequency of ", a[i] , " is ", count)
8.  Stop

[Flowchart](#contents.xhtml_sc3_583a)

[Figure 4.16](#ch04.xhtml_fig4-16) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.16.jpg)

Figure 4.16: Flowchart illustrating the program 4.16

[Python code](#contents.xhtml_sc3_584a)

Python code for the program is as follows:

1.  n=int(input("Enter the size of list: "))
2.  a=[]
3.  f=[]
4.  for i in range(0,n):
5.  x=int(input("Enter the number: "))
6.  a.append(x)
7.  f.append(-1)
8.  for i in range(0, n):
9.  count=0
10.  if f[i] == 1:
11.  continue
12.  for j in range(0,n):
13.  if a[i]==a[j]:
14.  f[j]=1
15.  count=count+1
16.  print("Frequency of ", a[i] , " is ", count)

[Python code explanation](#contents.xhtml_sc4_585a)

The Python code takes the size and elements of a list as input from the user, then it iterates through the list to count the frequency of each element and prints the frequency for each element. The f list is used to track whether an element has been counted or not.

First, it prompts the user to input the size of the list and stores it in the variable n. It initializes an empty list a which will store the elements of the list. It initializes another empty list f which will be used to track whether an element has been counted or not. The for-loop iterates n times. It reads n values from the user, appends them in the list a, and sets-1 to the list f. This indicates that the corresponding element in list a has not been counted yet. Another for-loop iterates through the list a using the indices from 0 to n-1. It checks if the element at index i in list a has already been counted (indicated by f[i] being 1). If yes, it uses the continue statement to skip the current iteration and move to the next element. Inside the loop, another nested for-loop iterates through the list a again, using the indices from 0 to n-1 to check if the element at index i in list a is equal to the element at index j in list a. This is done to count the frequency of occurrences of each element. If the condition is true, it sets the value at index j in list f to 1, indicating that this element has been counted. Also, the count variable value is incremented by 1. Finally, it prints the frequency of the element at index i in list a.

[C code](#contents.xhtml_sc3_586a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int a[50], f[50], n,count, i, j;

6.  printf("Enter the size of list: ");
7.  scanf("%d", &n);
8.  for( i =0; i<n; i++)
9.  {
10.  scanf("%d", &a[i]);
11.  f[i]= -1;
12.  }
13.  for( i =0; i<n; i++)
14.  {
15.  count=0;
16.  if (f[i] == 1)
17.  continue;
18.  for( j =0; j<n; j++)
19.  {
20.  if (a[i]==a[j])
21.  {
22.  f[j]=1;
23.  count=count+1;
24.  }
25.  }
26.  printf("\nFrequency of %d is %d ", a[i], count);
27.  }
28.  }

[C code explanation](#contents.xhtml_sc4_587a)

The C code takes the size and elements of a list as input from the user. Then, it iterates through the array to count the frequency of each element and prints the frequency for each element. The f array is used to track whether an element has been counted or not.

First, it prompts the user to input the size of the array and stores it in the variable n. It declares an empty array a, which will store the elements of the array. It initializes another empty array f, which will be used to track whether an element has been counted or not. The for-loop iterates n times. It reads n values from the user, appends them in the array a, and sets -1 to the array f. This indicates that the corresponding element in array a has not been counted yet. Another for-loop iterates through the array a using the indices from 0 to n-1. It checks if the element at index i in array a has already been counted (indicated by f[i] being 1). If yes, it uses the continue statement to skip the current iteration and move to the next element. Inside the loop, another nested for-loop iterates through the array a again, using the indices from 0 to n-1 to check if the element at index i in array a is equal to the element at index j in array a. This is done to count the frequency of occurrences of each element. If the condition is true, it sets the value at index j in array f to 1, indicating that this element has been counted. Also, the count variable value is incremented by 1. Finally, it prints the frequency of the element at index i in array a.

[Program 4.17: Find length of a string](#contents.xhtml_sc2_588a)

Find the length of a string (without using library functions).

[Sample input output](#contents.xhtml_sc3_589a)

Test case #1:

Input: Enter a String: codefactory

Output: The length of the string is 11

Test case #2:

Input: Enter a String: bookforprogramming

Output: The length of the string is 18

[Algorithm](#contents.xhtml_sc3_590a)

To run the above program, the following steps need to be followed:

1.  Start
2.  s=input("Enter a String: ")
3.  l=0
4.  for i in s:
    1.  l=l+1
5.  print("The length of the string is ", l)
6.  Stop

[Flowchart](#contents.xhtml_sc3_591a)

[Figure 4.17](#ch04.xhtml_fig4-17) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.17.jpg)

Figure 4.17: Flowchart illustrating the program 4.17

[Python code](#contents.xhtml_sc3_592a)

Python code for the program is as follows:

1.  s=input("Enter a String: ")
2.  l=0
3.  for i in s:
4.  l=l+1
5.  print("The length of the string is ", l)

[Python code explanation](#contents.xhtml_sc4_593a)

The Python code prompts the user to input a string, counts the number of characters in the string using a loop that iterates through all characters of the string, and then prints the length of the string.

It reads a string input from the user and stores it in s. The variable l is set to 0and is used to store the length of the string. The for-loop iterates through each character of the string s. Inside the loop, it increments the l variable for each character encountered, effectively counting the length of the string. After the loop completes, it prints the calculated length of the string.

[C code](#contents.xhtml_sc3_594a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  char  s[30];
5.  int l,i;
6.  printf("Enter a String: ");
7.  scanf("%s",s);
8.  l=0;
9.  for (i=0; s[i]!=’\0’; i++)
10.  l=l+1;
11.  printf("The length of the string is  %d", l);
12.  }

[C code explanation](#contents.xhtml_sc4_595a)

The C code prompts the user to input a string, counts the number of characters in the string using a loop that iterates until the null character is encountered, and then prints the length of the string using the printf function.

First, it declares a character array s that can hold up to 30 characters. It reads a string input from the user and stores it in array s. The variable l is set to 0and is used to store the length of the string. The for loop iterates through each character of the string s until the null character (\0) is encountered, which indicates the end of the string. Inside the loop, it increments the l variable for each character encountered, effectively counting the length of the string. After the loop completes, it prints the calculated length of the string.

[Program 4.18: Check if string is a palindrome](#contents.xhtml_sc2_596a)

Check whether a given string is palindrome or not (without using library functions).

Hint: Palindrome means a sequence of characters that reads the same forwards as it does backward.

[Sample input output](#contents.xhtml_sc3_597a)

Test case #1:

Input: Enter a String: madam

Output: The string is a palindrome

Test case #2:

Input: Enter a String: codefactory

Output: The string is not palindrome

[Algorithm](#contents.xhtml_sc3_598a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare the variables i, l, s
3.  Read s
4.  l=0
5.  for i in s:
    1.  l=l+1
6.  for i = 0 to l
    1.  if s[i] !=s[l-i-1]
        1.  print("The string is not palindrome")
        2.  break
7.  else //this else belongs to the loop statement
    1.  print("The string is a palindrome")
8.  Stop

[Flowchart](#contents.xhtml_sc3_599a)

[Figure 4.18](#ch04.xhtml_fig4-18) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.18.jpg)

Figure 4.18: Flowchart illustrating the program 4.18

[Python code](#contents.xhtml_sc3_600a)

Python code for the program is as follows:

1.  s=input("Enter a String: ")
2.  l=0
3.  for i in s:
4.  l=l+1
5.  for i in range(0, l):
6.  if s[i] !=s[l-i-1]:
7.  print("The string is not palindrome")
8.  break
9.  else: //else of for-loop
10.  print("The string is a palindrome")

[Python code explanation](#contents.xhtml_sc4_601a)

This Python code checks whether a given input string is a palindrome or not. The user is prompted to enter a string. It initializes a variable l to store the length of the string. Then, it iterate through each character in the string using a loop to count the length of the string. It starts another loop that runs from 0 to l-1. Within the loop, it compares characters at positions i and l-i-1 to check if the string is a palindrome. If a character pair is found that does not match, print The string is not a palindrome and exit the loop using break. Otherwise, if the loop completes without finding a mismatched character pair, print The string is a palindrome.

[C code](#contents.xhtml_sc3_602a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  char s[30];
5.  int l,i;
6.  printf("Enter a String: ");
7.  scanf("%s",s);
8.  l=0;
9.  for(i=0; s[i]!= ‘\0’; i++)
10.  l=l+1;
11.  for( i=0;i<l;i++)
12.  {
13.  if (s[i] !=s[l-i-1])
14.  {
15.  printf("The string is not palindrome");
16.  break;
17.  }
18.  }
19.  if (i==l)
20.  printf("The string is a palindrome");
21.  }

[C code explanation](#contents.xhtml_sc4_603a)

This C code checks whether a given input string is a palindrome or not. The user is prompted to enter a string. It initializes a variable l to store the length of the string. Then, it iterate through each character in the string using a loop to count the length of the string. It starts another loop that runs from 0 to l-1.Within the loop, it compares characters at positions i and l-i-1 to check if the string is a palindrome. If a character pair is found that does not match, print The string is not a palindrome and exit the loop using break. Otherwise, if the loop completes without finding a mismatched character pair, print The string is a palindrome.

[Program 4.19: Display even indexed characters](#contents.xhtml_sc2_604a)

Read a string from the user and display only those characters that are present at an even index. For example, str =’python’, so you should display p,t,o.

[Sample input output](#contents.xhtml_sc3_605a)

Test case #1:

Input: Enter a String: codefactory

Output: c d f c o y

Test case #2:

Input: Enter a String: programming

Output: p o r m i g

[Algorithm](#contents.xhtml_sc3_606a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare the variables l, i
3.  Read s
4.  l=0
5.  for i in s:
    1.  if (l%2==0)
        1.  print i
    2.  l=l+1
6.  Stop

[Flowchart](#contents.xhtml_sc3_607a)

[Figure 4.19](#ch04.xhtml_fig4-19) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.19.jpg)

Figure 4.19: Flowchart illustrating the program 4.19

[Python code](#contents.xhtml_sc3_608a)

Python code for the program is as follows:

1.  s=input("Enter a String: ")
2.  l=0
3.  for i in s:
4.  if l%2==0:
5.  print(i)
6.  l=l+1

[Python code explanation](#contents.xhtml_sc4_609a)

The Python code takes a string as input and then prints out every other character of the string (starting from the first character) using a loop. The variable l is used to determine whether the current character should be printed based on its position. For that, it checks if the current value of l (the position of the character being considered) is even. If the condition is true, the code inside this block will execute and print the character at index i in the string s.

[C code](#contents.xhtml_sc3_610a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  char s[30];
5.  int l,i;
6.  printf("Enter a String: ");
7.  scanf("%s",s);
8.  l=0;
9.  for(i=0; s[i]!= ‘\0’; i++)
10.  {
11.  if (l%2==0)
12.  {printf("%c ", s[i]);}
13.  l=l+1;
14.  }}

[C code explanation](#contents.xhtml_sc4_611a)

The C code takes a string as input and then prints out every other character of the string (starting from the first character) using a loop. The variable l is used to determine whether the current character should be printed based on its position. For that, it checks if the current value of l (the position of the character being considered) is even. If the condition is true, the code inside this block will execute and print the character at index i in the string s.

[Program 4.20: Concatenate two strings](#contents.xhtml_sc2_612a)

Concatenate two strings (without using library functions).

[Sample input output](#contents.xhtml_sc3_613a)

Test case #1:

Input: Enter a string: code

Enter second string: factory

Output: Concatenated string is codefactory

Test case #2:

Input: Enter a string: programming

Enter second string: book

Output: Concatenated string is programmingbook

[Algorithm](#contents.xhtml_sc3_614a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare variables as s1, s2, s3
3.  Read a string s1, s2
4.  i=0
5.  while(s1[i]!= ‘\0’)
    1.  s3[i]=s1[i]
    2.  i=i+1
6.  while(s2[i]!= ‘\0’)
    1.  s3[i]=s2[i]
    2.  i=i+1
7.  print(s3)
8.  Stop

[Flowchart](#contents.xhtml_sc3_615a)

[Figure 4.20](#ch04.xhtml_fig4-20) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_4.20.jpg)

Figure 4.20: Flowchart illustrating the program 4.20

[Python code](#contents.xhtml_sc3_616a)

Python code for the program is as follows:

1.  s1=input("Enter a String: ")
2.  s2=input("Enter second String: ")
3.  s3=s1+s2
4.  print(s3)

[Python code explanation](#contents.xhtml_sc4_617a)

This Python code takes two input strings from the user, concatenates them together, and then prints the resulting concatenated string. In Python, the + operator can be used with string as a concatenation operator.

[C code](#contents.xhtml_sc3_618a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  char s1[20], s2[20], s3[20];
5.  int i=0, j=0;
6.  printf("Enter a string: ");
7.  scanf("%s", s1);
8.  printf("Enter a string: ");
9.  scanf("%s", s2);
10.  while(s1[i]!= ‘\0’)
11.  {
12.  s3[i]=s1[i];
13.  i=i+1;
14.  }
15.  while(s2[j]!= ‘\0’)
16.  {
17.  s3[i]=s2[j];
18.  i=i+1;
19.  j=j+1;
20.  }
21.  printf("Concatenated string is %s", s3);
22.  }

[C code explanation](#contents.xhtml_sc4_619a)

The C code declares three character arrays,s1, s2, and s3, that can hold up to 20 characters each. These arrays will be used to store the input strings and the concatenated string. It reads two strings input from the user and stores them in the character arrayss1 and s2. The while loop iterates through each character of the string s1 until the null character (\0) is encountered, which indicates the end of the string and copies the character at index i from string s1 to the corresponding index i in the string s3. Similarly, another while loop iterates through each character of the string s2 until the null character (\0) and copies the character at index j from string s2 to the current index i in the string s3. Finally, it prints the concatenated string stored in s3 using the printf function.

[Conclusion](#contents.xhtml_sc2_620a)

The chapter has discussed complex control statements (while-loop and for-loop) with conditional statements in the form of flowcharts, algorithms, and coding. With the help of several examples, the different flavors of loop statements are presented.

In the next chapter, more complex programs will be discussed with the help of a good number of solved examples.

[Points to remember](#contents.xhtml_sc2_621a)

*   Range() function in Python generates the sequence from a lower value to one less than the upper value. For example, range(1,4) generates 1,2,3.
*   The append () function in Python is used to add elements to the list.
*   In C, #define can be used to define macro, an inline function.
*   In C, ?: operator is used to check condition and assign value.
*   Double equal, ==, is used for comparing the values, whereas single equal, =, is used to assign the value.
*   In the for-loop, the value of the induction variable is incremented/ decremented automatically. Meanwhile, in the while-loop, it is to be done in the loop deliberately.
*   In Python code, the loop block should be indented towards the right side.
*   In C code, the loop block should be enclosed within curly brackets {}.

[Questions](#contents.xhtml_sc2_622a)

1. Display even numbers between the range n and m where n and m are inclusive.

2. Display *** (three stars) if the number is divisible by 5\. Numbers are between the range n and m, where n and m are inclusive.

3. Display *** (three stars) if the number is divisible by 5\. Otherwise, display x (one cross). Numbers are between the range n and m, where n and m are inclusive.

4. Display the numbers divisible by three between the range n and m where n and m are inclusive.

5. Display the sum of all the numbers that are divisible by 11 between the range n and m where n and m are inclusive.

6. Find the smallest of n numbers as entered by the user.

7. Count the number of consonants in a string.

8. Copy one string into another (without using library functions).

9. Print all the prime numbers between 0 and 50

10. Print all the prime numbers between the values X and Y. For example, if X=1 and Y=10, then the output should display1, 2, 3, 5, 7.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](OPS/images/fm1.png)

# [CHAPTER 5Complex Problem Solving](#contents.xhtml_ch05a)

[Introduction](#contents.xhtml_sc2_623a)

This chapter discusses the complex logic building using various programming constructs (as discussed in previous chapters). The chapter’s main focus is solving difficult problems by thinking of some logic. The chapter presents the problems or challenges that require creative and intricate solutions. These problems often go beyond simple algorithmic steps and may involve multiple steps, conditional logic, loops, lists, and matrices. The chapter discusses creating a logical flow for solving complex problems, including algorithms and flowcharts, to plan solutions before writing code.

[Structure](#contents.xhtml_sc2_624a)

In this chapter, there are a total of 20 programs, and five sub-sections complement each program:

*   Understand the program objective with sample test cases consisting of inputs and outputs. It will give the user an understanding of what kind of user input is expected and what result will be projected for a particular program.
*   Understand the program with an algorithm. This will help the user to understand the logical flow for solving complex problems.
*   Visualize the program flow with flowcharts. Program objectives can be understood easily with the flowchart representation. Users will understand which symbols to use in which context throughout different program’s flowchart representations.
*   Python source code of each program. Each program’s source code in Python programming language is provided to the user so the user can understand the basic operations of the language. An explanation of each code is also provided.
*   C implementation of each program. Users can learn the basic concepts of C language with the provided C language code and its explanation for every program.

[Objectives](#contents.xhtml_sc2_625a)

In this chapter, readers will explore techniques for solving intricate problems that often involve multiple sequential steps, intricate combinations of conditional statements and nested loops, and manipulation of data structures like lists and matrices. The readers will also explore constructing a coherent problem-solving strategy, incorporating algorithm design and flowcharts to chart solutions before coding implementation.

Furthermore, the chapter strongly emphasizes practical application, demonstrating how to implement these logical approaches using Python and C programming languages. Sample codes are provided to offer hands-on experience, allowing readers to practice and gain confidence in effectively utilizing various programming constructs in different coding scenarios.

[Program 5.1: Find sum of digits of a number](#contents.xhtml_sc2_626a)

Find the sum of the digits of a number. For example, if number is 2134, then sum = 10.

[Sample input output](#contents.xhtml_sc3_627a)

Test case #1:

Input: Enter a number: 78

Output: The sum of the digits of the number is 15

Test case #2:

Input: Enter a number: 204874

Output: The sum of the digits of the number is 25

[Algorithm](#contents.xhtml_sc3_628a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Variable declaration: m, s, r
3.  Read m
4.  s=0
5.  Iterate till m>0
6.  r=m%10
7.  s=s+r
8.  m=m/10
9.  Print ("Sum of digits of the number is:",s)
10.  Stop

[Flowchart](#contents.xhtml_sc3_629a)

[Figure 5.1](#ch05_split_000.xhtml_fig5-1) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.1.jpg)

Figure 5.1: Flowchart illustrating the program 5.1

[Python code](#contents.xhtml_sc3_630a)

Python code for the program is as follows:

1.  m=int(input("Enter a number:")) 
2.  s=0 
3.  while(m>0):
4.  r=m%10
5.  m=m//10 
6.  s=s+r
7.  print("Sum of digits of the number is: ",s)

[Python code explanation](#contents.xhtml_sc4_631a)

This Python program calculates the sum of the digits of a number the user enters. It prompts the user to enter a number and stores it in the variable m. while loop is used to extract digits one by one from the number until there are no more digits left by repeatedly dividing m by 10 to extract and remove the rightmost digit of m, and storing quotient and reminder. In each iteration, the value of r (the rightmost digit) is added to the cumulative value of s. This is how the program keeps track of the sum of the digits. To obtain a quotient, the operator // is used. This operator gives the integer division of the numbers. Finally, it displays the result to the user.

[C code](#contents.xhtml_sc3_632a)

The C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int m, s, r;
5.  printf("Enter n: ");
6.  scanf("%d",&m);
7.  s=0 ;
8.  while(m>0)
9.  {
10.  r=m%10 ;
11.  s=s+r ;
12.  m=m/10 ;
13.  }
14.  printf("Sum of digits of the number is : %d",s);
15.  }

[C code explanation](#contents.xhtml_sc4_633a)

The C code takes a number as input from the user. It initializes a variable s to 0 to store the sum. It enters a loop where it repeatedly extracts the rightmost digit of m using the % operator, adds it to the sum s, and then removes that digit from m using the division operator. Unlike Python, / operator is used for integer division. The loop continues until there are no more digits left in m. Finally, it prints the total sum of the digits to the user.

[Program 5.2: Reverse the number](#contents.xhtml_sc2_634a)

Reverse an n digit number. For example, if the number is 2134, the reverse number is 4312.

[Sample input output](#contents.xhtml_sc3_635a)

Test case #1:

Input: Enter a number: 1234

Output: The reversed number is: 4321

Test case #2:

Input: Enter a number: 8720

Output: The reversed number is: 278

[Algorithm](#contents.xhtml_sc3_636a)

To run the above program, the following steps need to be followed:

1.  Start
2.  Variables declaration: n, s, r
3.  Read n
4.  s=0
5.  Iterate while(n>0)

rem=n%10

s=s*10+rem

n=n/10

1.  Print("The reversed number is: ",s)
2.  Stop

[Flowchart](#contents.xhtml_sc3_637a)

[Figure 5.2](#ch05_split_000.xhtml_fig5-2) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.2.jpg)

Figure 5.2: Flowchart illustrating the program 5.2

[Python code](#contents.xhtml_sc3_638a)

Python code for the program is as follows:

1.  n=int(input("Enter a number:")) 
2.  s=0 
3.  while(n>0):
4.  rem=n%10
5.  s=s*10+rem
6.  n=n//10 
7.  print("The reversed number is:",s)

[Python code explanation](#contents.xhtml_sc4_639a)

This Python program is a continuation of the previous program. It prompts the user to enter a number and stores it in the variable n. while loop is used to extract digits one by one from the number until there are no more digits left by repeatedly dividing n by 10 to extract and remove the rightmost digit of n, and storing quotient and reminder both. Here, to reverse the number, the current value of s is multiplied by 10 (which shifts all digits one position to the left), and then rem (rightmost digit) is added to it. This effectively builds the reversed number digit by digit. Finally, it displays the result to the user.

[C code](#contents.xhtml_sc3_640a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int n, s, rem;
5.  printf("Enter n: ");
6.  scanf("%d",&n);
7.  s=0 ;
8.  while(n>0)
9.  {
10.  rem=n%10 ;
11.  s=s*10+rem ;
12.  n=n/10 ;
13.  }
14.  printf("The total sum of digits is: %d",s);
15.  }

[C code explanation](#contents.xhtml_sc4_641a)

The C code takes a number as input from the user. It initializes a variable s to 0 to store the reversed number. It enters a loop where it repeatedly extracts the rightmost digit of n, multiplies the current value of s by 10 (which shifts all digits from one position to the left), and then adds rem (rightmost digit). Then, it removes that digit from n. The loop continues until there are no more digits left in n. Finally, it prints the reversed number to the user.

[Program 5.3: Find all Armstrong numbers](#contents.xhtml_sc2_642a)

Find all Armstrong numbers in the range of 0 and 999\. [Example: A 3-digit number N is an Armstrong number if N=A^3+B^3+C^3, where A, B, and C are individual digits of number N. 371 is an Armstrong).

[Sample input output](#contents.xhtml_sc3_643a)

Test case #1:

Output: 0 1 2 3 4 5 6 7 8 9 153 370 371 407

[Algorithm](#contents.xhtml_sc3_644a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Variables declaration: n, m, s, rem, i, j, ar, a[]
3.  m=0
4.  Iterate while m<=999

    n=m, ar=0 , i=0, j=0, a=[]

    Iterate while(n>0)

    rem=n%10

    a[i]=rem

    i=i+1

    n=n/10

    Iterate while (j<i)

    ar=ar+pow(a[j],i)

    j=j+1

    if m==ar

    Print(m," is an Armstrong Number")

    m=m+1

    del a

5.  Stop

[Flowchart](#contents.xhtml_sc3_645a)

[Figure 5.3](#ch05_split_000.xhtml_fig5-3) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.3.jpg)

Figure 5.3: Flowchart illustrating the program 5.3

[Python code](#contents.xhtml_sc3_646a)

Python code for the program is as follows:

1.  import math
2.  for m in range(0,1000):
3.  n=m
4.  a=[]
5.  i=0
6.  j=0
7.  ar=0
8.  while(n>0): 
9.  rem=n%10
10.  a.append(rem )
11.  n=n//10 
12.  i=i+1

14.  while (j<i):
15.  ar=ar+pow(a[j],i)
16.  j=j+1

18.  if ar == m:
19.  print(m)
20.  del a

[Python code explanation](#contents.xhtml_sc4_647a)

This Python program calculates and prints all Armstrong numbers from 0 to 999\. Armstrong numbers are numbers equal to the sum of their digits. Each raised to the power of the number of digits. The first math module is imported to use some math functions, such as pow(). A for loop iterates through the numbers from 0 to 999\. The variable m takes on each value in this range individually. It extracts all the digits of the number one by one and stores them in a list a[]. At the end of the while-loop, the variable i stores the number of digits of the number n. Then, next, the while-loop calculates the sum of the digits raised to the power of the number of digits and checks if it is equal to the original number. If it is equal, it prints the Armstrong number.

[C code](#contents.xhtml_sc3_648a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  #include<math.h>
3.  void main()
4.  {
5.  int n, ar, m, rem, a[10];
6.  for(m=0;m<=999;m++)
7.  {
8.  n=m;
9.  int i=0;
10.  int j=0;
11.  int ar=0;
12.  while(n>0)
13.  {
14.  rem=n%10 ;
15.  a[i]=rem ;
16.  n=n/10 ;
17.  i=i+1;
18.  }
19.  while (j<i)
20.  {
21.  ar=ar+pow(a[j],i);
22.  j=j+1;
23.  }
24.  if( ar == m)
25.  printf("%d ", m);
26.  }
27.  }

[C code explanation](#contents.xhtml_sc4_649a)

This C code calculates and prints all Armstrong numbers from 0 to 999\. Armstrong numbers are numbers equal to the sum of their digits, and each is raised to the power of the number of digits. Here, the first math.h library is included to use some maths functions such as pow(). A for loop iterates through the numbers from 0 to 999\. The variable m takes on each value in this range individually. It extracts all the digits of the number one by one and stores it in an array a[]. At the end of the while-loop, the variable i stores the number of digits of the number n. Then, next, the while-loop calculates the sum of the digits raised to the power of the number of digits and checks if it is equal to the original number. If it is equal, it prints the Armstrong number.

[Program 5.4: Find n based on a condition](#contents.xhtml_sc2_650a)

Given a list of numbers, find all its elements greater than their left neighbor and lesser than the right neighbor. For example, for the input [2 6 8 5 4], the output is [6].

[Sample input output](#contents.xhtml_sc3_651a)

Test case #1:

Input: l=[2, 6, 8, 5, 4]

Output: 6

Test case #2:

Input: l=[2, 6, 8, 9, 4]

Output: 6, 8

[Algorithm](#contents.xhtml_sc3_652a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  l=[2, 6, 8, 5, 4]
3.  for i = (1, len(l)-1):
4.  if (l[i] >l[i-1] and l[i] < l[i+1]):

    print(l[i])

5.  Stop

[Flowchart](#contents.xhtml_sc3_653a)

[Figure 5.4](#ch05_split_000.xhtml_fig5-4) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.4.jpg)

Figure 5.4: Flowchart illustrating the program 5.4

[Python code](#contents.xhtml_sc3_654a)

Python code for the program is as follows:

1.  l=[2, 6, 8, 9, 4]
2.  for i in range(1, len(l)-1):
3.  if (l[i] >l[i-1] and l[i] < l[i+1]):
4.  print(l[i])

[Python code explanation](#contents.xhtml_sc4_655a)

This Python code snippet analyzes a list l and prints elements greater than the preceding element and less than the succeeding element. First, a list l is initialized as l= [2, 6, 8, 9, 4]. Then, a for loop iterates through the list of l indices. It starts at index 1 and goes up to len(l) - 2. The reason for excluding the first and last elements is to ensure we do not get an out of range error when checking elements before and after the current element. Inside the loop, it checks if the element at index i is greater than the element at index i-1 (the preceding element) and less than the element at index i+1 (the succeeding element). If yes, it prints the element at index i.

[C code](#contents.xhtml_sc3_656a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void main()
3.  {
4.  int l[]={2, 6, 8, 9, 5, 4};
5.  int i ;
6.  for (i =1; i< 5; i++)
7.  {
8.  if ((l[i] >l[i-1])&& (l[i] < l[i+1]))
9.  {
10.  printf("%d ", l[i] );
11.  }
12.  }
13.  }

[C code explanation](#contents.xhtml_sc4_657a)

This C code analyzes an array l and prints elements greater than the preceding element and less than the succeeding element. First, an array, l, is initialized as l= [2, 6, 8, 9, 4]. Then, a for loop iterates through the list l indices. It starts at index 1 and goes up to 4. The reason for excluding the first and last elements is to ensure we do not get an out of range error when checking elements before and after the current element. Inside the loop, it checks if the element at index i is greater than the element at index i-1 (the preceding element) and less than the element at index i+1 (the succeeding element). If yes, it prints the element at index i.

[Program 5.5: Obtain list having prime numbers](#contents.xhtml_sc2_658a)

Create list L1 from list L2 such that L1 has all values that are prime numbers in L2.

[Sample input output](#contents.xhtml_sc3_659a)

Test case #1:

Input: L2 = [15, 17, 20, 25, 11]

Output: L1: [17, 11]

Test case #2:

Input: L2 = [45,31,17,33,97,118]

Output: L1: [31, 17, 97]

[Algorithm](#contents.xhtml_sc3_660a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare L2 = [45,31,17,33,97,118]
3.  L1 = []
4.  Iterate while n is in L2:

    bl = True    

    Iterate  for i = 2 to n

    if n % i == 0:

    bl = False

    break

    if bl == True:

    L1.append(n)

5.  Print  L1
6.  Stop

[Flowchart](#contents.xhtml_sc3_661a)

[Figure 5.5](#ch05_split_000.xhtml_fig5-5) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.5.jpg)

Figure 5.5: Flowchart illustrating the program 5.5

[Python code](#contents.xhtml_sc3_662a)

Python code for the program is as follows:

1.  L2 = [45,31,17,33,97,118]
2.  L1 = []
3.  for n in L2:
4.  bl = True    
5.  for i in range(2, n):
6.  if n % i == 0:
7.  bl = False
8.  break          
9.  if bl == True:
10.  L1.append(n)
11.  print("L1:", L1)

[Python code explanation](#contents.xhtml_sc4_663a)

The Python code is designed to find and store prime numbers from a list L2 into another list L1. First, it initializes the list L2 as [45, 31, 17, 33, 97, 118] and an empty list L1. for loop iterates through each element n in the list L2. bl is a boolean variable that is set to True before each iteration. It is used to track whether or not the current number n is prime. Inside the loop, another for loop starts that iterates through numbers i from 2 up to (but not including) n. This loop tests the divisibility of n by any number between 2 to n-1. Suppose n is divisible by any of them. In that case, the bl variable becomes false, indicating that n is not a prime number, and the inner loop is terminated using the break statement. After the inner for loop, it checks if bl is still True. If it is, it means that n cannot be divided by any number in the specified range, so it is a prime number and appends it to the L1 list. Now, the outer loop continues for the next number. Finally, it displays the prime numbers found in L2.

[C code](#contents.xhtml_sc3_664a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  #include <stdbool.h>
3.  int bl(int nn) {
4.  if (nn < 2) {
5.  return 0;
6.  }
7.  for (int ii = 2; ii * ii <= nn; i++) {
8.  if (nn % ii == 0) {
9.  return 0;
10.  }
11.  }
12.  return 1;
13.  }
14.  int main() {
15.  int L2[] = {45,31,17,33,97,118};
16.  int n = sizeof(L2) / sizeof(L2[0]);
17.  int L1[n];
18.  int c = 0;
19.  for (int i = 0; i < n; i++) {
20.  if (bl(L2[i])) {
21.  L1[c++] = L2[i];
22.  }
23.  }
24.  printf("L1 = { ");
25.  for (int i = 0; i < c; i++) {
26.  printf("%d ", L1[i]);
27.  }
28.  printf("}\n");
29.  return 0;
30.  }

[C code explanation](#contents.xhtml_sc4_665a)

This code declares an array L2 of integers and uses the bl() function to check if each number in the array is prime. If a number is prime, it is added to a new array L1. Finally, the program prints out the values in L1. Note that the code assumes that the maximum size of L2 is 9, the size of the provided list. To handle larger lists, the code would need to be modified accordingly. This program uses the concept of function definition (Line no 3-13) and function call (Line no 20). Each element of array L2 is passed to the function bl(). The function checks whether the element is prime and returns the value True if it is.

[Program 5.6: Remove duplicate items](#contents.xhtml_sc2_666a)

Remove duplicate items from a given list.

[Sample input output](#contents.xhtml_sc3_667a)

Test case #1:

Input: [78, 89, 78, 65, 89, 89, 65]

Output: [78, 89, 65]

Test case #2:

Input: [19, 24, 19, 19, 19, 19, 24, 24]

Output: [19, 24]

[Algorithm](#contents.xhtml_sc3_668a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare my_list = [19, 24, 19, 19, 19, 19, 24, 24]
3.  new_list = []
4.  Iterate for each item in my_list

    if item not in new_list:

    append item in new_list

5.  Print new_list
6.  Stop

[Flowchart](#contents.xhtml_sc3_669a)

[Figure 5.6](#ch05_split_000.xhtml_fig5-6) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.6.jpg)

Figure 5.6: Flowchart illustrating the program 5.6

[Python code](#contents.xhtml_sc3_670a)

Python code for the program is as follows:

1.  my_list = [19, 24, 19, 19, 19, 19, 24, 24]
2.  new_list = []

4.  for item in my_list:
5.  if item not in new_list:
6.  new_list.append(item)

8.  print(new_list)

[Python code explanation](#contents.xhtml_sc4_671a)

This Python code first creates a list with some duplicate items and then creates a new list that only includes the unique items from the original list. The for-loop iterates through each item in the original list and checks whether it is already in the new list. If not, it is added to the new list using the append() method. Finally, the new list is printed to the console.

[C code](#contents.xhtml_sc3_672a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int my_array[] = {19, 24, 19, 19, 19, 19, 24, 24};
4.  int new_array[11];
5.  int i, j, n, exists;
6.  n = 0;
7.  for (i = 0; i < 11; i++) {
8.  exists = 0;
9.  for (j = 0; j < n; j++) {
10.  if (my_array[i] == new_array[j]) {
11.  exists = 1;
12.  break;
13.  }
14.  }
15.  if (!exists) {
16.  new_array[n] = my_array[i];
17.  n++;
18.  }
19.  }
20.  for (i = 0; i < n; i++) {
21.  printf("%d ", new_array[i]);
22.  }
23.  return 0;
24.  }

[C code explanation](#contents.xhtml_sc4_673a)

This code declares an array my_array with some duplicate items and creates a new array new_array to hold the unique items. It then uses nested loops to iterate through the my_array and checks for duplicate items. The outer loop goes through each element in my_array, and the inner loop iterates through each item in new_array to check whether the item already exists. If the item does not exist in new_array, it is added to the array using the new_array[n] = my_array[i] syntax, where n is the current length of new_array. Finally, the new_array is printed to the console using a loop that iterates through each item in the array.

[Program 5.7: Sort the numbers](#contents.xhtml_sc2_674a)

Arrange all the elements of an array in increasing order.

[Sample input output](#contents.xhtml_sc3_675a)

Test case #1:

Input: [6, 3, 25, 1, 22, 11, 90]

Output: Sorted List is : [1, 3, 6, 11, 22, 25, 90]

Test case #2:

Input: [21,27,23,97,20,6,93]

Output: [6, 20, 21, 23, 27, 93, 97]

[Algorithm](#contents.xhtml_sc3_676a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Declare a_r = [6, 3, 25, 1, 22, 11, 90]
3.  n = len(a_r)
4.  Iterate for i =0 to n-1

Iterate for j =0 to n-i

if a_r[j] > a_r[j+1] :

interchange a_r[j], a_r[j+1]

1.  Print a_r
2.  Stop

[Flowchart](#contents.xhtml_sc3_677a)

[Figure 5.7](#ch05_split_000.xhtml_fig5-7) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.7.jpg)

Figure 5.7: Flowchart illustrating the program 5.7

[Python code](#contents.xhtml_sc3_678a)

Python code for the program is as follows:

1.  a_r = [6, 3, 25, 1, 22, 11, 90]
2.  n = len(a_r)
3.  for ii in range(n):
4.  for jj in range(0, n-ii-1):
5.  if a_r[jj] > a_r[jj+1] :
6.  a_r[jj], a_r[jj+1] = a_r[jj+1], a_r[jj]
7.  print("Sorted List is :",a_r)

[Python code explanation](#contents.xhtml_sc4_679a)

The provided Python code implements the Bubble Sort algorithm to sort a list called a_r in ascending order. In bubble sort, it repeatedly compares each element with its next element given in the list, and if the elements are not in increasing order, then the elements are interchanged. Here, a list is initialized as a_r = [6, 3, 25, 1, 22, 11, 90]. len() function returns the length of a list and assigns it to the variable n. It starts the outer loop, which iterates over the list of a_r elements. Inside the outer loop, it starts the inner loop, which iterates over a subset of the list from index 0 to n-ii-1. The reason for the -ii is that after each pass of the outer loop, the largest element (after sorting) is moved to the end, so there is no need to compare it again. The elements are swapped if the element at index jj is greater than at the next index jj+1. Finally, the sorted list is printed.

[C code](#contents.xhtml_sc3_680a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int a_r[100], n, i, j, tt, bl;
4.  printf("Enter the number of elements in the array: ");
5.  scanf("%d", &n);
6.  printf("Enter the elements of the array: ");
7.  for(i = 0; i < n; i++) {
8.  scanf("%d", &a_r[i]);
9.  }
10.  for(i = 0; i < n - 1; i++) {
11.  bl = 0;
12.  for(j = 0; j < n - i - 1; j++) {
13.  if(a_r[j] > a_r[j + 1]) {
14.  tt = a_r[j];
15.  a_r[j] = a_r[j + 1];
16.  a_r[j + 1] = tt;
17.  bl = 1;
18.  }
19.  }
20.  if(bl == 0) {
21.  break;
22.  }
23.  }
24.  printf("Sorted array in ascending order: «);
25.  for(i = 0; i < n; i++) {
26.  printf("%d ", a_r[i]);
27.  }
28.  printf("\n");
29.  return 0;
30.  }

[C code explanation](#contents.xhtml_sc4_681a)

The code repeatedly compares each element with its next element given in the list, and if the elements are not in increasing order, they are interchanged. This process continues until no more swaps are needed, indicating that the list is sorted. The result is a sorted list printed to the console.

[Program 5.8: Print matrix](#contents.xhtml_sc2_682a)

Input a matrix of size 3x3 from the user and print the same as the output.

[Sample input output](#contents.xhtml_sc3_683a)

Test case #1:

Input:

Enter element at position ({,i,},{,j, }): 6

Enter element at position ({,i,},{,j, }): 5

Enter element at position ({,i,},{,j, }): 6

Enter element at position ({,i,},{,j, }): 4

Enter element at position ({,i,},{,j, }): 6

Enter element at position ({,i,},{,j, }): 3

Enter element at position ({,i,},{,j, }): 3

Enter element at position ({,i,},{,j, }): 5

Enter element at position ({,i,},{,j, }): 2

Output:

The matrix is:

6 5 6

4 6 3

3 5 2

Test case #2:

Input:

Enter element at position ({i},{j}): 1

Enter element at position ({i},{j}): 2

Enter element at position ({i},{j}): 3

Enter element at position ({i},{j}): 4

Enter element at position ({i},{j}): 5

Enter element at position ({i},{j}): 6

Enter element at position ({i},{j}): 7

Enter element at position ({i},{j}): 8

Enter element at position ({i},{j}): 4

Output:

The matrix is:

1 2 3

4 5 6

7 8 4

[Algorithm](#contents.xhtml_sc3_684a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Initialize a 3x3 matrix
3.  Accept 9 integer inputs from the user and assign them to the matrix elements
4.  Print the matrix
5.  Stop

[Flowchart](#contents.xhtml_sc3_685a)

[Figure 5.8](#ch05_split_000.xhtml_fig5-8) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.8.jpg)

Figure 5.8: Flowchart illustrating the program 5.8

[Python code](#contents.xhtml_sc3_686a)

Python code for the program is as follows:

1.  matrix = [[0 for j in range(3)] for i in range(3)]
2.  for i in range(3):
3.  for j in range(3):
4.  matrix[i][j] = int(input("Enter element at position ({,i,},{,j, }): "))
5.  print("The matrix is:")
6.  for i in range(3):
7.  for j in range(3):
8.  print(matrix[i][j], end=" ")
9.  print()

[Python code explanation](#contents.xhtml_sc4_687a)

The provided Python code allows users to input elements for a 3x3 matrix and then print the matrix. In Python, a matrix is typically represented as a two-dimensional array or list of lists, where each element in the matrix is accessed by specifying both row and column indices. First, it initializes a 3x3 matrix (a list of lists) with all elements initially set to 0. It uses a nested list comprehension to create the matrix. Then, the nested for-loop takes all matrix elements as input from the user. Similarly, nested for-loop prints all matrix elements to the user.

[C code](#contents.xhtml_sc3_688a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int matrix[3][3];
4.  int i, j;

6.  printf("Enter the elements of the matrix:\n");
7.  for (i = 0; i < 3; i++) {
8.  for (j = 0; j < 3; j++) {
9.  scanf("%d", &matrix[i][j]);
10.  }
11.  }
12.  printf("The matrix you entered is:\n");
13.  for (i = 0; i < 3; i++) {
14.  for (j = 0; j < 3; j++) {
15.  printf("%d ", matrix[i][j]);
16.  }
17.  printf("\n");
18.  }
19.  return 0;
20.  }

[C code explanation](#contents.xhtml_sc4_689a)

This program declares a matrix of size 3x3 to store the input and then uses nested for loops to input and print the matrix elements. In C, a matrix is a 2-D array. A two-dimensional array in C is essentially an array of arrays where each element is identified by row and column indices. A nested for-loop takes the matrix as input and prints the matrix where the outer loop takes care of the rows, and the inner loop handles the columns in each row.

[Program 5.9: Add two matrics](#contents.xhtml_sc2_690a)

Add two matrices. Also, print error message when matrices are not of the same size.

[Sample input output](#contents.xhtml_sc3_691a)

Test case #1:

Input:

A=[[1,2,3,4],[3,4,5,7],[5,6,7,1]]

B=[[9,9,8,1],[3,6,5,3],[2,6,8,2]]

Output:

Matrix C (sum of A and B):

10 11 11 5

6 10 10 10

7 12 15 3

Test case #2:

Input:

A=[[1,1,2,2],[1,1,1,1],[3,3,3,3]]

B=[[9,9,8,8],[2,2,2,2],[4,4,8,6]]

Output:

Matrix C (sum of A and B):

10 10 10 10

3 3 3 3

7 7 11 9

[Algorithm](#contents.xhtml_sc3_692a)

Step 1\. To run the above program, the following steps are needed to be followed:

Step 2\. Take the dimensions (no of rows and no of columns) of two matrices, A and B, as input from the user.

Step 3\. If the dimension of A is not the same as that of B, print an error message
and terminate the program.

Step 4\. Take the matrices A and B elements as input.

Step 5\. Create an empty matrix C of the same size as A and B.

Step 6\. Perform the element-wise addition of A and B and store the result in C.

Step 7\. Print the matrices A, B, and C.

[Flowchart](#contents.xhtml_sc3_693a)

[Figure 5.9](#ch05_split_000.xhtml_fig5-9) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.9.jpg)

Figure 5.9: Flowchart illustrating the program 5.9

[Python code](#contents.xhtml_sc3_694a)

Python code for the program is as follows:

1.  m_a=[[1,1,2,2],[1,1,1,1],[3,3,3,3]]
2.  m_b=[[9,9,8,8],[2,2,2,2],[4,4,8,6]]
3.  r=len(m_a)
4.  c=len(m_a[0])
5.  r1=len(m_b)
6.  c1=len(m_b[0])
7.  if r != r1 or c!=c1:
8.  print("matrices are different dimensions.")
9.  exit()
10.  m_c = [[0 for j in range(c)] for i in range(r)]

12.  for i in range(r):
13.  for j in range(c):
14.  m_c[i][j] = m_a[i][j] + m_b[i][j]

16.  print("Matrix m_c (sum of m_a and m_b):")
17.  for i in range(r):
18.  for j in range(c):
19.  print(m_c[i][j], end=' ‘)
20.  print()

[Python code explanation](#contents.xhtml_sc4_695a)

The Python code performs matrix addition for two matrices m_a and m_b, and then prints the result in matrix m_c. Here, two matrix m_a and m_b are initialized as m_a = [[1, 1, 2, 2], [1, 1, 1, 1], [3, 3, 3, 3]] and m_b = [[9, 9, 8, 8], [2, 2, 2, 2], [4, 4, 8, 6]]. Then, the dimensions of both the matrices are compared. Addition can be performed if they are equal. Otherwise, an error message is printed, and the program exits using the exit() function. If the size of matrices is the same, nested for-loops are used to perform point-wise addition and are stored at the corresponding location in the m_c matrix. Finally, it prints the resulting matrix m_c using nested loops.

[C code](#contents.xhtml_sc3_696a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  #include <stdlib.h>
3.  int main() {
4.  int r, c, r1, c1, i, j;
5.  printf("Matrix 1: no of rows and columns «);
6.  scanf("%d %d", &r, &c);
7.  printf("Matrix 2: no of rows and columns ");
8.  scanf("%d %d", &r1, &c1);
9.  if ((r != r1) || (c != c1)) {
10.  printf("\matrices are different dimensions.");
11.  exit(0);
12.  }
13.  int m_a[r][c], m_b[r1][c1], m_c[r][c];

15.  printf("\nEnter the elements of the first matrix:\n»);
16.  for (i = 0; i < r; i++) {
17.  for (j = 0; j < c; j++) {
18.  printf("Enter element[%d][%d]: ", i, j);
19.  scanf("%d", &m_a[i][j]);
20.  }
21.  }

23.  printf("\nEnter the elements of the second matrix:\n»);
24.  for (i = 0; i < r1; i++) {
25.  for (j = 0; j < c1; j++) {
26.  printf("Enter element[%d][%d]: ", i, j);
27.  scanf("%d", &m_b[i][j]);
28.  }
29.  }

31.  for (i = 0; i < r; i++) {
32.  for (j = 0; j < c; j++) {
33.  m_c[i][j] = m_a[i][j] + m_b[i][j];
34.  }
35.  }

37.  printf("\nThe m_c of the matrices is:\n»);
38.  for (i = 0; i < r; i++) {
39.  for (j = 0; j < c; j++) {
40.  printf("%d ", m_c[i][j]);
41.  }
42.  printf("\n");
43.  }
44.  return 0;
45.  }

[C code explanation](#contents.xhtml_sc4_697a)

The C code performs matrix addition for two matrices m_a and m_b and then prints the result in matrix m_c. The library stdlib.h is used for the exit() function. Here, the user takes two matrices, m_a and m_b, as input. Then, the dimensions of both the matrices are compared. Addition can be performed if they are equal. Otherwise, an error message is printed, and the program exits using the exit() function. If the size of matrices is the same, nested for-loops are used to perform point-wise addition and are stored at the corresponding location in the m_c matrix. Finally, it prints the resulting matrix m_c using nested loops.

[Program 5.10: Check if matrix is upper triangular](#contents.xhtml_sc2_698a)

Input a matrix and check whether it is upper triangular or not.

[Sample input output](#contents.xhtml_sc3_699a)

Test case #1:

Input: [[1,1,1],[0,1,1],[0,0,1]]

Output:

Matrix is [[1, 1, 1], [0, 1, 1], [0, 0, 1]]

Matrix is upper triangular

Test case #2:

Input: [[1,1,1],[10,11,12],[0,0,1]]

Output:

Matrix is [[1, 1, 1], [10, 11, 12], [0, 0, 1]]

Matrix is not upper triangular

[Algorithm](#contents.xhtml_sc3_700a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Let a be a matrix
3.  bl= 0
4.  Iterate for i = 0 to 2

    Iterate for j = 0 to i - 1

    if a[i][j] is not equal to 0

    set bl to 1

    break out of inner loop

5.  if bl is equal to 0

    print "Matrix is upper triangular"

    else

    print "Matrix is not upper triangular"

6.  Stop

[Flowchart](#contents.xhtml_sc3_701a)

[Figure 5.10](#ch05_split_000.xhtml_fig5-10) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.10.jpg)

Figure 5.10: Flowchart illustrating the program 5.10

[Python code](#contents.xhtml_sc3_702a)

Python code for the program is as follows:

1.  a=[[1,1,1],[10,11,12],[0,0,1]]

3.  bl=0
4.  for i in range(0, 3):
5.  for j in range(0, i):
6.  if a[i][j]!=0:
7.  bl=1
8.  break

10.  print("Matrix is ", a)
11.  if bl==0:
12.  print("Matrix is upper triangular ")
13.  else:
14.  print("Matrix is not upper triangular ")

[Python code explanation](#contents.xhtml_sc4_703a)

The provided Python code checks whether a given matrix a is an upper triangular matrix. An upper triangular matrix is a square matrix in which all elements below the main diagonal (including the diagonal) are zero. Initially, the matrix is declared as a = [[1, 1, 1], [10, 11, 12], [0, 0, 1]]. The bl variable will determine whether the matrix is upper triangular. An outer loop iterates over the rows of the matrix. It runs three times since there are three rows in the 3x3 matrix. An inner loop starts and goes through the matrix’s columns inside the outer loop. It runs up to the current row index i, checking only the elements below the diagonal. If a[i][j] != 0, a non-zero element is found below the main diagonal; hence, the matrix is not upper triangular. So, bl is set to 1. The loop terminates using a break statement. Finally, outside the loop, if bl == 0, it prints that the matrix is upper triangular; otherwise, it prints that the matrix is not upper triangular.

[C code](#contents.xhtml_sc3_704a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int a[3][3] = {{1,1,1},{0,1,1},{0,0,1}};
4.  int bl = 0;

6.  for (int i = 0; i < 3; i++) {
7.  for (int j = 0; j < i; j++) {
8.  if (a[i][j] != 0) {
9.  bl = 1;
10.  break;
11.  }
12.  }
13.  if (bl == 1) {
14.  break;
15.  }
16.  }    
17.  if (bl == 0) {
18.  printf("Matrix is upper triangular\n");
19.  } else {
20.  printf("Matrix is not upper triangular\n");
21.  }    
22.  return 0;
23.  }

[C code explanation](#contents.xhtml_sc4_705a)

The C code checks whether a given matrix a is an upper triangular matrix. An upper triangular matrix is a square matrix in which all elements below the main diagonal (including the diagonal) are zero. Initially, the matrix is assigned some values. The bl variable will determine whether the matrix is upper triangular. An outer loop iterates over the rows of the matrix. It runs three times since there are three rows in the 3x3 matrix. Inside the outer loop, it starts an inner loop that iterates over the columns of the matrix. It runs up to the current row index i, checking only the elements below the diagonal. If a[i][j] != 0, a non-zero element is found below the main diagonal; hence, the matrix is not upper triangular. So, bl is set to 1. The loop terminates using the break statement. Finally, outside the loop, if bl == 0, it prints that the matrix is upper triangular; otherwise, it prints that the matrix is not upper triangular.

[Program 5.11: Check if matrix is symmetric](#contents.xhtml_sc2_706a)

Input a matrix and check whether it is symmetric or not.

[Sample input output](#contents.xhtml_sc3_707a)

Test case #1:

Input: [[1, 2, 3, 4], [3, 4, 5, 7], [5, 6, 7, 1]]

Output:

Original Matrix [[1, 2, 3, 4], [3, 4, 5, 7], [5, 6, 7, 1]]

Transposed Matrix [[1, 3, 5], [2, 4, 6], [3, 5, 7], [4, 7, 1]]

not Symmetric

Test case #2:

Input: [[1, 2, 3], [2, 3, 4], [3, 4, 6]]

Output:

Original Matrix [[1, 2, 3], [2, 3, 4], [3, 4, 6]]

Transposed Matrix [[1, 2, 3], [2, 3, 4], [3, 4, 6]]

Symmetric

[Algorithm](#contents.xhtml_sc3_708a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Let a be a matrix
3.  bl= 0
4.  Iterate for i = 0 to 2

    Iterate for j = 0 to i - 1

    if a[i][j] is not equal to a[j][i]

    set bl to 1

    break out of inner loop

5.  if bl is equal to 0

    print " Matrix is symmetric"

    else

    print " Matrix is not symmetric "

6.  Stop

[Flowchart](#contents.xhtml_sc3_709a)

[Figure 5.11](#ch05_split_000.xhtml_fig5-11) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.11.jpg)

Figure 5.11: Flowchart illustrating the program 5.11

[Python code](#contents.xhtml_sc3_710a)

Python code for the program is as follows:

1.  a=[[1, 2, 3], [2, 3, 4], [3, 4, 6]]
2.  c=[]
3.  for i in range(0, len(a[0])):
4.  t=[]
5.  for j in range(0, len(a)):
6.  t.append(a[j][i])
7.  c.append(t)
8.  del t
9.  print("Original Matrix",a)
10.  print("Transposed Matrix",c)

12.  if a==c:
13.  print("Symmetric")
14.  else:
15.  print("not Symmetric")

[Python code explanation](#contents.xhtml_sc4_711a)

The code checks whether a given matrix a is a symmetric matrix. A symmetric matrix is a square matrix with symmetric elements concerning the main diagonal. In other words, if you were to fold the matrix along its main diagonal, the elements on one side of the diagonal would match the elements on the other side. Initially, the matrix is assigned some values. Using the nested for loop, another matrix is created such that the row elements of a become the column elements of matrix c. So, the matrix c is the transposed matrix of a. Now, if a and c are the same, the matrix a is symmetric. Otherwise not.

[C code](#contents.xhtml_sc3_712a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int a_s[3][3] = {{5,5,5},{0,5,5},{0,0,5}};
4.  int bl = 0; int i, j;

6.  for (ii = 0; ii < 3; ii++) {
7.  for (jj = 0; jj < ii; jj++) {
8.  if (a_s[ii][jj] !=a_s[jj][ii]) {
9.  bl = 1;
10.  break;
11.  }
12.  }
13.  if (bl == 1) {
14.  break;
15.  }
16.  }    
17.  if (bl == 0) {
18.  printf("Matrix is symmetric \n");
19.  } else {
20.  printf("Matrix is not symmetric \n");
21.  }    
22.  return 0;
23.  }

[C code explanation](#contents.xhtml_sc4_713a)

The code checks whether a given matrix a_s is symmetric. A symmetric matrix is a square matrix with symmetric elements for the main diagonal. In other words, if you were to fold the matrix along its main diagonal, the elements on one side of the diagonal would match the elements on the other side. Initially, the matrix is assigned some values. The bl variable will determine if the matrix is symmetric. An outer loop iterates over the rows of the matrix. It runs three times since there are three rows in the 3x3 matrix. Inside the outer loop, it starts an inner loop that iterates over the columns of the matrix. It runs up to the current row index ii, checking only the elements below the diagonal. If a_s[ii][jj] != a_s[jj][ii], it means that elements are not the same along the main diagonal fold, and hence, the matrix is not symmetric. So, bl is set to 1. The loop terminates using a break statement. Finally, outside the loop, if bl == 0, it prints that the matrix is symmetric; otherwise, it prints that the matrix is not symmetric.

[Program 5.12: Print 2-D pattern 1](#contents.xhtml_sc2_714a)

Print the patterns (with n rows) as shown:

| $ |  |  |  |  |
| $ | $ |  |  |  |
| $ | $ | $ |  |  |
| $ | $ | $ | $ |  |
| $ | $ | $ | $ | $ |

[Sample input output](#contents.xhtml_sc3_715a)

Test case #1:

Input: 5

Output:

| $ |  |  |  |  |
| $ | $ |  |  |  |
| $ | $ | $ |  |  |
| $ | $ | $ | $ |  |
| $ | $ | $ | $ | $ |

[Algorithm](#contents.xhtml_sc3_716a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as nn
3.  Iterate for ii =1 to nn

    Iterate for jj = 1 to ii

    Print "$"

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_717a)

[Figure 5.12](#ch05_split_000.xhtml_fig5-12) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.12.jpg)

Figure 5.12: Flowchart illustrating the program 5.12

[Python code](#contents.xhtml_sc3_718a)

Python code for the program is as follows:

1.  nn= int(input("Enter a number"))
2.  for ii in range(1,nn+1):
3.  for jj in range(1, ii+1):
4.  print("$", end=" ")
5.  print("\n")

[Python code explanation](#contents.xhtml_sc4_719a)

The number of rows is taken as input from the user and stored in nn. The first loop runs n times, with ii taking on values from 1 to nn. The second loop runs ii times, with jj taking on values from 1 to ii. Inside the second loop, an asterisk is printed without a newline character (end=" " means to end the print statement with a space instead of a newline). After the second loop completes, a newline character is printed to move to the next row.

[C code](#contents.xhtml_sc3_720a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int nn;
4.  printf("Enter a number: ");
5.  scanf("%d", &nn);

7.  for (int ii = 1; ii <= nn; ii++) {
8.  for (int jj = 1; jj <= ii; jj++) {
9.  printf("$ «);
10.  }
11.  printf("\n");
12.  }    
13.  return 0;
14.  }

[C code explanation](#contents.xhtml_sc4_721a)

This C code uses the same logic as the Python code to print a triangle of asterisks with n rows. The scanf() function reads the user input for n, and the printf() function displays the asterisks and newline characters. The for loops work the same way as in the Python code, with the variables ii and jj taking on the values necessary to create the correct pattern of asterisks.

[Program 5.13: Print 2-D pattern 2](#contents.xhtml_sc2_722a)

Print the patterns (with n rows) shown:

| 1 |  |  |  |  |
| 2 | 2 |  |  |  |
| 3 | 3 | 3 |  |  |
| 4 | 4 | 4 | 4 |  |
| 5 | 5 | 5 | 5 | 5 |

[Sample input output](#contents.xhtml_sc3_723a)

Test case #1:

Input: 5

Output:

| 1 |  |  |  |  |
| 2 | 2 |  |  |  |
| 3 | 3 | 3 |  |  |
| 4 | 4 | 4 | 4 |  |
| 5 | 5 | 5 | 5 | 5 |

[Algorithm](#contents.xhtml_sc3_724a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as nn
3.  Iterate for ii =1 to nn

    Iterate for jj = 1 to ii

    Print ii

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_725a)

[Figure 5.13](#ch05_split_000.xhtml_fig5-13) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.13.jpg)

Figure 5.13: Flowchart illustrating the program 5.13

[Python code](#contents.xhtml_sc3_726a)

Python code for the program is as follows:

1.  nn= int(input("Enter a number"))
2.  for ii in range(1,nn+1):
3.  for jj in range(1, ii+1):
4.  print(ii, end=" ")
5.  print("\n")

[Python code explanation](#contents.xhtml_sc4_727a)

The program is the same as the previous one, and the only difference is that instead of $, the value of ii is printed.

[C code](#contents.xhtml_sc3_728a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int nn;
4.  printf("Enter a number: ");
5.  scanf("%d", &nn);

7.  for (int ii = 1; ii <= nn; ii++) {
8.  for (int jj = 1; jj <= ii; jj++) {
9.  printf("%d ", ii);
10.  }
11.  printf("\n");
12.  }    
13.  return 0;
14.  }

[C code explanation](#contents.xhtml_sc4_729a)

The program is the same as the previous one, and the only difference is that instead of $, the value of ii is printed.

[Program 5.14: Print 2-D pattern 3](#contents.xhtml_sc2_730a)

Print the patterns (with n rows) shown:

| 1 |  |  |  |  |
| 1 | 2 |  |  |  |
| 1 | 2 | 3 |  |  |
| 1 | 2 | 3 | 4 |  |
| 1 | 2 |  |  |  |

| 3 | 4 | 5 |

[Sample input output](#contents.xhtml_sc3_731a)

Test case #1:

Input: 5

Output:

| 1 |  |  |  |  |
| 1 | 2 |  |  |  |
| 1 | 2 | 3 |  |  |
| 1 | 2 | 3 | 4 |  |
| 1 | 2 | 3 | 4 | 5 |

[Algorithm](#contents.xhtml_sc3_732a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as nn
3.  Iterate for ii =1 to n

    Iterate for jj = 1 to ii

    Print jj

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_733a)

[Figure 5.14](#ch05_split_001.xhtml_fig5-14) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.14.jpg)

Figure 5.14: Flowchart illustrating the program 5.14

[Python code](#contents.xhtml_sc3_734a)

Python code for the program is as follows:

1.  nn= int(input("Enter a number"))
2.  for ii in range(1,nn+1):
3.  for jj in range(1, ii+1):
4.  print(jj, end=" ")
5.  print("\n")

[Python code explanation](#contents.xhtml_sc4_735a)

The program is the same as the previous one, and the only difference is that instead of the same value in the whole row, the value of jj is now printed to print 1,2,3,….

[C code](#contents.xhtml_sc3_736a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int nn;
4.  printf("Enter a number: ");
5.  scanf("%d", &nn);    
6.  for (int ii = 1; ii <= nn; ii++) {
7.  for (int jj = 1; jj <= ii; jj++) {
8.  printf("%d ", jj);
9.  }
10.  printf("\n");
11.  }    
12.  return 0;
13.  }

[C code explanation](#contents.xhtml_sc4_737a)

The program is the same as the previous one, and the only difference is that instead of the same value in the whole row, the value of jj is now printed to print 1,2,3,….

[Program 5.15: Print 2-D pattern 4](#contents.xhtml_sc2_738a)

Print the patterns (with n rows) shown:

| $ | $ | $ | $ | $ |
| $ | $ | $ | $ |  |
| $ | $ | $ |  |  |
| $ | $ |  |  |  |
| $ |  |  |  |  |

[Sample input output](#contents.xhtml_sc3_739a)

Test case #1:

Input: 5

Output:

| $ | $ | $ | $ | $ |
| $ | $ | $ | $ |  |
| $ | $ | $ |  |  |
| $ | $ |  |  |  |
| $ |  |  |  |  |

[Algorithm](#contents.xhtml_sc3_740a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as n
3.  Iterate for ii =1 to n

    Iterate for jj = 1 to n-ii+1

    Print "$"

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_741a)

[Figure 5.15](#ch05_split_001.xhtml_fig5-15) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.15.jpg)

Figure 5.15: Flowchart illustrating the program 5.15

[Python code](#contents.xhtml_sc3_742a)

Python code for the program is as follows:

1.  n= int(input("Enter a number"))
2.  for ii in range(1,n+1):
3.  for jj in range(1, n-ii+2):
4.  print("$", end=" ")
5.  print("\n")

[Python code explanation](#contents.xhtml_sc4_743a)

It should be observed that the pattern is reversed as compared to the previous program. Hence, the inner loop executes n-ii+1 times for each value of i. The rest of the logic remains the same.

[C code](#contents.xhtml_sc3_744a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n;
4.  printf("Enter a number: ");
5.  scanf("%d", &n);    
6.  for (int ii = 1; ii <= n; ii++) {
7.  for (int jj = 1; jj <= n-ii+1; jj++) {
8.  printf("$ «);
9.  }
10.  printf("\n");
11.  }    
12.  return 0;
13.  }

[C code explanation](#contents.xhtml_sc4_745a)

It should be observed that the pattern is reversed as compared to the previous program. Hence, the inner loop executes n-ii+1 times for each value of i. The rest of the logic remains the same.

[Program 5.16: Print 2-D pattern 5](#contents.xhtml_sc2_746a)

Print the patterns (with n rows) shown:

|  |  |  |  | $ |
|  |  |  | $ | $ |
|  |  | $ | $ | $ |
|  | $ | $ | $ | $ |
| $ | $ | $ | $ | $ |

[Sample input output](#contents.xhtml_sc3_747a)

Test case #1:

Input: 5

Output:

|  |  |  |  | $ |
|  |  |  | $ | $ |
|  |  | $ | $ | $ |
|  | $ | $ | $ | $ |
| $ | $ | $ | $ | $ |

[Algorithm](#contents.xhtml_sc3_748a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as n
3.  Iterate for i =1 to n

    Iterate for j = 1 to n-i+1

    Print " "

    Iterate for k = 1 to i

    Print "$"

4.  Print newline
5.  Stop

[Flowchart](#contents.xhtml_sc3_749a)

[Figure 5.16](#ch05_split_001.xhtml_fig5-16) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.16.jpg)

Figure 5.16: Flowchart illustrating the program 5.16

[Python code](#contents.xhtml_sc3_750a)

Python code for the program is as follows:

1.  n= int(input("Enter a number"))
2.  for i in range(1,n+1):
3.  for j in range(1, n-i+1):
4.  print(" ", end=" ")
5.  for k in range(1, i+1):
6.  print("$", end=" ")
7.  print("\n")

[Python code explanation](#contents.xhtml_sc4_751a)

Here, the pattern is right aligned. That means a blank space needs to be printed before printing the character. Hence, inside the outer loop, there are two inner loops consecutively. The first inner loop prints the blank space followed by $, to be printed by the second for-loop for each iteration.

[C code](#contents.xhtml_sc3_752a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n;
4.  printf("Enter a number: ");
5.  scanf("%d", &n);    
6.  for (int i = 1; i <= n; i++) {
7.  for (int j = 1; j <= n-i; j++) {
8.  printf("  ");
9.  }
10.  for (int k = 1; k <= i; k++) {
11.  printf("$ «);
12.  }
13.  printf("\n");
14.  }    
15.  return 0;
16.  }

[C code explanation](#contents.xhtml_sc4_753a)

Here, the pattern is right aligned. That means a blank space needs to be printed before printing the character. Hence, inside the outer loop, there are two inner loops consecutively. The first inner loop prints the blank space followed by $, to be printed by the second for-loop for each iteration.

[Program 5.17: Print 2-D pattern 6](#contents.xhtml_sc2_754a)

Print the patterns (with n rows) shown:

|  |  |  |  | $ |  |  |  |  |
|  |  |  | $ | $ | $ |  |  |  |
|  |  | $ | $ | $ | $ | $ |  |  |
|  | $ | $ | $ | $ | $ | $ | $ |  |
| $ | $ | $ | $ | $ | $ | $ | $ | $ |

[Sample input output](#contents.xhtml_sc3_755a)

Test case #1:

Input: 5

Output:

|  |  |  |  | $ |  |  |  |  |
|  |  |  | $ | $ | $ |  |  |  |
|  |  | $ | $ | $ | $ | $ |  |  |
|  | $ | $ | $ | $ | $ | $ | $ |  |
| $ | $ | $ | $ | $ | $ | $ | $ | $ |

[Algorithm](#contents.xhtml_sc3_756a)

To run the above program, the following steps need to be followed:

1.  Start
2.  Enter a number as n
3.  Iterate for i =1 to n

    Iterate for j = 1 to n-i+1

    Print " "

    Iterate for k = 1 to i

    Print "$"

    Iterate for l = 1 to i-1

    Print "$"

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_757a)

[Figure 5.17](#ch05_split_001.xhtml_fig5-17) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.17.jpg)

Figure 5.17: Flowchart illustrating the program 5.17

[Python code](#contents.xhtml_sc3_758a)

Python code for the program is as follows:

1.  n= int(input("Enter a number"))
2.  for i in range(1,n+1):
3.  for j in range(1, n-i+1):
4.  print(" ", end=" ")
5.  for k in range(1, i+1):
6.  print("$", end=" ")
7.  for j in range(1, i):
8.  print("$", end=" ")
9.  print("\n")

[Python code explanation](#contents.xhtml_sc4_759a)

In this program, the pattern is center-aligned. The first two inner loops in each row are the same as the previous program to print the blank space, then right-aligned $. The third inner for-loop is used to print the remaining $.

[C code](#contents.xhtml_sc3_760a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n;
4.  printf("Enter a number: ");
5.  scanf("%d", &n);
6.  for (int i = 1; i <= n; i++) {
7.  for (int j = 1; j <= n - i; j++) {
8.  printf("  ");
9.  }
10.  for (int k = 1; k <= i; k++) {
11.  printf("$ « );
12.  }
13.  for (int j = 1; j < i; j++) {
14.  printf("$ «);
15.  }
16.  printf("\n");
17.  }
18.  return 0;
19.  }

[C code explanation](#contents.xhtml_sc4_761a)

In this program, the pattern is center-aligned. The first two inner loops in each row are the same as the previous program to print the blank space, then right-aligned $. The third inner for-loop is used to print the remaining $.

[Program 5.18: Print 2-D pattern 7](#contents.xhtml_sc2_762a)

Print the patterns (with n rows) shown:

|  |  |  |  | 1 |  |  |  |  |
|  |  |  | 2 | 2 | 2 |  |  |  |
|  |  | 3 | 3 | 3 | 3 | 3 |  |  |
|  | 4 | 4 | 4 | 4 | 4 | 4 | 4 |  |
| 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |

[Sample input output](#contents.xhtml_sc3_763a)

Test case #1:

Input: 5

Output:

|  |  |  |  | 1 |  |  |  |  |
|  |  |  | 2 | 2 | 2 |  |  |  |
|  |  | 3 | 3 | 3 | 3 | 3 |  |  |
|  | 4 | 4 | 4 | 4 | 4 | 4 | 4 |  |
| 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |

[Algorithm](#contents.xhtml_sc3_764a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as n
3.  Iterate for i =1 to n

    Iterate for j = 1 to n-i

    Print " "

    Iterate for k = 1 to i

    Print i

    Iterate for l = 1 to i-1

    Print i

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_765a)

[Figure 5.18](#ch05_split_001.xhtml_fig5-18) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.18.jpg)

Figure 5.18: Flowchart illustrating the program 5.18

[Python code](#contents.xhtml_sc3_766a)

Python code for the program is as follows:

1.  n= int(input("Enter a number"))
2.  for i in range(1,n+1):
3.  for j in range(1, n-i+1):
4.  print(" ", end=" ")
5.  for k in range(1, i+1):
6.  print(i, end=" ")
7.  for j in range(1, i):
8.  print(i, end=" ")
9.  print("\n")

[Python code explanation](#contents.xhtml_sc4_767a)

This program is the same as the previous one. The only difference is to print the row number instead of $.

[C code](#contents.xhtml_sc3_768a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n;
4.  printf("Enter a number: ");
5.  scanf("%d", &n);
6.  for (int i = 1; i <= n; i++) {
7.  for (int j = 1; j <= n - i; j++) {
8.  printf("  ");
9.  }
10.  for (int k = 1; k <= i; k++) {
11.  printf("%d ", i);
12.  }
13.  for (int j = 1; j < i; j++) {
14.  printf("%d ", i);
15.  }
16.  printf("\n");
17.  }
18.  return 0;
19.  }

[C code explanation](#contents.xhtml_sc4_769a)

This program is the same as the previous one. The only difference is to print the row number instead of $.

[Program 5.19: Print 2-D pattern 8](#contents.xhtml_sc2_770a)

Print the patterns (with n rows) shown:

|  |  |  |  | 1 |  |  |  |  |
|  |  |  | 1 | 2 | 1 |  |  |  |
|  |  | 1 | 2 | 3 | 2 | 1 |  |  |
|  | 1 | 2 | 3 | 4 | 3 | 2 | 1 |  |
| 1 | 2 | 3 | 4 | 5 | 4 | 3 | 2 | 1 |

[Sample input output](#contents.xhtml_sc3_771a)

Test case #1:

Input: 5

Output:

|  |  |  |  | 1 |  |  |  |  |
|  |  |  | 1 | 2 | 1 |  |  |  |
|  |  | 1 | 2 | 3 | 2 | 1 |  |  |
|  | 1 | 2 | 3 | 4 | 3 | 2 | 1 |  |
| 1 | 2 | 3 | 4 | 5 | 4 | 3 | 2 | 1 |

Algorithm

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as n
3.  Iterate for i =1 to n

    Iterate for j = 1 to n-i

    Print " "

    Iterate for k = 1 to i

    Print k

    Iterate for l = 1 to i-1

    Print k-1

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_772a)

[Figure 5.19](#ch05_split_001.xhtml_fig5-19) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.19.jpg)

Figure 5.19: Flowchart illustrating the program 5.19

[Python code](#contents.xhtml_sc3_773a)

Python code for the program is as follows:

1.  n= int(input("Enter a number"))
2.  for i in range(1,n+1):
3.  for j in range(1, n-i+1):
4.  print(" ", end=" ")
5.  for k in range(1, i+1):
6.  print(k, end=" ")
7.  for l in range(1, i):
8.  print(k-l, end=" ")
9.  print("\n")

[Python code explanation](#contents.xhtml_sc4_774a)

This program is the same as the previous one. The only difference is to print the column number instead of $.

[C code](#contents.xhtml_sc3_775a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n, i,j,k,l;
4.  printf("Enter a number: ");
5.  scanf("%d", &n);

7.  for (i = 1; i <= n; i++) {
8.  for ( j = 1; j <= n - i; j++) {
9.  printf("  ");
10.  }
11.  for (k = 1; k <= i; k++) {
12.  printf("%d ", k);
13.  }
14.  for (l = 1; l < i; l++) {
15.  printf("%d ", k-l-1);
16.  }
17.  printf("\n");
18.  }
19.  return 0;
20.  }

[C code explanation](#contents.xhtml_sc4_776a)

This program is the same as the previous one. The only difference is to print the column number instead of $.

[Program 5.20: Print 2-D pattern 9](#contents.xhtml_sc2_777a)

Print the patterns (with n rows) shown:

| 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |
|  | 4 | 4 | 4 | 4 | 4 | 4 | 4 |  |
|  |  | 3 | 3 | 3 | 3 | 3 |  |  |
|  |  |  | 2 | 2 | 2 |  |  |  |
|  |  |  |  | 1 |  |  |  |  |

[Sample input output](#contents.xhtml_sc3_778a)

Test case #1:

Input: 5

Output:

| 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |
|  | 4 | 4 | 4 | 4 | 4 | 4 | 4 |  |
|  |  | 3 | 3 | 3 | 3 | 3 |  |  |
|  |  |  | 2 | 2 | 2 |  |  |  |
|  |  |  |  | 1 |  |  |  |  |

[Algorithm](#contents.xhtml_sc3_779a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Enter a number as n
3.  Iterate for i =1 to n

    Iterate for j = 1 to i-1

    Print " "

    Iterate for k = 1 to n-i+1

    Print n-i+1

    Iterate for l = 1 to n-i

    Print n-i+1

    Print newline

4.  Stop

[Flowchart](#contents.xhtml_sc3_780a)

[Figure 5.20](#ch05_split_001.xhtml_fig5-20) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_5.20.jpg)

Figure 5.20: Flowchart illustrating the program 5.20

[Python code](#contents.xhtml_sc3_781a)

Python code for the program is as follows:

1.  n= int(input("Enter a number"))
2.  for i in range(1,n+1): 
3.  for k in range(1, i):
4.  print(" ", end=" ")
5.  for j in range(1, n-i+2):
6.  print(n-i+1, end=" ")
7.  for l in range(1, n-i+1):
8.  print(n-i+1, end=" ")
9.  print("\n")

[Python code explanation](#contents.xhtml_sc4_782a)

The program is similar to the earlier program. So, the same logic is applied.

[C code](#contents.xhtml_sc3_783a)

C code for the program is as follows:

1.  #include <stdio.h>
2.  int main() {
3.  int n;
4.  printf("Enter a number: ");
5.  scanf("%d", &n);

7.  for (int i = 1; i <= n; i++) {
8.  for (int k = 1; k < i; k++) {
9.  printf(" ");
10.  }
11.  for (int j = 1; j <= n - i + 1; j++) {
12.  printf("%d ", n - i + 1);
13.  }
14.  for (int l = 1; l < n - i + 1; l++) {
15.  printf("%d ", n - i + 1);
16.  }
17.  printf("\n");
18.  }
19.  return 0;
20.  }

[C code explanation](#contents.xhtml_sc4_784a)

The program is similar to the earlier program. So, the same logic is applied.

[Conclusion](#contents.xhtml_sc2_785a)

This chapter has discussed complex logic building using various programming constructs like flowcharts, algorithms, and coding. With the help of several examples, the different flavors of multiple steps, conditional logic, loops, lists, and matrices are presented. In the next chapter, real-world problems will be discussed with the help of a good number of solved examples.

[Points to remember](#contents.xhtml_sc2_786a)

*   Math.h library includes the basic functions of math in C Programming. The counter module in Python is C.
*   A list (in Python) or array (in C) is a collection of homogenous elements that can be accessed using indices.
*   A matrix is a 2-D array represented with the help of rows and columns.
*   Logic to display various patterns can be developed by visualizing the pattern as a matrix.

[Questions](#contents.xhtml_sc2_787a)

1. Check if the reversed number is greater than the number.

2. Check if the input number is palindrome or not.

3. Given n numbers, find the first pair of two neighboring elements with the same sign. For example, l1= {1, -1, -5, 2, 3, -8}, output is (-1, -5).

4. Check whether a given number is an Armstrong number or not. [Example: A 3-digit number N is an Armstrong number if N=X^3+Y^3+Z^3, where X, Y, and Z are individual digits of the number N].

5. Input a matrix and print its transpose.

6. Convert Base 2 number to Base 10\. (For example, (101)2 = (5)10).

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](OPS/images/fm1.png)

# [CHAPTER 6Real World Problems](#contents.xhtml_ch06a)

[Introduction](#contents.xhtml_sc2_788a)

In this chapter, the real-world problems/puzzles using various programming constructs (as discussed in previous chapters) are discussed. The main focus of the chapter is to map real-world problems to already-studied concepts. The chapter presents the problems that require intricate design using simple programming constructs. Once the mapping is understood, the programming becomes simple. The chapter discusses creating a logical flow for solving real-world problems, including algorithms and flowcharts, to plan solutions before writing code.

[Structure](#contents.xhtml_sc2_789a)

In this chapter, there are a total of 10 programs, and five sub-sections complement each program:

*   Understand the program objective with sample test cases consisting of inputs and outputs. It will give the user an understanding of what kind of user input is expected and what result will be projected for a particular program.
*   Understand the program with an algorithm. This will help the user understand the logical flow of real-world problems.
*   Visualize the program flow with flowcharts. Program objectives can be understood easily with the flowchart representation. Users will understand which symbols to use in which context throughout different program’s flowchart representations.
*   Python source code of each program. Each program’s source code in Python programming language is provided to the user so the user can understand the basic operations of the language. An explanation of each code is also provided.
*   C implementation of each program. Users can learn the basic concepts of C language with the provided C language code and its explanation for every program.

[Objectives](#contents.xhtml_sc2_790a)

In this chapter, readers will explore techniques for solving real-world problems that often involve multiple sequential steps, intricate combinations of conditional statements and nested loops, and manipulating data structures like lists and functions. The main objective is to demonstrate how a real-world problem can be mapped to already studied concepts. Further, how to utilize simple conditional and loop statements to solve even complex real-world problems.

[Program 6.1: Optimize book storage](#contents.xhtml_sc2_791a)

An almirah can have m number of bags, and each bag can hold n number of books. Take the capacity of the almirah and bag (m and n) as input from the user. Also, take input the number of books the user has (in variable a). Then, calculate the number of bags and almirahs required to store a books.

[Sample input output](#contents.xhtml_sc3_792a)

Test case #1:

Input: Enter the capacity of the almirah: 5

Enter the capacity of the bag: 10

Enter the number of books the user has: 79

Output:

8 bags and 2 almirahs are required.

Test case #2:

Input: Enter the capacity of the almirah: 15

Enter the capacity of the bag: 4

Enter the Number of books the user has: 987

Output:

247 bags and 17 almirahs are required.

[Algorithm](#contents.xhtml_sc3_793a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read the capacity of the almirah as cap_al
3.  Read the capacity of the bag as cap_bag
4.  Read the number of books the user has as book
5.  n_bag=ceiling_value(book/cap_bag)
6.  n_al=ceiling_value(n_bag/cap_al)
7.  Display n_bag, " bags and ",n_al, " almirahs are required."
8.  Stop

[Flowchart](#contents.xhtml_sc3_794a)

[Figure 6.1](#ch06.xhtml_fig6-1) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.1.jpg)

Figure 6.1: Flowchart illustrating the program 6.1

[Python code](#contents.xhtml_sc3_795a)

Python code for the program is as follows:

1.  import math

3.  cap_al= int(input("Enter the capacity of the almirah: "))
4.  cap_bag= int(input("Enter the capacity of the bag: "))
5.  book= int(input("Enter the number of books user have: "))
6.  n_bag=math.ceil(book/cap_bag)
7.  n_al=math.ceil(n_bag/cap_al)

9.  print(n_bag, " bags and ", n_al, " almirah are required.")

[Python code explanation](#contents.xhtml_sc4_796a)

This Python code calculates the number of bags and almirahs required to store a given number of books based on the input capacities of the bags and almirah. The math module provides mathematical functions, and it is imported at the beginning of the code to use the ceil() function later. The user is prompted to enter the almirah’s capacity, the bag’s capacity, and the total number of books. The total number of bags required is calculated by dividing the total number of books by the capacity of each bag (cap_bag). The math.ceil() function rounds up the division result to the nearest whole number, ensuring enough bags to accommodate all the books. Similarly, the number of almirahs required is calculated by dividing the number of bags (n_bag) by the capacity of each almirah (cap_al). Finally, based on the input capacities, the code prints the number of bags and almirahs required to store the given number of books.

[C code](#contents.xhtml_sc3_797a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  #include<math.h>

4.  int  main()
5.  {
6.  int cap_al, cap_bag, book, n_bag, n_al;
7.  printf("Enter the capacity of the almirah: ");
8.  scanf("%d", &cap_al);

10.  printf("Enter the capacity of the bag: ");
11.  scanf("%d", &cap_bag);

13.  printf("Enter the Number of books user have: ");
14.  scanf("%d", &book);

16.  n_bag=ceil(book/(float)cap_bag);
17.  n_al=ceil(n_bag/(float)cap_al);

19.  printf("%d bags and %d almirah are required.", n_bag, n_al);
20.  return  0;
21.  }

[C code explanation](#contents.xhtml_sc4_798a)

This code calculates the number of bags and almirahs required to store a given number of books based on the input capacities of the bags and almirah. The math.h library provides mathematical functions, and it is imported at the beginning of the code to use the ceil() function later. The user is prompted to enter the almirah’s capacity, the bag’s capacity, and the total number of books. The total number of bags required is calculated by dividing the total number of books by the capacity of each bag (cap_bag). The denominator is typecast to float number to perform real value division. The math.ceil() function rounds up the division result to the nearest whole number, ensuring enough bags to accommodate all the books. Similarly, the number of almirahs required is calculated by dividing the number of bags (n_bag) by the capacity of each almirah (cap_al). Finally, based on the input capacities, the code prints the number of bags and almirahs required to store the given number of books.

[Program 6.2: Identify living creatures](#contents.xhtml_sc2_799a)

Identify a living creature (human, bird, or animal) based on features like the number of legs and feathers.

[Sample input output](#contents.xhtml_sc3_800a)

Test case #1:

Input: Enter the number of legs: 2

Enter if it has feather: y

Output: Bird

Test case #2:

Input: Enter the number of legs: 4

Enter if it has feather: n

Output: Animal

Test case #3:

Input: Enter the number of legs: 4

Enter if it has feather: y

Output: No such creature exists.

[Algorithm](#contents.xhtml_sc3_801a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read the number of legs as l
3.  Read if it has feather:as f
4.  If l == 2:
    1.  if f == 'y':
        1.  Display("Bird")
    2.  else:
        1.  Display("Human")
5.  Else if l == 4:
    1.  if f == 'n':
        1.  Display("Animal")
    2.  else:
        1.  Display("No such creature exists.")
6.  Else:
    1.  Display("No such creature exists.")
7.  Stop

[Flowchart](#contents.xhtml_sc3_802a)

[Figure 6.2](#ch06.xhtml_fig6-2) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.2.jpg)

Figure 6.2: Flowchart illustrating the program 6.2

[Python code](#contents.xhtml_sc3_803a)

Python code for the program is as follows:

1.  l=int(input("Enter the number of legs:"))
2.  f= input("Enter if it has feather:")
3.  if l == 2:
4.  if f == 'y':
5.  print("Bird")
6.  else:
7.  print("Human")
8.  elif l == 4:
9.  if f == 'n':
10.  print("Animal")
11.  else:
12.  print("No such creature exists.")
13.  else:
14.  print("No such creature exists.")

[Python code explanation](#contents.xhtml_sc4_804a)

The given code determines the type of creature based on the number of legs and the presence of feathers. First, it prompts the user to enter the number of legs of the creature and asks whether the creature has feathers, with the user entering y for yes or n for no. The type of creature is determined using the nested if- elif-else statements.

[C code](#contents.xhtml_sc3_805a)

C code for the program is as follows:

1.  #include<stdio.h>

3.  int  main()
4.  {
5.  int l;
6.  char f;

8.  printf("Enter the number of legs: ");
9.  scanf("%d", &l);

11.  fflush(stdin);

13.  printf("Enter if it has feather: ");
14.  scanf(" %c", &f);

17.  if(l == 2)
18.  {
19.  if (f == 'y')
20.  printf("Bird");
21.  else
22.  printf("Human");
23.  }
24.  else  if(l == 4)
25.  {
26.  if(f == 'n')
27.  printf("Animal");
28.  else
29.  printf("No such creature exists.");
30.  }
31.  else
32.  printf("No such creature exists.");
33.  return  0;
34.  }

[C code explanation](#contents.xhtml_sc4_806a)

The given code determines the type of creature based on the number of legs and the presence of feathers. First, it prompts the user to enter the number of legs of the creature and asks whether the creature has feathers, with the user entering y for yes or n for no. Since the value of the feather is to be read in character, fflush() function is used before the scanf() function to clear the input buffer. The type of creature is determined using the nested if- elseif-else statements.

[Program 6.3: Identify objects](#contents.xhtml_sc2_807a)

Take features such as shape and color as input and identify the object based on its shape and color as follows:

Sphere and red: Tomato

Sphere and orange: Orange

Cuboid and red: Brick

Cuboid and orange: Dustbin

[Sample input output](#contents.xhtml_sc3_808a)

Test case #1:

Input: Enter the shape of the object (s/ c): s

Enter the color of the object (r /o): o

Output: Object is Orange

Test case #2:

Input: Enter the shape of the object (s/ c): c

Enter the color of the object (r /o): o

Output: Object is Dustbin

[Algorithm](#contents.xhtml_sc3_809a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read the shape of the object as s
3.  Read the color of the object as co
4.  if s== "s":
    1.  if co == "r":
        1.  Display("Object is Tomato")
    2.  Else if co=="o":
        1.  Display("Object is Orange")
    3.  Else:
        1.  Display("Wrong input")
5.  Else if s == "c":
    1.  if co == "r":
        1.  Display("Object is Brick")
    2.  Else if co=="o":
        1.  Display("Object is Dustbin")
    3.  Else:
        1.  Display("Wrong input")
6.  Else:
    1.  Display("Wrong input")
7.  Stop

[Flowchart](#contents.xhtml_sc3_810a)

[Figure 6.3](#ch06.xhtml_fig6-3) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.3.jpg)

Figure 6.3: Flowchart illustrating the program 6.3

[Python code](#contents.xhtml_sc3_811a)

Python code for the program is as follows:

1.  s=input("Enter the shape of the object:")
2.  co= input("Enter the color of the object:")
3.  if s== "s":
4.  if co == "r":
5.  print("Object is Tomato")
6.  elif co=="o":
7.  print("Object is Orange")
8.  else:
9.  print("Wrong input")
10.  elif s == "c":
11.  if co == "r":
12.  print("Object is Brick")
13.  elif co=="o":
14.  print("Object is Dustbin")
15.  else:
16.  print("Wrong input")
17.  else:
18.  print("Wrong input")

[Python code explanation](#contents.xhtml_sc4_812a)

This code allows a user to input the shape and color of an object and then identify the object based on the given shape and color using a nested if-elif-else statement. It prompts the user to enter the shape and color of the object. Following various conditions, it identifies the object and displays it.

[C code](#contents.xhtml_sc3_813a)

C code for the program is as follows:

1.  int  main()
2.  {
3.  char s, co;

5.  fflush(stdin);
6.  printf("Enter the shape of the object (s/ c): ");
7.  scanf("%c", &s);

9.  fflush(stdin);
10.  printf("Enter the color of the object (r /o): ");
11.  scanf("%c", &co);

13.  if(s== 's')
14.  {
15.  if(co == 'r')
16.  printf("Object is Tomato");
17.  else  if(co == 'o')
18.  printf("Object is Orange");
19.  else
20.  printf("Wrong input");
21.  }
22.  else  if(s == 'c')
23.  {
24.  if(co == 'r')
25.  printf("Object is Brick");
26.  else  if(co == 'o')
27.  printf("Object is Dustbin");
28.  else
29.  printf("Wrong input");
30.  }
31.  else
32.  printf("Wrong input");

34.  }

[C code explanation](#contents.xhtml_sc4_814a)

This code allows a user to input the shape and color of an object and then identify the object based on the given shape and color using a nested if-else if-else statement. It prompts the user to enter the shape and color of the object. Following various conditions, it identifies the object and displays it. Like the previous program, wherever we read a character as input from the user, fflush() function is used before the scanf() function to clear the input buffer.

[Program 6.4: Rock-paper-scissors](#contents.xhtml_sc2_815a)

Make a two-player rock-paper-scissors game.

Hint: Ask for player plays (using input), compare them, print out a message of congratulations to the winner, and ask if the players want to start a new game.

The rules of the game are:

*   Rock beats scissors
*   Scissors beat paper
*   Paper beats rock

| Player 1 | Player 2 | Output |
| Scissor | Scissor | Tie |
| Scissor | Stone | Player 2 |
| Scissor | Paper | Player 1 |
| Stone | Scissor | Player 1 |
| Stone | Stone | Tie |
| Stone | Paper | Player 2 |
| Paper | Scissor | Player 2 |
| Paper | Stone | Player 1 |
| Paper | Paper | Tie |

[Sample input output](#contents.xhtml_sc3_816a)

Test case #1:

Input: Enter signs of the game: s for scissor, p for paper, r for stone: s s

Output: There is a tie

Test case #2:

Input: Enter signs of the game: s for scissor, p for paper, r for stone: s p

Output: x is the winner

[Algorithm](#contents.xhtml_sc3_817a)

To run the above program, the following steps needed to be followed:

1.  Start
2.  Input x and y
3.  if (x== "scissor" and y== "paper") or (x== "stone" and y== "scissor") or (x== "paper" and y== "stone") then
    1.  Print "x is the winner"
4.  Else if (y== "scissor" and x== "paper") or (y== "stone" and x== "scissor") or (y== "paper" and x== "stone") then
    1.  Print "y is the winner"
5.  Else if (x== "scissor" and y== "scissor") or (x== "stone" and y== "stone") or (x== "paper" and y== "paper") then
    1.  Print "There is a tie"
6.  Stop

[Flowchart](#contents.xhtml_sc3_818a)

[Figure 6.4](#ch06.xhtml_fig6-4) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.4.jpg)

Figure 6.4: Flowchart illustrating the program 6.4

[Python code](#contents.xhtml_sc3_819a)

Python code for the program is as follows:

1.  x=input("Enter first sign of the game ")
2.  y=input("Enter second sign of the game ")
3.  if (x== "scissor"  and y== "paper") or (x== "stone"  and y== "scissor") or (x== "paper"  and y== "stone"):
4.  print( "x is the winner")
5.  elif (y== "scissor"  and x== "paper") or (y== "stone"  and x== "scissor") or (y== "paper"  and x== "stone") :
6.  print("y is the winner")
7.  elif (x== "scissor"  and y== "scissor") or (x== "stone"  and y== "stone") or (x== "paper"  and y== "paper"):
8.  print( "There is a tie")

[Python code explanation](#contents.xhtml_sc4_820a)

This Python code represents a simple rock-paper-scissors game where the user inputs their choice of signs (scissor, stone, or paper), and the program determines the winner based on the rules of the game using if-elif-else statements. Inside the condition block of an if-statement, various conditions are combined using or/ and operators.

[C code](#contents.xhtml_sc3_821a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  void  main()
3.  {
4.  char x,y;
5.  fflush(stdin);
6.  printf("Enter signs of the game: s for scissor, p for paper, r for stone: ");
7.  scanf("%c", &x);
8.  fflush(stdin);
9.  scanf("%c", &y);

11.  if ((x== 's' && y== 'p') || (x== 'r' && y== 's') || (x== 'p' && y== 'r'))
12.  printf( "x is the winner");
13.  if ((y== 's' && x== 'p') || (y== 'r' && x== 's') || (y== 'p' && x== 'r'))
14.  printf("y is the winner");
15.  if ((x== 's' && y== 's') || (x== 'r' && y== 'r') || (x== 'p' && y== 'p'))
16.  printf( "There is a tie");
17.  }

[C code explanation](#contents.xhtml_sc4_822a)

This Python code represents a simple rock-paper-scissors game where the user inputs their choice of signs (scissor, stone, or paper), and the program determines the winner based on the rules of the game using if-else if-else statements. Inside the condition block of an if-statement, various conditions are combined using or/ and operators. Like the previous program, wherever we read a character as input from the user, fflush() function is used before the scanf() function to clear the input buffer.

[Program 6.5: Print hotel bill](#contents.xhtml_sc2_823a)

Calculate and print the bill for a hotel that provides hourly services of two types: Regular and premium. The rates for the regular services are as follows: base rate: $50 (applicable for 2 hrs). After that, $30 for every hour will be charged. The rate of a private pool for 1 hour is $70.

The rates for the premium services are as follows: base rate: $100 (applicable for 3 hrs). After that, $50 for every hour will be charged. 5% discount on private pool booking if booked for 2 hrs or more.

Ask the user to enter the inputs as a type of service (r – regular, p – premium), booking duration, and private pool required. Generate the bill for the customer.

[Sample input output](#contents.xhtml_sc3_824a)

Test case #1:

Input: Enter the type of service (r – regular, p – premium): r

Enter the booking duration (in hrs): 7

Private pool required?(y/n): y

Enter duration of pool (in hrs): 5

Output:

The bill amount is 550

Test case #2:

Input: Enter the type of service (r – regular, p – premium): p

Enter the booking duration (in hrs): 5

Private pool required?(y/n): y

Enter duration of pool (in hrs): 8

Output:

The bill amount is 732.0

[Algorithm](#contents.xhtml_sc3_825a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read the type of service (r – regular, p – premium) as ser
3.  Read the booking duration (in hrs) as dur
4.  Read if Private pool required?(y/n) as pool
5.  if ser == 'r':

    1.  rate_reg=50
    2.  if dur > 2:
        1.  rate_reg = rate_reg+ (dur-2)*30

    c. if pool=='y':

    1.  Read duration of pool (in hrs) as dur_pool
    2.  rate_reg = rate_reg+ dur_pool*70

    d. Display("The bill amount is ", rate_reg)

6.  else if ser == 'p':
    1.  rate_p=100
    2.  if dur > 3:
        1.  rate_p = rate_p+ (dur-3)*50
    3.  if pool=='y':
        1.  Read duration of pool (in hrs) as dur_pool
        2.  if dur_pool<2:
            1.  rate_p = rate_p+ dur_pool*70
        3.  else:
            1.  rate_p = rate_p+ dur_pool*70*0.95
    4.  Display("The bill amount is ", rate_p)
7.  else:
    1.  Display("Wrong service selected")
8.  Stop

[Flowchart](#contents.xhtml_sc3_826a)

[Figure 6.5](#ch06.xhtml_fig6-5) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.5.jpg)

Figure 6.5: Flowchart illustrating the program 6.5

[Python code](#contents.xhtml_sc3_827a)

Python code for the program is as follows:

1.  ser=input("Enter the type of service (r – regular, p – premium): ")
2.  dur=int(input("Enter the booking duration (in hrs): "))
3.  pool=input("Private pool required?(y/n): ")

5.  if ser == 'r':
6.  rate_reg=50
7.  if dur > 2:
8.  rate_reg = rate_reg+ (dur-2)*30
9.  if pool=='y':
10.  dur_pool=int(input("Enter duration of pool (in hrs): "))
11.  rate_reg = rate_reg+ dur_pool*70
12.  print("The bill amount is ", rate_reg)

15.  elif ser == 'p':
16.  rate_p=100
17.  if dur > 3:
18.  rate_p = rate_p+ (dur-3)*50
19.  if pool=='y':
20.  dur_pool=int(input("Enter duration of pool (in hrs): "))
21.  if dur_pool <2:
22.  rate_p = rate_p+ dur_pool*70
23.  else:
24.  rate_p = rate_p+ dur_pool*70*0.95
25.  print("The bill amount is ", rate_p)

27.  else:
28.  print("Wrong service selected")

[Python code explanation](#contents.xhtml_sc4_828a)

This Python code calculates a customer’s bill amount based on the service type (regular or premium), booking duration, and whether a private pool is required. It reads the type of service (regular or premium), the booking duration in hours, and if a private pool is required as input from the user. Using the nested if- elif-else statements, the bill is generated.

[C code](#contents.xhtml_sc3_829a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  int  main()
3.  {
4.  char ser, pool;
5.  int dur, dur_pool;
6.  float rate_reg, rate_p;
7.  fflush(stdin);
8.  printf("Enter the type of service (r--> regular, p-->premium): ");
9.  scanf("%c", &ser);

11.  fflush(stdin);
12.  printf("Enter the booking duration (in hrs): ");
13.  scanf("%d", &dur);

15.  fflush(stdin);
16.  printf("Private pool required?(y/n): ");
17.  scanf("%c", &pool);

19.  if(ser == 'r')
20.  {
21.  rate_reg=50;
22.  if(dur > 2)
23.  rate_reg = rate_reg+ (dur-2)*30;
24.  if(pool=='y')
25.  {
26.  printf("Enter duration of pool (in hrs): ");
27.  scanf("%d",&dur_pool);
28.  rate_reg = rate_reg+ dur_pool*70;
29.  }
30.  printf("The bill amount is %f", rate_reg);
31.  }
32.  else  if(ser == 'p')
33.  {
34.  rate_p=100;
35.  if(dur > 3)
36.  rate_p = rate_p+ (dur-3)*50;
37.  if(pool=='y')
38.  {
39.  printf("Enter duration of pool (in hrs): ");
40.  scanf("%d",&dur_pool);
41.  if(dur_pool <2)
42.  rate_p = rate_p+ dur_pool*70;
43.  else
44.  rate_p = rate_p+ dur_pool*70*0.95;
45.  }
46.  printf("The bill amount is %f", rate_p);
47.  }
48.  else
49.  printf("Wrong service selected");

51.  return(0);
52.  }

[C code explanation](#contents.xhtml_sc4_830a)

This code calculates a customer’s bill amount based on the service type (regular or premium), booking duration, and whether a private pool is required. It reads the type of service (regular or premium), the booking duration in hours, and if a private pool is required as input from the user. Using the nested if-else if-else statements, the bill is generated. fflush() function is used before reading a character value as input.

[Program 6.6: Find fewest denominations](#contents.xhtml_sc2_831a)

Take the amount from the user and print the minimum number of notes required. Let the denominations be 500, 100, 50, 20, 10, 5, 2, 1.

For example:

Input: amount: 576

Output: Total number of notes: 500: 1, 100: 0, 50: 1, 20: 1, 10: 0, 5: 1, 2: 0, 1: 1

[Sample input output](#contents.xhtml_sc3_832a)

Test case #1:

Input: Enter the amount 985

Output: 500: 1, 100 : 4, 50 : 1, 20 : 1, 10 : 1, 5 : 1, 2 : 0, 1 : 0,

Test case #2:

Input: Enter the amount: 772

Output: 500 : 1, 100 : 2, 50 : 1, 20 : 1, 10 : 0, 5 : 0, 2 : 1, 1 : 0,

[Algorithm](#contents.xhtml_sc3_833a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  deno=[500, 100, 50, 20, 10, 5, 2, 1]
3.  Read the amount as a_m
4.  d_freq=[]
5.  s=a_m
6.  for i= 0 to len(deno)
    1.  Append(s//deno[i]) as d_freq
    2.  s=s%deno[i]
    3.  Display(d_freq[i])
7.  for i= 0 to len(deno)
    1.  Display(deno[i], ":", d_freq[i], end=", ")
8.  Stop

[Flowchart](#contents.xhtml_sc3_834a)

[Figure 6.6](#ch06.xhtml_fig6-6) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.6.jpg)

Figure 6.6: Flowchart illustrating the program 6.6

[Python code](#contents.xhtml_sc3_835a)

Python code for the program is as follows:

1.  deno=[500, 100, 50, 20, 10, 5, 2, 1]
2.  a_m=int(input("Enter the amount"))
3.  d_freq=[]
4.  s=a_m

6.  for i in range(0, len(deno)):
7.  d_freq.append(s//deno[i])
8.  s=s%deno[i]

10.  for i in range(0, len(deno)):
11.  print(deno[i], ":", d_freq[i], end=", ")

[Python code explanation](#contents.xhtml_sc4_836a)

This Python code snippet is designed to calculate the minimum number of denominations (bills/coins) required to represent a given amount (a_m) using a predefined list of denominations (deno).

It prompts the user to enter an amount and stores the input as an integer in the variable a_m. An empty list d_freq stores the frequency of each denomination. Variable s will be used to keep track of the remaining amount as the code calculates the denominations. The for loop iterates through the denominations in descending order and calculates how many times the current denomination (deno[i]) can be used in the remaining amount (s) and appends that value to the d_freq list. It then updates the remaining amount (s) after subtracting the amount represented by the used denominations. Finally, it displays the number of denominations required to represent the given amount, using the denominations specified in the deno list.

[C code](#contents.xhtml_sc3_837a)

C code for the program is as follows:

1.  #include<stdio.h>

3.  int  main()
4.  {

6.  int deno[8]={500, 100, 50, 20, 10, 5, 2, 1};
7.  int a_m, s, i, d_freq[8];

9.  printf("Enter the amount: ");
10.  scanf("%d", &a_m);

12.  s=a_m;
13.  for(i=0; i<8; i++)
14.  {
15.  d_freq[i]=s/deno[i];
16.  s=s%deno[i];
17.  }

19.  for(i=0; i<8;i++)
20.  printf("%d : %d; ", deno[i], d_freq[i]);

22.  return(0);
23.  }

[C code explanation](#contents.xhtml_sc4_838a)

This C code snippet is designed to calculate the minimum number of denominations (bills/coins) required to represent a given amount (a_m) using a predefined array of denominations (deno).

It prompts the user to enter an amount and stores the input as an integer in the variable a_m. An array d_freq stores the frequency of each denomination. Variable s will be used to keep track of the remaining amount as the code calculates the denominations. The for loop iterates through the denominations in descending order and calculates how many times the current denomination (deno[i]) can be used in the remaining amount (s) and appends that value to the d_freq array. It then updates the remaining amount (s) after subtracting the amount represented by the used denominations. Finally, it displays the number of denominations required to represent the given amount using the denominations specified in the deno array.

[Program 6.7: Assign class rank](#contents.xhtml_sc2_839a)

Take the percentage marks of ten students as input from the user and assign them class rank.

[Sample input output](#contents.xhtml_sc3_840a)

Test case #1:

Input: Enter the percentage marks: 90

Enter the percentage marks: 50

Enter the percentage marks: 32

Enter the percentage marks: 76

Enter the percentage marks: 46

Enter the percentage marks: 98

Enter the percentage marks: 12

Enter the percentage marks: 23

Enter the percentage marks: 56

Enter the percentage marks: 77

Output: Students in order of their ranking are [6, 1, 10, 4, 9, 2, 5, 3, 8, 7]

[Algorithm](#contents.xhtml_sc3_841a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  n=10
3.  m_l=[]
4.  m_s=[]
5.  for ii =0 to n-1:
    1.  Read the percentage marks as m
    2.  Append m to m_l
    3.  Append ii+1 to m_s
6.  for jj= 0 to n-2
7.  for ii = 0 to n-jj-2
8.  if m_l[ii] <m_l[ii+1]:
    1.  swap(m_l[ii],m_l[ii+1])
    2.  swap(m_s[ii],m_s[ii+1])
9.  Display ("Students in order of their ranking are", m_s)
10.  Stop

[Flowchart](#contents.xhtml_sc3_842a)

[Figure 6.7](#ch06.xhtml_fig6-7) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.7.jpg)

Figure 6.7: Flowchart illustrating the program 6.7

[Python code](#contents.xhtml_sc3_843a)

Python code for the program is as follows:

1.  n=10
2.  m_l=[]
3.  m_s=[]
4.  for ii in range (0, n):
5.  m_l.append(int(input("Enter the percentage marks: ")))
6.  m_s.append(ii+1)

8.  for jj in range(0,n-1):
9.  for ii in range(0, n-jj-1):
10.  if m_l[ii] < m_l[ii+1]:
11.  m_l[ii],m_l[ii+1]=m_l[ii+1],m_l[ii]
12.  m_s[ii],m_s[ii+1]=m_s[ii+1],m_s[ii]

14.  print("Students in order of their ranking are", m_s)

[Python code explanation](#contents.xhtml_sc4_844a)

This Python code takes input for the percentage marks of 10 students and assigns each student a rank. It initializes an empty list m_l to store the percentage marks of the students and an empty list m_s to store the enrollment numbers of the students, which are assigned from 1 to 10.

The first marks of 10 students are taken as input from the user using a for-loop and stored in the m_l list. Then, marks are sorted in descending order using the sorting program discussed in [Chapter 5](#ch05_split_000.xhtml), Complex Problem Solving. The enrollment numbers are also swapped with marks to keep them in sync. Finally, it prints enrollment numbers in rank order.

[C code](#contents.xhtml_sc3_845a)

C code for the program is as follows:

1.  #include<stdio.h>

3.  int  main()
4.  {
5.  int n=10;
6.  int m_l[10];
7.  int m_s[10];
8.  int ii, jj, t;

10.  printf("Enter the percentage marks of 10 students: ");
11.  for(ii=0; ii<n; ii++)
12.  {
13.  scanf("%d", &m_l[ii]);
14.  m_s[ii]=ii+1;
15.  }

17.  for(jj=0; jj<n-1; jj++)
18.  {
19.  for(ii=0; ii<n-jj-1; ii++)
20.  {
21.  if(m_l[ii] < m_l[ii+1])
22.  {
23.  t=m_l[ii];
24.  m_l[ii]=m_l[ii+1];
25.  m_l[ii+1]=t;

27.  t=m_s[ii];
28.  m_s[ii]=m_s[ii+1];
29.  m_s[ii+1]=t;
30.  }
31.  }
32.  }
33.  printf("Students in order of their ranking are ");
34.  for(ii=0; ii<n; ii++)
35.  {
36.  printf("%d ", m_s[ii]);
37.  }
38.  return(0);
39.  }

[C code explanation](#contents.xhtml_sc4_846a)

This Python code takes input for the percentage marks of 10 students and assigns each student a rank. It initializes an empty array m_l to store the percentage marks of the students and an empty array m_s to store the enrollment numbers of the students who are assigned from 1 to 10.

The first marks of 10 students are taken as input from the user using a for-loop and stored in the m_l array. Then, marks are sorted in descending order using the sorting program discussed in [Chapter 5](#ch05_split_000.xhtml), Complex Problem Solving. The enrollment numbers are also swapped with marks to keep them in sync. Finally, it prints enrollment numbers in the order of rank.

[Program 6.8: Minimize the difference](#contents.xhtml_sc2_847a)

Take marks of n students and input from the user. Obtain a subset of m students to minimize the difference between the highest and lowest scorers in that subset.

For example:

Input:

Let marks[] = {50, 70, 10, 90, 20, 100, 30} and m = 3

Output:

Subset is {10, 20, 30}

Difference is 20

[Sample input output](#contents.xhtml_sc3_848a)

Test case #1:

Input: Enter the number of students: 6

Marks: 70

Marks: 10

Marks: 90

Marks: 20

Marks: 100

Marks: 30

Enter the group size: 3

Output: Subset is [10, 20, 30]

Test case #2:

Input: Enter the number of students: 5

Marks: 3

Marks: 7

Marks: 8

Marks: 10

Marks: 14

Enter the group size: 2

Output: Subset is [7, 8]

[Algorithm](#contents.xhtml_sc3_849a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  st_l=[]
3.  Read the number of students as nn
4.  for ii =0 to nn-1
    1.  Read marks as m
    2.  Append m to st_l
5.  Read the group size as mm
6.  for jj= 0 to nn-2
    1.  for ii = 0 to nn-jj-2
        1.  if st_l[ii] >st_l[ii+1]:
            1.  swap(st_l[ii],st_l[ii+1])
7.  diff=[]
8.  min_no=max(st_l)
9.  ind=nn
10.  for jj0 to nn-mm
    1.  Appendst_l[jj+mm-1]-st_l[jj] to diff
    2.  if diff[jj] <min_no:
        1.  min_no=diff[jj]
        2.  ind=jj
11.  Display("Subset is ", st_l[ind: ind+mm])
12.  Stop

[Flowchart](#contents.xhtml_sc3_850a)

[Figure 6.8](#ch06.xhtml_fig6-8) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.8.jpg)

Figure 6.8: Flowchart illustrating the program 6.8

[Python code](#contents.xhtml_sc3_851a)

Python code for the program is as follows:

1.  st_l=[]
2.  nn=int(input("Enter the number of students: "))

4.  for ii in range(0, nn):
5.  st_l.append(int(input("Marks: ")))

7.  mm=int(input("Enter the group size: "))

10.  for jj in range(0,nn-1):
11.  for ii in range(0, nn-jj-1):
12.  if st_l[ii] > st_l[ii+1]:
13.  st_l[ii],st_l[ii+1]=st_l[ii+1],st_l[ii]

15.  diff=[]
16.  min_no=max(st_l)
17.  ind=nn
18.  for jj in range(0,nn-mm):
19.  diff.append(st_l[jj+mm-1]-st_l[jj])
20.  if diff[jj] < min_no:
21.  min_no=diff[jj]
22.  ind=jj

24.  print("Subset is ", st_l[ind: ind+mm])

[Python code explanation](#contents.xhtml_sc4_852a)

This Python code snippet takes input for the marks of a group of students and a group size and then finds and displays the subset of students that minimizes the difference between the highest and lowest scorers in that subset. It initializes an empty list st_l to store the students’ marks and reads the input from the user using a for-loop. It prompts the user to enter the group size and stores the input as an integer in the variable mm. Then, sorting is carried out on the students’ marks using the code discussed in [Chapter 5](#ch05_split_000.xhtml), Complex Problem Solving. Then, the code calculates the difference in marks between each group of mm students and finds the group with the smallest range.

[C code](#contents.xhtml_sc3_853a)

C code for the program is as follows:

1.  #include<stdio.h>

3.  int  main()
4.  {

6.  int st_l[100];
7.  int nn, ii, jj, mm, min_no, diff[100], ind, t;

9.  printf("Enter the number of students: ");
10.  scanf("%d", &nn);
11.  printf("Enter Marks of the students: ");
12.  for(ii=0; ii<nn; ii++)
13.  scanf("%d", &st_l[ii]);

15.  printf("Enter the group size: ");
16.  scanf("%d", &mm);

18.  for(jj=0; jj<nn-1; jj++)
19.  {
20.  for(ii=0; ii<nn-jj-1; ii++)
21.  {
22.  if(st_l[ii] > st_l[ii+1])
23.  {
24.  t=st_l[ii];
25.  st_l[ii]=st_l[ii+1];
26.  st_l[ii+1]=t;
27.  }
28.  }
29.  }
30.  min_no=200;
31.  ind=nn;
32.  for(jj=0; jj<(nn-mm); jj++)
33.  {
34.  diff[jj]=st_l[jj+mm-1]-st_l[jj];
35.  if(diff[jj] < min_no)
36.  {
37.  min_no=diff[jj];
38.  ind=jj;
39.  }
40.  }
41.  printf("Subset is ");
42.  for(jj=ind; jj<ind+mm; jj++)
43.  {
44.  printf("%d ", st_l[jj]);
45.  }
46.  return(0);
47.  }

[C code explanation](#contents.xhtml_sc4_854a)

This C code snippet takes input for the marks of a group of students and a group size and then finds and displays the subset of students that minimizes the difference between the highest and lowest scorers in that subset. It declares an array st_l to store the students’ marks and reads the input from the user using a for-loop. It prompts the user to enter the group size and stores the input as an integer in the variable mm. Then, sorting is carried out on the students’ marks using the code discussed in [Chapter 5](#ch05_split_000.xhtml), Complex Problem Solving. Then, the code calculates the difference in marks between each group of mm students and finds the group with the smallest range.

[Program 6.9: Convert decimals to different bases](#contents.xhtml_sc2_855a)

The number system is a mathematical representation of a number in an understandable machine format. For instance, Binary numbers are used by computers to perform various arithmetic operations. Octal numbers are used to set file permissions in UNIX operating systems. Your task is to take a decimal number and the desired base (from 2 to 9) as inputs from the user and convert the decimal number to the required base representation.

For example:

Input: 5,2

Output: 101

[Sample input output](#contents.xhtml_sc3_856a)

Test case #1:

Input:

Enter the decimal number: 56

Enter the required base: 2

Output: The base 2 representation of 0 is 111000

Test case #2:

Input:

Enter the decimal number: 97

Enter the required base: 8

Output: The base 8 representation of 0 is 141

Test case #3:

Input:

Enter the decimal number: 284

Enter the required base: 5

Output: The base 5 representation of 0 is 2114

[Algorithm](#contents.xhtml_sc3_857a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  bina = 0
3.  i = 1
4.  Read the decimal number as nn
5.  Read the required base as bb
6.  if bb<2 or bb > 9:
    1.  Display("Base should be between 2 to 9")
    2.  Quit the program
7.  Repeatnn != 0 :
    1.  re = nn % bb
    2.  nn = nn//bb
    3.  bina += re * i
    4.  i *= 10
8.  Display("The base ", bb, " representation of ", nn, " is ", bina)
9.  Stop

[Flowchart](#contents.xhtml_sc3_858a)

[Figure 6.9](#ch06.xhtml_fig6-9) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.9.jpg)

Figure 6.9: Flowchart illustrating the program 6.9

[Python code](#contents.xhtml_sc3_859a)

Python code for the program is as follows:

1.  bina = 0
2.  i = 1
3.  nn=int(input("Enter the decimal number: "))
4.  bb=int(input("Enter the required base: "))

6.  if bb<2  or bb > 9:
7.  print("Base should be between 2 to 9")
8.  exit(0)

10.  while nn != 0 :
11.  re = nn % bb
12.  nn = nn//bb
13.  bina += re * i
14.  i *= 10

16.  print("The base ", bb, " representation of ", nn, " is ", bina)

[Python code explanation](#contents.xhtml_sc4_860a)

The Python code takes the decimal number and the base of the number as input and converts the decimal number to the equivalent representation in the desired base. The logic behind the conversion is the successive division of the number and recording of the remainder. The program will only work from base 10 to base between 2 to 9 conversions. The first base value is checked. The program will terminate with an appropriate error message if it is less than 2 or greater than 9. Otherwise, it will keep dividing the number with the base until it becomes 0. The remainder is recorded in every division. Finally, all the remainder are combined to form one number by multiplying them by 10.

[C code](#contents.xhtml_sc3_861a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  #include<stdlib.h>

4.  int  main () {
5.  // variable to store the result
6.  long bina = 0;
7.  int re, i = 1;
8.  int nn, bb;
9.  printf("Enter the decimal number: ");
10.  scanf("%d", &nn);

12.  printf("Enter the required base: ");
13.  scanf("%d", &bb);

15.  if(bb<2 || bb > 9)
16.  {
17.  printf("Base should be between 2 to 9");
18.  exit(0);
19.  }
20.  // loop to convert to binary
21.  while (nn != 0) {
22.  // get remainder of nn divided by base
23.  re = nn % bb;
24.  // divide nn by base
25.  nn = nn/bb;
26.  // multiply remainder by i
27.  // add the product to bin
28.  bina += re * i;
29.  // multiply i by 10
30.  i *= 10;
31.  }

33.  printf("The base %d representation of %d is %ld", bb,nn,bina);

35.  return  0;
36.  }

[C code explanation](#contents.xhtml_sc4_862a)

The C code takes the decimal number and the base of the number as input and converts the decimal number to the equivalent representation in the desired base. The logic behind the conversion is the successive division of the number and recording of the remainder. The program will only work from base 10 to base between 2 to 9 conversions. The first base value is checked. The program will terminate with an appropriate error message if it is less than 2 or greater than 9. Otherwise, it will keep dividing the number with the base until the number becomes 0. The remainder is recorded in every division. Finally, all the remainder are combined to form one number by multiplying them by 10.

[Program 6.10: Password validation and encryption](#contents.xhtml_sc2_863a)

Validate and encrypt the password as per the following conditions:

1.  Length of the password should be between 8-12 characters. It should contain the alphabet, digits, and special characters.
2.  For encryption, replace alphabets with a 6-bit binary number such that the first bit represents lower case (by 0) or upper case (by 1), and the remaining 5 bits are the binary encoding. For example: a 000001, B 100010 and so.
3.  Replace digits as 0-A, 1-B, 2-C, 3-D, 4-E, 5-F, 6-G,7-H, 8-I, 9-J
4.  Keep the special characters as it is

For example:

Password: @Ab_%%82

Encrypted Password: @100001000010_%%IC

[Sample input output](#contents.xhtml_sc3_864a)

Test case #1:

Input: Enter your password: @asO9$%$%

Output: The encrypted password is @000001010011101111J$%$%

Test case #2:

Input: Enter your password: A@gh1

Output: Length of the password should be between 8-12 characters.

Test case #3:

Input: Enter your password: Coding11

Output: The password must contain at least one uppercase alphabet, lowercase alphabet, digits, and special characters.

[Algorithm](#contents.xhtml_sc3_865a)

To run the above program, the following steps are needed to be followed:

1.  Start
2.  Read your password p_s
3.  encry_ps=""
4.  Ac=0
5.  ac=0
6.  nc=0
7.  sc=0
8.  if len(p_s) < 8 or len(p_s) > 12:
    1.  Display("Length of the password should be between 8-12 characters." )
    2.  Quit the Program
9.  for each character ii ofp_s:
    1.  if ord(ii) in range(65,91):
        1.  Ac=1
    2.  else if ord(ii) in range(97, 123):
        1.  ac=1
    3.  else if ord(ii) in range(48, 58):
        1.  nc=1
    4.  else if ord(ii) in range(33,127):
        1.  sc=1
10.  if not(Ac==1 and ac==1 and nc==1 and sc==1):
    1.  Display("Password must contain atleast one uppercase alphabet, lowercase alphabet, digits and special characters.")
    2.  Quit the program
11.  for each character ii ofp_s:
    1.  if ord(ii) in range(65,91):
        1.  x="1"
        2.  x1=bin(ord(ii)-65+1)
        3.  x2=x1[2:]
        4.  for h = 1 to 5-len(x2)+1):
            1.  x=x+'0'
        5.  x=x+x2
        6.  encry_ps=encry_ps+str(x)
    2.  else if ord(ii) in range(97, 123):
        1.  x="0"
        2.  x1=bin(ord(ii)-97+1)
        3.  x2=x1[2:]
        4.  for h = 1 to 5-len(x2)+1):
            1.  x=x+'0'
        5.  x=x+x2
        6.  encry_ps=encry_ps+str(x)
    3.  else if ord(ii) in range(48, 58):
        1.  encry_ps=encry_ps+chr(ord(ii)+17)
    4.  else if ord(ii) in range(33,127):
        1.  encry_ps=encry_ps+ ii
12.  Display("The encrypted password is ", encry_ps)
13.  Stop

[Flowchart](#contents.xhtml_sc3_866a)

[Figure 6.10](#ch06.xhtml_fig6-10) illustrates the program in the form of a flowchart:

![](OPS/images/Figure_6.10.jpg)

Figure 6.10: Flowchart illustrating the program 6.10

[Python code](#contents.xhtml_sc3_867a)

Python code for the program is as follows:

1.  p_s=input("Enter your password: ")
2.  encry_ps=""
3.  Ac=0
4.  ac=0
5.  nc=0
6.  sc=0
7.  if len(p_s) < 8  or len(p_s) > 12:
8.  print("Length of the password should be between 8-12 characters." )
9.  exit()
10.  for ii in p_s:
11.  if ord(ii) in range(65,91):
12.  Ac=1
13.  elif ord(ii) in range(97, 123):
14.  ac=1
15.  elif ord(ii) in range(48, 58):
16.  nc=1
17.  elif ord(ii) in range(33,127):
18.  sc=1

20.  if  not(Ac==1  and ac==1  and nc==1  and sc==1):
21.  print("Password must contain atleast one uppercase alphabet, lowercase aphabet, digits and special characters.")
22.  exit()
23.  for ii in p_s:
24.  if ord(ii) in range(65,91):
25.  x="1"
26.  x1=bin(ord(ii)-65+1)
27.  x2=x1[2:]
28.  for h in range(1,5-len(x2)+1):
29.  x=x+'0'
30.  x=x+x2
31.  encry_ps=encry_ps+str(x)
32.  elif ord(ii) in range(97, 123):
33.  x="0"
34.  x1=bin(ord(ii)-97+1)
35.  x2=x1[2:]
36.  for h in range(1,5-len(x2)+1):
37.  x=x+'0'
38.  x=x+x2
39.  encry_ps=encry_ps+str(x)
40.  elif ord(ii) in range(48, 58):
41.  encry_ps=encry_ps+chr(ord(ii)+17)
42.  elif ord(ii) in range(33,127):
43.  encry_ps=encry_ps+ ii

45.  print("The encrypted password is ", encry_ps)

[Python code explanation](#contents.xhtml_sc4_868a)

This Python code prompts the user to input a password and then encrypts the password based on specific criteria. It prompts the user to input a password, stores the input in the variable, and initializes an empty string encry_ps to store the encrypted password. The variables Ac, ac, nc, and scare are initialized to 0 and are used to track whether the password contains at least one uppercase alphabet, one lowercase alphabet, one digit, and one special character, respectively. The code checks the length of the password and whether it contains at least one character from each category (uppercase, lowercase, digit, and special character). If these conditions are not met, an error message is printed, and the program exits. If the password meets the length and character type requirements, the code encrypts the password using specific rules. Finally, the encrypted password is printed to the console. Here, the function len() returns the length of the string. Function ord() returns the ASCII value of the character. ASCII value of uppercase alphabets is from 65-90, lowercase (97-122), digits (48-57), and others are treated as special characters. Bin() is a predefined function in Python to obtain the binary equivalent of any decimal number.

[C code](#contents.xhtml_sc3_869a)

C code for the program is as follows:

1.  #include<stdio.h>
2.  #include<string.h>
3.  #include<stdlib.h>

5.  int  ord(char s)
6.  {
7.  return((int)s);
8.  }

10.  void  bin (int nn, int ss[]) {
11.  // variable to store the result
12.  long bina = 0;
13.  int re, i = 1;
14.  int j=0;
15.  // loop to convert to binary
16.  while (nn != 0) {
17.  // get remainder of n divided by 2
18.  re = nn % 2;
19.  // divide n by 2
20.  nn /= 2;
21.  // multiply remainder by i
22.  // add the product to bin
23.  bina += re * i;
24.  // multiply i by 10
25.  i *= 10;
26.  ss[j]=re;
27.  j=j+1;
28.  //printf("in func=%c\n", ss[j-1]);
29.  }
30.  while(j<6)
31.  {
32.  ss[j]=0;
33.  j=j+1;
34.  }
35.  //ss[j]='\0';
36.  //printf("in func=%d\n", strlen(ss));

38.  //return bina;
39.  }

41.  int  main()
42.  {
43.  char encry_ps[100]="";
44.  char p_s[13];
45.  int Ac=0;
46.  int ac=0;
47.  int nc=0;
48.  int sc=0;
49.  int ii, h;

51.  fflush(stdin);
52.  printf("Enter your password: ");
53.  scanf("%s", p_s);

55.  if(strlen(p_s) < 8 || strlen(p_s) > 12)
56.  {
57.  printf("Length of the password should be between 8-12 characters." );
58.  getch();
59.  exit(0);
60.  }
61.  for(ii=0; ii< strlen(p_s); ii++)
62.  {
63.  if (ord(p_s[ii]) >=65 && ord(p_s[ii]) <=90)
64.  Ac=1;
65.  else  if (ord(p_s[ii]) >=97 && ord(p_s[ii]) <=122)
66.  ac=1;
67.  else  if (ord(p_s[ii]) >=48 && ord(p_s[ii]) <=57)
68.  nc=1;
69.  else  if (ord(p_s[ii]) >=33 && ord(p_s[ii]) <=126)
70.  sc=1;
71.  }
72.  if (!(Ac==1 && ac==1 && nc==1 && sc==1))
73.  {
74.  printf("Password must contain atleast one uppercase alphabet, lowercase aphabet, digits and special characters.");
75.  getch();
76.  exit(0);
77.  }

79.  for(ii=0; ii< strlen(p_s); ii++)
80.  {
81.  if (ord(p_s[ii]) >=48 && ord(p_s[ii]) <=57)
82.  {
83.  encry_ps[strlen(encry_ps)]=p_s[ii]+16;
84.  }
85.  else  if (ord(p_s[ii]) >=65 && ord(p_s[ii]) <=90)
86.  { char xx[7]="";
87.  int xx2[6];
88.  long xx2_int;
89.  bin(ord(p_s[ii])-65+1, xx2);
90.  xx2[5]=1;
91.  int h1;
92.  for(h1=0; h1<=5; h1++)
93.  xx[h1]=xx2[h1]+48;
94.  xx[h1]='\0';
95.  strrev(xx);
96.  strcat(encry_ps,xx);
97.  }
98.  else  if (ord(p_s[ii]) >=97 && ord(p_s[ii]) <=122)
99.  { char xa[7]="";
100.  int xa2[6];
101.  bin(ord(p_s[ii])-97+1, xa2);
102.  xa2[5]=0;
103.  for(h=0; h<=5; h++)
104.  xa[h]=xa2[h]+'0';
105.  xa[h]='\0';
106.  strrev(xa);
107.  strcat(encry_ps,xa);
108.  }
109.  else
110.  {
111.  encry_ps[strlen(encry_ps)]=p_s[ii];
112.  }
113.  }
114.  printf("The encrypted password is %s", encry_ps);

116.  return(0);
117.  }

[C code explanation](#contents.xhtml_sc4_870a)

This C code prompts the user to input a password and then encrypts the password based on specific criteria. It prompts the user to input a password, stores the input in the variable, and initializes an empty string encry_ps to store the encrypted password. The variables Ac, ac, nc, and scare are initialized to 0 and are used to track whether the password contains at least one uppercase alphabet, one lowercase alphabet, one digit, and one special character, respectively. The code checks the length of the password and whether it contains at least one character from each category (uppercase, lowercase, digit, and special character). If these conditions are not met, an error message is printed, and the program exits. If the password meets the length and character type requirements, the code encrypts the password using specific rules. Finally, the encrypted password is printed to the console. Here, the function strlen() returns the length of the string. Strrev() is used to reverse the string. Strcat() is used to concatenate two strings. All these string functions are defined in string.h library. The function is defined as ord(), which returns the ASCII value of the character. ASCII value of uppercase alphabets is from 65-90, lowercase (97-122), digits (48-57), and others are treated as special characters. Bin() is a defined function in Python to obtain the binary equivalent of any decimal number. Unlike Python, ord() and bin()are not the predefined function. So, they are defined in the program.

[Conclusion](#contents.xhtml_sc2_871a)

The chapter has discussed real-world problems/puzzles using various programming constructs like flowcharts, algorithms, and coding. With the help of several examples, the different flavors of multiple steps, conditional logic, loops, lists, and functions are presented.

[Points to remember](#contents.xhtml_sc2_872a)

*   Math.h library includes the basic functions of math in C Programming. The counter module in Python is math.
*   String.h is the C library where various string-related functions are already defined.
*   Predefined functions can be called to include the corresponding libraries.
*   Users can also define the functions which can be called in the program.

[Questions](#contents.xhtml_sc2_873a)

1. Convert any base number to Base 10.

2. Display the enrollment number of the student who scored the highest marks in the exam.

3. Ask the user to input 10 phone numbers. Then, take a phone number as input from the user and check if it exists in the list.

4. Sort elements at even index in increasing and odd index in decreasing order

5. Given a set of n nuts of different sizes and n bolts of different sizes. There is a one-one mapping between nuts and bolts. Your task is to match nuts and bolts. Constraint: Comparison of a nut to another nut or a bolt to another bolt is not allowed. It means a nut can only be compared with a bolt, and a bolt can only be compared with a nut to see which one is bigger/smaller.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](OPS/images/fm1.png)

# Index

A

add two matrices program [255](#ch05_split_000.xhtml_page255)

algorithm [256](#ch05_split_000.xhtml_page256)

C code [259](#ch05_split_000.xhtml_page259), [260](#ch05_split_000.xhtml_page260)

flowchart [256](#ch05_split_000.xhtml_page256)

Python code [258](#ch05_split_000.xhtml_page258)

assign class rank program [320](#ch06.xhtml_page320)

algorithm [321](#ch06.xhtml_page321)

C code [323](#ch06.xhtml_page323), [324](#ch06.xhtml_page324)

flowchart [321](#ch06.xhtml_page321)

Python code [322](#ch06.xhtml_page322), [323](#ch06.xhtml_page323)

B

book storage optimization program [296](#ch06.xhtml_page296)

algorithm [297](#ch06.xhtml_page297)

C code [298](#ch06.xhtml_page298), [299](#ch06.xhtml_page299)

flowchart [297](#ch06.xhtml_page297)

Python code [298](#ch06.xhtml_page298)

C

calculate the grade of a student program [102](#ch02.xhtml_page102)

algorithm [103](#ch02.xhtml_page103)

C code [105](#ch02.xhtml_page105), [106](#ch02.xhtml_page106)

flowchart [103](#ch02.xhtml_page103)

Python code [104](#ch02.xhtml_page104), [105](#ch02.xhtml_page105)

check divisibility by 7 and 5 program [75](#ch02.xhtml_page75)

algorithm [76](#ch02.xhtml_page76)

C code [77](#ch02.xhtml_page77), [78](#ch02.xhtml_page78)

flowchart [76](#ch02.xhtml_page76)

Python code [77](#ch02.xhtml_page77)

check if a number is prime program [190](#ch04.xhtml_page190)

algorithm [191](#ch04.xhtml_page191)

C code [193](#ch04.xhtml_page193), [194](#ch04.xhtml_page194)

flowchart [191](#ch04.xhtml_page191)

Python code [192](#ch04.xhtml_page192), [193](#ch04.xhtml_page193)

check if character is a vowel or consonant program [78](#ch02.xhtml_page78)

algorithm [78](#ch02.xhtml_page78)

C code [79](#ch02.xhtml_page79), [80](#ch02.xhtml_page80)

flowchart [78](#ch02.xhtml_page78)

Python code [79](#ch02.xhtml_page79)

check if matrix is symmetric program [264](#ch05_split_000.xhtml_page264)

algorithm [265](#ch05_split_000.xhtml_page265)

C code [267](#ch05_split_000.xhtml_page267), [268](#ch05_split_000.xhtml_page268)

flowchart [265](#ch05_split_000.xhtml_page265)

Python code [266](#ch05_split_000.xhtml_page266), [267](#ch05_split_000.xhtml_page267)

check if matrix is upper triangular program [260](#ch05_split_000.xhtml_page260)

algorithm [261](#ch05_split_000.xhtml_page261)

C code [263](#ch05_split_000.xhtml_page263), [264](#ch05_split_000.xhtml_page264)

flowchart [261](#ch05_split_000.xhtml_page261)

Python code [262](#ch05_split_000.xhtml_page262), [263](#ch05_split_000.xhtml_page263)

check if number is even or odd program

algorithm [68](#ch02.xhtml_page68)

C code [69](#ch02.xhtml_page69), [70](#ch02.xhtml_page70)

flowchart [68](#ch02.xhtml_page68)

Python code [69](#ch02.xhtml_page69)

check if string is palindrome program [216](#ch04.xhtml_page216)

algorithm [217](#ch04.xhtml_page217)

C code [219](#ch04.xhtml_page219), [220](#ch04.xhtml_page220)

flowchart [218](#ch04.xhtml_page218)

Python code [218](#ch04.xhtml_page218), [219](#ch04.xhtml_page219)

check if year is a leap year program [93](#ch02.xhtml_page93)

algorithm [94](#ch02.xhtml_page94)

C code [95](#ch02.xhtml_page95), [96](#ch02.xhtml_page96)

flowchart [94](#ch02.xhtml_page94)

Python code [95](#ch02.xhtml_page95)

check if you are an adult program

algorithm [66](#ch02.xhtml_page66)

C code [67](#ch02.xhtml_page67), [68](#ch02.xhtml_page68)

flowchart [66](#ch02.xhtml_page66)

Python code [67](#ch02.xhtml_page67)

check if you can sit in exam program [80](#ch02.xhtml_page80), [83](#ch02.xhtml_page83)

algorithm [81](#ch02.xhtml_page81), [84](#ch02.xhtml_page84)

C code [82](#ch02.xhtml_page82), [83](#ch02.xhtml_page83), [86](#ch02.xhtml_page86)

flowchart [81](#ch02.xhtml_page81), [85](#ch02.xhtml_page85)

Python code [82](#ch02.xhtml_page82), [85](#ch02.xhtml_page85)

check type of integer program [70](#ch02.xhtml_page70)

algorithm [71](#ch02.xhtml_page71)

C code [72](#ch02.xhtml_page72)

flowchart [71](#ch02.xhtml_page71)

Python code [71](#ch02.xhtml_page71), [72](#ch02.xhtml_page72)

check who spent more money program [87](#ch02.xhtml_page87)

algorithm [87](#ch02.xhtml_page87)

C code [89](#ch02.xhtml_page89), [90](#ch02.xhtml_page90)

flowchart [88](#ch02.xhtml_page88)

Python code [89](#ch02.xhtml_page89)

complex loops, in programming [162](#ch04.xhtml_page162)

check if a number is prime program [190](#ch04.xhtml_page190)

check if string is palindrome program [216](#ch04.xhtml_page216)

concatenate two strings program [223](#ch04.xhtml_page223)

count number of consonants program [187](#ch04.xhtml_page187)

count number of even numbers program [168](#ch04.xhtml_page168)

count of frequency of occurrence of elements [210](#ch04.xhtml_page210)

display even indexed characters program [220](#ch04.xhtml_page220)

display list of divisor program [179](#ch04.xhtml_page179)

display odd numbers program [165](#ch04.xhtml_page165)

display sum of even numbers program [171](#ch04.xhtml_page171)

display sum of numbers divisible by 9 program [173](#ch04.xhtml_page173)

find difference of sum of even and odd numbers program [176](#ch04.xhtml_page176)

find HCF program [199](#ch04.xhtml_page199)

find LCM program [194](#ch04.xhtml_page194)

find length of string program [214](#ch04.xhtml_page214)

find max 1 program [181](#ch04.xhtml_page181)

find max 2 program [184](#ch04.xhtml_page184)

find sum and check if even program [162](#ch04.xhtml_page162)

handling list/arrays program [206](#ch04.xhtml_page206)

search a number program [202](#ch04.xhtml_page202)

complex problem solving programs

add two matrices [255](#ch05_split_000.xhtml_page255)

check if matrix is symmetric [264](#ch05_split_000.xhtml_page264)

check if matrix is upper triangular [260](#ch05_split_000.xhtml_page260)

find all Armstrong numbers [236](#ch05_split_000.xhtml_page236)

find n based on a condition [239](#ch05_split_000.xhtml_page239)

find sum of digits of a number [230](#ch05_split_000.xhtml_page230)

obtain list having prime numbers [242](#ch05_split_000.xhtml_page242)

print 2-D pattern 1 [268](#ch05_split_000.xhtml_page268)

print 2-D pattern 2 [271](#ch05_split_000.xhtml_page271)

print 2-D pattern 3 [273](#ch05_split_000.xhtml_page273)

print 2-D pattern 4 [276](#ch05_split_001.xhtml_page276)

print 2-D pattern 5 [278](#ch05_split_001.xhtml_page278)

print 2-D pattern 6 [281](#ch05_split_001.xhtml_page281)

print 2-D pattern 7 [284](#ch05_split_001.xhtml_page284)

print 2-D pattern 8 [286](#ch05_split_001.xhtml_page286)

print 2-D pattern 9 [289](#ch05_split_001.xhtml_page289)

print matrix [251](#ch05_split_000.xhtml_page251)

remove duplicate items [245](#ch05_split_000.xhtml_page245)

reverse the number [233](#ch05_split_000.xhtml_page233)

sort the numbers [248](#ch05_split_000.xhtml_page248)

concatenate two strings program

algorithm [223](#ch04.xhtml_page223)

C code [225](#ch04.xhtml_page225), [226](#ch04.xhtml_page226)

flowchart [223](#ch04.xhtml_page223)

Python code [224](#ch04.xhtml_page224), [225](#ch04.xhtml_page225)

conditional statements [61](#ch02.xhtml_page61)-[63](#ch02.xhtml_page63)

conditional statements, in programming

calculate the grade of a student program [102](#ch02.xhtml_page102)

check divisibility by 7 and 5 program [75](#ch02.xhtml_page75)

check if character is a vowel or consonant program [78](#ch02.xhtml_page78)

check if number is even or odd program [68](#ch02.xhtml_page68)

check if year is a leap year program [93](#ch02.xhtml_page93)

check if you are an adult program [65](#ch02.xhtml_page65)

check if you can sit in exam program [80](#ch02.xhtml_page80), [83](#ch02.xhtml_page83)

check type of integer program [70](#ch02.xhtml_page70)

check who spent more money program [87](#ch02.xhtml_page87)

design arithmetic calculator program [99](#ch02.xhtml_page99)

find absolute value of number program [63](#ch02.xhtml_page63)

find gross salary program [106](#ch02.xhtml_page106)

find largest number program [96](#ch02.xhtml_page96)

find type of triangle program [90](#ch02.xhtml_page90)

generate shopping bill during sale program [113](#ch02.xhtml_page113)

generate shopping bill program [110](#ch02.xhtml_page110)

validate a triangle program [73](#ch02.xhtml_page73)

convert decimals to different bases program [330](#ch06.xhtml_page330)

algorithm [331](#ch06.xhtml_page331)

C code [333](#ch06.xhtml_page333)-[335](#ch06.xhtml_page335)

flowchart [332](#ch06.xhtml_page332)

Python code [333](#ch06.xhtml_page333)

convert degree F to degree C program [40](#ch01.xhtml_page40)

algorithm [40](#ch01.xhtml_page40)

C code [42](#ch01.xhtml_page42)

flowchart [40](#ch01.xhtml_page40)

Python code [41](#ch01.xhtml_page41)

convert inch to feet program [42](#ch01.xhtml_page42)

algorithm [43](#ch01.xhtml_page43)

C code [44](#ch01.xhtml_page44)

flowchart [43](#ch01.xhtml_page43)

Python code [43](#ch01.xhtml_page43), [44](#ch01.xhtml_page44)

convert meter to centimeter program [37](#ch01.xhtml_page37)

algorithm [38](#ch01.xhtml_page38)

C code [39](#ch01.xhtml_page39)

flowchart [38](#ch01.xhtml_page38)

Python code [39](#ch01.xhtml_page39)

count number of consonants program

algorithm [187](#ch04.xhtml_page187)

C code [189](#ch04.xhtml_page189), [190](#ch04.xhtml_page190)

flowchart [188](#ch04.xhtml_page188)

Python code [188](#ch04.xhtml_page188), [189](#ch04.xhtml_page189)

count number of even numbers program

algorithm [168](#ch04.xhtml_page168)

C code [170](#ch04.xhtml_page170), [171](#ch04.xhtml_page171)

flowchart [169](#ch04.xhtml_page169)

Python code [170](#ch04.xhtml_page170)

count of frequency of occurrence of elements [210](#ch04.xhtml_page210)

algorithm [210](#ch04.xhtml_page210)

C code [213](#ch04.xhtml_page213), [214](#ch04.xhtml_page214)

flowchart [211](#ch04.xhtml_page211)

Python code [212](#ch04.xhtml_page212)

D

Dearness Allowance (DA) [109](#ch02.xhtml_page109)

design arithmetic calculator program [99](#ch02.xhtml_page99)

algorithm [100](#ch02.xhtml_page100)

C code [101](#ch02.xhtml_page101), [102](#ch02.xhtml_page102)

flowchart [100](#ch02.xhtml_page100)

Python code [101](#ch02.xhtml_page101)

display cube of numbers program [126](#ch03.xhtml_page126)

algorithm [126](#ch03.xhtml_page126)

C code [128](#ch03.xhtml_page128)

Python code [127](#ch03.xhtml_page127)

display even indexed characters program

algorithm [220](#ch04.xhtml_page220)

C code [222](#ch04.xhtml_page222)

flowchart [221](#ch04.xhtml_page221)

Python code [221](#ch04.xhtml_page221), [222](#ch04.xhtml_page222)

display factorial program

algorithm [136](#ch03.xhtml_page136)

C code [137](#ch03.xhtml_page137), [138](#ch03.xhtml_page138)

flowchart [136](#ch03.xhtml_page136)

Python code [137](#ch03.xhtml_page137)

display Fibonacci series program [157](#ch03.xhtml_page157)

algorithm [157](#ch03.xhtml_page157)

C code [159](#ch03.xhtml_page159)

flowchart [158](#ch03.xhtml_page158)

Python code [158](#ch03.xhtml_page158)

display list of divisor program

algorithm [179](#ch04.xhtml_page179)

C code [181](#ch04.xhtml_page181)

flowchart [179](#ch04.xhtml_page179)

Python code [180](#ch04.xhtml_page180)

display multiples program [128](#ch03.xhtml_page128)

algorithm [129](#ch03.xhtml_page129)

C code [130](#ch03.xhtml_page130)

flowchart [129](#ch03.xhtml_page129)

Python code [129](#ch03.xhtml_page129), [130](#ch03.xhtml_page130)

display natural numbers program [121](#ch03.xhtml_page121)

algorithm [121](#ch03.xhtml_page121)

C code [123](#ch03.xhtml_page123)

flowchart [122](#ch03.xhtml_page122)

Python code [122](#ch03.xhtml_page122)

display odd numbers program [165](#ch04.xhtml_page165)

algorithm [166](#ch04.xhtml_page166)

C code [167](#ch04.xhtml_page167), [168](#ch04.xhtml_page168)

flowchart [166](#ch04.xhtml_page166)

Python code [167](#ch04.xhtml_page167)

display square of natural numbers program [123](#ch03.xhtml_page123)

algorithm [124](#ch03.xhtml_page124)

C code [125](#ch03.xhtml_page125)

flowchart [124](#ch03.xhtml_page124)

Python code [125](#ch03.xhtml_page125)

display sum and average program

algorithm [131](#ch03.xhtml_page131)

C code [132](#ch03.xhtml_page132), [133](#ch03.xhtml_page133)

flowchart [131](#ch03.xhtml_page131)

Python code [132](#ch03.xhtml_page132)

display sum of even numbers program

algorithm [171](#ch04.xhtml_page171)

C code [173](#ch04.xhtml_page173)

flowchart [172](#ch04.xhtml_page172)

Python code [172](#ch04.xhtml_page172)

display sum of numbers divisible by 9 program

algorithm [173](#ch04.xhtml_page173)

C code [175](#ch04.xhtml_page175)

flowchart [174](#ch04.xhtml_page174)

Python code [174](#ch04.xhtml_page174), [175](#ch04.xhtml_page175)

display sum of square program

algorithm [133](#ch03.xhtml_page133)

C code [135](#ch03.xhtml_page135)

flowchart [134](#ch03.xhtml_page134)

Python code [134](#ch03.xhtml_page134), [135](#ch03.xhtml_page135)

display the multiplication table program [143](#ch03.xhtml_page143)

algorithm [144](#ch03.xhtml_page144)

C code [145](#ch03.xhtml_page145), [146](#ch03.xhtml_page146)

flowchart [144](#ch03.xhtml_page144)

Python code [145](#ch03.xhtml_page145)

display '*' program [118](#ch03.xhtml_page118)

algorithm [119](#ch03.xhtml_page119)

C code [120](#ch03.xhtml_page120), [121](#ch03.xhtml_page121)

flowchart [119](#ch03.xhtml_page119)

Python code [120](#ch03.xhtml_page120)

F

find 2 raise to the power n program [138](#ch03.xhtml_page138)

algorithm [139](#ch03.xhtml_page139)

C code [140](#ch03.xhtml_page140), [141](#ch03.xhtml_page141)

flowchart [139](#ch03.xhtml_page139)

Python code [139](#ch03.xhtml_page139), [140](#ch03.xhtml_page140)

find absolute value of a number program [63](#ch02.xhtml_page63)

algorithm [63](#ch02.xhtml_page63)

C code [64](#ch02.xhtml_page64), [65](#ch02.xhtml_page65)

flowchart [63](#ch02.xhtml_page63)

Python code [64](#ch02.xhtml_page64)

find all Armstrong numbers program

algorithm [236](#ch05_split_000.xhtml_page236)

C code [238](#ch05_split_000.xhtml_page238), [239](#ch05_split_000.xhtml_page239)

flowchart [237](#ch05_split_000.xhtml_page237)

Python code [237](#ch05_split_000.xhtml_page237), [238](#ch05_split_000.xhtml_page238)

find area of a circle program [47](#ch01.xhtml_page47)

algorithm [47](#ch01.xhtml_page47)

C code [49](#ch01.xhtml_page49), [50](#ch01.xhtml_page50)

flowchart [48](#ch01.xhtml_page48)

Python code [48](#ch01.xhtml_page48), [49](#ch01.xhtml_page49)

find area of a rectangle program [45](#ch01.xhtml_page45)

algorithm [45](#ch01.xhtml_page45)

C code [46](#ch01.xhtml_page46), [47](#ch01.xhtml_page47)

flowchart [45](#ch01.xhtml_page45)

Python code [46](#ch01.xhtml_page46)

find area of parallelogram program [50](#ch01.xhtml_page50)

algorithm [50](#ch01.xhtml_page50)

C code [52](#ch01.xhtml_page52)

flowchart [51](#ch01.xhtml_page51)

Python code [51](#ch01.xhtml_page51)

find average program [31](#ch01.xhtml_page31)

algorithm [32](#ch01.xhtml_page32)

C code [34](#ch01.xhtml_page34)

flowchart [32](#ch01.xhtml_page32)

Python code [33](#ch01.xhtml_page33), [34](#ch01.xhtml_page34)

find cube of a number program [29](#ch01.xhtml_page29)

algorithm [30](#ch01.xhtml_page30)

C code [31](#ch01.xhtml_page31)

flowchart [30](#ch01.xhtml_page30)

Python code [31](#ch01.xhtml_page31)

find difference of sum of even and odd numbers program

algorithm [176](#ch04.xhtml_page176)

C code [178](#ch04.xhtml_page178)

flowchart [176](#ch04.xhtml_page176)

Python code [177](#ch04.xhtml_page177), [178](#ch04.xhtml_page178)

find distance between two points program [52](#ch01.xhtml_page52)

algorithm [53](#ch01.xhtml_page53)

C code [55](#ch01.xhtml_page55), [56](#ch01.xhtml_page56)

flowchart [53](#ch01.xhtml_page53)

Python code [54](#ch01.xhtml_page54), [55](#ch01.xhtml_page55)

find fewest denominations program [317](#ch06.xhtml_page317)

algorithm [317](#ch06.xhtml_page317)

C code [319](#ch06.xhtml_page319), [320](#ch06.xhtml_page320)

flowchart [318](#ch06.xhtml_page318)

Python code [318](#ch06.xhtml_page318), [319](#ch06.xhtml_page319)

find gross salary program [106](#ch02.xhtml_page106)

algorithm [107](#ch02.xhtml_page107)

C code [109](#ch02.xhtml_page109), [110](#ch02.xhtml_page110)

flowchart [107](#ch02.xhtml_page107), [108](#ch02.xhtml_page108)

Python code [108](#ch02.xhtml_page108), [109](#ch02.xhtml_page109)

find HCF program

algorithm [199](#ch04.xhtml_page199)

C code [201](#ch04.xhtml_page201), [202](#ch04.xhtml_page202)

flowchart [200](#ch04.xhtml_page200)

Python code [200](#ch04.xhtml_page200), [201](#ch04.xhtml_page201)

find largest number program [96](#ch02.xhtml_page96)

algorithm [96](#ch02.xhtml_page96)

C code [98](#ch02.xhtml_page98), [99](#ch02.xhtml_page99)

flowchart [97](#ch02.xhtml_page97)

Python code [97](#ch02.xhtml_page97), [98](#ch02.xhtml_page98)

find LCM program [194](#ch04.xhtml_page194)

algorithm [195](#ch04.xhtml_page195)

C code [197](#ch04.xhtml_page197), [198](#ch04.xhtml_page198), [199](#ch04.xhtml_page199)

flowchart [195](#ch04.xhtml_page195)

Python code [196](#ch04.xhtml_page196), [197](#ch04.xhtml_page197)

find length of string program

algorithm [214](#ch04.xhtml_page214)

C code [216](#ch04.xhtml_page216)

flowchart [215](#ch04.xhtml_page215)

Python code [215](#ch04.xhtml_page215)

find max 1 program [181](#ch04.xhtml_page181)

algorithm [182](#ch04.xhtml_page182)

C code [183](#ch04.xhtml_page183), [184](#ch04.xhtml_page184)

flowchart [182](#ch04.xhtml_page182)

Python code [183](#ch04.xhtml_page183)

find max 2 program [184](#ch04.xhtml_page184)

algorithm [184](#ch04.xhtml_page184)

C code [186](#ch04.xhtml_page186)

flowchart [185](#ch04.xhtml_page185)

Python code [185](#ch04.xhtml_page185), [186](#ch04.xhtml_page186)

find n based on a condition program [239](#ch05_split_000.xhtml_page239)

algorithm [240](#ch05_split_000.xhtml_page240)

C code [241](#ch05_split_000.xhtml_page241), [242](#ch05_split_000.xhtml_page242)

flowchart [240](#ch05_split_000.xhtml_page240)

Python code [241](#ch05_split_000.xhtml_page241)

find percentage marks program [34](#ch01.xhtml_page34)

algorithm [35](#ch01.xhtml_page35)

C code [37](#ch01.xhtml_page37)

flowchart [35](#ch01.xhtml_page35)

Python code [36](#ch01.xhtml_page36), [37](#ch01.xhtml_page37)

find product of two numbers program [13](#ch01.xhtml_page13)

algorithm [14](#ch01.xhtml_page14)

C code [15](#ch01.xhtml_page15)

flowchart [14](#ch01.xhtml_page14)

Python code [14](#ch01.xhtml_page14), [15](#ch01.xhtml_page15)

find square of a number program [27](#ch01.xhtml_page27)

algorithm [28](#ch01.xhtml_page28)

C code [29](#ch01.xhtml_page29)

flowchart [28](#ch01.xhtml_page28)

Python code [28](#ch01.xhtml_page28), [29](#ch01.xhtml_page29)

find sum and check if even program [162](#ch04.xhtml_page162)

algorithm [162](#ch04.xhtml_page162)

C code [164](#ch04.xhtml_page164), [165](#ch04.xhtml_page165)

flowchart [163](#ch04.xhtml_page163)

Python code [163](#ch04.xhtml_page163), [164](#ch04.xhtml_page164)

find sum of digits of a number program [230](#ch05_split_000.xhtml_page230)

algorithm [230](#ch05_split_000.xhtml_page230)

C code [232](#ch05_split_000.xhtml_page232), [233](#ch05_split_000.xhtml_page233)

flowchart [231](#ch05_split_000.xhtml_page231)

Python code [232](#ch05_split_000.xhtml_page232)

find sum of n elements program [154](#ch03.xhtml_page154)

algorithm [155](#ch03.xhtml_page155)

C code [156](#ch03.xhtml_page156), [157](#ch03.xhtml_page157)

flowchart [155](#ch03.xhtml_page155)

Python code [156](#ch03.xhtml_page156)

find sum of series 1 program

algorithm [146](#ch03.xhtml_page146)

C code [148](#ch03.xhtml_page148)

flowchart [147](#ch03.xhtml_page147)

Python code [147](#ch03.xhtml_page147), [148](#ch03.xhtml_page148)

find sum of series 2 program

algorithm [149](#ch03.xhtml_page149)

C code [151](#ch03.xhtml_page151)

flowchart [149](#ch03.xhtml_page149)

Python code [150](#ch03.xhtml_page150)

find sum of series 3 program [151](#ch03.xhtml_page151)

algorithm [152](#ch03.xhtml_page152)

C code [153](#ch03.xhtml_page153), [154](#ch03.xhtml_page154)

flowchart [152](#ch03.xhtml_page152)

Python code [153](#ch03.xhtml_page153)

find sum of two numbers program [10](#ch01.xhtml_page10)

algorithm [11](#ch01.xhtml_page11)

C code [12](#ch01.xhtml_page12), [13](#ch01.xhtml_page13)

flowchart [11](#ch01.xhtml_page11)

Python code [12](#ch01.xhtml_page12)

find type of triangle program [90](#ch02.xhtml_page90)

algorithm [91](#ch02.xhtml_page91)

C code [92](#ch02.xhtml_page92), [93](#ch02.xhtml_page93)

flowchart [91](#ch02.xhtml_page91)

Python code [92](#ch02.xhtml_page92)

find x raise to the power n program

algorithm [141](#ch03.xhtml_page141)

C code [142](#ch03.xhtml_page142), [143](#ch03.xhtml_page143)

flowchart [142](#ch03.xhtml_page142)

Python code [142](#ch03.xhtml_page142)

for loop [117](#ch03.xhtml_page117)

G

generate shopping bill during sale program [113](#ch02.xhtml_page113)

algorithm [113](#ch02.xhtml_page113)

C code [115](#ch02.xhtml_page115)

flowchart [114](#ch02.xhtml_page114)

Python code [114](#ch02.xhtml_page114), [115](#ch02.xhtml_page115)

generate shopping bill program [110](#ch02.xhtml_page110)

algorithm [110](#ch02.xhtml_page110)

C code [112](#ch02.xhtml_page112), [113](#ch02.xhtml_page113)

flowchart [111](#ch02.xhtml_page111)

Python code [111](#ch02.xhtml_page111), [112](#ch02.xhtml_page112)

greatest common divisor (GCD) [201](#ch04.xhtml_page201)

H

handling list/arrays program [206](#ch04.xhtml_page206)

algorithm [206](#ch04.xhtml_page206)

C code [208](#ch04.xhtml_page208), [209](#ch04.xhtml_page209)

flowchart [207](#ch04.xhtml_page207)

Python code [207](#ch04.xhtml_page207), [208](#ch04.xhtml_page208)

highest common factor (HCF) [201](#ch04.xhtml_page201)

House Rent Allowance (HRA) [109](#ch02.xhtml_page109)

L

living creatures identification program [299](#ch06.xhtml_page299)

algorithm [300](#ch06.xhtml_page300)

C code [302](#ch06.xhtml_page302), [303](#ch06.xhtml_page303)

flowchart [300](#ch06.xhtml_page300)

Python code [301](#ch06.xhtml_page301), [302](#ch06.xhtml_page302)

loops [117](#ch03.xhtml_page117)

for loop [117](#ch03.xhtml_page117)

while loop [117](#ch03.xhtml_page117)

M

minimize the difference program [325](#ch06.xhtml_page325), [328](#ch06.xhtml_page328)

algorithm [326](#ch06.xhtml_page326)

C code [329](#ch06.xhtml_page329), [330](#ch06.xhtml_page330)

flowchart [326](#ch06.xhtml_page326), [327](#ch06.xhtml_page327)

Python code [328](#ch06.xhtml_page328)

O

objects identification program [303](#ch06.xhtml_page303)

algorithm [304](#ch06.xhtml_page304)

C code [306](#ch06.xhtml_page306), [307](#ch06.xhtml_page307)

flowchart [305](#ch06.xhtml_page305)

Python code [305](#ch06.xhtml_page305), [306](#ch06.xhtml_page306)

obtain list having prime numbers

algorithm [242](#ch05_split_000.xhtml_page242)

C code [244](#ch05_split_000.xhtml_page244), [245](#ch05_split_000.xhtml_page245)

flowchart [243](#ch05_split_000.xhtml_page243)

Python code [243](#ch05_split_000.xhtml_page243), [244](#ch05_split_000.xhtml_page244)

obtain logical truth table program [56](#ch01.xhtml_page56)

algorithm [56](#ch01.xhtml_page56)

C code [58](#ch01.xhtml_page58), [59](#ch01.xhtml_page59)

flowchart [56](#ch01.xhtml_page56)

Python code [57](#ch01.xhtml_page57), [58](#ch01.xhtml_page58)

P

password validation and encryption program [335](#ch06.xhtml_page335)

algorithm [336](#ch06.xhtml_page336)

C code [340](#ch06.xhtml_page340), [344](#ch06.xhtml_page344)

flowchart [337](#ch06.xhtml_page337), [338](#ch06.xhtml_page338)

Python code [339](#ch06.xhtml_page339), [340](#ch06.xhtml_page340)

perform division program [16](#ch01.xhtml_page16)

algorithm [16](#ch01.xhtml_page16)

C code [18](#ch01.xhtml_page18)

flowchart [17](#ch01.xhtml_page17)

Python code [17](#ch01.xhtml_page17)

print 2-D pattern 1 program [268](#ch05_split_000.xhtml_page268)

algorithm [269](#ch05_split_000.xhtml_page269)

C code [270](#ch05_split_000.xhtml_page270)

flowchart [269](#ch05_split_000.xhtml_page269)

Python code [270](#ch05_split_000.xhtml_page270)

print 2-D pattern 2 program

algorithm [271](#ch05_split_000.xhtml_page271)

C code [273](#ch05_split_000.xhtml_page273)

flowchart [272](#ch05_split_000.xhtml_page272)

Python code [272](#ch05_split_000.xhtml_page272)

print 2-D pattern 3 program [273](#ch05_split_000.xhtml_page273)

algorithm [274](#ch05_split_001.xhtml_page274)

C code [275](#ch05_split_001.xhtml_page275)

flowchart [274](#ch05_split_001.xhtml_page274)

Python code [275](#ch05_split_001.xhtml_page275)

print 2-D pattern 4 program [276](#ch05_split_001.xhtml_page276)

algorithm [276](#ch05_split_001.xhtml_page276)

C code [277](#ch05_split_001.xhtml_page277), [278](#ch05_split_001.xhtml_page278)

flowchart [276](#ch05_split_001.xhtml_page276)

Python code [277](#ch05_split_001.xhtml_page277)

print 2-D pattern 5 program [278](#ch05_split_001.xhtml_page278)

algorithm [279](#ch05_split_001.xhtml_page279)

C code [280](#ch05_split_001.xhtml_page280), [281](#ch05_split_001.xhtml_page281)

flowchart [279](#ch05_split_001.xhtml_page279)

Python code [280](#ch05_split_001.xhtml_page280)

print 2-D pattern 6 program [281](#ch05_split_001.xhtml_page281)

algorithm [281](#ch05_split_001.xhtml_page281)

C code [283](#ch05_split_001.xhtml_page283)

flowchart [282](#ch05_split_001.xhtml_page282)

Python code [282](#ch05_split_001.xhtml_page282), [283](#ch05_split_001.xhtml_page283)

print 2-D pattern 7 program [284](#ch05_split_001.xhtml_page284)

algorithm [284](#ch05_split_001.xhtml_page284)

C code [286](#ch05_split_001.xhtml_page286)

flowchart [285](#ch05_split_001.xhtml_page285)

Python code [285](#ch05_split_001.xhtml_page285)

print 2-D pattern 8 program [286](#ch05_split_001.xhtml_page286)

algorithm [287](#ch05_split_001.xhtml_page287)

C code [289](#ch05_split_001.xhtml_page289)

flowchart [287](#ch05_split_001.xhtml_page287)

Python code [288](#ch05_split_001.xhtml_page288)

print 2-D pattern 9 program [289](#ch05_split_001.xhtml_page289)

algorithm [290](#ch05_split_001.xhtml_page290)

C code [292](#ch05_split_001.xhtml_page292)

flowchart [290](#ch05_split_001.xhtml_page290)

Python code [291](#ch05_split_001.xhtml_page291)

print equivalent rational numbers program [19](#ch01.xhtml_page19)

algorithm [19](#ch01.xhtml_page19)

C code [21](#ch01.xhtml_page21)

flowchart [19](#ch01.xhtml_page19)

Python code [20](#ch01.xhtml_page20)

print hotel bill program [311](#ch06.xhtml_page311)

algorithm [312](#ch06.xhtml_page312)

C code [315](#ch06.xhtml_page315), [316](#ch06.xhtml_page316)

flowchart [313](#ch06.xhtml_page313)

Python code [314](#ch06.xhtml_page314)

print matrix program [251](#ch05_split_000.xhtml_page251)

algorithm [252](#ch05_split_000.xhtml_page252)

C code [254](#ch05_split_000.xhtml_page254), [255](#ch05_split_000.xhtml_page255)

flowchart [253](#ch05_split_000.xhtml_page253)

Python code [254](#ch05_split_000.xhtml_page254)

print your details program [7](#ch01.xhtml_page7)

algorithm [8](#ch01.xhtml_page8)

C code [9](#ch01.xhtml_page9), [10](#ch01.xhtml_page10)

flowchart [8](#ch01.xhtml_page8)

Python code [8](#ch01.xhtml_page8), [9](#ch01.xhtml_page9)

print your lucky number program [5](#ch01.xhtml_page5)

algorithm [5](#ch01.xhtml_page5)

C code [6](#ch01.xhtml_page6), [7](#ch01.xhtml_page7)

flowchart [5](#ch01.xhtml_page5)

Python code [6](#ch01.xhtml_page6)

print your name program [3](#ch01.xhtml_page3), [5](#ch01.xhtml_page5)

algorithm [3](#ch01.xhtml_page3)

C code [4](#ch01.xhtml_page4), [5](#ch01.xhtml_page5)

flowchart [3](#ch01.xhtml_page3)

Python code [4](#ch01.xhtml_page4)

R

real-world problem solving programs

assign class rank [320](#ch06.xhtml_page320)

book storage optimization [296](#ch06.xhtml_page296)

convert decimals to different bases [330](#ch06.xhtml_page330)

find fewest denominations [317](#ch06.xhtml_page317)

minimize the difference [325](#ch06.xhtml_page325)

objects identification [303](#ch06.xhtml_page303)

password validation and encryption [335](#ch06.xhtml_page335)

print hotel bill [311](#ch06.xhtml_page311)

rock-paper-scissors [307](#ch06.xhtml_page307)

remove duplicate items program [245](#ch05_split_000.xhtml_page245)

algorithm [246](#ch05_split_000.xhtml_page246)

C code [247](#ch05_split_000.xhtml_page247), [248](#ch05_split_000.xhtml_page248)

flowchart [246](#ch05_split_000.xhtml_page246)

Python code [247](#ch05_split_000.xhtml_page247)

reverse the number program [233](#ch05_split_000.xhtml_page233)

algorithm [233](#ch05_split_000.xhtml_page233)

C code [235](#ch05_split_000.xhtml_page235)

flowchart [234](#ch05_split_000.xhtml_page234)

Python code [234](#ch05_split_000.xhtml_page234), [235](#ch05_split_000.xhtml_page235)

rock-paper-scissors game [307](#ch06.xhtml_page307), [308](#ch06.xhtml_page308)

algorithm [308](#ch06.xhtml_page308)

C code [310](#ch06.xhtml_page310), [311](#ch06.xhtml_page311)

flowchart [309](#ch06.xhtml_page309)

Python code [310](#ch06.xhtml_page310)

S

search a number program

algorithm [202](#ch04.xhtml_page202)

C code [205](#ch04.xhtml_page205)

flowchart [203](#ch04.xhtml_page203)

Python code [204](#ch04.xhtml_page204)

simple input output programs [2](#ch01.xhtml_page2)

convert degree F to degree C [40](#ch01.xhtml_page40)

convert inch to feet [42](#ch01.xhtml_page42)

convert meter to centimeter [37](#ch01.xhtml_page37)

find area of a circle [47](#ch01.xhtml_page47)

find area of a rectangle [45](#ch01.xhtml_page45)

find area of parallelogram [50](#ch01.xhtml_page50)

find average [31](#ch01.xhtml_page31)

find cube of a number [29](#ch01.xhtml_page29)

find distance between two points [52](#ch01.xhtml_page52)

find percentage marks [34](#ch01.xhtml_page34)

find product of two numbers [13](#ch01.xhtml_page13)

find square of a number [27](#ch01.xhtml_page27)

find sum of two numbers [10](#ch01.xhtml_page10)

obtain logical truth table [56](#ch01.xhtml_page56)

perform division [16](#ch01.xhtml_page16)

print equivalent rational numbers [19](#ch01.xhtml_page19)

print your details [7](#ch01.xhtml_page7)

print your lucky number [5](#ch01.xhtml_page5)

print your name [3](#ch01.xhtml_page3)

swapping using temporary variable [21](#ch01.xhtml_page21)

swapping without temporary variable [24](#ch01.xhtml_page24)

simple loops, in programming

display cube of numbers program [126](#ch03.xhtml_page126)

display factorial program [136](#ch03.xhtml_page136)

display Fibonacci series program [157](#ch03.xhtml_page157)

display multiples program [128](#ch03.xhtml_page128)

display natural numbers program [121](#ch03.xhtml_page121)

display square of natural numbers program [123](#ch03.xhtml_page123)

display sum and average program [131](#ch03.xhtml_page131)

display sum of square program [133](#ch03.xhtml_page133)

display the multiplication table program [143](#ch03.xhtml_page143)

display '*' program [118](#ch03.xhtml_page118)

find 2 raise to the power n program [138](#ch03.xhtml_page138)

find sum of n elements program [154](#ch03.xhtml_page154)

find sum of series 1 program [146](#ch03.xhtml_page146)

find sum of series 2 program [149](#ch03.xhtml_page149)

find sum of series 3 program [151](#ch03.xhtml_page151)

find x raise to the power n program [141](#ch03.xhtml_page141)

flowchart [126](#ch03.xhtml_page126)

sort the numbers program [248](#ch05_split_000.xhtml_page248)

algorithm [248](#ch05_split_000.xhtml_page248)

C code [250](#ch05_split_000.xhtml_page250), [251](#ch05_split_000.xhtml_page251)

flowchart [249](#ch05_split_000.xhtml_page249)

Python code [250](#ch05_split_000.xhtml_page250)

swapping using temporary variable program [21](#ch01.xhtml_page21)

algorithm [22](#ch01.xhtml_page22)

C code [23](#ch01.xhtml_page23), [24](#ch01.xhtml_page24)

flowchart [22](#ch01.xhtml_page22)

Python code [23](#ch01.xhtml_page23)

swapping without temporary variable program [24](#ch01.xhtml_page24)

algorithm [25](#ch01.xhtml_page25)

C code [26](#ch01.xhtml_page26), [27](#ch01.xhtml_page27)

flowchart [25](#ch01.xhtml_page25)

Python code [25](#ch01.xhtml_page25), [26](#ch01.xhtml_page26)

V

validate a triangle program [73](#ch02.xhtml_page73)

algorithm [73](#ch02.xhtml_page73)

C code [75](#ch02.xhtml_page75)

flowchart [74](#ch02.xhtml_page74)

Python code [74](#ch02.xhtml_page74)

W

while loop [117](#ch03.xhtml_page117)