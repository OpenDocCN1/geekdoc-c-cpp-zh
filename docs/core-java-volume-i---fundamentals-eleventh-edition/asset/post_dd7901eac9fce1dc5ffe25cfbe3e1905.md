
## 10.2.1 Creating a Frame

In this section, we will go over the most common methods for working with a Swing JFrame. Listing 10.1 lists a simple program that displays an empty frame on the screen, as illustrated in Figure 10.1.

![](img/127bccebb2cfadea3f02579edaad63c3_594_0.png)

**Figure 10.1** The simplest visible frame

**Listing 10.1** `simpleframe/SimpleFrameTest.java`

```java
package simpleFrame;

import java.awt.*;
import javax.swing.*;

/**
 * @version 1.34 2018-04-10
 * @author Cay Horstmann
 */
public class SimpleFrameTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new SimpleFrame();
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

class SimpleFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 200;

    public SimpleFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
    }
}
```

Let's work through this program, line by line.

The Swing classes are placed in the `javax.swing` package. The package name `javax` indicates a Java extension package, not a core package. For historical reasons, Swing is considered an extension. However, it is present in every Java implementation since version 1.2.

By default, a frame has a rather useless size of 0 × 0 pixels. We define a subclass `SimpleFrame` whose constructor sets the size to 300 × 200 pixels. This is the only difference between a `SimpleFrame` and a `JFrame`.

In the `main` method of the `SimpleFrameTest` class, we construct a `SimpleFrame` object and make it visible.

There are two technical issues that we need to address in every Swing program.

First, all Swing components must be configured from the *event dispatch thread*, the thread of control that passes events such as mouse clicks and keystrokes to the user interface components. The following code fragment is used to execute statements in the event dispatch thread:

```java
EventQueue.invokeLater(() ->
{
    statements
});
```

> **NOTE:** You will see many Swing programs that do not initialize the user interface in the event dispatch thread. It used to be perfectly acceptable to carry out the initialization in the main thread. Sadly, as Swing components got more complex, the developers of the JDK were no longer able to guarantee the safety of that approach. The probability of an error is extremely low, but you would not want to be one of the unlucky few who encounter an intermittent problem. It is better to do the right thing, even if the code looks rather mysterious.

![](img/127bccebb2cfadea3f02579edaad63c3_597_0.png)

**Figure 10.2** Inheritance hierarchy for the frame and component classes in AWT and Swing

where you need to look for the methods to resize and reshape frames. For example, the setLocation method in the Component class is one way to reposition a component. If you make the call

```java
setLocation(x, y)
```

the top left corner is located x pixels across and y pixels down, where (0, 0) is the top left corner of the screen. Similarly, the setBounds method in Component lets you resize and relocate a component (in particular, a JFrame) in one step, as

```java
setBounds(x, y, width, height)
```

Many methods of component classes come in getter/setter pairs, such as the following methods of the Frame class:

```java
public String getTitle()
public void setTitle(String title)
```

Such a getter/setter pair is called a *property*. A property has a name and a type. The name is obtained by changing the first letter after the get or set to lowercase. For example, the Frame class has a property with name title and type String.

Conceptually, title is a property of the frame. When we set the property, we expect the title to change on the user’s screen. When we get the property, we expect to get back the value that we have set.

There is one exception to the get/set convention: For properties of type boolean, the getter starts with is. For example, the following two methods define the resizable property:

```java
public boolean isResizable()
public void setResizable(boolean resizable)
```

To determine an appropriate size for a frame, first find out the screen size. Call the static getDefaultToolkit method of the Toolkit class to get the Toolkit object. (The Toolkit class is a dumping ground for a variety of methods interfacing with the native windowing system.) Then call the getScreenSize method, which returns the screen size as a Dimension object. A Dimension object simultaneously stores a width and a height, in public (!) instance variables width and height. Then you can use a suitable percentage of the screen size to size the frame. Here is the code:

```java
Toolkit kit = Toolkit.getDefaultToolkit();
Dimension screenSize = kit.getScreenSize();
int screenWidth = screenSize.width;
int screenHeight = screenSize.height;
setSize(screenWidth / 2, screenHeight / 2);
```

You can also supply frame icon:

```java
Image img = new ImageIcon("icon.gif").getImage();
setIconImage(img);
```

### java.awt.Component 1.0

- `boolean isVisible()` / `void setVisible(boolean b)`
  - gets or sets the visible property. Components are initially visible, with the exception of top-level components such as `JFrame`.
- `void setSize(int width, int height)` **1.1**
  - resizes the component to the specified width and height.
- `void setLocation(int x, int y)` **1.1**
  - moves the component to a new location. The x and y coordinates use the coordinates of the container if the component is not a top-level component, or the coordinates of the screen if the component is top level (for example, a `JFrame`).
- `void setBounds(int x, int y, int width, int height)` **1.1**
  - moves and resizes this component.
- `Dimension getSize()` **1.1** / `void setSize(Dimension d)` **1.1**
  - gets or sets the size property of this component.

### java.awt.Window 1.0

- `void setLocationByPlatform(boolean b)` **5**
  - gets or sets the locationByPlatform property. When the property is set before this window is displayed, the platform picks a suitable location.

### java.awt.Frame 1.0

- `boolean isResizable()` / `void setResizable(boolean b)`
  - gets or sets the resizable property. When the property is set, the user can resize the frame.
- `String getTitle()` / `void setTitle(String s)`
  - gets or sets the title property that determines the text in the title bar for the frame.

![](img/127bccebb2cfadea3f02579edaad63c3_601_0.png)

**Figure 10.3** A frame that displays information

The *content pane*. Any components that you add to a frame are automatically placed into the content pane:

```java
    Component c = . . .;
    frame.add(c); // added to the content pane
```

![](img/127bccebb2cfadea3f02579edaad63c3_601_1.png)

**Figure 10.4** Internal structure of a JFrame

In our case, we want to add a single component to the frame onto which we will draw our message. To draw on a component, you define a class that extends `JComponent` and override the `paintComponent` method in that class.

The `paintComponent` method takes one parameter of type `Graphics`. A `Graphics` object remembers a collection of settings for drawing images and text, such as the font you set or the current color. All drawing in Java must go through a `Graphics` object. It has methods that draw patterns, images, and text.

Here’s how to make a component onto which you can draw:

```java
class MyComponent extends JComponent
{
    public void paintComponent(Graphics g)
    {
        code for drawing
    }
}
```

Each time a window needs to be redrawn, no matter what the reason, the event handler notifies the component. This causes the `paintComponent` methods of all components to be executed.

Never call the `paintComponent` method yourself. It is called automatically whenever a part of your application needs to be redrawn, and you should not interfere with this automatic process.

What sorts of actions trigger this automatic response? For example, painting occurs when the user increases the size of the window, or minimizes and then restores the window. If the user popped up another window that covered an existing window and then made the overlaid window disappear, the window that was covered is now corrupted and will need to be repainted. (The graphics system does not save the pixels underneath.) And, of course, when the window is displayed for the first time, it needs to process the code that specifies how and where it should draw the initial elements.

> **TIP:** If you need to force repainting of the screen, call the `repaint` method instead of `paintComponent`. The `repaint` method will cause `paintComponent` to be called for all components, with a properly configured `Graphics` object.

As you saw in the code fragment above, the `paintComponent` method takes a single parameter of type `Graphics`. Measurement on a `Graphics` object for screen
