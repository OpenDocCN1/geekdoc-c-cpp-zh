# 14.2 Windows Forms 587

discussed in Chapter 15. A component is an instance of a class that implements the IComponent interface, such as a Button or Label, is a component that has a graphical representation at runtime. Some components lack graphical representations (e.g., class Timer of namespace System.windows.Forms—see Chapter 15). Such components are not visible at runtime.

Figure 14.3 displays the Windows forms and controls from the C# Toolbox. The controls and controls are organized by functionality. Selecting the category All Windows Forms at the top of the Toolbox allows you to view all the controls and components from the other tabs in list (as shown in Fig. 14.3). In this chapter and next, we discuss many of these controls and components. To add a control or component to a Form, select that control or component from the Toolbox and drag it onto the Form. To select a control or component, select the Pointer item in the Toolbox (the one at the top of list).

![](bbox=[0.243, 0.375, 0.757, 0.758])

Display all controls and components

Categories by functionality

Fig. 14.3 Active Window and Controls for Windows Forms.

# Active Window and Focus

When there are several windows on the screen, the active window is the frontend and has a highlighted title bar. A window becomes the active window when the user clicks inside it. The active window is said to "have the focus.\ For example, in Visual Studio the active window is the Toolbox when you're selecting an item from it, or the Properties window when you're editing a control's properties.