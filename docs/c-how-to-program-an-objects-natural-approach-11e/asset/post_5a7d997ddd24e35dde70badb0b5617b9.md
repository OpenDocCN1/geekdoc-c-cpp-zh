
ing and managing your application’s files. In this book’s examples, you’ll typically place each program’s code files in the **Source Files** folder. If the **Solution Explorer** is not displayed, you can display it by selecting **View > Solution Explorer**.

### Step 4: Adding the GuessNumber.cpp File to the Project

Next, you’ll add to the project you created in *Step 3* the file GuessNumber.cpp, containing the C++ code that implements the guess-the-number game. In the **Solution Explorer**:

- 1. Right-click the **Source Files** folder and select **Add > Existing Item...**
- 2. In the dialog that appears, navigate to the ch01 subfolder of the book’s examples folder, select GuessNumber.cpp and click **Add**.[^64]

### Step 5: Configuring Your Project to Use C++20

The Visual C++ compiler in Visual Studio supports several C++ versions. For this book, we use C++20, which you must configure in your project’s settings:

- 1. Right-click the project’s node—**cpp20_test**—in the **Solution Explorer** and select **Properties** to display the project’s **cpp20_test Property Pages** dialog.
- 2. In the **Configuration** drop-down list, select **All Configurations**. In the **Platform** drop-down list, select **All Platforms**.
- 3. In the left column below **Configuration Properties**, expand the **C/C++** node, then select **Language**.
- 4. In the right column, click in the field to the right of **C++ Language Standard**, click the down arrow, then select **ISO C++20 Standard (/std:c++20)**[^65] and click **OK**.

### Step 6: Compiling and Running the Project

To compile and run the project so you can test-drive the guess-the-number game, select **Debug > Start without debugging** or type *Ctrl + F5*. If the program compiles correctly, Visual Studio opens a **Command Prompt** window and executes the program. We changed the **Command Prompt**’s color scheme and font size for readability:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_88_0.png)

The title bar shows the location and name of the currently executing project.

### Step 7: Entering Your First Guess

At the ? prompt, type **500**, and press *Enter*—the program selects a number randomly each time you run it, so your interactions with the program will vary during each execution. In our case, the application displayed "Too low. Try again." to indicate the value was less than the number the application chose as the correct guess:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_89_0.png)

### Step 8: Entering Another Guess

At the next prompt, if your system said the first guess was too low, type **750** and press *Enter*; otherwise, type **250** and press *Enter*. In our case, we entered **750**, and the application displayed "Too high. Try again." because the value was greater than the correct guess:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_89_1.png)

### Step 9: Entering Additional Guesses

Continue to play the game by entering values until you guess the correct number. When you guess correctly, the application displays "Excellent! You guessed the number!".

![](img/7b5e2088e71c7f78681d4ddbcf104c06_89_2.png)

### Step 10: Playing the Game Again or Exiting the Application

After guessing the correct number (which you should always be able to do in 10 or fewer guesses), the application asks if you’d like to play another game. At the "Would you like to play again (y or n)?" prompt, entering y causes the application to choose a new number and start a new game. Entering n terminates the application.

## Reusing This Project for Subsequent Examples

You can follow the steps in this section to create a separate project for every application in the book. However, for our examples, you may find it more convenient to remove the current program from the project, then add a new program. To remove a file from your project (but not your system), select it in the **Solution Explorer**, then press *Del* (or *Delete*). You can then repeat *Step 4* to add a different program to the project. When you begin creating programs yourself, you can right-click the **Source Files** folder and select **Add > New Item...** to display a dialog for adding a new file.

## Using Ubuntu Linux in the Windows Subsystem for Linux

Some Windows users may want to use the GNU g++ compiler on Windows. You can do this using the GNU Compiler Collection Docker container (Section 1.11.3), or you can use g++ in Ubuntu Linux running in the Windows Subsystem for Linux. To install the Windows Subsystem for Linux, follow the instructions at

```text
https://docs.microsoft.com/en-us/windows/wsl/install
```

Once you install and launch the Ubuntu app on your Windows system, you can use the following command to change to the folder containing the test-drive code example on your Windows system:

```text
cd /mnt/c/Users/YourUserName/Documents/examples/ch01
```

Then you can continue with *Step 2* in Section 1.11.2.

## 1.11.2 Compiling and Running with GNU C++ on Linux

In this section, you’ll run a C++ program in a Linux shell using the GNU C++ compiler (g++).[^66] For this test-drive, we assume that you’ve read the *Before You Begin* section and that you’ve placed the book’s examples in your user account’s Documents/examples folder.

### Step 1: Changing to the ch01 Folder

From a Linux shell or Terminal window, use the cd command to change to the ch01 sub-folder of the book’s examples folder:

```bash
~$ cd ~/Documents/examples/ch01
~/Documents/examples/ch01$
```

In this section’s figures, we use **bold** to highlight the user inputs. The prompt in our Ubuntu Linux shell uses a tilde (~) to represent the home directory. Each prompt ends with the dollar sign ($). The prompt may differ on your Linux system.

### Step 2: Compiling the Application

Before running the application, you must first compile it with the g++ command.[^67]

- The `-std=c++20` option indicates that we’re using C++20.
- The `-o` option names the executable file (GuessNumber) that you’ll use to run the program. If you do not include this option, g++ automatically names the executable a.out.

```text
~/Documents/examples/ch01$ g++ -std=c++20 GuessNumber.cpp -o GuessNumber
~/Documents/examples/ch01$
```

### Step 3: Running the Application

Type ./GuessNumber at the prompt and press *Enter* to run the program:

```text
~/Documents/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
?
```

The ./ before GuessNumber tells Linux to run GuessNumber from the current directory.

### Step 4: Entering Your First Guess

The application displays "Please type your first guess.", then displays a question mark (?) as a prompt on the next line. At the prompt, enter 500—the program selects a number randomly each time you run it, so your interactions with the program will vary during each execution:

```text
~/Documents/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
? 500
Too high. Try again.
?
```

In our case, the application displayed "Too high. Try again." because the value entered was greater than the number the application chose as the correct guess.

[^64]: For the multiple source-code-file programs that you’ll see in later chapters, select all the files for a given program.

[^65]: To try new C++ features as Microsoft adds them to Visual C++, select **Preview—Features from the Latest C++ Working Draft (/std:c++latest)** rather than **ISO C++20 Standard (/std:c++20)**.

[^66]: At the time of this writing, the current g++ version was 13.1. You can determine your system’s g++ version number with the command `g++ --version`. If you have an older version of g++, consider searching online for the instructions to upgrade the GNU Compiler Collection (GCC) for your Linux distribution or consider using the GCC Docker container discussed in Section 1.11.3.

[^67]: If you have multiple g++ versions installed, you might need to use `g++-##`, where `##` is the g++ version number. For example, the command `g++-13` might be required to run g++ version 13.
