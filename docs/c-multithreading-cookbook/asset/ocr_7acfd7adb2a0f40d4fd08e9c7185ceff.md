# Threads in the .NET Framework

```
{
```

```
UpdateLabelTextDelegate* textAction = gcnew
UpdateLabelTextDelegate(form, &MyForm::UpdateLabelText);
form->BeginInvoke(textAction, L"Result: = +
Convert::ToString(iResult));
```

```
}
```

```
delegate void UpdateProgressBarDelegate(void);
```

```
{
```

```
System::UpdateProgressBar(void)
```

```
progress->PerformStep();
```

```
}
```

```
delegate void UpdateLabelText(String^ szText);
```

```
System::UpdateLabelText(String* szText)
```

```
{
```

```
label->AutoSize = false;
label->Text = szText;
label->AutoSize = true;
```

```
}
```

```
#pragma region Windows Form Designer generated code
/// <summary>
/// Required method for Designer
/// support - do not modify
/// the contents of this method with the code editor.
/// </summary>
void InitializeComponent(void)
```

```
{
this->components = gcnew System::ComponentModel::Container();
this->Size = System::Drawing::Size(300, 300);
this->Text = L"MyForm"
this->Padding = System::Windows::Forms::Padding(0);
this->AutoScaleMode = System::Windows::Forms::AutoScale::Font;
```

```
}
#pragma endregion
```

```
}
```