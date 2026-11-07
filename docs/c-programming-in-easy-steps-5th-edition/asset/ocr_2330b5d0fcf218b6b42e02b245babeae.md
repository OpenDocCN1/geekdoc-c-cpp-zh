![](bbox=[0.116, 0.073, 0.206, 0.131])

There is no **Enabled** property in UWP apps; but it is called **IsEnabled** instead.

+   8. In the **BtnReset_Click** event-handler block, insert statements to assign strings to the **<TextBlock>** components.

```
textBlock1->Text = “...”;
textBlock2->Text = “...”;
textBlock3->Text = “...”;
textBlock4->Text = “...”;
textBlock5->Text = “...”;
textBlock6->Text = “...”;
// Statements to be inserted here (Step 9).
```

+   9. Finally, insert statements to set the **<Button>** states.

```
BtnPick->IsEnabled = true ;
BtnReset->IsEnabled = false ;
```

![](bbox=[0.116, 0.337, 0.207, 0.396])

The **BtnReset** button simply returns the **<TextBox>** and **<Button>** components to their original states.

The **MainPage.xaml.cpp** code-behind page should now look like the screenshot below:

![](bbox=[0.311, 0.463, 0.689, 0.62])

+   10. Return to the **MainPage.xaml** file, then in **XAML** view, see that attributes have been automatically added to the **<Button>** elements to call the event-handler code.

![](bbox=[0.151, 0.679, 0.848, 0.71])

![](bbox=[0.116, 0.723, 0.207, 0.779])

Notice that the first for loop contains only one statement to be executed on each iteration, so braces are not required.