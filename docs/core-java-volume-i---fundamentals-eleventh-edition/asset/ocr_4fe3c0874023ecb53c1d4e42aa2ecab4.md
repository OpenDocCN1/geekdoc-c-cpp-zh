+   - The call to `updateMessage` causes a property change on the UI thread that triggers the setter of the bound property.

# **Listing 13.21** u1task/TaskDemo.java

```
```java
package uitask;

import java.io.*;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.*;

import javafx.application.*;
import javafx.concurrent.*;
import javafx.geometry.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.*;

public class TaskDemo extends Application
{
    private TextArea content = new TextArea("");
    private Label status = new Label();
    private ExecutorService executor = Executors.newCachedThreadPool();
    private Task<Integer> task;
    private Button open = new Button("Open");
    private Button cancel = new Button("Cancel");

    public void start(Stage stage)
    {
        open.setOnAction(event -> read(stage));
        cancel.setOnAction(event ->
        {
            if (task != null) task.cancel();
        });
        cancel.setDisable(true);
        stage.setOnCloseRequest(event ->
        {
            if (task != null) task.cancel();
            executor.shutdown();
            Platform.exit();
        });

        HBox box = new HBox(10, open, cancel);
        VBox pane = new VBox(10, content, box, status);
        pane.setPadding(new Insets(10));
        stage.setScene(new Scene(pane));
```
```