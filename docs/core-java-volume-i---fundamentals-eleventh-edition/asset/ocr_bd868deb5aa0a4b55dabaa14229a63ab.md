paintComponent automatically receive an object of the Graphics2D class. Simply use a cast, as follows:

```
```java
public void paintComponent(Graphics g)
{
    Graphics2D g2 = (Graphics2D) g;
    . . .
}
```

The Java 2D library organizes geometric shapes in an object-oriented fashion. In particular, there are classes to represent lines, rectangles, and ellipses:

+   - `Line2D`
+   - `Rectangle2D`
+   - `Ellipse2D`

These classes all implement the shape interface. The Java 2D library supports more complex shapes—arcs, quadratic and cubic curves, and general paths—that we do not discuss in this chapter.

To draw a shape, you first create an object of a class that implements the Shape interface and then call the draw method of the Graphics2D class. For example:

```
```java
Rectangle2D rect = . . .;
g2.draw(rect);
```
```

The Java 2D library uses floating-point coordinates, not integers, for pixels. Internal calculations are carried out with single-precision float quantities. Single precision is sufficient—after all, the ultimate purpose of the geometric computations is to set pixels on the screen or printer. As long as any roundoff errors stay within one pixel, the visual outcome is not affected.

However, manipulating float values is sometimes inconvenient for the programmer because Java is adamant about requiring casts when converting double values into float values. For example, consider the following statement:

```
```java
float f = 1.2; // ERROR--possible loss of precision
```
```

This statement does not compile because the constant 1.2 has type double, and the compiler is nervous about loss of precision. The remedy is to add an F suffix to the floating-point constant:

```
```java
float f = 1.2F; // OK
```
```

Now consider this statement:

```
```java
float f = r.getWidth(); // ERROR
```
```

This statement does not compile either, for the same reason. The getWidth method returns a double. This time, the remedy is to provide a cast: