When you type `MyFrame extends JFrame`, you declare that your new `MyFrame` class has all the methods and other things that are built into Java’s own `JFrame` class, and possibly more. For example, a `JFrame` instance has `setDefaultCloseOperation`, `pack`, and `setVisible` methods, so every new `MyFrame` instance has `setDefaultCloseOperation`, `pack`, and `setVisible` methods (see Figure 20-6).

![](bbox=[0.296, 0.267, 0.775, 0.515])

**Figure 20-6:** A `MyFrame` instance has many methods.

When you put the words `extends JFrame` in your code, you get all of the `JFrame` methods for free. The `MyFrame` class’s code doesn’t need declarations for methods, such as `setDefaultCloseOperation`, `pack`, and `setVisible`. Those declarations are already in the `JFrame` class in Java’s API. The only declarations in the `MyFrame` class’s code are for brand-new things — things that are specific to your newly declared `MyFrame` class. It’s as though Listing 20-2 contained the following information:

```
```java
public class MyFrame is a kind of JFrame {

    And in addition what's in JFrame, MyFrame also has
    a brand new constructor:
    public MyFrame() {
        // Etc.
    }
}
```
```