# Listing 13.1 *(Continued)*

```
```java
public class NotHelloWorld extends Application
{
    private static final int MESSAGE_X = 75;
    private static final int MESSAGE_Y = 100;

    private static final int PREFERRED_WIDTH = 300;
    private static final int PREFERRED_HEIGHT = 200;

    public void start(Stage stage)
    {
        Text message = new Text(MESSAGE_X, MESSAGE_Y,
            "Not a Hello World program");

        Pane root = new Pane(message);
        root.setPrefSize(PREFERRED_WIDTH, PREFERRED_HEIGHT);

        Scene scene = new Scene(root);
        stage.setScene(scene);
        stage.setTitle("NotHelloWorld");
        stage.show();
    }
}
```
```

![](bbox=[0.194, 0.551, 0.234, 0.584])

> > **NOTE:** As you see from this example, no main method is required to launch a JavaFX application. The java program launcher knows about JavaFX and calls its launch method.

In previous versions of JavaFX, you were required to include a main method of the form

```
```java
public class MyApp extends Application
{
    public static void main(String[] args)
    {
        launch(args);
    }
    . . . .
}
```
```

You can still do this if your tool chain is flustered by an absence of public static void main.