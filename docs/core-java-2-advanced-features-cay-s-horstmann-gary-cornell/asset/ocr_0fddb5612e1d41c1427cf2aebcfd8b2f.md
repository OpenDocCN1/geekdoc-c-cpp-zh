In the following sections, we will explain how to make simple tables, how the user interacts with them, and how to make some of the most common adjustments. As with the other complex Swing controls, it is impossible to cover all aspects in complete detail. For more information, look in *Graphic Java™, Third Edition*, by David M. Geary (Prentice Hall, 1999), or *Core Swing* by Kim Topley (Prentice Hall, 1999).

# 10.2.1  A Simple Table

Similar to the `JList` component, a `JTable` does not store its own data but obtains them from a *table model*. The JTable class has a constructor that wraps a two-dimensional array of objects into a default model. That is the strategy that we use in our first example; later in this chapter, we will turn to table models.

Figure 10.5 shows a typical table, describing the properties of the planets of the solar system. (A planet is *gaseous* if it consists mostly of hydrogen and helium. You should take the “Color” entries with a grain of salt—that column was added because it will be useful in later code examples.)

![](bbox=[0.28, 0.482, 0.807, 0.684])

**Figure 10.5**  A simple table

As you can see from the code in Listing 10.5, the data of the table is stored as a two-dimensional array of Object values:

```
Object[][] cells =
{
    { "Mercury", 2440.0, 0, false, Color.YELLOW },
    { "Venus", 6052.0, 0, false, Color.YELLOW },
    ...
}
```