
## What's Next?

If you're reading this paragraph, you've probably followed some of the instructions in this chapter — instructions for installing Java and the Eclipse IDE on your computer. So the burning question is this: Have you done the installation correctly? The answer to that question lies in Chapter 3 because in that chapter, you use these tools to run a brand-new Java program.

## Chapter 3
## Running Programs

### In This Chapter

- Compiling and running a program
- Working with a workspace
- Editing your own Java code

If you're a programming newbie, for you, running a program probably means clicking a mouse. You want to run Internet Explorer, so you double-click the Internet Explorer icon. That's all there is to it.

When you create your own programs, the situation is a bit different. With a new program, the programmer (or someone from the programmer's company) creates the program's icon. Before that process, a perfectly good program may not have an icon at all. So what do you do with a brand-new Java program? How do you get the program to run? This chapter tells you what you need to know.

### Running a Canned Java Program

The best way to get to know Java is to do Java. When you're doing Java, you're writing, testing, and running your own Java programs. This section prepares you by describing how you run and test a program. Instead of writing your own program, you run a program that I've already written for you. The program calculates your monthly payments on a home mortgage loan.

The mortgage-calculating program doesn't open its own window. Instead, the program runs in Eclipse's Console view. The Console view is one of the tabs in the lower-right part of the Eclipse workbench (see Figure 3-1). A program that operates completely in this Console view is called a text-based program.

Figure 3-1: A run of this chapter's text-based mortgage program.

![](img/f938eba5f15e231d828a6255e7ec5523_69_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_69_1.png)

You may not see a Console tab in the lower-right part of the Eclipse workbench. To coax the Console view out of hiding, choose Window→Show View→Other. In the resulting Show View dialog box, expand the General branch. Finally, within that General branch, double-click the Console item.

For more information about the Console view (and about Eclipse's workbench in general), see the "Views, editors, and other stuff" section, later in this chapter.

![](img/f938eba5f15e231d828a6255e7ec5523_69_2.png)

You can see GUI versions of the program in Figure 3-1, and of many other examples from this book, by visiting the book's website (allmycode.com/BeginProg).

Actually, as you run the mortgage program, you see two things in Eclipse's Console view:

> Messages and results that the mortgage program sends to you: Messages include things like How much are you borrowing?. Results include lines like Your monthly payment is $552.20.

> Responses that you give to the mortgage program while it runs: If you type 100000.00 in response to the program's question about how much you're borrowing, you see that number echoed in Eclipse's Console view.

Here's how you run the mortgage program:

1. Make sure that you've followed the instructions in Chapter 2 — instructions for installing Java, for installing and configuring Eclipse, and for getting this book's sample programs.
   Thank goodness! You don't have to follow those instructions more than once.
2. Launch Eclipse.
   The Eclipse Workspace Launcher dialog box appears (see Figure 3-2).

![](img/f938eba5f15e231d828a6255e7ec5523_70_0.png)

Figure 3-2: The Eclipse Workspace Launcher.

A workspace is a folder on your computer's hard drive. Eclipse stores your Java programs in one or more workspace folders. Along with these Java programs, each workspace folder contains some Eclipse settings. These settings store things like the version of Java that you're using, the colors that you prefer for words in the editor, the size of the editor area when you drag the area's edges, and other things. You can have several workspaces with different programs and different settings in each workspace.

By default, the Workspace Launcher offers to open whatever workspace you opened the last time you ran Eclipse. You want to open the workspace that you used in Chapter 2, so don't modify the stuff in the Launcher's Workspace field.

3. In the Workspace Launcher dialog box, click OK.

   The big Eclipse workbench stares at you from your computer screen (see Figure 3-3).

In Figure 3-3, the leftmost part of the workbench is Eclipse's Package Explorer, which contains numbers like 03-01, 04-01, and so on. Each number is actually the name of an Eclipse project. Formally, a project is a collection of files and folders inside a workspace. Intuitively, a project is a basic work unit. For example, a self-contained collection of Java program files to manage your CD collection (along with the files containing the data) may constitute a single Eclipse project.

Looking again at the Package Explorer in Figure 3-3, you see projects named 03-01, 04-01, and so on. My project 03-01 holds the first and only example in Chapter 3 (this chapter). Project 06-02 contains the Java program in Listing 6-2 (the second code listing in Chapter 6 of this book). Project names can include letters, digits, blank spaces, and other characters, but for the names of this book's examples, I stick with digits and dashes.

To read more about things like Eclipse's Package Explorer, see the upcoming section "What's All That Stuff in Eclipse's Window?"

![](img/f938eba5f15e231d828a6255e7ec5523_71_0.png)

Figure 3-3: The Eclipse workbench.

![](img/f938eba5f15e231d828a6255e7ec5523_71_1.png)

When you launch Eclipse, you may see something different from the stuff in Figure 3-3. You may see Eclipse's Welcome screen with only a few icons in an otherwise barren window. You may also see a workbench like the one in Figure 3-3, but without a list of numbers (03-01, 04-01, and so on) in the Package Explorer. If so, you may have missed some instructions on configuring Eclipse in Chapter 2. Alternatively, you may have modified the stuff in the Launcher's Workspace field in Step 2 of this section's instructions.

In any case, make sure that you see numbers like 03-01 and 04-01 in the Package Explorer. Seeing these numbers assures you that Eclipse is ready to run the sample programs from this book.

4. In the Package Explorer, click the 03-01 branch.

   This chapter's Java project — the 03-01 project — appears highlighted.

![](img/f938eba5f15e231d828a6255e7ec5523_71_2.png)

You may want to see a sneak preview of some Java code. To see the Java program that you're running in Project 03-01, expand the 03-01 branch in the Package Explorer. Inside the 03-01 branch, you find a src branch, which in turn contains a (default package) branch. Inside the (default package) branch, you find the Mortgage.java branch. That Mortgage.java branch represents my Java program. Double-clicking the Mortgage.java branch makes my code appear in Eclipse's editor.

5. Choose Run→Run As→Java Application from the main menu, as shown in Figure 3-4.

   When you choose Run As→Java Application, the computer runs the project's code. (In this example, the computer runs a Java program that I wrote.) As part of the run, the message How much are you borrowing? appears in Eclipse's Console view. (The Console view shares the lower-right area of Eclipse's workbench with the Problems view, the Javadoc view, the Declaration view, and possibly other views. Refer to Figure 3-1.)

Figure 3-4: One of the ways to run the code in Project 03-01.

![](img/f938eba5f15e231d828a6255e7ec5523_72_0.png)

6. Click anywhere inside Eclipse's Console view and then type a number, like 100000.00, and press Enter.

![](img/f938eba5f15e231d828a6255e7ec5523_72_1.png)

   When you type a number in Step 6, don't include your country's currency symbol and don't group the digits. (U.S. residents, don't type a dollar sign and don't use any commas.) Things like $100000.00 and 1,000,000.00 cause the program to crash. You see a NumberFormatException message in the Console view.

Grouping separators vary from one country to another. The run shown in Figure 3-1 is for a computer configured in the United States where 100000.00 (with a dot) means one hundred thousand. But the run might look different on a computer that's configured in what I call a comma country — a country where 100000,00 (with a comma) means one hundred thousand. If you live in a comma country, and you type 100000.00 exactly as it's shown in Figure 3-1, you probably get an error message (an InputMismatchException). If so, change the number amounts in your file to match your country's number format. When you do, you should be okay.

After you press Enter, the Java program displays another message (What's the interest rate?) in the Console view. (Again, refer to Figure 3-1.)

7. In response to the interest rate question, type a number, like 5.25, and press Enter.

   After you press Enter, the Java program displays another message (How many years . . . ?) in the Console view.
