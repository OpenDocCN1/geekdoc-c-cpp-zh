# EXERCISES

+   1. [WPF, SimpleEdit] Repeat the Try It using the WPF program you built for Lesson 6's Exercise 10. Hint: To delete the current selection, use the statement `contentRichTextBox.Selection.Text = ""`.
+   
+   2. [SimpleEdit] Copy the program you built for the Try It and add simple code to handle the File menu's New, Open, Save, and Exit commands. For the New command, simply clear the RichTextBox. (Hint: Use the Clear method.)
+   
+   For the Open and Save commands, just load and save the file Test.rtf. (The program will create the file the first time you save. If you try to open the file before it exists, the program will crash so don't use Open before you use Save.) Lesson 8 explains how to use file open and save dialogs to let the user pick the file that should be opened or saved.
+   
+   3. [WPF, SimpleEdit] Repeat Exercise 2 using the program you built for Exercise 1. Hints:
+   
+   - One way to clear the control's contents is to use the following code:
+   ```
+   contentRichTextBox.SelectAll();
+   contentRichTextBox.Selection.Text = "";
+   ```
+   - The preceding code works but is rather slow if the control contains a lot of text. The following code is more complicated but more efficient:
+   ```
+   TextRange range = new TextRange(
+       contentRichTextBox.Document.ContentStart,
+       contentRichTextBox.Document.ContentEnd);
+   range.Text = "";
+   ```
+   - To load the saved file, use the following code (sorry, but WPF's version of the RichTextBox is a bit more complicated):
+   ```
+   TextRange range = new TextRange(
+       contentRichTextBox.Document.ContentStart,
+       contentRichTextBox.Document.ContentEnd);
+   using (System.IO.Stream stream =
+       new System.IO.FileStream("Test.rtf", System.IO.FileMode.Open))
+   {
+       range.Load(stream, DataFormats.Rtf);
+   }
+   ```
+   - To save text into a file, use the following code:
+   ```
+   TextRange range = new TextRange(
+       contentRichTextBox.Document.ContentStart,
+       contentRichTextBox.Document.ContentEnd);
+   using (System.IO.Stream stream =
+       new System.IO.FileStream("Test.rtf", System.IO.FileMode.Create))
+   {
+       range.Save(stream, DataFormats.Rtf);
+   }
+   ```
+   
+   4. [SimpleEdit] Copy the SimpleEdit program you built for Exercise 2 and add code to handle the Format menu's commands (except for the Font command and color commands, which are covered in Lesson 8).