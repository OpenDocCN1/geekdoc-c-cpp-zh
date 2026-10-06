# CHAPTER 4 Making Decisions

Event-driven programs often require fewer coded decisions. That's because of event-driven programs, some events are determined by the user's actions when the program is running (also called at runtime), rather than by the programmer's coding beforehand. You might say that in many situations, a console-based application may act, but an event-driven application has to react.

Suppose you want to write a program in which the user must select whether to receive instructions in English or Spanish. In a console application, you would issue a prompt such as the following:

Which language do you prefer? Enter 1 for English or 2 for Spanish >>

The program would accept the user's entry, make a decision about it, and take appropriate action. However, in a GUI application, you are more likely to place controls on a Form to get a user's response. For example, you might use two Buttons—one for English and one for Spanish. The user clicks a Button, and an appropriate method executes. No decision is written in the program because a different event is fired from each Button, causing execution of a different Click() method. The interactive environment decides which method is called, so the programmer does not have to code a decision. (Of course, you might alternatively place a TextBox on a Form and ask the user to enter a 1 or 2. In that case, the decision-making process would be identical to that in the console-based program.)

An additional benefit of having the user click to select an option is that the user cannot enter an invalid value. For example, if the user enters a letter in response to a prompt for an integer, the program will fail unless you write additional code to handle the mistake. However, if the user has a limited selection of buttons to click, no invalid entry can be made.

TWO TRUTHS & A LIE

Decision-Making Issues in GUI Programs

1. Event-driven programs can contain if...else, and switch statements.
2. Event-driven programs often require fewer coded decisions than console applications.
3. Event-driven programs usually contain more coded decisions than corresponding console-based applications.

The false statement is #3. Event-driven programs often require fewer coded decisions because user actions, such as clicking a button, are often trigger different methods.

172

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202