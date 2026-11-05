![](bbox=[0.22, 0.15, 0.88, 0.66])

# FIGURE 15-35 Metric/English Converter final design

As shown on Figure 15-35, two RadioButton objects provide functionality for the app. The GroupName property was set to the same name, Convert, for both controls. This was done to make sure that only one button was checked at a time. The only programming statements added were those included in the RadioButtons Checked event-handler method. One event-handler method was written and both RadioButton objects were wired to that method. These statements for the event-handler method are placed in the code-behind file stored with an .xaml.cs file extension. The program statements in the code-behind file for the MainPage.xaml.cs file are shown in Example 15-17.