A member variable pointer of type Web is added to the MainForm class to hold a reference to the created Web control:

```
Osp::Web::Controls::Web* pWeb;
```

The Web control can be created during initialisation of the MainForm (OnInitializing()):

+   1. Set the orientation of the MainForm to landscape.
+   2. Create the Web control.
+   3. Initialise the Web control with the size and position of the available screen area.
+   4. Add the Web control to the MainForm.
+   5. Load the specified URL into the Web control.

The following code snippet is an example of code that would be added to the MainForm's OnInitializing() method, in order to create a Web control:

```
// Set the orientation of the Form to landscape
SetOrientation(ORIENTATION_LANDSCAPE);

// Create Web control object
pWeb = new Web();

// Initialise the Web control
pWeb->Construct(Rectangle(0, 0, GetClientAreaBounds().width, GetClientAreaBounds().height));

// Add the Web control to the Form
AddControl(*pWeb);

// Load the specified URL in the Web control
pWeb->LoadUrl(L"http://developer.bada.com");
```

# Example 2: Downloading a File

This example creates a Web control using the Osp::Web::Controls::Web class and uses it to download a file from the Web. The file is saved to the application's /Home directory and can be used as required by the application.

To download a file from a remote server the Osp::Web::Controls::Web control is used to embed a browser within the application. The Osp::Web::Controls::ILoadingListener interface class is implemented to listen to events occurring during an loading operation and inform the web control that the application wants to handle the data by itself. The Osp::Web::Controls::IWebDownloadListener interface class is used to download data to the application.