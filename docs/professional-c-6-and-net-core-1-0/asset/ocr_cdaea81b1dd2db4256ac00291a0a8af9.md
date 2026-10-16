```
Content = $"You entered {sampleDataText.Text}",
    PrimaryButtonText ="Ok"
};
await dialog.ShowAsync();
}
```

And the OnError method throws an unhandled exception:

```
private void OnError(object sender, RoutedEventArgs e)
{
    throw new Exception("something bad happened");
}
```

> **NOTE** You can read more information about creating apps using the Universal Windows Platform starting with Chapter 29, “Core XAML,” and especially in Chapter 32, “Windows Apps: User Interfaces,” and Chapter 33, “Advanced Windows Apps.”

# Creating an Application Insights Resource

For using Application Insights, you need to create an Application Insights resource to your Microsoft Azure account. In the Microsoft Azure portal (http://portal.azure.com), you can find this resource with the Developer Services. When you create this resource, you need to specify the name, application type, resource group, subscription, and location of the service (see Figure 20.5).

![](bbox=[0.105, 0.5, 0.895, 0.885])

Figure 20.5