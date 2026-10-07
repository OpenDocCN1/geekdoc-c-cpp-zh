
# 464 | APPENDIX D USER INTERACTION CONTROLS

## TABLE D-5: Key Events for ComboBox

| EVENT | PURPOSE |
| - | - |
| DropDownClosed | Occurs when the control closes its dropdown list. |
| DropDownOpened | Occurs when the control opens its dropdown list. |
| SelectionChanged | Occurs when the user makes a new selection. |

The ComboBoxItem objects also provide some useful events (see Table D-6).

## TABLE D-6: Key Events for ComboBoxItem Objects

| EVENT | PURPOSE |
| - | - |
| Selected | Occurs when the item is selected. |
| Unselected | Occurs when the item is unselected. |

## EXAMPLE Using ComboBox

The following XAML code builds a ComboBox that lists the names of the solar system's planets. (with parentheses around Pluto it's technically no longer considered a planet.)

```
<ComboBox Selected="2">
  <ComboBoxItem Content="Mercury" />
  <ComboBoxItem Content="Venus" />
  <ComboBoxItem Content="Earth" />
  <ComboBoxItem Content="Mars" />
  <ComboBoxItem Content="Jupiter" />
  <ComboBoxItem Content="Saturn" />
  <ComboBoxItem Content="Uranus" />
  <ComboBoxItem Content="Neptune" />
  <ComboBoxItem Content="(Pluto)" />
</ComboBox>
```

## CONTEXTMENU

The ContextMenu displays a pop-up menu associated with another control (see Table D-7). The ContextMenu should contain MenuItems that act like other MenuItems do.

## TABLE D-7: Key Properties of ContextMenu

| PROPERTY | PURPOSE |
| - | - |
| IsOpen | Determines whether the ContextMenu is displayed. You can use this property to display the menu programmatically. |

Normally you can simply react to events raised by the MenuItems inside the ContextMenu, you can also respond to the following events (see Table D-8).

## TABLE D-8: Key Events for ContextMenu

| EVENT | PURPOSE |
|---|---|
| Closed | Occurs when the ContextMenu closes. |
| Opened | Occurs when the ContextMenu opens. |

## EXAMPLE Using ContextMenu

The following code builds two Rectangles that have ContextMenu:

```
<StackPanel>
  <StackPanel.Resources>
    <ContextMenu x:Key="ctxColor">
      <MenuItem Header="Red"/>
      <MenuItem Header="Green"/>
      <MenuItem Header="Blue"/>
    </ContextMenu>
  </StackPanel.Resources>

  <Rectangle Width="20" Height="20" Fill="Red"
    ContextMenu="{StaticResource ctxColor}"/>

  <Rectangle Width="20" Height="20" Fill="Orange">
    <Rectangle.ContextMenu>
      <MenuItem Header="Orange"/>
      <MenuItem Header="Yellow"/>
      <MenuItem Header="Purple"/>
    </ContextMenu>
  </Rectangle>
</StackPanel>
```

The code defines a ContextMenu resource named ctxColors that displays items Red, Green, and Blue. It creates a new Rectangle, setting the Rectangle's ContextMenu property to the resource.

Next the code creates an orange Rectangle. It gives the new Rectangle a ContextMenu attribute that has menu items Orange, Yellow, and Purple.

## FRAME

The Frame displays Web or XAML content and provides navigation buttons (see Tables D-9 through D-1).

## TABLE D-9:

| PROPERTY | PURPOSE |
| - | - |
| CanGoBack | Indicates whether the control can move backward in its navigation history. |
| CanGoForward | Indicates whether the control can move forward in its navigation history. |
| Source | The location of the web page or XAML file that the Frame should display |

## TABLE D-10:

| PROPERTY | PURPOSE |
| - | - |
| GoBack | Moves to the previous entry in the navigation history if one exists. |
| GoForward | Moves to the next entry in the navigation history if one exists. |
| Navigate | Moves to a new Source. |
| Refresh | Reloads the current Source. |

## TABLE D-11:

| EVENT | PURPOSE |
| - | - |
| Contented | Occurs after the Frame finishes displaying its content |
| LoadCompleted | Occurs after a Source has loaded and rendering is beginning. |
| Loaded | Occurs after a Source has loaded and rendered, and the control is ready to interact with the user. |
| Navigated | Occurs when content has been found and is available through the Content property but may not yet displayed. |
| Navigating | Occurs when the control is starting a new navigation. |
| NavigationFailed | Occurs when a navigation fails. |
| NavigationProgress | Occurs during navigation to give progress. |
| NavigationStopped | Occurs when navigation stops because of a call to the Frame’s Loading method or because a new navigation began. |

## EXAMPLE Using Frame

The following simple XAML example creates a Frame that loads www.frame.com:

```xml
<Frame Source="http://www.frame.com"/>
```

## EXAMPLE Using Frame Bound to ComboBox

The more interesting XAML code creates a Grid that contains a ComboBox and a Frame. The Frame's Source property is bound to the ComboBox's SelectedItem value when you pick a new entry from the ComboBox, the Frame displays the corresponding web page.

```
<Grid>
  <RowDefinition Height="3"/>
  <RowDefinition Height="*"/>
  <Grid.Definitions>
    <ComboBox Row="0" SelectedIndex="0" Name="sites" Margin="5"/>
    <ComboBox Content="Beginning Solutions" Tag="http://vb-helper.com/design.html"/>
    <ComboBox Content="VB Helper" Tag="http://www.vb-helper.com/"/>
    <ComboBox Content="VB Bookstore" Tag="http://store.amazon.com/helper/about/"/>
    <ComboBox Content="Books To Keep" Tag="http://www.BooksToKeep.com/"/>
    <ComboBox Content="Astronomy Picture of the Day" Tag="http://archive.nasa.gov/apod/"/>
  </ComboBox>
</Grid>
<Frame Name="fraGo" Row="1" HorizontalAlignment="Stretch"
      VerticalAlignment="Stretch" Margin="5"
      Source="{Binding ElementName=sites, Path=SelectedItem.Tag}">
</Frame>
</Grid>
```

The following C# code makes the Frame named fraGo navigate to the URL http://amazon.com/helper/about:
```csharp
fraGo.Navigate(new Uri("http://amazon.com/helper/about"));

## GRIDSPLITTER

The GridSplit lets users resize two adjacent rows or columns in a Grid control (see Table D-12). To use a vertical GridSplit, add a cell to the Grid's first row and set its Grid.RowSpan property so it spans all of the Grid's rows. Next, set its HorizontalAlignment property to Left or Right. That makes the GridSplit stick to the side of its alignment and determines which column it will add. Finally, set the control's Width to something big enough for the user to grab and drag, perhaps 3 or 5.

To make a horizontal GridSplit, switch the roles of the Grid's rows and columns, use the GridSplitter's VerticalAlignment property, and set its Height to a reasonable value.

## TABLE D-12:

| PROPERTY | PURPOSE |
| --- | --- |
| Grid.Column | Sets the Grid cell where the splitter starts. For horizontal splitters, set this to 0. |
| Grid.ColumnSpan | For a horizontal splitter, set this so the control spans all columns. |
| Grid.Row | Sets the Grid cell where the splitter starts. For vertical splitters, set this to 0. |
| Grid.RowSpan | For a vertical splitter, set this so the control spans all rows. |
| HorizontalAlignment | For a vertical splitter, determines which side of its column the splitter sticks to and adjusts. |
| ShowsPreview | Determines whether the control resizes the Grid's rows or columns when you drag it, or only shows a preview by displaying a gray version of the GridSplit moving. If ShowsPreview is False, the control resizes the rows or columns. If ShowsPreview is True, the control displays the gray splitter and resizes the rows or columns when you release the mouse. (A preview is more efficient if the contents of the rows or columns take a long time to redraw) |
| VerticalAlignment | For a horizontal splitter, determines which side of its column the splitter sticks to and adjusts. |

Usually the Grid and its controls can rearrange themselves when the user drags the GridSplitter, but the following events let you take action during the drag if you must (see Table D13).

## TABLE D-13:

| EVENT | PURPOSE |
| --- | --- |
| DragCompleted | Occurs when the user has finished dragging the control. |
| DragDelta | Occurs when the user has moved the splitter during a drag. |
| DragStarted | Occurs when the user has started dragging the control. |

## EXAMPLE Using GridSplitter

The following code creates a Grid with three rows and columns. It places GridSplitters inside the middle Grid cell. The first splitter has HorizontalAlignment set to Left so it lets the user adjust the left and middle columns. The second splitter has HorizontalAlignment set to Right so it lets the user adjust the middle and right columns.

```
<Grid>
  <Grid.ColumnDefinitions>
```
