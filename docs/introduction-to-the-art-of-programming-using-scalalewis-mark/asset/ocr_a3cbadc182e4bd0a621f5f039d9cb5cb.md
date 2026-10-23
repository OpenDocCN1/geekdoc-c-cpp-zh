![](bbox=[0.15, 0.04, 0.85, 0.5])

**FIGURE 11.1:** This is a sample window brought up by a simple script. The window is 500x500 pixels and has the title “First GUI”. When you close the window, the script will exit.

a **MainFrame**. Other options include a regular **Frame** and a **Dialog**. The advantage of the **MainFrame** is that it terminates the program when it is closed. The following is a little script that you can run to bring up a window.

```
import scala.swing._

val frame=new MainFrame {
	title = "First GUI"
	size = new Dimension(500,500)
}

frame.visible=true
```

When you run this it should pop up a window that looks like figure 11.1. There are quite a few things in this script that are worth describing. We start with an **import** statement. The underscore is a wild card that tells Scala to import everything in the `scala.swing` package. We do not have to do that here, but it will be more useful as we go on because we will use a lot of different types from this package.

Below the import we make the **Frame** and store it in a **val** named **frame**. The syntax here can be read in the following way. We are making a new **MainFrame** object and the