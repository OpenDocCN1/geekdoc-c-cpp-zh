
data types in the remainder of this chapter. In Chapter 4, we will talk more about
Boolean data types when we write apps with decision-making.

> NOTE: Localizing your app is the process of writing your app so users can buy and use it in their
native language. This process is so advanced for this book, but it is a simple one to complete
when you plan from the beginning. Localizing your app greatly expands the total number of
potential customers and revenue for your app without having to rewrite it for each language.
Be sure to localize your app. It is not hard to do and can easily double or triple the number
people who buy it.

## Using Variable and Data Types with Alice

Now that we have learned about data types, let's write an Alice app that adds two
numbers and displays the sum using object and methods.

- 1. Open Alice and select File ➤ New World.

- 2. Select the Grass template and click Open. See Figure 3–4.

![](img/322e107ddf8f5cd963a6efafdcd86f38_53_0.png)

Figure 3–4. Choosing the Grass template

Next, we need to make our variables and select the data types.

- 3. Click and drag the local tile on the top right of your editor

- 4. Name your first variable "firstNumber" and define the variable, as shown Figure 3–5.

- 5. The variable's data type is an integer. It is initialized with the value of 2.

![](img/322e107ddf8f5cd963a6efafdcd86f38_54_0.png)

Figure 3–5. Creating a new local variable

It is always good programming practice to initialize our variables when they are declared.

- 6. Create another local variable called "secondNumber", as shown in Figure 3–6 and as done in step 5. The variable's data type is an integer and is initialized with the value of 3.

## CHAPTER 3: It's All About the Data

![](img/322e107ddf8f5cd963a6efafdcd86f38_55_0.png)

**Figure 3–6.** Creating a second local variable

- 7. Create another local variable called "totalSum", as shown in Figure 3–7 and as done in step 5. The variable's data type is an integer and is initialized with the value of 0. This local variable will eventually hold the sum of firstNumber and secondNumber.

## CHAPTER 3: It's All About the Data

![](img/322e107ddf8f5cd963a6efafdcd86f38_56_0.png)

- 8. Add your two variables together. Drag the totalSum tile to the last row. Right now, O is assigned to the local variable totalSum. Click on the 0 and assign firstNumber to totalSum. See Figure 3-8.

![](img/322e107ddf8f5cd963a6efafdcd86f38_56_1.png)

- 9. Now that firstNumber is assigned to totalSum, click on the firstNumber tile.

- 10. Select secondNumber to add to firstNumber. See figure 3-9.

![](img/322e107ddf8f5cd963a6efafdcd86f38_57_0.png)

- 11. **totalNumber** is now assigned to the total of firstNumber and secondNumber. See Figure 3–10.

![](img/322e107ddf8f5cd963a6efafdcd86f38_58_0.png)

Now we need to add a character to our world to display our total.

- 12. Click on Edit Scene and then add any object of your choosing from the Object Gallery at the bottom of the screen. We have selected a bunny. See Figure 3–11.

## CHAPTER 3: It's All About the Data

![](img/322e107ddf8f5cd963a6efafdcd86f38_59_0.png)

Figure 3-11. Adding a bunny to the world

We need to declare a variable of type String. The variable will hold the string, “The sum of 2 + 3 is:5”.

- 13. Click “Edit Code” in the bottom right of the scene to go back to our Editor.

- 14. Select the Bunny instance. From the Procedures Tab, drag the this.bunny text:??? procedure tile to the editor. See Figure 3–12.

## CHAPTER 3: It's All About the Data

![](img/322e107ddf8f5cd963a6efafdcd86f38_60_0.png)

Figure 3-12. Adding the procedure (method) say to the editor

- 15. Click on Custom TextString and enter the string “The sum of 2 + 3 is:” as the parameter value. See Figure 3–13.

![](img/322e107ddf8f5cd963a6efafdcd86f38_60_1.png)

Figure 3–13. Entering the string parameter

- 16. Click OK and then click on the first parameter for the say procedure.
Append the totalSum to our first parameter. See Figure 3–14.

![](img/322e107ddf8f5cd963a6efafdcd86f38_61_0.png)

Figure 3–14. Adding the totalNumber to our customized string to display to the user

Alice did something very nice for us in the last step. It automatically converted the data type totalSum from an integer to a string when it appended its value to the "The sum of 2 + 3 is". We will learn how to do this using Objective-C.

You can run the program now and notice the customized string doesn't display for very long.

To increase the display time of our customized string, click on the option for a second parameter of the say procedure and change the duration to 2 seconds or any other value you like. See Figure 3–15.

## CHAPTER 3: It's All About the Data

![](img/322e107ddf8f5cd963a6efafdcd86f38_62_0.png)

Figure 3–15. The editor section

- 17. Press the play button and if you've done everything correctly, your app should look like Figure 3-16 when it runs.

![](img/322e107ddf8f5cd963a6efafdcd86f38_62_1.png)

Figure 3–16. The app has run successfully!

## Data Types and Objective-C

Now that we have covered the principles of data types and have written an Alice app to help show how these principles apply, let's write an Objective-C app that accomplishes what we just did in Alice.

In Objective-C, we have similar data types as we did in Alice. Some of the most frequently used data types for storing numbers are integers, doubles, floats, and longs.

Table 3–5. Objective-C basic types

| Type | Examples | Specifiers |
| :--- | :--- | :--- |
| char | 'a' | %c |
| int | 42 | %d |
| unsigned int | 42 | %u |
| long | 42 | %ld |
| unsigned long | 42 | %lu |
| long long | 42 | %llu |
| float | 3.1 | %f |
| double | 3.1 | %f |
| long double | 3.1 | %Lf |
| id | Nil | %@ |

- 1. Open Alice and select File ➤ New World.

- 2. Select the Grass template and click Open. See Figure 3–4.

![](img/322e107ddf8f5cd963a6efafdcd86f38_53_0.png)

Figure 3–4. Choosing the Grass template

- 3. Click and drag the local tile on the top right of your editor

- 4. Name your first variable "firstNumber" and define the variable, as shown Figure 3–5.

- 5. The variable's data type is an integer. It is initialized with the value of 2.

![](img/322e107ddf8f5cd963a6efafdcd86f38_54_0.png)

Figure 3–5. Creating a new local variable

- 6. Create another local variable called "secondNumber", as shown in Figure 3–6 and as done in step 5. The variable's data type is an integer and is initialized with the value of 3.

![](img/322e107ddf8f5cd963a6efafdcd86f38_55_0.png)

**Figure 3–6.** Creating a second local variable

- 7. Create another local variable called "totalSum", as shown in Figure 3–7 and as done in step 5. The variable's data type is an integer and is initialized with the value of 0. This local variable will eventually hold the sum of firstNumber and secondNumber.

- 8. Add your two variables together. Drag the totalSum tile to the last row. Right now, O is assigned to the local variable totalSum. Click on the 0 and assign firstNumber to totalSum. See Figure 3-8.

![](img/322e107ddf8f5cd963a6efafdcd86f38_56_1.png)

- 9. Now that firstNumber is assigned to totalSum, click on the firstNumber tile.

- 10. Select secondNumber to add to firstNumber. See figure 3-9.

![](img/322e107ddf8f5cd963a6efafdcd86f38_57_0.png)

- 11. **totalNumber** is now assigned to the total of firstNumber and secondNumber. See Figure 3–10.

![](img/322e107ddf8f5cd963a6efafdcd86f38_58_0.png)

- 12. Click on Edit Scene and then add any object of your choosing from the Object Gallery at the bottom of the screen. We have selected a bunny. See Figure 3–11.

![](img/322e107ddf8f5cd963a6efafdcd86f38_59_0.png)

Figure 3-11. Adding a bunny to the world

- 13. Click “Edit Code” in the bottom right of the scene to go back to our Editor.

- 14. Select the Bunny instance. From the Procedures Tab, drag the this.bunny text:??? procedure tile to the editor. See Figure 3–12.

![](img/322e107ddf8f5cd963a6efafdcd86f38_60_0.png)

Figure 3-12. Adding the procedure (method) say to the editor

- 15. Click on Custom TextString and enter the string “The sum of 2 + 3 is:” as the parameter value. See Figure 3–13.

![](img/322e107ddf8f5cd963a6efafdcd86f38_60_1.png)

Figure 3–13. Entering the string parameter

- 16. Click OK and then click on the first parameter for the say procedure.
Append the totalSum to our first parameter. See Figure 3–14.

![](img/322e107ddf8f5cd963a6efafdcd86f38_61_0.png)

Figure 3–14. Adding the totalNumber to our customized string to display to the user

- 17. Press the play button and if you've done everything correctly, your app should look like Figure 3-16 when it runs.

![](img/322e107ddf8f5cd963a6efafdcd86f38_62_1.png)

Figure 3–16. The app has run successfully!
