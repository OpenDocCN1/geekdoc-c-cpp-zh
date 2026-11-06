# USING BOOST LIBRARIES ON CERTAIN 64-BIT SYSTEMS

If you performed the Boost installation for your system using the techniques found in the “Boost Installation on Certain 64-bit Systems” sidebar in Book 7 Chapter 4, then you may not have any library files to use because they won’t build. However, that means skipping the instructions in this section. In this case, you can try a header-only example using the code in the next section of the chapter to see if RegEx will work on your system. In at least some cases, it will work, but you may lose functionality provided by the library. When problems occur, you’ll see an error message telling you there is a configuration (or sometimes other) error and that the Boost RegEx library is missing. The example in the “Accessing the Operating System Using Filesystem” section won’t run on a 64-bit system using the alternative configuration.

Two techniques exist for adding the required headers and libraries to an application. The first technique is to add it to the compiler settings, as you do for the “Testing the installation” section of Book 7, Chapter 4. The second technique is to add the settings to a specific project. You use the first technique when you work with Boost for a large number of projects and require access to all libraries. The second technique is best when you use Boost only for specific projects and require access only to specific libraries. The following steps show you how to perform the project-specific setup for any library, not just the RegEx library:

+   1. **Use the Project wizard to create a new project.**
+   
+      Nothing has changed from the beginning of this book: every application begins with a new project. The next section discusses the RegEx example, and you can use that project name as a starting point here.
+   2. **Choose Project > Build Options.**
+   
+      Code::Blocks displays the Project Build Options dialog box.
+   3. **Select the project name, such as RegEx, in the left pane.**
+   4. **Select the Linker Settings tab.**
+   
+      You see a number of linker settings, including a Link Libraries list, which will be blank.
+   5. **Click Add.**
+   
+      Code::Blocks displays the Add Library dialog box, shown in Figure 5-1.
+   6. **Click the Browse button — the button sporting an opening file folder.**
+   
+      You see the Choose Library to Link dialog box.