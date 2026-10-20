```
92      }
93
94      btnPrev.IsEnabled = true;
95
96      UpdateScreen();
97    }
98
99    private void UpdateScreen()
100    {
101      lblInfo.Text = string.Format("5", currentIndex); {0}
102      string path =
string.Format("ResourceImageApp.Images.res0{0}.jpg", currentIndex);
103      resourceImage.Source = ImageSource.FromResource(path);
104    }
105  }
106}
```

Then navigate to the App.cs file and make sure that it looks like this:

```
public App ()
{
    // The root page of your application
    MainPage = new ResourceImagePage ();
}
```

Right-click on the ResourceImageApp (Portable) joint project and choose Add and from the side menu that appears choose New Folder. This will create a new volume within this project, called Images. Then right-click on our new Images folder and select Add. Choose image files: res01.jpg, res02.jpg, res03.jpg, res04.jpg, res05.jpg (click here to download Images.zip). The images in this order contain the words "Welcome to Hassoub Academy". Right-click again on each file name you just added to the project and from the menu select Properties. The file properties will appear, set the Build Action property to Embedded Resource as shown in the following file