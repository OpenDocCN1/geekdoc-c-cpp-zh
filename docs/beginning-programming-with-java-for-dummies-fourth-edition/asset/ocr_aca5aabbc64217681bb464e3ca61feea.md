# 9. Click on the Controller section in the Document panel.

Doing so expands the Controller section at the expense of the Hierarchy section.

# 10. In the Controller Class field (inside the Controller section) type application.Main (with a dot between the two words) and then press Enter (see Figure 20-18).

You have leeway in carrying out some of the other steps in this section. For example, if you type Click Me! instead of Capitalize in Step 4, the program still runs. But you have very little leeway when you fill in this step's Controller Class field. By default, the e(fx)clipse tool names your program Main.java, and puts your program in a package named application. So in the Controller Class field, you have to point to this application.Main program. If you point somewhere else, you have to rename the program or the package or both. And with more than 40 steps to follow in this chapter so far, you probably don't want to rename things unnecessarily.

At last! Your work with Scene Builder is coming to a close!

![](bbox=[0.12, 0.25, 0.2, 0.38])

![](bbox=[0.26, 0.55, 0.5, 0.72])

Figure 20-18: Specifying the FXML file's controller class.

# 11. In the Scene Builder's main menu, select File→Save.

# 12. Close the Scene Builder application.

Whew! You're back to the Eclipse workbench.

Eclipse might not update the Root.fxml file's contents automatically when you close Scene Builder. If you don't see the word Capitalize in the code, click your mouse inside the editor window. (Clicking your mouse updates the editor to reflect the changes made by Scene Builder.)

![](bbox=[0.12, 0.8, 0.2, 0.92])

# 13. In the Main.java file, add the boldface code near the start of Listing 20-4 and near the end of Listing 20-4.

The edits in Listing 20-4 tell Java to change the text that appears in your TextField control when the user clicks your Button control.

And with that step, you have a real GUI application!

# 14. Run the project.