
```
{
    Person person = peopleListBox.SelectedItem as Person;
    MessageBox.Show(person.GetAddress());
}
```

This code converts the ListBox's selected item into a Person object. The item is actually either a Student or an Employee, but both of those inherit from Person (they are kinds of Person) so the program can treat them as Persons.

The program calls the Person's GetAddress method and displays the result. If the object was actually a Student, the result is a basic name and address. If the object was actually an Employee, the result is a name and address plus mailstop.

In addition to ListBoxes and ComboBoxes, some parts of Visual Studio use an object's ToString method, too. For example, if you stop an executing program and hover the mouse over an object in the debugger, a tooltip appears that displays the result of the object's ToString method. Similarly, if you type an object's name in the Immediate window and press Enter, the result is whatever is returned by the object's ToString method.

## TRY IT

In this Try It, you improve the shape drawing program you built for Exercise 24-9 by overriding the Shape class's Draw method so Ellipse and Circle objects can draw themselves appropriately.

### Lesson Requirements

In this lesson, you:

- Copy the program you wrote for Exercise 24-9 (or download the version that's available on the book's website).
- Add the virtual keyword to the Shape class's Draw method.
- Override the Draw method in the Ellipse class so it draws an ellipse instead of a rectangle.
- Modify the form's Paint event handler to draw smooth shapes.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

### Hints

If gr is the Graphics object, you can use these techniques:

- gr.SmoothingMode = SmoothingMode.AntiAlias—Makes the object draw shapes smooth. (SmoothingMode is defined in the System.Drawing.Drawing2D namespace.)
- gr.FillEllipse(brush, rect)—Fills an ellipse defined by the Rectangle rect with brush.
- gr.DrawEllipse(pen, rect)—Outlines an ellipse defined by the Rectangle rect with pen.

### Step-by-Step

Copy the program you wrote for Exercise 24-9 (or download the version that's available on the book's website).

- 1. This is straightforward.

Add the virtual keyword to the Shape class's Draw method.

- 1. Change the Shape class's Draw method so its declaration looks like this. (The virtual keyword is highlighted in bold.)

  ```csharp
  public virtual void Draw(Graphics gr)
  ```

Override the Draw method in the Ellipse class so it draws an ellipse instead of a rectangle.

- 1. Use code similar to the following:

  ```csharp
  // Draw the ellipse.
  public override void Draw(Graphics gr)
  {
      using (Brush brush = new SolidBrush(Background))
      {
          gr.FillEllipse(brush, Bounds);
      }
      using (Pen pen = new Pen(Foreground, Thickness))
      {
          gr.DrawEllipse(pen, Bounds);
      }
  }
  ```

- 2. Note that you don't need to override the Circle class's Draw method. The Circle class inherits from Ellipse, so it will inherit the version shown here that's defined by the Ellipse class. The Circle class's constructors ensure that the Circle's width and height are the same, and that makes the ellipse-drawing code produce a circle.

Modify the form's Paint event handler to draw smooth shapes.

- 1. Add the following using directive at the top of the form's code file:

  ```csharp
  using System.Drawing.Drawing2D;
  ```

- 2. Add the following statement at the beginning of the form's Paint event handler:

  ```csharp
  e.Graphics.SmoothingMode = SmoothingMode.AntiAlias;
  ```

![](img/d5be6ade75773ca6cec5c78f96a98bb1_405_0.png)

FIGURE 25-2

Figure 25-2 shows the result for the objects I created.

## EXERCISES

- 1. [Graphics] Copy the program you built for the Try It and override the `Shape` class's `Draw` method to create a new version that takes a `Pen` and `Brush` as parameters and uses them to draw. Then make similar changes to the `Ellipse` and `Circle` classes. Test the new methods by modifying the form's code so it passes `Pens.Red` and `Brushes.Pink` into the objects' `Draw` methods.

- 2. [Graphics] Copy the program you built for Exercise 1 and add `Rect` and `Square` classes. (I'm calling the first of those classes `Rect` instead of `Rectangle` because .NET already has a `Rectangle` class so that name could cause confusion.) Modify the form's code to create a random `Shape`, `Ellipse`, `Circle`, `Rect`, and `Square`. Hints:

  - Make the `Rect` class analogous to the `Ellipse` class.
  - Make the `Square` class somewhat analogous to the `Circle` class but give its constructor X and Y coordinates and a width instead of a center point and radius.
  - Make a `GetRandomParameters` method to generate random thickness, width, height, and position for a new shape.
  - Remove the code that makes all of the shapes pink so you can see the shapes' colors.

- 3. [Graphics, Advanced] The `abstract` keyword is somewhat similar to the `virtual` keyword. When you mark a method as `abstract`, you allow it to be overridden in derived classes. In fact, an abstract method has no code so you *must* override it before you can make an instance of the class.

  Because you cannot make an instance of a class that contains an `abstract` method, you must also mark the class as `abstract`.

  Why would you do this? Think about the program you wrote for the Try It. You probably don't really intend the program to make instances of the `Shape` class. It's really just there to be a base class so you can treat other objects such as `Ellipses` and `Circles` as `Shapes`.

  Copy the program you wrote for Exercise 2 and make the `Shape` class's `Draw` methods abstract. Then modify the form's code so it doesn't try to make a `Shape` object. Hints:

  - An abstract method cannot include any code. Just end it with a semicolon after the method's parameter list.
  - Place the `abstract` keyword before the `class` keyword.
  - An abstract class can contain non-abstract properties and methods and they are inherited as usual. In this example, the `Shape` class can still define drawing parameters (`Bounds`, `Foreground`, `Background`, and `Thickness`) and constructors.

- 4. [Graphics, Hard] Create a new program that displays a PictureBox with Cursor property set to Cross. Copy the shape classes you build for Exercise 3 into it. To copy a class from one project to another, you can create a class with the same name in the new project and then copy and paste its code into it. Alternatively you can:

  - Copy the class's file into the new project's directory.
  - Use the Project menu's Add Existing Item command to add the class to the project.
  - Edit the class's code and change its namespace statement so it uses the same namespace as the rest of the project. (You can look at the top of the main form's code to see what the statement should look like.)

  Next create a class-level `List<Shape>` named Shapes.

  Write code to allow the user to select a rectangle on the PictureBox.

  - Create two class-level Point variables named StartPoint and EndPoint. Also create a class-level bool variable named Drawing and initialize it to false.
  - In the PictureBox's MouseDown event handler, save the mouse's location in StartPoint and EndPoint and set Drawing = true.
  - In the PictureBox's MouseMove event handler, if Drawing is false, return. Otherwise, save the mouse's current position in EndPoint and refresh the PictureBox.
  - In the PictureBox's MouseUp event handler, if Drawing is false, return. Otherwise, if StartPoint and EndPoint have different X and Y coordinates, use them to create a new Rect and add it to the Shapes list.
  - In the PictureBox's Paint event handler, loop through the Shapes list and make the objects it contains draw themselves. Then if Drawing is true, draw a red dashed rectangle with corners at StartPoint and EndPoint. (Hints: The DrawRectangle method can't draw rectangles with negative widths or heights so you'll need to figure out where the upper-left corner of the newly selected rectangle is. The Math.Min and Math.Abs methods may help.)

  ![](img/d5be6ade75773ca6cec5c78f96a98bb1_407_0.png)

  FIGURE 25-3

- 5. [Graphics, Hard] Copy the program you built for Exercise 4 and add the toolbar holding four dropdown buttons shown in Figure 25-3.

  The dropdown buttons represent the user's selected shape, line thickness, foreground color, and background color. When the user finishes selecting an area on the PictureBox, add the appropriate shape to the Shapes list. Hints:

  - Use the properties of the menu items to store the selected values.
  - Use the menu items' Tag properties to store the line thickness values. (You'll need to parse those values when you need them.)
