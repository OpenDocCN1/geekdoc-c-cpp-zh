
The ShowTemplate program uses the following code to display the Target control's control:

```csharp
private void btnTemplate_Click(object sender, RoutedEventArgs e)
{
    XmlWriterSettings writer_settings = new XmlWriterSettings();
    writer_settings.Indent = true;
    writer_settings.IndentChars = " ";
    writer_settings.NewLineOnAttributes = true;

    StringBuilder sb = new StringBuilder();
    XmlWriter xml_writer = XmlWriter.Create(sb, writer_settings);
    XmlWriter.Save(Target.Template, xml_writer);

    txtResult.Text = sb.ToString();
}
```

ShowTemplate

The key to this code is the XmlWriter class, which methods extract XAML from a WPF object such as a control or template.

The code starts by initializing an XmlWriterSettings object to make the writer produce nicely formatted output. If you do not do this, the code will appear in one line of XAML without carriage returns or indentation.

The program then creates a StringBuilder to hold the result text. It uses the writer settings to create an XmlWriter attached to the StringBuilder.

The code calls the XmlWriter class's static Save method to write a XAML representation of the Target control's Template property into the StringBuilder.

The program finishes by displaying the result in its TextBox txtResult.

After you find a control's default template, you can modify it to make your own template that lets you change the control's appearance. That lets you your templates behave the same way as the default template except in those places where you want changes.

## SUMMARY

Properties and styles let you change a control's appearance in superficial ways. Templates let you change a control more fundamentally, altering the pieces that make up the control and changing the way it responds to events and changes in property values. By using templates, you can give your applications a distinctive look and feel.

The next chapter explains two topics closely related to styles and templates: themes and skins. Skins let an application change its entire appearance, sometimes radically. They let you change the application to suit your immediate need or your mood.

Themes provide a unifying appearance across controls, windows, and even separate applications. By providing a common look and feel, themes can make even unrelated programs seem to fit together in a single system.

# 16

## Themes and Skins

WPF lets you build applications that have engaging, distinctive appearances. By using relatively simple techniques as drop shadows, partial transparency, and transparency masks, you can make an eye-catching interface that adds interest and excitement to even the most routine application.

Properties let you change the appearance of controls. They let you change visual characteristics such as a control's colors, size, location, and contents. Resources and styles let you package those changes so that you can easily apply them to many controls simultaneously.

Templates let you alter the controls behave by changing the pieces that make the controls. They let you change the appearance and behavior of Buttons, ListBoxes, Menus, and other controls in fundamental ways while still allowing them to perform their essential functions.

Themes and skins bring all of these ideas together to let you easily change the appearance and behavior of an entire application to suit the users' needs and moods.

# THEMES

Some developers use the theme and skin interchangeably, but I make the distinction that a skin applies to a single application (or part of an application), and a theme applies to more than one application.

More precisely, a theme is a unifying plan that helps determine the appearance and behavior of more than one application. The most common themes are those provided by Windows. Windows 7 provides the themes:

- Aero
- Classic
- Luna (Homestead, Metallic, and Normal versions)
- Royale

## Using the System Theme

The ShowThemes example program shown in Figure 16-1 displays controls that use each of the themes that come with Windows 7. The differences are fairly subtle, you'll need to look closely to see the changes in each theme.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_321_0.png)

Figure 16-1

If you don't use properties, styles, or templates to change a control's appearance or behaviors, it uses the values defined by the system's current theme. In Figure 16-1, you can see that the controls in the "default" group have the same appearance as those that use the Aero theme. This is because the system had the Aero selected when I ran the program.

To change the system's theme in Windows 7, open the Control Panel. Under "Appearance and Personalization" click "Change the theme." On the dialog shown in Figure 16-2, click the theme that you want to.

After taking the screenshot in Figure 16-1, I followed these steps to change the system's theme to Windows Classic without closing the ShowThemes program. The program automatically detected the change in the system theme and redrew itself appropriately.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_321_1.png)

FIGURE 16-2

Figure 16-3 shows the result. If you look CLOSELY, you'll see that the controls in the default group now match those that use the Classic theme.

# Themes | 285

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_322_0.png)

Figure 16-3

If you compare Figures 16-1 and 16-3 very closely, you'll also see that the controls in the ShowThemes program look a little different. In Figure 16-3, the window's upper corners are not rounded, the title bar is darker, the border is no longer shaded with a light blue pattern, and the system icons in the form's upper-left and upper-right corners are different.

## Using a Specific Theme

Normally you don't need to think about themes. If you leave a control's appearance alone, it will automatically use the system's current theme and even change its appearance if you change the theme. If you really want to, however, you can select a specific theme.

> CHANGING THEMES
> This technique is probably more useful for testing an application to see what it looks like in a particular theme than it is for forcing the theme on the users.
Some users may select a particular theme for a good reason. For example, a visually impaired user may select a high-contrast theme to make programs easier to see. If you change the theme, they may be unable to use your application.
If you don't really need a specific theme, you should let your program use the default.

To use a specific system in Visual Studio, begin a new WPF project. Project the Menu and select "Add Reference.\ On the .NET tab, select the theme(s) that you want to use and click OK. Figure 16-4 shows the Add Reference dialog with the Aero, Classic, Luna, and Royale themes selected.

Next, in a resource dictionary, use a MergedDictionaries object to load the theme. The theme will apply to any controls that should be modified by the dictionary.

# 286 | CHAPTER 16 THEMES AND SKINS

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_323_0.png)

FIGURE 16-4

For example, the code below shows how the Show program uses the Luna Metallic theme. Each group of controls shown in Figures 16-1 and 16-3 is contained in a StackPanel. Each StackPanel has a ResourceDictionary that loads its theme.

```xml
<StackPanel>
  <StackPanel.Resources>
    <ResourceDictionary>
      <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary Source="/PresentationFramework.Luna;component/themes/luna.metallic.xaml" />
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </StackPanel.Resources>
  <Label Style={StaticResource Style} Content="luna.metallic"/>
  <Button Margin="10" Content="Click Me"/>
  <CheckBox Margin="10" Content="Check Me"/>
  <RadioButton Margin="10" Content="Press Me"/>
</StackPanel>
```

Available for download on Wprox.com

ShowThemes

Notice the unusual syntax for the ResourceDictionary.Source property. The PresentationFramework Luna piece WPF which contains the library, and the rest of the Source gives the theme within the library.

For more information on Microsoft's standard themes, go to msdn.microsoft.com/aa358533.aspx. Links at the bottom of the web page lead to pages about the specific themes Aero, Classic, and Royale. From those pages, you can download XAML files that show how themes are defined. You can modify those files to build your own theme files.
