
In the expression new JFrame(), Java's new keyword signals a call to a constructor. A constructor is like a method, except that a constructor's name is the same as the name of a Java class. Java's standard API contains classes named JFrame, ImageIcon, and JLabel, and the code in Listing 20-1 calls the JFrame, ImageIcon, and JLabel constructors.

As the terminology suggests, a constructor is a piece of code that constructs an object. So in Listing 20-1, when you call

```
JFrame frame = new JFrame();
```

you make a frame variable refer to a newly constructed object (an object constructed from the JFrame class).

Constructors and methods have a lot in common with one another. You can't call a method without having a corresponding method declaration somewhere in the code. (In the case of Java's nextLine method, the method declaration lives somewhere inside Java's enormous bunch of API classes.) The same is true of constructors. You can't call new JFrame() without having a constructor for the JFrame class somewhere in your code. And, sure enough, inside the Java API class, you can find a declaration for the JFrame() constructor. The code looks something like this:

```
public class JFrame {
    int height;
    int width;
    public Component add() ...
    public void setDefaultCloseOperation() ...
    public void pack() ...
    public void setVisible() ...
    ...

    /**
     * Constructs a new frame that is initially invisible.
     */
    public JFrame() {
        ...
    }
    ...
}
```

The constructor declaration looks almost like a method declaration. But notice that the constructor declaration doesn't start with public void JFrame() or with public double JFrame() or with public anything JFrame(). Aside from the optional word public, a constructor declaration contains only the name of the class whose object is being constructed. More on this in the next section.

## The Swing Classes: Round 2

In your Java-related travels, you’ll see several variations on the code in Listing 20-1. This section explores one such variation.

This section’s example does exactly what the previous section’s example does. The only difference is the way the two examples deal with the JFrame class. This section’s code is in Listing 20-2.

### Listing 20-2: Extending Java’s JFrame Class

```java
import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JLabel;

class ShowPicture {

    public static void main(String args[]) {
        new MyFrame();
    }
}

class MyFrame extends JFrame {

    MyFrame() {
        ImageIcon icon = new ImageIcon("androidBook.jpg");
        JLabel label = new JLabel(icon);
        add(label);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        pack();
        setVisible(true);
    }
}
```

![](img/bf4858233d2b2a32ff4e3991860526b3_418_0.png)

When you view Listing 20-2 in the Eclipse editor, you see a little yellow marker. A yellow marker represents a warning rather than an error, so you can ignore the warning and still run your code. If you hover over the marker, you see a tip about something called a serialVersionUID. A serialVersionUID is a number that helps Java avoid version conflicts when you send different copies of an object from one place to another. You can get rid of the warning by applying one of Eclipse’s quick fixes, but if you’re not fussy, don’t bother with these quick fixes.

![](img/bf4858233d2b2a32ff4e3991860526b3_418_1.png)

For information about Eclipse’s Quick Fix feature, refer to Chapter 3.

### Extending a class

In Listing 20-2, the words extends JFrame are particularly important. When you see Java’s extends keyword, imagine replacing that keyword with the phrase “is a kind of.”

```java
public class MyFrame is a kind of JFrame {
```

In Listing 20-2, the words new MyFrame() get the MyFrame constructor to do its work. And the constructor in Listing 20-2 does quite a bit of work! The constructor does the stuff that the main method does in Listing 20-1.

- ✔ The constructor creates an ImageIcon containing the androidBook.jpg picture.
- ✔ The constructor creates a JLabel object and puts the androidBook.jpg icon on the new label's face.
- ✔ The constructor adds the JLabel object.

Time out! What's being added to what? In Listing 20-1, the statement

```
frame.add(label);
```

adds the JLabel object to the frame. But in Listing 20-2, there's no frame variable. In Listing 20-2, all you have is

```
add(label);
```

Well, here's the good news: Inside a constructor declaration, the object that you're constructing is "a given." You don't name that new object in order to refer to that new object. It's as though the constructor's code looked like this:

```java
MyFrame() {
    ImageIcon icon = new ImageIcon("androidBook.jpg");
    JLabel label = new JLabel(icon);
    new_frame_that_is_being_constructed.add(label);
    new_frame_that_is_being_constructed.
    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    new_frame_that_is_being_constructed.pack();
    new_frame_that_is_being_constructed.
    setVisible(true);
}
```

Here's how the constructor in Listing 20-2 finishes its work:

- The constructor adds the JLabel object to the MyFrame object that's being constructed.
- The constructor tells the Java Virtual Machine to shut itself down when you close the frame.
- The constructor shrink-wraps the frame around the image that appears on the frame.
- The constructor makes the frame appear on your screen.

The extends keyword adds a very important idea to Java programming — the notion of inheritance. In Listing 20-2, the newly created MyFrame class inherits the methods (and other things) that are declared in the existing JFrame class. Inheritance is a pivotal feature of an object-oriented programming language.

## Code Soup: Mixing XML with Java

Go back and feast your eyes one more time on the code in Listing 20-1. Despite Java's object-oriented flavor, the code displays a window using a "do this, then do that" approach.

```
Here's how you show a picture:
Construct a frame
Construct an icon containing a certain image
Construct a label containing the icon
Add the icon to the frame
...
Pack the frame
Make the frame be visible
```

This "do this, then do that" approach is called procedural programming.

Now imagine you're at the Louvre looking at the Mona Lisa. You don't think "Da Vinci added a face, then he put a smile on the face, then he added a body, and then a background." The painting doesn't progress from one action to another. Instead, the painting simply is.

In the same way, a window in a GUI application doesn't need a procedural progression. Instead, you can describe a window declaratively. You write code that says "Here's how the window looks." The Java Virtual Machine uses your description to decide (on its own) what to display and when.

Consider, for example, the grid in Figure 20-7.

![](img/bf4858233d2b2a32ff4e3991860526b3_421_0.png)

The following Swing code creates a grid like the one in Figure 20-7. Don't look at all the details in the code. Instead, notice all the verbs: "set the layout to a new GridLayout, add a label to the frame, set the font, pack the frame, and so on." It's all procedural.

```
import java.awt.Font;
import java.awt.GridLayout;

import javax.swing.JFrame;
import javax.swing.JLabel;
```

```
public class Main {
    public static void main(String[] args) {
        JFrame frame = new JFrame();
        frame.setLayout(new GridLayout(4, 2));
        JLabel labels[] =
            { new JLabel("Name"), new JLabel("Phone"),
              new JLabel("Alice"), new JLabel("555-1234"),
              new JLabel("Bob"), new JLabel("555-4321"),
              new JLabel("Carol"), new JLabel("555-3000") };
        frame.add(labels[0]);
        frame.add(labels[1]);
        JLabel boldLabel = new JLabel("Name");
        Font boldFont = boldLabel.getFont();
        Font plainFont = new Font(boldFont.getName(),
            Font.PLAIN, boldFont.getSize());
        for (int i = 2; i < 8; i++) {
            labels[i].setFont(plainFont);
            frame.add(labels[i]);
        }
        frame.pack();
        frame.setVisible(true);
    }
}
```

To save the world from its procedural fixation, JavaFX offers a declarative option. Using JavaFX, you can describe a scene as an outline using XML (eXtensible Markup Language) tags. Here's a JavaFX version of the grid from Figure 20-7:

```
<GridPane gridLinesVisible="true"
    layoutX="100.0" layoutY="165.0">
    <children>
        <Label text="Name"
            GridPane.columnIndex="0" GridPane.rowIndex="0">
            <font>
                <Font name="System Bold" size="12.0" fx:id="x1" />
            </font>
        </Label>
        <Label font="$x1" text="Phone"
            GridPane.columnIndex="1" GridPane.rowIndex="0" />
        <Label text="Alice"
            GridPane.columnIndex="0" GridPane.rowIndex="1" />
        <Label text="555-1234"
            GridPane.columnIndex="1" GridPane.rowIndex="1" />
        <Label text="Bob"
