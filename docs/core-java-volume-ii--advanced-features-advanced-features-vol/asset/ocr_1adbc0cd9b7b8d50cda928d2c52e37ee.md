+   2. To use a class in a different module if it is available, and otherwise do something else, such as:

```
try
{
    new oracle.jdbc.driver.OracleDriver();
    . . .
}
catch (NoClassDefFoundError er)
{
    *Do something else*
}
```

# 9.12 Qualified Exporting and Opening

In this section, you will see a variant of the exports and opens statement that narrows their scope to a specified set of modules. For example, the javafx.base module contains a statement

```
exports com.sun.javafx.collections to
    javafx.controls, javafx.graphics, javafx.fxml, javafx.swing;
```

Such a statement is called a *qualified export*. The listed modules can access the package, but other modules cannot.

Excessive use of qualified exports can indicate a poor modular structure. Nevertheless, they can arise when modularizing an existing code base. Here, the Java platform designers distributed the code for JavaFX into multiple modules, which is a good idea because not all JavaFX applications need FXML or Swing interoperability. However, the JavaFX implementors liberally used internal classes such as com.sun.javafx.collections.ListListenerHelper in their code. In a greenfield project, one can instead design a more robust public API.

Similarly, you can restrict the opens statement to specific modules. For example, in Section 9.7, “Modules and Reflective Access,” on p. 511 we could have used a qualified opens statement, like this:

```
module v2ch09.openpkg
{
    requires com.horstmann.util;
    opens com.horstmann.places to com.horstmann.util;
}
```

Now the com.horstmann.places package is only opened to the com.horstmann.util module.