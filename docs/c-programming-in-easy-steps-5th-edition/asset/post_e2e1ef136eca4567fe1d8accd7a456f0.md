
![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_0.png)

There is no **Enabled** property in UWP apps, but it is called **IsEnabled** instead.

- 8. In the **BtnReset_Click** event-handler block, insert statements to assign strings to the **<TextBlock>** components.

```
textBlock1->Text = "...";
textBlock2->Text = "...";
textBlock3->Text = "...";
textBlock4->Text = "...";
textBlock5->Text = "...";
textBlock6->Text = "...";
// Statements to be inserted here (Step 9).
```

- 9. Finally, insert statements to set the **<Button>** states.

```
BtnPick->IsEnabled = true;
BtnReset->IsEnabled = false;
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_1.png)

The **BtnReset** button simply returns the **<TextBox>** and **<Button>** components to their original states.

The **MainPage.xaml.cpp** code-behind page should now look like the screenshot below:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_2.png)

- 10. Return to the **MainPage.xaml** file, then in **XAML** view, see that attributes have been automatically added to the **<Button>** elements to call the event-handler code.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_4.png)

Notice that the first for loop contains only one statement to be executed on each iteration, so braces are not required.

## Testing the program

Having added functionality with C++ code above, you are now ready to test the program for two devices:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_0.png)

- 1. On the Visual Studio standard toolbar, select **Debug** for **x64** architecture and **Local Machine** options, then click the **Start** button to run the app for a PC device

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_1.png)

- 2. Wait while the application gets built and loaded, then click the buttons to try out their functionality

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_2.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_4.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_5.png)

You must have your PC set to **Developer Mode** in **Settings, Update & Security, For developers**.

The app looks good on PC devices – numbers are being randomized and the button states are changing as required.

- 3. Now, on the Visual Studio standard toolbar, select **Debug**, **Stop Debugging** to exit the running program

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_1.png)

You can safely ignore the DEBUG numbers that appear in the black boxes, but if you prefer not to see them, select **Project**, **ProjectName Properties**, **Build** then uncheck the **Define DEBUG** constant option.

- 4. On the Visual Studio standard toolbar, select **Debug** for x86 architecture and small **Mobile Emulator** options, then click the **Start** button to run the app for a mobile device

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_2.png)

- 5. Wait while the emulator starts up – this takes a while

- 6. When the application gets built and loaded, you see the controls are not visible – so you can’t try out their functionality!

- 7. What’s going on here? Click one of the emulator’s **Rotate** buttons to flip it over to Landscape orientation and look for clues

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_4.png)

- 8. Ah-ha! Some of the controls are now visible, but this is unsatisfactory – adjustments will be needed to the interface layout so the app looks good on mobile devices

- 9. Again, on the Visual Studio standard toolbar, select **Debug**, **Stop Debugging** to exit the running program

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_5.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_183_0.png)

Test on the emulator with lowest memory and smallest screen, and it should be fine running on those emulators with better features.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_183_1.png)

Do not click the X button on the emulator window to stop the running program, as that will also close the emulator.

## Adjusting the interface

The app test for mobile devices above failed to satisfactorily present the controls, as the interface is too wide for small screen devices. Happily, the interface can be made to adapt to different screen sizes so it can also look good on mobile devices. The adaptation relies upon recognizing the screen size and changing the orientation of a **<StackPanel>** element in **XAML** for narrow screen devices:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_184_0.png)

- 1. Open **MainPage.xaml**, then in XAML view add these elements immediately below the opening **<Grid>** element and before the component elements.

```xml
<VisualStateManager.VisualStateGroups>
    <VisualStateGroup>
        <!-- Elements to be inserted here (Steps 2-3) -->
    </VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```

- 2. Next, insert elements to recognize wide screens.

```xml
<VisualState x:Name="wideState">
    <VisualState.StateTriggers>
        <AdaptiveTrigger MinWindowWidth="641" />
    </VisualState.StateTriggers>
</VisualState>
```

- 3. Now, insert elements to recognize narrow screens and to change the **Orientation** of the outer **<StackPanel>**.

```xml
<VisualState x:Name="narrowState">
    <VisualState.StateTriggers>
        <AdaptiveTrigger MinWindowWidth="0" />
    </VisualState.StateTriggers>

    <VisualState.Setters>
        <Setter
            Target="MainStack.Orientation" Value="Vertical" />
    </VisualState.Setters>
</VisualState>
```

The beginning of the **MainPage.xaml** file should now look similar to the screenshot below:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_184_1.png)

XAML code recognizes the same `<!-- -->` comment tags that are used in HTML code.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_184_2.png)

Remember that the outer **<StackPanel>** in this app contains an **<Image>** and a nested **<StackPanel>** displayed horizontally, side-by-side. If displayed vertically, they should appear one above the other.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_0.png)

- 4. Select **x64** and **Local Machine** to run the app for a PC device once more – it still looks and functions well

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_1.png)

- 5. Now select **x86** and **Mobile Emulator** to run the app for a mobile device – it also now looks and functions well

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_2.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_3.png)

You can have Visual Studio nicely format the XAML code by pressing Ctrl + K, Ctrl + D.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_4.png)

Although an app may work well on an emulator, it is recommended you always test on actual devices before deployment.

## Deploying the application

Having tested the app in a **Mobile Emulator** above, it can now be tested on a real device before deployment:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_0.png)

- 1. On a Windows 10 device select **Developer mode** from the **Settings, Update & Security, For developers** menu

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_1.png)

- 2. Next, connect the device to your PC via a USB socket

- 3. On the Visual Studio toolbar, select **Debug** for **ARM** architecture and **Device** options, then click the **Start** button to run the app on the connected device

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_2.png)

- 4. Wait while the application gets built and loaded, then tap the buttons to try out their functionality

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_4.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_5.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_6.png)

You can choose the **Remote Machine** option to test via a network connection.

The app looks good, numbers are being randomized, and the button states are changing as required – the app can be deployed.
