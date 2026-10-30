# Method 1: Adding a Form to the Frame using the Osp::Ui::Controls::Form class

This simple recipe creates a new Form object using the system’s Osp::Ui::Controls::Form class and adds it to the application’s Frame.

The Form should be created and added to the application’s Frame during the application initialisation phase (OnAppInitializing()):

+   1. Create an instance of a Form and initialise it with the style parameters required to display a normal Form containing a title bar and an indicator bar.
+   2. Set the name of the Form and the text to be displayed in the Form’s Title area.
+   3. Add the Form to the application Frame.
+   4. Set the Form as the current form of the Frame.
+   5. Draw and Show the Form.

The following code snippet is an example of code that would be added to the Application’s OnAppInitializing() method:

```
// Create a Form
Form* pForm = new Form();
pForm->Construct(
    FORM_STYLE_NORMAL|FORM_STYLE_TITLE|FORM_STYLE_INDICATOR);
pForm->SetName(L"MainForm");
pForm->SetTitleText(L"MainForm");

// Get a frame pointer and add the Form to the Frame
Frame* pFrame = GetAppFrame()->GetFrame();
pFrame->AddControl(*pForm);
// Set the current Form
pFrame->SetCurrentForm(*pForm);
// Call Draw & Show to display Form
pForm->Draw();
pForm->Show();
```

# Method 2: Adding a Form to the Frame Using a User-defined Form Class

This recipe creates the same results as Method 1, but does it using a newly created Form class. This method may be more suitable for applications that contain multiple forms, as the creation of the Form’s controls and its logic is implemented by the Form rather than in the application code.