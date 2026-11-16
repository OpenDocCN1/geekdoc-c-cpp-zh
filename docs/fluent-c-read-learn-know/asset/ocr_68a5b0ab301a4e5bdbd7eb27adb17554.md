# HOW'D YOU DO?
Here's my version.

![](bbox=[0.09, 0.05, 0.21, 0.21])

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