
# Introduction to Programming and Problem-Solving Using Scala

When Java was originally released in 1995, there was one GUI library called the Abstract Windowing Toolkit. The AWT library makes direct calls to the operating system or windowing environment for building elements of the GUI. This gave a significant benefit in speed. However, it also provided a limitation. Due to the cross-platform nature of Java, it only included elements in the AWT that were present on all platforms. They are the most fundamental parts of GUI construction like windows, buttons, text boxes. These elements were drawn by the underlying platform and always looked like the underlying platform.

Both the restriction in appearance and the limited number of component types led to the creation of a "pure" Java library for the Java standard. This second library was called Swing, and it was meant that all the code in Swing was written in Java. It uses calls to AWT to make things happen, but does not directly call anything that is not in Java itself. The Swing library included a lot of different elements that were more powerful and flexible than what was provided in AWT. It also gave the ability to have elements of the GUI rendered in different ways so do not have to look like the underlying system. Originally this flexibility came at a cost of speed. Over time various optimizations were made and now Swing runs perfectly for most applications.

In 2007, a new Java and graphics framework called JavaFX was introduced to fix problems with Swing. The primary goals were to make something that was easier and make it easier for programmers to create rich and visually pleasing interfaces. JavaFX started as a scripting language, but later became a library for Java. With the release of Java 8 in 2014, JavaFX became the standard that developers are supposed to use for graphical interfaces on the JVM. It has an even variety of options than Swing, and runs faster than.

There is a Scala library that is a wrapper around JavaFX called ScalaFX. This is the library that will be used in this book for writing GUIs. It makes calls to JavaFX, but provides a syntax that takes full advantage of the features of the Scala language. Unfortunately, this library is not part of the standard Scala installation. To find, you might go to http://www.scalafx.org/ to get the most recent version of ScalaFX. A JAR file for a reasonably recent version can be found on the GitHub repository.

All the types for ScalaFX are organized in packages that start with scalafx. The ScalaFX web site has a link to the API on the right side. At the time of writing, the current version is 8.0. We will introduce each of the subpackages as they are needed. With the standard Scala API, the ScalaFX API is a useful tool that you will want to familiarize yourself with. Unlike previous chapters, this chapter and the following one can truly skip the top of what is in ScalaFX. The API is a good resource for those who want to go further.

## 11.2 First Steps

To get started, we will write a little program that does nothing more than pop up a window with nothing inside it. The code for it is shown here:

Listing 11.1: FirstGUI

```
import scalafx.application.JFXApp
```

> 1 ScalaFX provides types that you may call to JavaFX using a more Scala like style.

> 2 Java Archive File is a compressed file used by the Java platform to distribute code.

```
val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "First GUI"
    width = 500
    height = 500
  }
}
```

```
app.main(args)
```

At the top, you can see there is an import of the JFXApp type from the scalafx package. We declare a val called app of that type. Inside of our new JFXApp object we set the stage to be a new JFXApp.PrimaryStage. If you look at scalafx.applicationFX in the API, you will have a var called stage, and that is what we are setting here.

The Stage has members for title, width, and height that we set inside of new JFXApp.PrimaryStage object. The meanings of these will be fairly obvious. The script ends with a call to the main method of app passing the command line arguments. That call is what makes happen and should pop up a window.

Now you have to run [it]. We assume you are running your scripts from the command line as described in Appendix A. If you try, you will get a number of errors telling you that scalafx.JFXApp cannot be found, along with other information that is basically caused by the same issue. The problem is that ScalaFX is not part of the standard Scala library. For reason, we need to tell ScalaFX where to find the JAR file for ScalaFX. This is done by specifying what is called classpath. There are several ways to do this. The simplest is to use the -cp option at the command line. On my system, I do that with the following command.

```
scala -cp /home/mlevis/scalafax firstGUI.scala
```

-cp is followed by the path to the JAR file. On your machine that will be different and the JFX file might have a number that includes versions details. Another approach is to specify a place that the JVM always goes to look for extra libraries. This can be done by making a CLSPATH environment variable. The details of how you do this vary between operating systems, versions, and other details that make it impossible to work forever. You can find such information on the web. On one of the author's Windows machines a CLASSPATH environment variable was created with a variable value of "C:\Users\liben_000\scalafax.jar"; (C:\Users\lieben_000 is the location of the scalafax.jar file. Do not include the double quotes.). Under the Bash for Linux, add the export CLSPATH=:home/mlevis/scalafax.jar to your.

On a Linux machine, a third approach would be to make an alias for the command that includes the classpath specification. That might look like alias scalafax="scala -cp /home/mlevis/scalafax.jar". Once you have defined this, you can execute scalafax firstGUI.scala and you do not need to worry about the classpath variable.

> 3 There are several ways you can find the JAR file. You could build from the main repository through http://www.scalafx.org (there are several steps involved in this, but the advantage of this approach is that it will always match your current version of Scala or download it from the book's GitHub repository. If you are taking a course, your instructor might tell you where you can find one.

However you go doing it, when you run this little script, it will pop up a window that is 500 pixels by 500 pixels with a title that says “First GUI”. Closing the window will end the script.

## 11.3 Stages and Scenes

The Stage type that was created in our first application is what defined the window. To make the GUI more interesting, we need to put things on the Stage. This is done by adding a Scene to the Stage. That Scene can then have contents that will show up in the window. The following example demonstrates adding a Scene with one thing of it to your GUI.

Listing 11.2: JButton.scala

```
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.paint.Color
import scalafx.scene.control.Button

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "First GUI"
    scene = new Scene(300,200) {
      fill = Color.Coral
      val button = new Button("Click me!")
      content = button
    }
  }
}

app.main(args)
```

There are three additional imports added here to bring in the Scene, the Color type, and the Button type, which is what we added to the scene. The String “Click me!” is the text that appears on the button. You can see the window that results from running this code in figure 11.1.

Note that the button is located in the top left. This is probably not the ideal location for the button, but it is where things goes in the scene. The default is a coordinate system using the x and y coordinates. The top left is at location (0,0) in our scene. However, 2D graphics coordinates are slightly different than what you are used to math. In math you are used to z growing as you move right and y growing as you move up. The scene uses graphical coordinates where x still grows from left to right and the y-coordinate increases as it goes down. The x-coordinate value, as it grows right and the y-coordinate increases as it goes down. The following code moves the button to be roughly centered on the window.

Listing 11.3: MoveButton.scala

```
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.paint.Color
```
