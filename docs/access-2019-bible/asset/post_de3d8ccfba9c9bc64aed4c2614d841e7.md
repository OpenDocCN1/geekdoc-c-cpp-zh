
A collection might contain many thousands of objects. Although performance suffers when a collection contains tens of thousands of objects, a collection is a handy way to store an arbitrary number of items as an application runs. You'll see several examples of using collections as storage devices in this book.

> NOTE
> The period that exists between an object and its properties or methods is commonly known as the dot operator. The dot operator gives you access to an object's properties and methods.

## Properties and methods

Objects have properties and methods. They also have events, which we'll discuss thoroughly in Chapter 26.

## Properties

Properties let you read and change simple values that are the characteristics of the object. The Label object has a Caption property. The Caption property is the string that is displayed in the label. The Label object also has Height and Width properties that hold numbers determining the object's size. These are examples of properties that hold simple values.

Properties can also return other objects. As you've seen, the Form object has a Controls property. But isn't Controls a collection object? Yes, it is. And for each collection object, there is a property that returns it. When you write MyForm.Controls.Count, you're using the Controls property of MyForm to get access to the Controls collection object. Fortunately, the Access object model is so well designed that you don't have to worry about what is a simple property and what is a property returning an object. When you see two dot operators in a single statement, you can be sure you're accessing another object. Typing a dot operator after a simple value property won't give you any options.

## Methods

You can also access an object's methods through the dot operator. Methods differ from properties because they don't return a value. Methods can generally be put into two categories:

- Methods that change more than one property at once
- Methods that perform an action external to the object

The first type of method changes two or more properties at once. The CommandButton object has a method called SizeToFit. The SizeToFit property changes the Height property, the Width property, or both so that all the text in the Caption property can be displayed.

The second type of method performs some action outside its parent object. It usually also changes a few properties on the way. The Form object has an Undo method. The Undo
method has to go outside of the form and read the undo stack from Access to determine what the last action was. When this method is called after a text box is changed, the text box's Text property is changed back to its previous value.

## The With statement

The With statement enables you to access an object's properties and methods without typing the object's name over and over. Any properties or methods used between With and End With automatically refer to the object specified in the With statement. Any number of statements can appear between the With and End With statements, and With statements can be nested. Properties and methods will refer to the object in the innermost With block that contains them.

For example, consider the code using the following For...Next looping construct. This code loops through all members of a form's Controls collection, examining each control. If the control is a command button, the button's font is set to 12 point, bold, Times New Roman:

```
Private Sub cmdOld_Click()
    Dim i As Integer
    Dim MyControl As Control

    For i = 0 To Me.Controls.Count - 1
        Set MyControl = Me.Controls(i) 'Grab a control
        If TypeOf MyControl Is CommandButton Then
            'Set a few properties of the control:
            MyControl.FontName = "Times New Roman"
            MyControl.FontBold = True
            MyControl.FontSize = 12
        End If
    Next
End Sub
```

Don't be confused by the different expressions you see in this example. The heart of this procedure is the For...Next loop. The loop begins at zero (the start value) and executes until the i variable reaches the number of controls on the form minus one. (The controls on an Access form are numbered beginning with zero. The Count property tells you how many controls are on the form.) Within the loop, a variable named MyControl is pointed at the control indicated by the i variable. The If TypeOf statement evaluates the exact type of control referenced by the MyControl variable.

Within the body of the If...Then block, the control's properties (FontName, FontBold, and FontSize) are adjusted. You'll frequently see code such as this when it's necessary to manipulate all the members of a collection.

Notice that the control variable is referenced in each of the assignment statements. Referencing control properties one at a time is a fairly slow process. If the form contains many controls, this code executes relatively slowly.

An improvement on this code uses the With statement to isolate one member of the Controls collection and apply a number of statements to that control. The following code uses the With statement to apply a number of font settings to a single control:

```
Private Sub cmdWith_Click()
    Dim i As Integer

    Dim MyControl As Control

    For i = 0 To Me.Controls.Count - 1
        Set MyControl = Me.Controls(i) 'Grab a control
        If TypeOf MyControl Is CommandButton Then
            With MyControl
                'Set a few properties of the control:
                .FontName = "Arial"
                .FontBold = True
                .FontSize = 8
            End With
        End If
    Next
End Sub
```

The code in this example (cmdWith_Click) executes somewhat faster than the previous example (cmdOld_Click). Once Access has a handle on the control (with MyControl), it’s able to apply all the statements in the body of the With without having to fetch the control from the controls on the form as in cmdOld_Click.

In practical terms, however, it’s highly unlikely that you’ll notice any difference in execution times when using the With construct as shown in this example. However, when working with massive sets of data, the With statement might contribute to overall performance. In any case, the With statement reduces the wordiness of the subroutine and makes the code much easier to read and understand. It also saves tons of typing when you’re changing a lot of properties of an object.

Think of the With statement as if you’re handing Access a particular item and saying “Here, apply all these properties to this item.” The previous example said, “Go get the item named x and apply this property to it” over and over again.

## The For Each statement

The code in cmdWith_Click is further improved by using the For Each statement to traverse the Controls collection. For Each walks through each member of a collection, making it available for examination or manipulation. The following code shows how For Each simplifies the example:

```
Private Sub cmdForEach_Click()
    Dim MyControl As Control
```

## 1. 引言

在当今快速发展的科技时代，人工智能（AI）已成为推动社会进步的关键力量。从智能助手到自动驾驶，AI 技术正在深刻改变我们的生活方式和工作模式。本文旨在探讨 AI 技术的最新进展及其在各领域的应用前景。

## 2. AI 技术的主要分支

- 机器学习（Machine Learning）
- 深度学习（Deep Learning）
- 自然语言处理（Natural Language Processing）
- 计算机视觉（Computer Vision）

## 3. 应用领域

| 领域 | 应用示例 |
|------|----------|
| 医疗 | 疾病诊断、药物研发 |
| 交通 | 自动驾驶、智能调度 |
| 教育 | 个性化学习、智能辅导 |
| 金融 | 风险评估、智能投顾 |

## 4. 未来展望

随着技术的不断突破，AI 将在更多领域发挥重要作用。然而，我们也需要关注 AI 带来的伦理和社会问题，确保技术发展造福全人类。

## Exploring the Visual Basic Editor

To be a productive Access developer, you need to know your way around the Visual Basic Editor (VBE). This section explores the features of the VBE and how to use them.

### The Immediate window

When you write code for a procedure, you might want to try the procedure while you're in the module, or you might need to check the results of an expression. The Immediate window (shown in Figure 24.13) enables you to try your procedures without leaving the module. You can run the module and check variable values.

**FIGURE 24.13**

The Immediate window.

![](img/1e45673ab6eca9d20e67635ff5b9b318_835_0.png)

Press Ctrl+G to view the Immediate window, or choose View ◇ Immediate Window in the VBA code editor.

> **NOTE**
> 
> Notice that the VBE window doesn’t use the Ribbon. Instead, the code window appears much as it has in every version of Access since Access 2000. Therefore, in this book, you’ll see references to the code window’s toolbar and menu whenever we describe working with Access VBA modules. Don’t confuse references to the code editor’s toolbar with the main Access window’s Ribbon.
