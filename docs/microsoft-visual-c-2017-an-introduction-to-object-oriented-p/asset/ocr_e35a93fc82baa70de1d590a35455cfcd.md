# Chapter Summary

```
private void InitializeComponent()
{
    this.button1 = new System.Windows.Forms.Button();
    this.SuspendLayout();
    //
    button1
    this.button1.Location = new System.Drawing.Point(69, 60);
    this.button1.Name = "button1";
    this.button1.Size = new System.Drawing.Size(75, 23);
    this.button1.TabIndex = 0;
    this.button1.Text = "button1";
    this.UseVisualBackColor = true;
    //
    form1
    this.AutoScaleDimensions = new System.Drawing.SizeF(8F, 16F);
    this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
    this.ClientSize = new System.Drawing.Size(282, 253);
    this.Controls.Add(this.button1);
    this.Name = "Form1";
    this.Text = "Form1";
    this.ResumeLayout(false);
}
```

| Button constructor |
| Setting Location | 407 |
| Setting Name |
| Setting Size |
| Setting Text |

Figure 9-48 Some automatically generated button1 references in the IDE

In Figure 9-48, this reference preceding each occurrence of button1 refers to the class (Form1) that contains these statements.

+   Now you understand how to create properties in your own classes, you can understand the properties of GUI objects and how they were created for your use.

![](bbox=[0.102, 0.577, 0.158, 0.633])

# Chapter Summary

+   * Application classes contain a Main() method. You can also create classes from which you instantiate objects; these classes need not have a Main() method. The data components of a class are instance variables (or fields) and methods. A program or class that instantiates objects of another preset class is a class client or server class.

+   * When you create a class, you must assign a name to it and determine what data and methods will be part of the class. A class header or class definition contains an optional modifier, the keyword class, and an identifier. A class body is enclosed between curly braces. When you create a class, you usually declare instance variables to be private and instance methods to be public.

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-022-200-22