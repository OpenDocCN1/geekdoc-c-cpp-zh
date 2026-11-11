
```java
var menuBar = new JMenuBar();
setJMenuBar(menuBar);

var menu = new JMenu("File");
menuBar.add(menu);

openItem = new JMenuItem("Open");
menu.add(openItem);
openItem.addActionListener(event -> {
    // show file chooser dialog
    int result = chooser.showOpenDialog(null);

    // if file selected, set it as icon of the label
    if (result == JFileChooser.APPROVE_OPTION)
    {
        textArea.setText("");
        openItem.setEnabled(false);
        textReader = new TextReader(chooser.getSelectedFile());
        textReader.execute();
        cancelItem.setEnabled(true);
    }
});

cancelItem = new JMenuItem("Cancel");
menu.add(cancelItem);
cancelItem.setEnabled(false);
cancelItem.addActionListener(event -> textReader.cancel(true));
pack();
}

private class ProgressData
{
    public int number;
    public String line;
}

92  private class TextReader extends SwingWorker<StringBuilder, ProgressData>
93  {
94      private File file;
95      private StringBuilder text = new StringBuilder();
96
97      public TextReader(File file)
98      {
99          this.file = file;
100     }
101
102     // the following method executes in the worker thread; it doesn't touch Swing components
103
104     public StringBuilder doInBackground() throws IOException, InterruptedException
105     {
106         int lineNumber = 0;
107         try (var in = new Scanner(new FileInputStream(file), StandardCharsets.UTF_8))
108         {
109             while (in.hasNextLine())
110             {
111                 String line = in.nextLine();
112                 lineNumber++;
113                 text.append(line).append("\n");
114                 var data = new ProgressData();
115                 data.number = lineNumber;
116                 data.line = line;
117                 publish(data);
118                 Thread.sleep(1); // to test cancellation; no need to do this in your programs
119             }
120         }
121         return text;
122     }
123
124     // the following methods execute in the event dispatch thread
125
126     public void process(List<ProgressData> data)
127     {
128         if (isCancelled()) return;
129         var builder = new StringBuilder();
130         statusLine.setText("" + data.get(data.size() - 1).number);
131         for (ProgressData d : data)
132             builder.append(d.line).append("\n");
133         textArea.append(builder.toString());
134     }
135     public void done()
136     {
137         try
138         {
139             StringBuilder result = get();
140             textArea.setText(result.toString());
141             statusLine.setText("Done");
142         }
143         catch (InterruptedException ex)
144         {
145         }
146         catch (CancellationException ex)
147         {
148             textArea.setText("");
149             statusLine.setText("Cancelled");
150         }
151         catch (ExecutionException ex)
152         {
153             statusLine.setText("" + ex.getCause());
154         }
155
156         cancelItem.setEnabled(false);
157         openItem.setEnabled(true);
158     }
159     }
160 }
```

## javax.swing.SwingWorker<T, V>

- `abstract T doInBackground()`
  是要重写的方法，用于执行后台任务并返回工作结果。
- `void process(List<V> data)`
  是要重写的方法，用于在事件调度线程中处理中间进度数据。
- `void publish(V... data)`
  将中间进度数据转发到事件调度线程。从 `doInBackground` 中调用此方法。
- `void execute()`
  安排此工作器在工作线程上执行。
- `SwingWorker.StateValue getState()`
  获取此工作器的状态，为 `PENDING`、`STARTED` 或 `DONE` 之一。

## 12.8 进程

到目前为止，你已经了解了如何在同一个程序内的单独线程中执行 Java 代码。有时，你需要执行另一个程序。为此，请使用 `ProcessBuilder` 和 `Process` 类。`Process` 类在单独的操作系统进程中执行命令，并允许你与其标准输入、输出和错误流交互。`ProcessBuilder` 类允许你配置 `Process` 对象。

![](img/0e7b74ef51a065c077b42cd87b362288_1182_0.png)

> **注意：**
> 
> `ProcessBuilder` 类是对 `Runtime.exec` 调用的更灵活的替代。

### 12.8.1 构建进程

首先指定要执行的命令。你可以提供一个 `List<String>`，或者直接提供组成该命令的各个字符串。

```java
var builder = new ProcessBuilder("gcc", "myapp.c");
```

> **警告：**
> 
> 第一个字符串必须是可执行命令，而不是 shell 内建命令。例如，要在 Windows 中运行 `dir` 命令，需要用字符串 `"cmd.exe"`、`"/C"` 和 `"dir"` 构建一个进程。

每个进程都有一个*工作目录*，用于解析相对目录名。默认情况下，进程的工作目录与虚拟机相同，通常就是你启动 `java` 程序时所在的目录。你可以用 `directory` 方法更改它：

```java
builder = builder.directory(path.toFile());
```

> **注意：**
> 
> 用于配置 `ProcessBuilder` 的每个方法都返回自身，因此你可以链式调用这些方法。最终，你会调用
> 
> ```java
> Process p = new ProcessBuilder(command).directory(file)...start();
> ```

接下来，你会希望指定进程的标准输入、输出和错误流应当如何处理。默认情况下，它们各自都是一个管道，你可以通过以下方式访问：

```java
OutputStream processIn = p.getOutputStream();
InputStream processOut = p.getInputStream();
InputStream processErr = p.getErrorStream();
```

注意，进程的输入流在 JVM 中是一个输出流！你向该流写入内容，写入的内容就会成为进程的输入。反过来，你读取进程写入输出流和错误流的内容。对你而言，它们是输入流。

你可以指定新进程的输入、输出和错误流与 JVM 的相同。如果用户在控制台中运行 JVM，任何用户输入都会转发给该进程，而进程输出会显示在控制台中。调用

```java
builder.inheritIO()
```

即可对全部三个流进行此设置。如果你只想继承其中一些流，请将值

```java
ProcessBuilder.Redirect.INHERIT
```

传递给 `redirectInput`、`redirectOutput` 或 `redirectError` 方法。例如，

```java
builder.redirectOutput(ProcessBuilder.Redirect.INHERIT);
```

你可以通过提供 `File` 对象将进程流重定向到文件：

```java
builder.redirectInput(inputFile)
        .redirectOutput(outputFile)
        .redirectError(errorFile)
```

输出和错误对应的文件会在进程启动时创建或截断。要追加到现有文件，请使用

```java
builder.redirectOutput(ProcessBuilder.Redirect.appendTo(outputFile));
```

合并输出流和错误流通常很有用，这样你就能按进程生成它们的顺序看到输出和错误消息。调用

```java
builder.redirectErrorStream(true)
```

以启用合并。如果这样做，你就不能再在 `ProcessBuilder` 上调用 `redirectError`，也不能在 `Process` 上调用 `getErrorStream`。

你可能还想修改进程的环境变量。这时，构建器的链式语法就不适用了。你需要获取构建器的环境（它由运行 JVM 的进程的环境变量初始化），然后放入或移除条目。

```java
Map<String, String> env = builder.environment();
env.put("LANG", "fr_FR");
env.remove("JAVA_HOME");
Process p = builder.start();
```

如果你想把一个进程的输出通过管道送入另一个进程的输入（就像 shell 中的 `|` 运算符那样），Java 9 提供了 `startPipeline` 方法。传入一个进程构建器列表，并从最后一个进程读取结果。下面是一个示例，枚举目录树中不重复的扩展名：

```java
List<Process> processes = ProcessBuilder.startPipeline(List.of(
    new ProcessBuilder("find", "/opt/jdk-17"),
    new ProcessBuilder("grep", "-o", "\\.[^.]*$"),
    new ProcessBuilder("sort"),
    new ProcessBuilder("uniq")
));
```
