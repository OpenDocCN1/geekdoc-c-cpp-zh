```
<Grid>
    <TextBlock Text ="The ListBox control allows you to display a list of items" TextWrapping="wrap"></TextBlock>
</Grid>
</DataTemplate>
</Button.ContentTemplate>
</Button>
</Popup.Child>
</Popup>
<TextBlock Text="Calendar" Margin="50,225,0,0"/>
<my:Calendar DisplayMode="Year" IsTodayHighlighted="True" SelectionMode="SingleDate" Margin="0,200,150,0" Foreground="Red" MouseEnter="showCalendarPopup" MouseLeave="hideCalendarPopup"/>
<Popup x:Name="popup3" HorizontalOffset="400" VerticalOffset="225">
    <Popup.Child>
        <Button Background="Green" VerticalAlignment="Top" MaxWidth="200" FontWeight="Bold" Foreground="DarkBlue" IsEnabled="False">
            <Button.ContentTemplate>
                <DataTemplate>
                    <Grid>
                        <TextBlock Text ="The Calendar control provides you the facility to select a particular date from the visible month or year. You can switch between months, years, or decades by using scroll arrows." TextWrapping="wrap"></TextBlock>
                    </Grid>
                </DataTemplate>
            </Button.ContentTemplate>
        </Button>
    </Popup.Child>
</Popup>
</Grid>
</UserControl>
```

In Listing 17.11, three Popup controls named popup1, popup2, and popup3 are added to the page. Each of the Popup controls has a button as their children. The button provides the bounded area where the help information is displayed. Note that the Popup controls appear when the mouse-pointer is placed inside the text box, list box or calendar and the Popup controls disappear when the mouse-pointer is taken out of the text box, list box, or calendar.

+   2. Open the code-behind file and type the code, as shown in Listing 17.12:

# Listing 17.12: Showing the Code for the Code-Behind File of the MainPage.xaml File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
namespace PopUpHelpAppCS
{
    public partial class MainPage : UserControl
    {
        public MainPage()
```