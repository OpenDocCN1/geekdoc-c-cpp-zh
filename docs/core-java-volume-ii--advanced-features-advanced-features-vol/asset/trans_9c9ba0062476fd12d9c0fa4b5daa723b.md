
**提示：** 要查看各轮次，请使用 `-XprintRounds` 标志运行 `javac` 命令：

```text
Round 1:
    input files: {rect.Point, rect.Rectangle,
        rect.SourceLevelAnnotationDemo}
    annotations: [sourceAnnotations.ToString]
    last round: false
Round 2:
    input files: {sourceAnnotations.ToStrings}
    annotations: []
    last round: false
Round 3:
    input files: {}
    annotations: []
    last round: true
```

此示例演示了工具如何收集源文件注解以生成其他文件。生成的文件不必是源文件。注解处理器可以选择生成 XML 描述符、属性文件、shell 脚本、HTML 文档等。

**注意：** 有些人建议使用注解来消除更大的苦差事。如果简单的 getter 和 setter 能够自动生成，那岂不是很好？例如，注解

```java
@Property private String title;
```

可以生成以下方法

```java
public String getTitle() { return title; }
public void setTitle(String title) { this.title = title; }
```

然而，这些方法需要添加到同一个类中。这需要编辑源文件，而不仅仅是生成另一个文件，并且超出了注解处理器的能力。可以为此构建另一个工具，但这样的工具将超出注解的使命。注解旨在作为*关于*代码项的说明，而不是用于添加或更改代码的指令。

## 8.7 字节码工程

你已经看到注解如何在运行时或源代码级别进行处理。还有第三种可能：在字节码级别进行处理。除非在源代码级别移除注解，否则它们会存在于类文件中。类文件格式已有文档记录（见 http://docs.oracle.com/javase/specs/jvms/se10/html）。该格式相当复杂，如果没有专用库，处理类文件将颇具挑战性。其中一个这样的库是 ASM 库，可从 http://asm.ow2.org 获取。

### 8.7.1 修改类文件

在本节中，我们使用 ASM 向带注解的方法添加日志消息。如果一个方法使用

```java
@LogEntry(logger=loggerName)
```

进行注解，那么我们在该方法开头添加以下语句的字节码：

```java
Logger.getLogger(loggerName).entering(className, methodName);
```

例如，如果我们把 Item 类的 hashCode 方法注解为

```java
@LogEntry(logger="global") public int hashCode()
```

那么每当调用该方法时，都会打印类似以下内容的消息：

```text
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
```

为此，我们执行以下操作：

- 1. 加载类文件中的字节码。
- 2. 定位所有方法。
- 3. 对于每个方法，检查它是否有 LogEntry 注解。
- 4. 如果有，则在方法开头添加以下指令的字节码：

```text
ldc loggerName
invokestatic
    java/util/logging/Logger.getLogger:(Ljava/lang/String;)Ljava/util/logging/Logger;
ldc className
ldc methodName
invokevirtual
    java/util/logging/Logger.entering:(Ljava/lang/String;Ljava/lang/String;)V
```

插入这些字节码听起来很棘手，但 ASM 使其相当简单。我们不会详细描述分析和插入字节码的过程。重点在于，代码清单 8.9 中的程序编辑一个类文件，并在带有 LogEntry 注解的方法开头插入日志调用。

例如，下面展示如何将日志指令添加到代码清单 8.10 中的 Item.java，其中 `asm` 是你安装 ASM 库的目录：

```text
javac set/Item.java
javac -classpath .:asm/lib/* bytecodeAnnotations/EntryLogger.java
java -classpath .:asm/lib/* bytecodeAnnotations.EntryLogger set.Item
```

尝试运行

```text
javap -c set.Item
```

在修改 Item 类文件之前和之后。你可以看到在 hashCode、equals 和 compareTo 方法开头插入的指令。

```text
public int hashCode();
  0: ldc           #85; // String global
  2: invokestatic  #89;
     // Method java/util/logging/Logger.getLogger:(Ljava/lang/String;)Ljava/util/logging/Logger;
  5: ldc           #86; // String Item
  7: ldc           #88; // String hashCode
  9: invokevirtual #84;
     // Method java/util/logging/Logger.entering:(Ljava/lang/String;Ljava/lang/String;)V
 12: bipush        13
 14: aload_0
 15: getfield       #2; // Field description:Ljava/lang/String;
 18: invokevirtual #15; // Method java/lang/String.hashCode:()I
 21: imul
 22: bipush        17
 24: aload_0
 25: getfield       #3; // Field partNumber:I
 28: imul
 29: iadd
 30: ireturn
```

代码清单 8.11 中的 SetTest 程序将 Item 对象插入哈希集。使用修改后的类文件运行它时，你将看到日志消息。

```text
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
May 17, 2016 10:57:59 AM Item hashCode
FINER: ENTRY
May 17, 2016 10:57:59 AM Item equals
FINER: ENTRY
[[description=Toaster, partNumber=1729], [description=Microwave, partNumber=4104]]
```

注意，当我们两次插入同一个项时，会调用 equals。

此示例展示了字节码工程的强大之处。注解用于向程序添加指令，而字节码编辑工具会读取这些指令并修改虚拟机指令。

**代码清单 8.9** `bytecodeAnnotations/EntryLogger.java`

```java
 1  package bytecodeAnnotations;
 2
 3  import java.io.*;
 4  import java.nio.file.*;
 5
 6  import org.objectweb.asm.*;
 7  import org.objectweb.asm.commons.*;
 8
 9  /**
10   * Adds "entering" logs to all methods of a class that have the LogEntry annotation.
11   * @version 1.21 2018-05-01
12   * @author Cay Horstmann
13   */
14  public class EntryLogger extends ClassVisitor
15  {
16      private String className;
17
18      /**
19       * Constructs an EntryLogger that inserts logging into annotated methods of a given class.
20       * @param cg the class
21       */
22      public EntryLogger(ClassWriter writer, String className)
23      {
24          super(Opcodes.ASM5, writer);
25          this.className = className;
26      }
27
28      public MethodVisitor visitMethod(int access, String methodName, String desc,
29            String signature, String[] exceptions)
30      {
31          MethodVisitor mv = cv.visitMethod(access, methodName, desc, signature, exceptions);
32          return new AdviceAdapter(Opcodes.ASM5, mv, access, methodName, desc)
33          {
34              private String loggerName;
35
36              public AnnotationVisitor visitAnnotation(String desc, boolean visible)
37              {
38                  return new AnnotationVisitor(Opcodes.ASM5)
39                  {
40                      public void visit(String name, Object value)
41                      {
42                          if (desc.equals("LbytecodeAnnotations/LogEntry;")
43                              && name.equals("logger"))
44                              loggerName = value.toString();
45                      }
46                  };
47              }
48
49              public void onMethodEnter()
50              {
51                  if (loggerName != null)
52                  {
53                      visitLdcInsn(loggerName);
54                      visitMethodInsn(INVOKESTATIC, "java/util/logging/Logger", "getLogger",
55                          "(Ljava/lang/String;)Ljava/util/logging/Logger;", false);
56                      visitLdcInsn(className);
57                      visitLdcInsn(methodName);
58                      visitMethodInsn(INVOKEVIRTUAL, "java/util/logging/Logger", "entering",
59                          "(Ljava/lang/String;Ljava/lang/String;)V", false);
60                      loggerName = null;
61                  }
62              }
63          };
64      }
65
66      /**
67       * Adds entry logging code to the given class.
68       * @param args the name of the class file to patch
69       */
70      public static void main(String[] args) throws IOException
71      {
72          if (args.length == 0)
73          {
74              System.out.println("USAGE: java bytecodeAnnotations.EntryLogger classfile");
75              System.exit(1);
76          }
77          Path path = Paths.get(args[0]);
78          var reader = new ClassReader(Files.newInputStream(path));
79          var writer = new ClassWriter(
80              ClassWriter.COMPUTE_MAXS | ClassWriter.COMPUTE_FRAMES);
81          var entryLogger = new EntryLogger(writer,
82              path.toString().replaceAll("[/\\\\]", "."));
83          reader.accept(entryLogger, ClassReader.EXPAND_FRAMES);
84          Files.write(Paths.get(args[0]), writer.toByteArray());
85      }
86  }
```
