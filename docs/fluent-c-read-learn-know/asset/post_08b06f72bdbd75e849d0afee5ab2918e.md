
## HOW'D YOU DO?

Here's the full definition of the ListBox:

```
<ListBox ... ItemsSource="{Binding}" >
<ListBox.ItemTemplate>
<DataTemplate>
<Label x:Name="itemLabel" Content="{Binding Path=Name}" />
<DataTemplate.Triggers>
<DataTrigger Binding="{Binding Path=Available}" Value="0">
<Setter Property="Foreground" Value="Red" TargetName="itemLabel" />
</DataTrigger>
</DataTemplate.Triggers>
</DataTemplate>
</ListBox.ItemTemplate>
</ListBox>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_826_0.png)

## TAKE A BREAK

One of the things I really like about WPF is that once you know how one part of it works, you know a lot about how other parts of it work. That's certainly true of templates. Each type has little idiosyncrasies, but they have more in common than not.

So now that we have our ListBox working properly, why don't you take a break before we explore some of the other functionality WPF provides when you're working with collections?

## WORKING WITH COLLECTIONS

The list of ingredients isn't all that useful by itself. What we really want the window to do is display the details of whichever item is selected in the ListBox. It's a UI pattern called MASTER-DETAIL, and it's wonderfully easy to do in WPF. Just set the magic IsSynchronizedWithCurrentItem property to true. (IsSynchronizedWithCurrentItem is defined by Selector and inherited by all the items controls that support selection, including ListBox.) Any other elements bound to the same collection will automatically display values from the selected item.

The IsSynchronizedWithCurrentItem property keeps all the elements bound to the ItemsSource (including other items controls) synchronized. It defaults to false, so you'll need to set it if you want this behavior (which you almost always do).

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_827_0.png)

### PUT ON YOUR THINKING HAT

Set the IsSynchronizedWithCurrentItem property of the ListBox and bind the remaining control in the StackPanel.

## HOW'D YOU DO?

Here's the whole window definition (or at least my version of it):

```
<Window ...>
<Grid TextBlock.FontSize="14">
<Grid.ColumnDefinitions ... >
<ListBox ... ItemsSource="{Binding}" IsSynchronizedWithCurrentItem="True" >
<ListBox.ItemTemplate>
<DataTemplate>
<Label x:Name="itemLabel" Content="{Binding Path=Name}" />
<DataTemplate.Triggers>
<DataTrigger Binding="{Binding Path=Available}" Value="0">
<Setter Property="Foreground" Value="Red" TargetName="itemLabel" />
</DataTrigger>
</DataTemplate.Triggers>
</DataTemplate>
</ListBox.ItemTemplate>
</ListBox>
<StackPanel Grid.Column="1">
<Label>Name:</Label>
<Label FontStyle="Italic" Content="{Binding Path=Name}" />
<Label>Description:</Label>
<ScrollViewer Height="100" FontStyle="Italic">
<Content>{Binding Path=Description}</Content>
</ScrollViewer>
<Label>On Hand:</Label>
<Label FontStyle="Italic" Content="{Binding Path=OnHand}" />
<Label>Allocated:</Label>
<Label FontStyle="Italic" Content="{Binding Path=Allocated}" />
<Label>Available:</Label>
<Label FontStyle="Italic" Content="{Binding Path=Available}" />
</StackPanel>
</Grid>
</Window>
```

## THE MAGIC OF VIEWS

The first time you see master-detail binding in action, it seems like magic. Well, it seems like magic if you've spent much time working with older, clunkier binding systems. If you look at the basic binding structural diagram, you'll see that there's an object that sits between the collection and the Binding called a CollectionView. It's this class, which WPF creates for you, that provides the master-detail magic by providing Currency.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_829_0.png)

A default CollectionView is created whenever the binding source is a set of data.

## WORDS FOR THE WISE

> CURRENCY simply means that there's a pointer to one item in the collection. That item is considered the current item. Not a difficult concept, but don't confuse it with CONCURRENCY, which is multiple processes operating at the same time.

| CurrentItem |
|---|
| Item |
| Item |
| Item |
| Item |
| Item |
| Item |

## NAVIGATING THE VIEW

If the CollectionView provides a current item, it stands to reason that it has to provide some way to change the item it points to, right? And, of course, it does, by way of a set of methods that begin with MoveCurrentTo...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_830_0.png)

> I LIED.
> 
> Of course, before you can call a method on the CollectionView, you have to have a reference to the CollectionView. But before we see the method that will give you that reference, I have a confession to make.
> 
> I lied when I said that WPF creates a default CollectionView. (Only just this one time. I haven't done it before, I promise.) It's a little more complicated than that. What actually happens is that WPF creates an instance of a CollectionView or one of the classes that descends from CollectionView (BindingListCollectionView, ListCollectionView, or ItemCollection, depending on what kind of collection you're working with). Each of these classes provides special functionality for working with a specific type of data, and when you're doing advanced binding, you'll need to figure out what class you're working with and what it can do for you.
> 
> There's another class, the CollectionViewSource, that acts as a proxy for all the CollectionView classes in XAML. We'll see how that works when we look at filtering and sorting in a few pages.
> 
> So, now that I've confessed, how do you get a reference to the CollectionView that WPF created for you? By calling the static GetDefaultView() method of CollectionViewSource and passing it the collection:
> 
> `(CollectionView) CollectionViewSource.GetDefaultView(<collection>);`
> 
> GetDefaultView() actually returns an instance of the ICollectionView interface, so you'll have to cast it.

### PUT ON YOUR THINKING HAT

You wouldn't ordinarily add separate navigation controls to an application that uses the Master-Detail interface pattern (because the items control performs the same function), but just to get some experience with navigating a CollectionView, add a Toolbar element to the bottom of the detail pane.

HINT: You'll find it easier if you declare a private variable to contain the reference to the view and set it in the window constructor.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_831_0.png)

The event handlers for these buttons call the appropriate MoveCurrentTo...() methods.

Before you decide you're finished with this exercise, try this Run it, click the Last button, and then click the Next button. What happen? How can you fix it? (HINT: The CollectionView exposes two useful properties for this situation: CurrentPosition and Count.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_831_1.png)

### ON YOUR OWN

If you find this exercise really easy (or you're just in the mood for a challenge), try adding a TextBox between the Previous and Next buttons that lets you type a position number. (Make sure you check the number entered against the Count property before you try to move!)

## HOW'D YOU DO?

Here's my version.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_832_0.png)

```
public partial class MainWindow : Window
{
    private CollectionView view;
    public MainWindow()
    {
        InitializeComponent();
        SampleIngredients Ingredients = new SampleIngredients();
        this.DataContext = Ingredients;
        view = (CollectionView) CollectionViewSource.
        GetDefaultView(Ingredients);
    }

    private void First_Click(object sender, RoutedEventArgs e)
    {
        view.MoveCurrentToFirst();
    }

    private void Previous_Click(object sender, RoutedEventArgs e)
    {
        if (view.CurrentPosition > 0)
        view.MoveCurrentToPrevious();
    }

    private void Next_Click(object sender, RoutedEventArgs e)
    {
        if (view.CurrentPosition < view.Count)
        view.MoveCurrentToNext();
    }

    private void Last_Click(object sender, RoutedEventArgs e)
    {
        view.MoveCurrentToLast();
    }
}
```

Declaring a value to hold the CollectionView reference saves a bit of code.

Did you remember the cast? The compiler would have caught the omission.

This is how you make sure you don't move past the end or the beginning of the collection.
