
## GUIs

## 279

![](img/06d4e84f27a8884ea40ba6182ec7c778_303_0.png)

**FIGURE 11.1:** This is the window that pops up running JustButton.scala. There is a single button in a 300 by 200 pixel scale. Note that the button is, by default, in the top left corner.

```scala
import scalafx.scene.control.Button

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "First GUI"
    scene = new Scene(300,200) {
      fill = Color.Coral
      button = new Button("Click me!")
      content = button
      button.layoutX = 115
      button.layoutY = 70
    }
  }
}

app.main(args)
```

This code sets the values of layoutX and layoutY on the button. Those values are specified in pixels on the graphics coordinates, so the top left corner of the button is 115 pixels to the right and 70 pixels below the top of the scene. Figure 11.2 shows the results of running this program.

Having a window with only one thing in it is a bit limiting. As happens, the contents of the scene can also be set to sequence, and all elements of the scene are placed in the scene. This is shown in the program called SeveralFiles.scala.

### Listing 11.4: SeveralItems.scala

```scala
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.paint.Color
import scalafx.scene.control._
import scalafx.scene.shape._

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "First GUI"
    scene = new Scene(500,300) {
    }
  }
}
```

## Introduction to Programming and Problem-Solving Using Scala

![](img/06d4e84f27a8884ea40ba6182ec7c778_304_0.png)

**FIGURE 11.2:** This is the window that pops up when you run Button.scala. Notice that the button has been moved to what is roughly centered in our 300 by 200 pixel window.

app.main(args)

This code uses imports as we are using multiple types from those packages. It then goes through and creates several Nodes to place in the scene. Each element that is placed on the screen is a Node. In addition to the Button, it includes a Rectangle, a Label, a CheckBox, a ComboBox, and a ListView. The end of the block for the scene sets the contents that includes all those elements. The layoutX and layoutY of each one are set so that they do not overlap. To prevent the ListView from going below the bottom of the window, we set its preferred size. The ComboBox and ListView

![](img/06d4e84f27a8884ea40ba6182ec7c778_305_0.png)

**FIGURE 11.3:** This is the window created when you run SeveralItems.scala. It has several Nodes added to the scene and moved to different locations that they are supposed to display. To illustrate how it works, the ComboBox was created with a List[String], while the ListView was created with an Array[String]. Running this program produces the window shown in figure 11.3.

### 11.4 Events and Handlers

The next thing we need to do is learn how to allow the user to interact with the GUI. Before learning about GUIs, we did this using functions like handlers. Things are more complex with the GUI as there are many ways that you can interact with them. There are some elements that accept keystrokes, but many others interact with the mouse. The way that GUIs typically deal with user interaction is through events and handlers. When the user does something, it produces an event.

To illustrate this, we modify the GUI from the last example and put different types of interactivity on various elements. Here is the modified code:

### Listing 11.5: InteractiveItems.scala

```scala
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.paint.Color
import scalafx.scene.control._
import scalafx.scene.shape._
import scalafx.event.ActionEvent
import scalafx.scene.input._

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "First GUI"
    scene = new Scene(500,300) {
    // ... implementation details
    }
  }
}
```

Other than altering the text in the Button and the Label, changes come near the end of the script where event handlers are added to the different elements. The handlers are added by setting values that start with "on", such as onAction and onMouseClicked. They are set to functions that take an appropriate type of event. When the user specifies the type, the function is called (e: ActionEvent). These functions are just like lambda expressions with a variable name and the body of the function. The one thing to note is that you generally have to specify the type of argument for these; that is why the argument is given as (e:ActionEvent). As usual, the variable name could be anything you choose; the letter e is chosen here to represent an event.

In this example, handlers are added to the combo box. For both of them the value is set. This function is called when the most common action for that element occurs, as clicking on the button. The code removes all the selected items from the list view. This does by first getting all the items that are selected in the list view and then setting the list items to be the original list with the selected ones. For the combo box, the handler adds whatever item was selected to the end of the list.

This code also sets the onClick handler of the whole scene. Note that onAction follows an object and the onClick does not. Because the code is inside the scene, it uses the scene's version of onMouseClicked. This usage is just like setting the type of the Stage or the fill on the scene. The handler checks if the checkbox has been selected. If it is not, nothing else. If it is selected, then the rectangle is moved to the location of the click, and the label is updated with the appropriate text. Note that this is part of the scene; only clicks on the background invoke. If you click on one of the other components in the GUI, this code is not called, so the rectangle cannot be placed directly on top of the other elements.

Running this code will bring up a window that looks like figure 11.4.

## 11.5 Controls

ScalaFX has a long list of elements that can be added into a scene, a few of which were shown in the previous examples but not explained. All of these elements that can be added into a Scene are subtypes of the type Node. Looking at the whole picture, for a ScalaFX GUI we have the JFXApp at the top level. This is inside Stage that represents the primary window for the application. The Stage needs to contain a Scene and finally the Scene can contain the different Nodes that appear in it.

There are 120 subtypes of scene, which give you an indication of how much you can do with this library. Only a few of the keys will be covered in this book. This section focuses on some of the GUI controls, which are covered in the scalafx.scene and scalafx.shape packages.

The term Control is used in JavaFX to define basic GUI elements that the user can interact with. We break this into different categories for discussion and show examples of each. The sample code shows how to create each element and add it into a Scene, but also how to code basic interactions with that element.

> ⁴There are many types of events that can occur for each element, but the Scala developers have determined which is the most common event action for each GUI element.

![](img/06d4e84f27a8884ea40ba6182ec7c778_308_0.png)

**FIGURE 11.4:** This shows the window that results from running InteractiveItems.scala after the user has done a few things.
