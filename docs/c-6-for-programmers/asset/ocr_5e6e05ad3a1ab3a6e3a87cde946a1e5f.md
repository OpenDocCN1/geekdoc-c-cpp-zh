```
```csharp
if (imagesListBox.SelectedItem != null)
{
    string selectedURL =
        ((FlickrResult) imagesListBox.SelectedItem).URL;

    // use HttpClient to get selected image's bytes asynchronously
    byte[] imageBytes =
        await flickrClient.GetByteArrayAsync(selectedURL);

    // display downloaded image in pictureBox
    MemoryStream memoryStream = new MemoryStream(imageBytes);
    pictureBox.Image = Image.FromStream(memoryStream);
}
}
}
```
```

![](bbox=[0.127, 0.366, 0.871, 0.893])

**Fig. 2.4** | Invoking a web service asynchronously with class `HttpClient`. (Part 3 of 3.) [Photos used in this example ©Paul Deitel. All rights reserved.]