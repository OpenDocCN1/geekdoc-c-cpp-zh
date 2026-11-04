+   - Enter **Ctrl+X** followed by the letter **Y** to save the file. You should now see the file listed in your directory if you enter the command:

```
    pi@raspberrypi:~$ ls myfile.txt
    myfile.txt
    pi@raspberrypi:~$
```

+   - Let us now edit the file we just created to learn some of the editor commands. Restart **nano** as above by specifying the filename.

+   - Let us search for text starting with the word **simple**: press **Ctrl+W** and type **simple** and press **Enter** (see Figure 2.2). You should see the cursor moving to the start of the word **simple**. Delete **simple** and change it to **difficult**.

![](bbox=[0.27, 0.325, 0.76, 0.378])

+   - Let us replace the word **third** with **fourth**: press Ctrl+\ and type **third**, and then **fourth** when **Replace with:** is displayed. Press **Enter**. The message **Replace this instance?** will be displayed. Type **Y**. You should see that the word **third** is replaced with **fourth**.

+   - Let us delete the second line of text: Move the cursor to the second line and enter **Ctrl+K**. You should see all the text on the second line is deleted.

+   - To recall the line just deleted, enter **Ctrl+U**.

+   - To get help on using **nano**, enter **Ctrl+G**. An example help screen is shown in Figure 2.3. Enter **Ctrl+N** to display the next page, and **Ctrl+P** to display the previous page. Enter **Ctrl+X** to close the help screen.

![](bbox=[0.219, 0.606, 0.802, 0.818])

+   - Enter **Ctrl+X** followed by **Y** to save and exit the editor.

+   - The contents of the edited file are shown in Figure 2.4.