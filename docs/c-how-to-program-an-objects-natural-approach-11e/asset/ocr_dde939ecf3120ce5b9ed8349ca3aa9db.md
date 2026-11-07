ing and managing your application’s files. In this book’s examples, you’ll typically place each program’s code files in the **Source Files** folder. If the **Solution Explorer** is not displayed, you can display it by selecting **View > Solution Explorer**.

# Step 4: Adding the GuessNumber.cpp File to the Project

Next, you’ll add to the project you created in *Step 3* the file GuessNumber.cpp, containing the C++ code that implements the guess-the-number game. In the **Solution Explorer**:

+   1. Right-click the **Source Files** folder and select **Add > Existing Item...**
+   2. In the dialog that appears, navigate to the ch01 subfolder of the book’s examples folder, select GuessNumber.cpp and click **Add**.[^64]

# Step 5: Configuring Your Project to Use C++20

The Visual C++ compiler in Visual Studio supports several C++ versions. For this book, we use C++20, which you must configure in your project’s settings:

+   1. Right-click the project’s node—**cpp20_test**—in the **Solution Explorer** and select **Properties** to display the project’s **cpp20_test Property Pages** dialog.
+   2. In the **Configuration** drop-down list, select **All Configurations**. In the **Platform** drop-down list, select **All Platforms**.
+   3. In the left column below **Configuration Properties**, expand the **C/C++** node, then select **Language**.
+   4. In the right column, click in the field to the right of **C++ Language Standard**, click the down arrow, then select **ISO C++20 Standard (/std:c++20)**[^65] and click **OK**.

# Step 6: Compiling and Running the Project

To compile and run the project so you can test-drive the guess-the-number game, select **Debug > Start without debugging** or type *Ctrl + F5*. If the program compiles correctly, Visual Studio opens a **Command Prompt** window and executes the program. We changed the **Command Prompt**’s color scheme and font size for readability:

![](bbox=[0.367, 0.626, 0.808, 0.71])

The title bar shows the location and name of the currently executing project.

# Step 7: Entering Your First Guess

At the ? prompt, type **500**, and press *Enter*—the program selects a number randomly each time you run it, so your interactions with the program will vary during each execution. In our case, the application displayed "Too low. Try again." to indicate the value was less than the number the application chose as the correct guess:

64. For the multiple source-code-file programs that you’ll see in later chapters, select all the files for a given program.

65. To try new C++ features as Microsoft adds them to Visual C++, select **Preview—Features from the Latest C++ Working Draft (/std:c++latest)** rather than **ISO C++20 Standard (/std:c++20)**.