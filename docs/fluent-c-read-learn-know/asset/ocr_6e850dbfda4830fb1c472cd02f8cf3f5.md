# ADDING TASK LIST TOKENS

By default, Visual Studio only knows a few tokens, but you can add more through the Options dialog available from the Tools menu.

![](bbox=[0.5, 0.16, 0.91, 0.37])

# ON YOUR OWN

![](bbox=[0.11, 0.43, 0.29, 0.54])

+   1. In the Project you created for this chapter, display the Task List window by choosing Task List from the View menu or pressing Ctrl+W, T. Make sure the drop-down is showing Comments, not User Tasks.
+   
+   2. In the editor, add a ToDo comment before the click procedure:
+      ```
+      //Hack: Make a note of something dodgy
+      private void button1_Click(object sender, RoutedEventArgs e)
+      ```
+   
+   3. As soon as you move your cursor off the comment line, the comment should show up in the Task List window. If it doesn't, make sure the window is showing Comments, not User Tasks, and that you spelled “Todo” correctly (capitalization doesn’t count).