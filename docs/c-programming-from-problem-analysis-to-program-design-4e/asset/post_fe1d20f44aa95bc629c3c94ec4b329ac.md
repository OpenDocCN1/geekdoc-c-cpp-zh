
![](img/36e48639a06772bcb0fa1ea2525b33a3_532_0.png)

## Chapter 9

Nate Goussal / Shutterstock.com

## Introduction to Windows Programming

### IN THIS CHAPTER, YOU WILL:

- Differentiate between the functions of Windows applications and console applications
- Learn about graphical user interfaces
- Become aware of some elements of good design
- Use C# and Visual Studio to create Windows-based applications
- Create Windows forms and be able to change form properties
- Add control objects such as buttons, labels, and text boxes to a form
- Work through a programming example that illustrates the chapter's concepts

- 28. Using the following declarations, write solutions for Steps a through e.

  ```
  int[,] cArray = new int[2, 3];
  string[,] dArray = new string[5, 2, 6];
  ```

  - a. Write a `foreach` loop to display the contents of cArray.
  - b. Write a `for` loop to increment each element in cArray by 5.
  - c. Write a `foreach` loop to display the contents of dArray.
  - d. Can you use a `foreach` loop to initialize all elements of dArray with zero? If so, show your code. If not, explain why.
  - e. Write a `for` loop to initialize all elements in dArray to zero.

- 29. Create array declarations for the following problem specifications.

  - a. An array to hold the name of the largest 3 cities for 5 states. Initialize with the 5 states closest to your campus.
  - b. A single array to hold the names of 10 people. You should be able to reference each person’s first name without having to use `string` manipulation methods to split the data apart.
  - c. A single array to store keys for five exams each consisting of 15 true/false questions.

- 30. Explain the difference between the .NET Hashtable and Dictionary classes.

## PROGRAMMING EXERCISES

- 1. Write an application that creates and returns a one-dimensional array containing all the elements in the two-dimensional array. Store the values in a row-major format. For testing purposes, you may do a compile-time initialization of a 12 x 5 two-dimensional array. Display both the two-dimensional and the one-dimensional array. Be sure the values in the array are number-aligned.

- 2. Write an application that will let you keep a tally of how well three salesmen are performing selling five different products. You should use a two-dimensional array to solve the problem. Allow the user to input any number of sales amounts. Do a compile-time initialization of the salespersons' names and product list. Produce a report by salesman, showing the total sales per product.

- 3. Revise your solution for problem 2 so that you display the total sales per salesman. Place the first and last names for the salesmen in an array. Write your solution so that any number of salesmen and any number of products can be displayed. When you display your final output, print the salesman’s name only, sales for each product, and the final sales for the salesman. After you display the tables of sales, display the largest sales figure indicating which salesman sold it and which product was sold.

- 4. Write a two-class application that creates a customer code to be placed on a mailing label for a magazine. Allow the user to input their full name with the first name entered first. Prompt them to separate their first and last name with a space. Ask for their birthdate in the format of mm/dd/yyyy. Ask for the month (number) they purchased a subscription and ask for their zip code. Your mailing label should contain the last name, followed by their year of birth, the number of characters in the full name, the first three characters of the month they purchased the subscription, and the last two digits of their zip. The code for Bob Clocksom born 01/22/1993, who purchased his subscription during the 10th month of the year and lists 32226 as his zip code would be Clocksom9312Oct26.

- 5. Write a program that allows the user to enter any number of names. Your prompt can inform the user to input their first name followed by a space and last name. Order the names in ascending order and display the results with the last name listed first, followed by a comma and then the first name. If a middle initial is entered, it should follow the first name. Your solution should also take into consideration that some users may only enter their last name (one name).

- 6. Write an application that creates a two-dimensional array. Allow the user to input the size of the array (number of rows and number of columns). Fill the array with random numbers between 0 and 100. Search the array for the largest value. Display the array values, number-aligned, and the indexes where the largest value is stored.

- 7. Write a program that creates a two-dimensional array with 10 rows and 2 columns. The first column should be filled with 10 random numbers between 0 and 100. The second column should contain the squared value of the element found in column 1. Using the Show() method of the MessageBox class, display a table.

- 8. reAay ouyay aay hizway ithway igPay atinLay? (Translated: “Are you a whiz with Pig Latin?”) Write a program that converts an English phrase into a pseudo-Pig Latin phrase (that is Pig Latin that doesn’t follow all the Pig Latin syntax rules). Use predefined methods of the Array and string classes to do the work. For simplicity in your conversion, place the first letter as the last character in the word and prefix the characters “ay” onto the end. For example, the word “example” would become “xampleeay”, and “method” would become “ethodmay.” Allow the user to input the English phrase. After converting it, display the new Pig Latin phrase.

- 9. Write an application that displays revenue generated for exercise classes at the Tappan Gym. The gym offers two types of exercise classes, zumba and spinning, six days per week, four times per day. Zumba is offered at 1, 3, 5, and 7 p.m.; spinning is offered at 2, 4, 6, and 8 p.m. When attendees sign up, they agree to pay $4.00 per class for zumba and $5.00 for spinning. Produce a table displaying the number of attendees per time slot. Display a row and column of totals showing the total number of attendees by day and also time period. Also include a column showing the revenue generated each day and the overall revenue per type of exercise. Do a compile-time initialization of your data structures using data from the following table.

  | Zumba | 1:00 | 3:00 | 5:00 | 7:00 |
  |---|---:|---:|---:|---:|
  | Monday | 12 | 10 | 17 | 22 |
  | Tuesday | 11 | 13 | 17 | 22 |
  | Wednesday | 12 | 10 | 22 | 22 |
  | Thursday | 9 | 14 | 17 | 22 |
  | Friday | 12 | 10 | 21 | 12 |
  | Saturday | 12 | 10 | 5 | 10 |

  | Spinning | 2:00 | 4:00 | 6:00 | 8:00 |
  |---|---:|---:|---:|---:|
  | Monday | 7 | 11 | 15 | 8 |
  | Tuesday | 9 | 9 | 9 | 9 |
  | Wednesday | 3 | 12 | 13 | 7 |
  | Thursday | 2 | 9 | 9 | 10 |
  | Friday | 8 | 4 | 9 | 4 |
  | Saturday | 4 | 5 | 9 | 3 |

- 10. Write an application that enables you to randomly record water depths for 5 different locations at 0700 (7 a.m.), 1200 (noon), 1700 (5 p.m.), and 2100 (9 p.m.). The locations are Surf City, Solomons, Hilton Head, Miami, and Savannah. For ease of input, you may want to code the locations (i.e., Surf City = 1, Solomons = 2, etc.) and code the time (i.e., 0700 = 1, 1200 = 2, etc.). If the same location and time are entered more than one time, store the last value entered into the array. After the data is entered, display the average depth at each location and the average depth by time period.

If you have read and completed the exercises in the previous chapters, you now have a solid programming foundation and can build fairly sophisticated console-based applications. These types of applications are excellent for learning the basic elements of programming and are appropriate for many types of small, utility applications today. However, you probably consider them boring. In your daily life, you have become accustomed to using modern programs that look and act like Windows applications. In this chapter, you will learn to create those types of applications.

Building Windows-based applications was a complicated endeavor in the past; this is no longer the case. Included in the .NET Framework class library is an entire subsystem of classes that enables you to create highly interactive, attractive, graphical user interface (GUI) applications. Using Visual Studio, it is easy to perform drag-and-drop constructions. In the next two chapters, you will be introduced to many classes in the System.Windows.Forms namespace, including control classes such as Label, Button, and TextBox that can be placed on a Windows Form container class. A different way of programming based on interactively responding to events such as mouse clicks will be introduced. In Chapter 10, you will extend this knowledge by creating applications that are more event-driven and are used for capturing and responding to user input. By the time you complete Chapter 10, you will be building fun, interactive Windows-based applications.

### Contrasting Windows and Console Applications

When a Windows application executes, it functions differently from the console-based applications you have been writing. With a console-based application, each line in the Main() method is executed sequentially. Then the program halts. Method calls might branch to different locations in your program; however, control always returns back to the Main() method. When the closing curly brace is encountered in Main(), execution halts with console-based applications. With your console applications, the program initiates interaction with the operating system by calling the operating system to get data using the ReadLine() method. It calls on the operating system to output data through method calls such as WriteLine() or Write().

For both Windows and console applications, execution begins with the first statement in the Main() method. However, with a Windows application, instead of the program executing sequential statements from top to bottom, the application, once launched, sits in what is called a process loop waiting for an event to execute. An event is a notification from the operating system that an action, such as the user clicking the mouse or pressing a key, has occurred. Instead of calling on the operating system with a request, as a console application does, Windows applications receive messages from the operating system that an event has occurred. With Windows applications, you write methods called event handlers to indicate what should be done when an event such as a mouse click on a button or the press of a key occurs.
