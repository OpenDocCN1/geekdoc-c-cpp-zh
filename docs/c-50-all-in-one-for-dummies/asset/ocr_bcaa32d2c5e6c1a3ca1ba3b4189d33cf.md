# 668 Working in Visual Studio

As promised, the ASP.NET Label control became a <span>, and the ASP.NET Button control becomes an <input> control. All that the designer is doing is helping you markup code. There is no magic here.

All the controls that you just have their default values. In order to have clean code, you need to intelligently manage your controls. Additionally, you may have other values you need to set on those controls. There might even be things you didn't even know the control could do that you can.

The trick to do this is in the Properties panel, which was introduced in Book IV, Chapter 2. The Properties panel handles the properties of ASP.NET controls just well as it does anything else. For instance, to rename the controls from the preceding example, follow these steps:

+   1. Open the project you were working on earlier, if it isn't already open.
2. Double-click Default.aspx in the Solution Explorer.
3. Change to Design view.
4. Press the <F4> to bring up the Properties panel.
5. In the Designer, click the Label you added.
6. Change the Text Property to This is The Text to Change.
7. Open the Font tree view by clicking the little triangle next to the Font.
8. Change the size property to 14.
See the label change in the designer?

Notice the Properties panel changes to look like Figure 2-3.

![](bbox=[0.25, 0.638, 0.875, 0.903])

Figure 2-3: Properties look like this!