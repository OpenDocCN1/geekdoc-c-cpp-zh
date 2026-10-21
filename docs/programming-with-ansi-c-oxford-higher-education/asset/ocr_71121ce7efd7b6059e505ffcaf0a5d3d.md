```
{
	cout << "Circle is drawn\n";
}
```

```
int main()
{
	// Shape SomeShape;
	Shape *PtrShape;
	Circle Ring;
	// SomeShape.draw();
	/*
	 * We cannot call the draw() function of the Shape class, as we cannot have an object of the abstract class. */
	PtrShape->Shape::draw(); //Static call to Shape draw()
	PtrShape = &Ring;
	PtrShape->draw(); // Draws a circle
	cout << "Messages from destructor start now\n";
	PtrShape = new Circle;
	delete PtrShape;
	/*
	 * If ~Shape is not virtual, this will not work as expected.
	 * It will only delete the base class subobject (shape subobject of circle) and not the entire derived class object (circle). */
	cout << "Above messages are from delete\n";
	cout << "Following are normal messages exiting the program\n";
}
```

# Output

+   Shape is drawn
+   Circle is drawn
+   Messages from destructor start now
+   Circle destroyed
+   Shape destroyed
+   Above messages are from delete
+   Following are normal messages exiting the program
+   Circle destroyed
+   Shape destroyed

# How the Program Works

# Defining pure virtual function

```
virtual void draw() = 0;
```

is important here. It shows the pure virtual function being defined, which makes the class Shape an abstract class. It should also be noted how the body is also defined outside the class.

```
void Shape::draw()
{
	cout << "Shape is drawn\n";
}
```

So, this is how one can define a body for a pure virtual function. It should be remembered that every class that inherits from Shape must implement this function (otherwise, it becomes abstract). What a designer wants to convey when he/she defines a pure virtual function is