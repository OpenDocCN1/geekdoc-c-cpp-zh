
## 25 ATM Case Study, Part 1: Object-Oriented Design with the UML

![](img/bfd978e7e9b192bab46ec2a89e481263_1104_0.png)

> Action speaks louder than words but not nearly as often.  
> —Mark Twain

> Always design a thing by considering it in its next larger context.  
> —Eliel Saarinen

> Oh, life is a glorious cycle of song.  
> —Dorothy Parker

> The Wright brothers’ design allowed them to survive long enough to learn how to fly.  
> —Michael Potts

### Objectives

In this chapter you’ll learn:

- A simple object-oriented design methodology.
- What a requirements document is.
- To identify classes and class attributes from a requirements document.
- To identify objects’ states, activities and operations from a requirements document.
- To determine the collaborations among objects in a system.
- To work with the UML’s use case, class, state, activity, communication and sequence diagrams to graphically model an object-oriented system.

- 25.1 Introduction
- 25.2 Introduction to Object-Oriented Analysis and Design
- 25.3 Examining the ATM Requirements Document
- 25.4 Identifying the Classes in the ATM Requirements Document
- 25.5 Identifying Class Attributes
- 25.6 Identifying Objects’ States and Activities
- 25.7 Identifying Class Operations
- 25.8 Indicating Collaboration Among Objects
- 25.9 Wrap-Up

### 25.1 Introduction

Now begin the optional portion of our object-oriented design and implementation case study. In this chapter and Chapter 26, you’ll design and implement an object-oriented automated teller machine (ATM) software system. The case study provides you with a concise, carefully paced, complete design and implementation experience. You’ll perform the steps of an object-oriented design (OOD) process using the UML while relating them to the object-oriented concepts discussed in Chapters 2–13. In this chapter, you’ll work with six popular types of UML diagrams to graphically represent the design. In Chapter 26, you’ll tune the design with inheritance and polymorphism, then fully implement the ATM in an 850-line C++ application (Section 26.4).

This is not an exercise; rather, it’s an end-to-end learning experience that concludes with a detailed walkthrough of the complete C++ code that implements our design. It will acquaint you with the kinds of substantial problems encountered in industry.

These chapters can be studied as a continuous unit after you’ve completed the introduction to object-oriented programming in Chapters 2–13. Or, you can pace the sections after Chapters 3–7, 9 and 13. Each section of the case study begins with a note telling you the chapter after which it can be covered.

### 25.2 Introduction to Object-Oriented Analysis and Design

What if you were asked to create a software system to control thousands of automated teller machines for a major bank? Or suppose you were asked to work on a team of 1000 software developers building the next U.S. air traffic control system. For projects so large and complex, you cannot simply sit down and start writing programs.

To create the best solutions, you should follow a process for analyzing your project’s requirements (i.e., determining what the system should do) and developing a design that satisfies them (i.e., deciding how the system should do it). Ideally, you’d go through this process and carefully review the design (or have your design reviewed by other software professionals) before writing any code. If this process involves analyzing and designing your system from an object-oriented point of view, it’s called an object-oriented analysis and design (OOAD) process. Analysis and design can save many hours by helping you to avoid an ill-planned system-development approach that has to be abandoned part of the way through its implementation, possibly wasting considerable time, money and effort. Small problems do not require an exhaustive OOAD process. It may be sufficient to write pseudocode before you begin writing C++ code.

As problems and the groups of people solving them increase in size, the methods of OOAD become more appropriate than pseudocode. Ideally, members of a group should agree on a strictly defined process for solving their problem and a uniform way of communicating the results of that process to one another. Although many different OOAD processes exist, a single graphical language for communicating the results of *any* OOAD process has come into wide use. This language, known as the Unified Modeling Language (UML), was developed in the mid-1990s under the initial direction of three software methodologists—Grady Booch, James Rumbaugh, and Ivar Jacobson.

### 25.3 Examining the ATM Requirements Document

*[Note: This section can be studied after Chapter 3.]*

We begin our design process by presenting a **requirements document** that specifies the ATM system’s overall purpose and *what it must do*. Throughout the case study, we refer to the requirements document to determine what functionality the system must include.

### Requirements Document

A local bank intends to install a new automated teller machine (ATM) to allow users (i.e., bank customers) to perform basic financial transactions (Fig. 25.1). Each user can have only one account at the bank. ATM users should be able to *view their account balance*, *withdraw cash* (i.e., take money out of an account) and *deposit funds* (i.e., place money into an account).

![](img/bfd978e7e9b192bab46ec2a89e481263_1106_0.png)

**Fig. 25.1 |** *Automated teller machine user interface.*

The user interface of the automated teller machine contains the following hardware components:

- a screen that displays messages to the user

![](img/bfd978e7e9b192bab46ec2a89e481263_1108_0.png)

**Fig. 25.2 |** *ATM main menu.*

After the ATM authenticates the user, the main menu (Fig. 25.2) displays a numbered option for each of the three types of transactions: balance inquiry (option 1), withdrawal (option 2) and deposit (option 3). The main menu also displays an option that allows the user to exit the system (option 4). The user then chooses either to perform a transaction (by entering 1, 2 or 3) or to exit the system (by entering 4). If the user enters an invalid option, the screen displays an error message, then redisplays the main menu.

If the user enters 1 to make a balance inquiry, the screen displays the user’s account balance. To do so, the ATM must retrieve the balance from the bank’s database.

The following actions occur when the user enters 2 to make a withdrawal:

- **1.** The screen displays a menu (shown in Fig. 25.3) containing standard withdrawal amounts: $20 (option 1), $40 (option 2), $60 (option 3), $100 (option 4) and $200 (option 5). The menu also contains an option to allow the user to cancel the transaction (option 6).
- **2.** The user enters a menu selection (1–6) using the keypad.
- **3.** If the withdrawal amount chosen is greater than the user’s account balance, the screen displays a message stating this and telling the user to choose a smaller amount. The ATM then returns to *Step 1*. If the withdrawal amount chosen is less than or equal to the user’s account balance (i.e., an acceptable withdrawal amount), the ATM proceeds to *Step 4*. If the user chooses to cancel the transaction (option 6), the ATM displays the main menu (Fig. 25.2) and waits for user input.
- **4.** If the cash dispenser contains enough cash to satisfy the request, the ATM proceeds to *Step 5*. Otherwise, the screen displays a message indicating the problem and telling the user to choose a smaller withdrawal amount. The ATM then returns to *Step 1*.

![](img/bfd978e7e9b192bab46ec2a89e481263_1109_0.png)

**Fig. 25.3 |** *ATM withdrawal menu.*

- **5.** The ATM debits (i.e., subtracts) the withdrawal amount from the user’s account balance in the bank’s database.
- **6.** The cash dispenser dispenses the desired amount of money to the user.
- **7.** The screen displays a message reminding the user to take the money.

The following actions occur when the user enters 3 (while the main menu is displayed) to make a deposit:

- **1.** The screen prompts the user to enter a deposit amount or to type 0 (zero) to cancel the transaction.
- **2.** The user enters a deposit amount or 0, using the keypad. [*Note:* The keypad does not contain a decimal point or a dollar sign, so the user cannot type a real dollar amount (e.g., $1.25). Instead, the user must enter a deposit amount as a number of cents (e.g., 125). The ATM then divides this number by 100 to obtain a number representing a dollar amount (e.g., 125 ÷ 100 = 1.25).]
- **3.** If the user specifies a deposit amount, the ATM proceeds to **Step 4**. If the user chooses to cancel the transaction (by entering 0), the ATM displays the main menu (Fig. 25.2) and waits for user input.
- **4.** The screen displays a message telling the user to insert a deposit envelope into the deposit slot.
- **5.** If the deposit slot receives a deposit envelope within two minutes, the ATM credits (i.e., adds) the deposit amount to the user’s account balance in the bank’s database. *This money is not immediately available for withdrawal. The bank first must physically verify the amount of cash in the deposit envelope, and any checks in the envelope.*
