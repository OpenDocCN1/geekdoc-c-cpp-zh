
{ return this.customers.Count > 1 && !this.IsAtEnd; } is specified as the function to call when the CanExecute method runs.

This expression returns true as long as the customers list contains more than one customer and the ViewModel is not positioned on the final customer in this list. The PreviousCustomer Command follows the same pattern: it invokes the Previous method to retrieve the previous customer from the list, and the CanExecute method references the expression () => { return this.customers.Count > 0 && !this.IsAtStart; }, which returns true as long as the customers list contains at least one customer and the ViewModel is not positioned on the first customer in this list.

+   9. On the Build menu, click Build Solution and verify that your app still builds without errors.

Now that you have added the NextCustomer and PreviousCustomer commands to the ViewModel, you can bind these commands to buttons in the view. When the user clicks a button, the appropriate command will run.

Microsoft publishes guidelines for adding buttons to views in UWP apps, and the general recommendation is that buttons that invoke commands should be placed on a command bar. UWP apps provide two command bars: one appears at the top of the form and the other at the bottom. Buttons that navigate through an app or data are commonly placed on the top command bar, and this is the approach that you will adopt in the next exercise.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_791_0.png)

## Note

> You can find the Microsoft guidelines for implementing command bars at http://msdn.microsoft.com/library/windows/apps/hh465302.aspx.

## Add Next and Previous buttons to the Customers form

+   1. Open the MainPage.xaml file in the Design View window.

+   2. Scroll to the bottom of the XAML pane and add the following markup shown in bold, immediately above the closing </Page> tag:

Click here to view code image

```
...
<Page.TopAppBar>
    <CommandBar>
        <AppBarButton x:Name="previousCustomer" Icon="Previous" Label="Previous" Command="{Binding Path=PreviousCustomer}"/>
        <AppBarButton x:Name="nextCustomer" Icon="Next" Label="Next" Command="{Binding Path=NextCustomer}"/>
    </CommandBar>
</Page.TopAppBar>
```

```
</Page>
```

There are several points to notice in this fragment of XAML markup:

- By default, the command bar appears at the top of the screen and displays icons for the buttons that it contains. The label for each button is displayed only when the user clicks the More (...) button that appears on the right side of the command bar. However, if you are designing an application that could be used in multiple cultures, you should not use hard-coded values for labels but instead store the text for these labels in a culture-specific resources file and bind the *Label* property dynamically when the application runs. For more information, visit the page “Quickstart: Translating UI resources (XAML)” on the Microsoft website at https://msdn.microsoft.com/library/windows/apps/xaml/hh965329.aspx.
- The *CommandBar* control can contain only a limited set of controls (controls that implement the *ICommandBarElement* interface). This set includes the AppBarButton, AppBarToggleButton, and AppBarSeparator controls. These controls are specifically designed to operate within a *CommandBar*. If you attempt to add a control such as a button to a command bar, you will receive the error message “The specified value cannot be assigned to the collection.”
- The UWP app templates include a variety of stock icons (such as for Previous and Next, shown in the sample code above), that you can display on an *AppBarButton* control. You can browse the full set of available stock icons by using the Properties window. In the Icon section, click Symbol Icon. The available stock icons appear in the list box that is displayed. You can also define your own icons and bitmaps.
- Each button has a *Command* property, which is the property that you can bind to an object that implements the *ICommand* interface. In this application, you have bound the buttons to the *PreviousCustomer* and *NextCustomer* commands in the *ViewModel* class. When the user clicks either of these buttons at run time, the corresponding command will run.

3. On the Debug menu, click Start Debugging.

The Customers form should appear and display the details for John Sharp. The command bar should be displayed at the top of the form and contain the Next and Previous buttons, as shown in the following image:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_793_0.png)

Notice that the Previous button is not available. This is because the IsAtStart property of the ViewModel is true, and the CanExecute method of the Command object referenced by the Previous button indicates that the command cannot run.

+   4. Click the ellipsis button on the command bar. The labels for the buttons should appear. These labels will be displayed until you click one of the buttons on the command bar.

+   5. On the command bar, click Next.

The details for customer 2, Diana Sharp, should appear, and after a short delay (of up to one second), the Previous button should become available. The IsAtStart property is no longer true, so the CanExecute method of the command returns true. However, the button is not notified of this change in state until the timer object in the command expires and triggers the

CanExecuteChanged event, which might take up to a second to occur.

## Note

If you require a more instantaneous reaction to the change in state of commands, you can arrange for the timer in the Command class to expire more frequently. However, avoid reducing the time by too much because raising the CanExecuteChanged event too frequently can impact the performance of the UI.

+   6. On the command bar, click Next again.

+   7. The details for customer 3, Francesca Sharp, should appear, and after a short delay of up to one second, the Next button should no longer be available. This time, the IsAtEnd property of the ViewModel is true, so the CanExecute method of the Command object for the Next button returns false and the command is disabled.

+   8. Resize the window to display the app in the narrow view and verify that the app continues to function correctly. The Next and Previous buttons should step forward and backward through the list of customers.

+   9. Return to Visual Studio and stop debugging.

## Searching for data using Cortana

A key feature of Windows 10 apps is the ability to integrate with the voice-activated digital assistant, also known as Cortana. Using Cortana, you can activate applications and pass them commands. A common requirement is to use Cortana to initiate a search request and have an application respond with the results of that request. The app can send the results back to Cortana for display (known as background activation), or the app itself can display the results (known as foreground activation). In this section, you will extend the Customers app to enable a user to search for specific customers by name. You can expand this example to cover other attributes or possibly combine search elements into more complex queries.

## Note

The exercises in this section assume that you have enabled Cortana. To do this, click the Search button on the Windows taskbar. In the toolbar on the left side of the window, click Settings (the cog icon). In the Settings menu, slide the Cortana switch from Off to On.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_795_0.png)

Cortana also requires that you have signed in to your computer by using a Microsoft account, and will prompt you to connect if necessary. This step is required because speech recognition is handled by an external service running in the cloud rather than on your local device.

Adding voice activation to an app is a three-stage process:

+   1. Create a voice-command definition (VCD) file that describes the commands to which your app can respond. This is an XML file that you deploy as part of your application.

+   2. Register the voice commands with Cortana. You typically do this when the app starts running. You must run the app at least once before Cortana will recognize it. Thereafter, if Cortana associates a particular command with your app, it will launch your app automatically. To avoid cluttering up its vocabulary, Cortana will “forget” commands associated with an app if the app is not activated for a couple of weeks, and the commands have to be registered again to be recognized. Therefore, it is common practice to register voice commands every time the app starts running—to reset the “forget” counter and give the app another couple of weeks of grace.

+   3. Handle voice activation in your app. Your app is passed information from Cortana about the command that causes the app to be activated. It is the responsibility of your code to parse this command, extract any arguments, and perform the appropriate operations. This is the most complicated part of implementing voice integration.

The following exercises walk through this process using the Customers app.

## Create the voice-command definition (VCD) file for the Customers app

+   1. In Visual Studio, open the Customers project in the \Microsoft Press\VCSBS\Chapter 26\Cortana folder in your Documents folder.

This version of the Customers app has the same ViewModel that you created in the previous exercise, but the data source contains details for many more customers. The customer information is still held in a List<Customer> object, but this object is now created by the DataSource class in the DataSource.cs file. The ViewModel class references this list instead of creating the small collection of three customers used in the previous exercise.

+   2. In Solution Explorer, right-click the Customers project, point to Add, and then click New Item.

+   3. In the Add New Item – Customers dialog box, in the left pane, click Visual C#. In the middle pane, scroll down and select the XML File template. In the Name box, type CustomerVoiceCommands.xml, and then click Add, as shown in the following image:
