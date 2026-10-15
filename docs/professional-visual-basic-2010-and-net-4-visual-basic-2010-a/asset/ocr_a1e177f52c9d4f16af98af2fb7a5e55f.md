application starts, you might expect that Image control to immediately block the buttons, but it doesn’t. That’s because there is no image to display, so the Image control essentially stays out of the way, enabling the controls that would otherwise be behind it to both be displayed and receive input. WPF fully supports the concept of transparency, as demonstrated later in this chapter.

When there is something to display, the resulting image can block the same buttons that were used to load it (refer to Figure 17-6). Because the image isn’t part of the content for any of these buttons, none of the click events that would occur on the image at this point are raised to those buttons, so the buttons that are hidden don’t respond. This is different behavior from what you get when you layer controls, and much closer to what a Windows Forms developer might expect. As a result, you need to be aware, just as with other user interfaces, of the order in which controls overlap in the same display area that’s loaded.

Thus, everything you’ve done in the past, both with Windows Forms and ASP.NET, is still possible. On the surface, the WPF controls have more in common with existing programming models than might at first seem apparent.

Now that we have uttered heresy against this new UI paradigm, it’s time to examine what is meant by a paradigm shift with the XAML model. As noted, it starts with a new set of classes and a new declarative language, but it continues with being able to have much finer control over your application’s UI behavior.

# Customizing the User Interface

While you can create a user interface that looks disappointingly similar to a Windows Forms application, the real power of WPF is the customization it enables you to create for your application. At this point, our example moves from the ProVB_WPF application to the second application, ProVB_WPF_Step2. The goal here is to provide, through Visual Studio 2010, an even cleaner interface — not one that leverages all of WPF’s power, but one that at least reduces the Windows Forms look and feel of this application.

The first step is to change some of the application. For starters, a text box with the name of the selected directory is redundant. You don’t expect users to type that name, but rather to select it, so you can instead display the currently selected directory on the actual button label. Accordingly, the current Label and TextBox controls in the form can be removed. Additionally, both at load and following a change to the selected folder, instead of waiting for the user to request the image folder, the application should just query and pull the initial image.

Carrying out these changes is relatively simple. The first step is to adjust the existing button handler for the View Images button. Because this button will be deleted but the actions that the handler implements are still needed, change the method definition from being an event handler with associated parameters to being a private method that doesn’t require any parameters:

```
Private Sub LoadImages()
```

Next, this method needs to be called when a new directory is chosen, so update the event handler for ButtonBrowse_Click to include a call to this method when the name of the directory is updated.

Now you can get rid of the Label and TextBox controls. Eliminating the Label control is easy, as it isn’t referenced in the code, but the TextBox poses a challenge. You can replace the TextBox control with a reference to the content of the Button control, but in this case you’ve jumped from the frying pan into the fire in terms of maintenance. Face it: The button content over time could be anything.