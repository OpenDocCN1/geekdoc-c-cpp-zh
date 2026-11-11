> > **C++ NOTE:** C and C++ distinguish between the *declaration* and *definition* of a variable. For example,
> >
> >     int i = 10;
> >
> > is a definition, whereas
> >
> >     extern int i;
> >
> > is a declaration. In Java, no declarations are separate from definitions.

# ### 3.4.3 Constants

In Java, you use the keyword `final` to denote a constant. For example:

```
```java
public class Constants
{
   public static void main(String[] args)
   {
      final double CM_PER_INCH = 2.54;
      double paperWidth = 8.5;
      double paperHeight = 11;
      System.out.println("Paper size in centimeters: "
            + paperWidth * CM_PER_INCH + " by " + paperHeight * CM_PER_INCH);
   }
}
```
```

The keyword `final` indicates that you can assign to the variable once, and then its value is set once and for all. It is customary to name constants in all uppercase.

It is probably more common in Java to create a constant so it’s available to multiple methods inside a single class. These are usually called *class constants*. Set up a class constant with the keywords `static final`. Here is an example of using a class constant:

```
```java
public class Constants2
{
   public static final double CM_PER_INCH = 2.54;

   public static void main(String[] args)
   {
      double paperWidth = 8.5;
      double paperHeight = 11;
      System.out.println("Paper size in centimeters: "
            + paperWidth * CM_PER_INCH + " by " + paperHeight * CM_PER_INCH);
   }
}
```
```