

## 创建GUI

第22行将TextFieldFrame的布局设置为FlowLayout。第25行创建了包含10列文本的textField1。文本列的像素宽度由文本字段当前字体中字符的平均宽度决定。当文本在文本字段中显示且文本比字段本身宽时，右侧的部分文本不可见。如果您在文本字段中键入，且光标到达右边缘，则左边缘的文本会被挤出字段的左侧并且不再可见。用户可以使用左右箭头键浏览完整文本。第26行将textField1添加到JFrame中。

第29行创建textField2，并在文本字段中显示初始文本“Enter text here”。字段的宽度由构造函数中指定的默认文本的宽度决定。第30行将textField2添加到JFrame中。

第33行创建textField3，并使用两个参数调用JTextField构造函数——要显示的默认文本“Uneditable text field”和文本字段的列宽（21）。第34行使用setEditable方法（JTextField从JTextComponent类继承而来）使文本字段不可编辑——即用户不能在字段中修改文本。第35行将textField3添加到JFrame中。

第38行创建passwordField，并在文本字段中显示文本“Hidden text”。字段的宽度由默认文本的宽度决定。当您执行应用程序时，请注意文本显示为星号字符串。第39行将passwordField添加到JFrame中。

## 为GUI组件设置事件处理所需的步骤

本示例应在用户在文本字段中按下Enter时显示一个消息对话框，其中包含该文本字段中的文本。在应用程序能够响应特定GUI组件的事件之前，您必须：

- 1. 创建一个表示事件处理程序并实现适当接口的类——称为事件监听器接口。
- 2. 指示当事件发生时，应通知第1步中类的对象——这称为注册事件处理程序。

## 使用嵌套类实现事件处理程序

到目前为止讨论的所有类都是所谓的顶层类——也就是说，它们没有在另一个类内部声明。Java允许您在另一个类内部声明类——这些类称为嵌套类。嵌套类可以是静态的或非静态的。非静态嵌套类称为内部类，并且经常用于实现事件处理程序。

内部类对象必须由包含该内部类的顶层类的对象创建。每个内部类对象都隐式地引用了其顶层类的对象。内部类对象可以使用此隐式引用直接访问顶层类的所有变量和方法。静态嵌套类不需要其顶层类的对象，也不隐式引用顶层类的对象。正如您将在第15章“图形与Java 2D”中看到的那样，Java 2D图形API广泛使用静态嵌套类。

## 内部类TextFieldHandler

本示例中的事件处理由私有内部类TextFieldHandler的对象执行（第50–80行）。该类是私有的，因为它仅用于为顶层类TextFieldFrame中的文本字段创建事件处理程序。与其他类成员一样，内部类可以声明为public、protected或private。由于事件处理程序往往特定于定义它们的应用程序，因此它们通常实现为私有内部类或匿名内部类（第14.11节）。

GUI组件可以生成许多事件以响应用户交互。每个事件都由一个类表示，并且只能由适当类型的事件处理程序处理。通常，组件的受支持事件在Java API文档中针对该组件的类及其超类进行描述。当用户在JTextField或JPasswordField中按Enter时，会发生ActionEvent（包 java.awt.event）。此类事件由实现ActionListener接口（包 java.awt.event）的对象处理。这里讨论的信息可在类JTextField和ActionEvent的Java API文档中找到。由于JPasswordField是JTextField的子类，因此JPasswordField支持相同的事件。

为了准备处理本示例中的事件，内部类TextFieldHandler实现了ActionListener接口，并声明了该接口中唯一的方法——actionPerformed（第53–79行）。此方法指定了当ActionEvent发生时需要执行的任务。因此，内部类TextFieldHandler满足了本节前面列出的第1步。我们稍后将讨论actionPerformed方法的细节。

## 为每个文本字段注册事件处理程序

在TextFieldFrame构造函数中，第42行创建了TextFieldHandler对象并将其赋值给变量handler。当用户在GUI的任何文本字段中按Enter时，该对象的actionPerformed方法将自动调用。但是，在此之前，程序必须将此对象注册为每个文本字段的事件处理程序。第43–46行是事件注册语句，指定handler作为三个JTextField和JPasswordField的事件处理程序。应用程序调用JTextField的addActionListener方法为每个组件注册事件处理程序。该方法接收一个ActionListener对象作为其参数，该对象可以是任何实现了ActionListener的类的对象。对象handler是一个ActionListener，因为类TextFieldHandler实现了ActionListener。在第43–46行执行后，对象handler监听事件。现在，当用户在这四个文本字段中的任何一个中按Enter时，将调用TextFieldHandler类中的actionPerformed方法（第53–79行）来处理该事件。如果特定文本字段没有注册事件处理程序，则用户在该文本字段中按Enter时发生的事件将被消耗——即应用程序只是忽略它。

软件工程观察 14.1
事件的事件监听器必须实现适当的事件监听器接口。

常见编程错误 14.2
忘记为特定GUI组件的事件类型注册事件处理程序对象会导致该类型的事件被忽略。

## TextFieldHandler类的actionPerformed方法的细节

在本示例中，我们使用一个事件处理对象的actionPerformed方法（第53–79行）来处理四个文本字段生成的事件。由于为了演示目的，我们要输出每个文本字段实例变量的名称，因此必须确定每次调用actionPerformed时是哪个文本字段生成了该事件。事件源是用户与之交互的GUI组件。当用户在某个文本字段或密码字段具有焦点时按Enter，系统会创建一个唯一的ActionEvent对象，其中包含关于刚发生事件的信息，例如事件源和文本字段中的文本。系统将此ActionEvent对象传递给事件监听器的actionPerformed方法。

第55行声明了将要显示的String。该变量以空字符串初始化——一个不包含任何字符的String。编译器要求该变量初始化，以防第58–75行的嵌套if的任何分支都不执行。

ActionEvent的getSource方法（在第58、63、68和73行调用）返回对事件源的引用。第58行的条件询问：“事件源是textField1吗？”此条件使用==运算符比较引用，以确定它们是否引用同一对象。如果它们都引用textField1，则用户是在textField1中按了Enter。然后，第59–60行创建了一个String，其中包含第78行在消息对话框中显示的消息。第60行使用ActionEvent的getActionCommand方法获取用户在生成事件的文本字段中输入的文本。

在本示例中，当用户在JPasswordField中按Enter时，我们会显示该字段中密码的文本。有时有必要以编程方式处理密码中的字符。JPasswordField类的getPassword方法将密码的字符作为char类型数组返回。

## TextFieldTest类

TextFieldTest类（图14.10）包含执行此应用程序并显示TextFieldFrame类对象的主方法。当您执行应用程序时，即使不可编辑的JTextField（textField3）也能生成ActionEvent。要测试这一点，请单击文本字段使其获得焦点，然后按Enter。此外，当您在JPasswordField中按Enter时，会显示密码的实际文本。当然，您通常不会显示密码！

此应用程序使用一个TextFieldHandler类的对象作为四个文本字段的事件监听器。从第14.10节开始，您将看到可以声明多个相同类型的事件监听器对象，并将每个对象注册到单独的GUI组件事件。这种技术使我们能够通过为每个组件的事件提供单独的事件处理程序，来消除本示例事件处理程序中使用的if…else逻辑。

```
1  // Fig. 14.10: TextFieldTest.java
2  // Testing TextFieldFrame.
3  import javax.swing.JFrame;
4
5  public class TextFieldTest
6  {
7      public static void main( String[] args )
8      {
9          TextFieldFrame textFieldFrame = new TextFieldFrame();
10         textFieldFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
11         textFieldFrame.setSize( 350, 100 ); // set frame size
```

图14.10 | TextFieldFrame的测试类。（第1部分，共2部分。）

