
This new Root.fxml file describes the layout of the buttons, text fields, and other things in your new JavaFX application. This is the XML document that I make such a fuss about at the start of the “Code Soup: Mixing XML with Java” section.

![](img/bf4858233d2b2a32ff4e3991860526b3_428_0.png)

**Figure 20-9:** The FXML File dialog box.

- 7. **Right-click (or on a Mac, control-click) the new Root.fxml branch in Eclipse’s Package Explorer.** In the context menu that appears, select **Open with SceneBuilder**.

The Scene Builder application window appears (see Figure 20-10).

The Scene Builder window contains several areas:

- The middle of the Scene Builder window contains the *Content panel*, where you see a preview of your new app. (Currently, there’s nothing in your app to see, so the Content panel is a big empty space.)
- The upper-left portion of the window contains a *Library panel*, which houses a Containers section, a Controls section, and several other sections.

In the GUI world, things like buttons, text fields, labels, and check boxes are called *controls*. The Library panel’s Controls section forms a palette. To create a GUI window, you drag controls from the palette and drop them onto the Content panel.

![](img/bf4858233d2b2a32ff4e3991860526b3_429_0.png)

- The lower-left portion of the window contains a *Document* panel, which contains a Hierarchy section and a Controller section. The Hierarchy section contains an AnchorPane item.

The Hierarchy section contains a tree showing which elements of your window are inside which other elements. The Controller section helps you link the window that you design with the application’s Java code.

- The rightmost portion of the window contains an *Inspector panel*, which contains a Properties section, a Layout section, and a Code section.

In the Properties section, you describe the features of the elements in your window. In the Code section, you name the Java methods associated with elements in your window.

![](img/bf4858233d2b2a32ff4e3991860526b3_429_1.png)

Your mileage may vary! These instructions work on a preview release of Scene Builder 2.0. If you have a different version of Scene Builder, your steps might be a bit different.

- 8. **Select the AnchorPane item in the Hierarchy section.**

A marker appears in the middle of the Scene Builder’s Content panel.

- 9. **Drag the marker in the Content panel to enlarge the AnchorPane (see Figure 20-11).**

Figure 20-11:
Enlarging the AnchorPane.

![](img/bf4858233d2b2a32ff4e3991860526b3_430_0.png)

10. Find the Text Field entry in the Controls section of the Library panel; then drag a TextField control into the AnchorPane in the Content panel.

11. Find the Button entry in the Controls section of the Library panel. Drag a Button control into the AnchorPane in the Content panel. (See Figure 20-12 for a peek at both the TextField control and the Button control.)

Figure 20-12:
A TextField and a Button.

![](img/bf4858233d2b2a32ff4e3991860526b3_430_1.png)

## Listing 20-3: How to Edit the Main.java File

```
package application;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        try {
            // BorderPane root = new BorderPane();
            Parent root = FXMLLoader.load(getClass().
                    getResource("Root.fxml"));
            Scene scene = new Scene(root, 400, 400);
            scene.getStylesheets().
                    add(getClass().getResource("application.css").
                            toExternalForm());
            primaryStage.setScene(scene);
            primaryStage.show();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

As you follow this section's steps, Scene Builder modifies your project's Java code. Having followed this section's steps, you can run the project in the usual way (by choosing Run→Run As→Java Application). But when the project runs, the application doesn't do anything. When you click the button, nothing happens. When you type in the text field, nothing happens. What a waste!

In the next section, you get the button and the text field to do something.

## Taking Action

The program that you create in this chapter is approximately 50 lines long. But up to this point in the chapter, you type only one line of code. In this section's instructions, you make a button respond to a mouse click. You do this by typing only a few more lines of code!

- 1. **Follow the instructions in this chapter's earlier "Adding Stuff to Your JavaFX Project" section.**

As a result, you have code that displays a TextField control and a Button control. It's time to reopen Scene Builder.

- 2. **Right-click (or on a Mac, control-click) the Root.fxml branch in Eclipse's Package Explorer. In the resulting context menu, select Open with SceneBuilder.**

The Scene Builder application window appears (refer to Figure 20-12).

- 3. **In the Scene Builder window, select your app's Button control.**

You can do this by clicking the Button control's picture in the Content panel or by clicking the word Button in the Hierarchy section of the Document panel.

When you select the Button control, the Properties section of the Inspector panel displays some information about your Button control. Near the top of the section, you see an item labeled Text. Whatever you type in the field next to the word Text is displayed on the face of the button.

- 4. **In the field next to the word Text, type the word Capitalize, and then press Enter.**

When you do this, the word Capitalize appears on the face of the Button control in the Content panel (see Figure 20-15)

Remember that the Inspector panel contains three sections — the Properties section, the Layout section, and the Code section. At this point, the Properties section is expanded, and the other two sections are collapsed.

Figure 20-15: Working with the Button control's properties.

![](img/bf4858233d2b2a32ff4e3991860526b3_433_0.png)

5. In the Inspector panel, click on the Code section.

Doing so expands the Code section (at the expense of the Properties section).

6. In the Code section, look for a field that's labeled On Action. In that field, type onClick and then press Enter (see Figure 20-16).

Before typing the word onClick, make sure you see the word Button at the top of the Code section. If you see another word (such as TextField or AnchorPane), you're about to change the wrong component's On Action field.

So much for your Button control! Now, you work with your TextField control.

![](img/bf4858233d2b2a32ff4e3991860526b3_434_0.png)

Figure 20-16:
When a user clicks your Button control, call the code's onClick method.

![](img/bf4858233d2b2a32ff4e3991860526b3_434_1.png)

7. Select your TextField control (either in the Content panel or in the Hierarchy section of the Document panel).

8. In the Code section, look for a field that's labeled fx:id. In that field, type textField and then press Enter (see Figure 20-17).

Before bidding a fond farewell to Scene Builder, you link the Scene Builder's work to the Java code:

Figure 20-17:
Assigning an id to your TextField control.

![](img/bf4858233d2b2a32ff4e3991860526b3_434_2.png)

- 9. Click on the Controller section in the Document panel.

Doing so expands the Controller section at the expense of the Hierarchy section.

- 10. In the Controller Class field (inside the Controller section) type application.Main (with a dot between the two words) and then press Enter (see Figure 20-18).

You have leeway in carrying out some of the other steps in this section. For example, if you type Click Me! instead of Capitalize in Step 4, the program still runs. But you have very little leeway when you fill in this step's Controller Class field. By default, the e(fx)clipse tool names your program Main.java, and puts your program in a package named application. So in the Controller Class field, you have to point to this application.Main program. If you point somewhere else, you have to rename the program or the package or both. And with more than 40 steps to follow in this chapter so far, you probably don't want to rename things unnecessarily.

At last! Your work with Scene Builder is coming to a close!

![](img/bf4858233d2b2a32ff4e3991860526b3_435_0.png)

Figure 20-18: Specifying the FXML file's controller class.

![](img/bf4858233d2b2a32ff4e3991860526b3_435_1.png)

- 11. In the Scene Builder's main menu, select File→Save.

- 12. Close the Scene Builder application.

Whew! You're back to the Eclipse workbench.

Eclipse might not update the Root.fxml file's contents automatically when you close Scene Builder. If you don't see the word Capitalize in the code, click your mouse inside the editor window. (Clicking your mouse updates the editor to reflect the changes made by Scene Builder.)

![](img/bf4858233d2b2a32ff4e3991860526b3_435_2.png)

- 13. In the Main.java file, add the boldface code near the start of Listing 20-4 and near the end of Listing 20-4.

The edits in Listing 20-4 tell Java to change the text that appears in your TextField control when the user clicks your Button control.

And with that step, you have a real GUI application!

- 14. Run the project.
