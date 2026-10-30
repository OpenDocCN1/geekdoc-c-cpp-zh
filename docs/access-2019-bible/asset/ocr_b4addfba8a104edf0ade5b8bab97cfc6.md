statements that are all doing roughly the same operation. If your statements are long or diverse, it actually hinders the readability of the code and should be avoided.

# IntelliSense

Suppose that you know you want to use a specific command, but you can't remember the exact syntax. Access includes four features (collectively known as IntelliSense) to help you find the proper keyword and determine the correct parameters as you create each line of code:

+   - **Complete Word:** Any time you're in a code pane, you can press Ctrl+spacebar to get a list of keywords. The list automatically scrolls to the keyword that matches what you've already typed. If there is only one match, you don't see the list and the word is simply completed for you. Figure 24.5 shows what happens when you type “do” and press Ctrl+spacebar.

# FIGURE 24.5

Complete Word shows a list of keywords.

![](bbox=[0.22, 0.58, 0.75, 0.78])

If you were to type “doc” instead of just “do,” the keyword DoCmd would be completed rather than a list because there is only one keyword that starts with doc.

+   - **Auto List Members:** Auto List Members is a drop-down list that is automatically displayed when you type the beginning of a keyword that has associated objects, properties, or methods. For example, if you enter DoCmd.openf, a list of the possible options displays, as shown in Figure 24.6. Scroll through the list box and press Enter to select the option you want or continue typing to narrow the selections in the list.