![](bbox=[0.176, 0.095, 0.449, 0.654])

Figure 15-24 Using the Properties window to set the SelectedDate property

If you are going to set the date programmatically, use the Page_Load() event-handler method.

The Calendar control is based on the .NET DateTime class, which enables you to work with dates in different formats. Program statements were added to the Page_Load() event handler to set the date to the current day the application is run. This is shown in Example 15-11. Notice that the statements are placed in a try...catch exception block.