# EXERCISES

1. [Graphics] Copy the program you built for the Try It and override the `Shape` class's `Draw` method to create a new version that takes a `Pen` and `Brush` as parameters and uses them to draw. Then make similar changes to the `Ellipse` and `Circle` classes. Test the new methods by modifying the form's code so it passes `Pens.Red` and `Brushes.Pink` into the objects' `Draw` methods.

2. [Graphics] Copy the program you built for Exercise 1 and add `Rect` and `Square` classes. (I'm calling the first of those classes `Rect` instead of `Rectangle` because .NET already has a `Rectangle` class so that name could cause confusion.) Modify the form's code to create a random `Shape`, `Ellipse`, `Circle`, `Rect`, and `Square`. Hints:

+   - Make the `Rect` class analogous to the `Ellipse` class.
+   - Make the `Square` class somewhat analogous to the `Circle` class but give its constructor X and Y coordinates and a width instead of a center point and radius.
+   - Make a `GetRandomParameters` method to generate random thickness, width, height, and position for a new shape.
+   - Remove the code that makes all of the shapes pink so you can see the shapes' colors.

3. [Graphics, Advanced] The `abstract` keyword is somewhat similar to the `virtual` keyword. When you mark a method as `abstract`, you allow it to be overridden in derived classes. In fact, an abstract method has no code so you *must* override it before you can make an instance of the class.

Because you cannot make an instance of a class that contains an `abstract` method, you must also mark the class as `abstract`.

Why would you do this? Think about the program you wrote for the Try It. You probably don't really intend the program to make instances of the `Shape` class. It's really just there to be a base class so you can treat other objects such as `Ellipses` and `Circles` as `Shapes`.

Copy the program you wrote for Exercise 2 and make the `Shape` class's `Draw` methods abstract. Then modify the form's code so it doesn't try to make a `Shape` object. Hints:

+   - An abstract method cannot include any code. Just end it with a semicolon after the method's parameter list.
+   - Place the `abstract` keyword before the `class` keyword.
+   - An abstract class can contain non-abstract properties and methods and they are inherited as usual. In this example, the `Shape` class can still define drawing parameters (`Bounds`, `Foreground`, `Background`, and `Thickness`) and constructors.