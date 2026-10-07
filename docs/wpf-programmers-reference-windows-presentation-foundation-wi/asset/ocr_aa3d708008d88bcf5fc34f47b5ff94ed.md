Figure 15-8 shows the program when the user presses the mouse down on Button 3.

![](bbox=[0.147, 0.131, 0.581, 0.233])

FIGURE 15-8

At this point, the pressed button is opaque. Pressing the button also moves focus to that. button. Because focus is now on Button 3, the default button is no longer defaulted. In fact, no button is default right now. Button 3 has the focus so it will fire if the user presses [Enter] but is not defaulted so it won't display the border even after the user releases the mouse.

If you drag the mouse off the button while it is still pressed, the button returns to its focused "mouse over" appearance. If you release the mouse, no mouse click occurs.Thefollowing three sections describe the glass button Template. The first describes the Template at a high level, explaining the controls Template uses and how they fit together. The two sections that follow describe the Template's *Styles* and *Triggers.*

> This program is fairly long so the complete code isn't shown in these sections. You can download the example program from the book's web site to see the details.

# Glass Button Template Overview

The following code shows the Template's main sections and the controls that it uses.

```
<ControlTemplate x:Key="temGlassButton" TargetType="Button">
  <ControlTemplate.Resources>
    Template Styles omitted here...
  </ControlTemplate.Resources>
  <Grid Name="grMain" ClipToBounds="True" Opacity="0.5"
    Width="{TemplateBinding Width}"
    Height="{TemplateBinding Height}">
    <Rectangle Name="rectMain"/>
    <ContentPresenter
      VerticalAlignment="Center"
      HorizontalAlignment="Center"/>
  </Grid>

<!-- Behaviors. -->
```