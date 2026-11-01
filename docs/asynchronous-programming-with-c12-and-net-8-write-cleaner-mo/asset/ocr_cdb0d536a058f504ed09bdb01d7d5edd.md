```
LoadDataAsync();
}
private async void LoadDataAsync()
{
    try
    {
        // Simulate data retrieval asynchronously
        await Task.Delay(3000); // Represents fetching
data from a remote source

        // Update DataList property (bound to UI) with
retrieved data
        DataList = new ObservableCollection<string> {
            "Item 1", "Item 2", "Item 3" };
    }
    catch (Exception ex)
    {
        // Handle exceptions or show error message
        MessageBox.Show("Error loading data: " +
ex.Message);
    }
}
}
```

In this example, `LoadDataAsync` is called during the window initialization to load data asynchronously. The `DataList` property is updated after data retrieval, and the UI automatically reflects the changes due to data binding.

# 3. Asynchronous Button Click Handling in Windows Forms:

Similarly, in Windows Forms applications, handling button clicks asynchronously can be achieved using async/await to ensure a responsive UI.