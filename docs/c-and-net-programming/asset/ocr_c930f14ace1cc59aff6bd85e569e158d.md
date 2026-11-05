# 3. Add control inside a control

+   - WPF introduced a very handy feature to add a control inside another control. WPF provides not only the text but it also allows to define a control as a content of another basic control like a Button. This feature is truly astonishing fact for the developers and this lets the world know, what the power of WPF is when it comes to user interfaces. So a TextBox can be embedded inside a Button as shown in Fig. 19.3.1. This is not possible in Windows application.

![](bbox=[0.1, 0.28, 0.85, 0.7])

Fig. 19.3.1 Textbox Control embedded in Button Control

# 4. Control templates

+   - What if the user wants to change the shape of a button, this will definitely sound weird for .NET developers. Now it can be done in WPF by defining the control template. For example a Button can be declared on for WPF window and its shape can be changed to elliptic. Templates are an integral part of user interface design in WPF.
+   - WPF has the following three types of templates, Control Template, Items Panel Template, and Data Template.

# 5. Control transforms

WPF contains a handful of 2D transforms which enables to change the size, position, rotation angle and also allows skewing. Control transforms can be performed in two ways Layout Transform and Render Transform.

+   - Layout Transform - Transform is applied before the control is laid out on the form
+   - Render Transform - Transform is applied after the control is laid on the form