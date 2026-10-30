```
pButton->Construct(Rectangle(10, 100, 460, 60));

// Set button text
pButton->SetText(L"Ok");

// Set button Action identifier
pButton->SetActionId(ID_BUTTON_OK);

// Register an event listener
pButton->AddActionEventListener(*this);

// Add the button control to the Main Form
AddControl(*pButton);
```

# Example 2: Creating a Button Containing an Image

In this example a Button control with an image is created on the Form (see Figure R2.5).

The Button control should be added to the Form during initialisation of the MainForm (OnInitializing()):

![](bbox=[0.35, 0.6, 0.7, 0.88])

Figure R2.5 Form with image.