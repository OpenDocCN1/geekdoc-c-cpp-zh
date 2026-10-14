```
protected override async void OnNavigatedTo(NavigationEventArgs e)
{
    NavigationArgs args = e.Parameter as NavigationArgs;
    if (args != null)
    {
        string customerName = args.customerName;
        ViewModel viewModel = new ViewModel(customerName);
        this.DataContext = viewModel;
        if (args.commandMode == "voice")
        {
            if (viewModel.Current != null)
            {
                await Say($"Here are the details for {customerName}");
            }
            else
            {
                await Say($"{customerName} was not found");
            }
        }
    }
}
```