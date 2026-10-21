

```
public;
    // Disables controls for selecting upper limits
    void SetLowerEnabled(void)
    {
        upperValuesLimits->Enabled = false;
        upperStarsLimits->Enabled = false;
        lowerValuesLimits->Enabled = true;
        lowerStarsLimits->Enabled = true;
    }
```

```
// Disables controls for selecting lower limits
void SetUpperEnabled(void)
{
    upperValuesLimits->Enabled = true;
    upperStarsLimits->Enabled = true;
    lowerValuesLimits->Enabled = false;
    lowerStarsLimits->Enabled = false;
}
```

Enabled 属性的值决定控件是否启用。true 值启用控件，而 false 值禁用它，使用户无法与其交互。SetLowerEnabled() 函数禁用用于输入上限的控件并启用用于输入下限的控件。SetUpperEnabled() 函数执行相反操作。

## 更新 Limits 菜单项处理程序

完成对 Euromillions 彩票输入限制的支持的最后一步是更新 Form1 类中 Limits 菜单项的 Click 事件处理程序。Upper 菜单项的处理程序应修改如下：

```
System::Void upperMenuItem_Click(System::Object^ sender, System::EventArgs^ e)
{
    ::DialogResult result;
    if(lottoTab->Visible)
    {
        lottoLimitsDialog->SetUpperEnabled();
        result = lottoLimitsDialog->ShowDialog(this);
        if(result == ::DialogResult::OK)
        {
            lottoUserMaximum = lottoLimitsDialog->UpperLimit;
            lottoUserMinimum = lottoLimitsDialog->LowerLimit;
        }
    }
    else if(euroTab->Visible)
    {
        euroLimitsDialog->SetUpperEnabled();
        result = euroLimitsDialog->ShowDialog(this);
        if(result == ::DialogResult::OK)
        {
            euroUserMaximum = euroLimitsDialog->UpperValuesLimit;
            euroUserMinimum = euroLimitsDialog->LowerValuesLimit;
            euroStarsUserMaximum = euroLimitsDialog->UpperStarsLimit;
```
```
euroStarsUserMinimum = euroLimitsDialog->LowerStarsLimit;
}
}
```

局部变量 result 在两个 if 语句中都使用，因此现在在函数开头声明。调用对话框对象的 SetUpperEnabled() 函数适当启用对话框中的控件后，您以模态方式显示对话框。如果用户通过单击 OK 按钮关闭对话框，您将通过对话框对象的属性可用的结果存储起来。

Lower 菜单项的 Click 事件处理程序的更改非常相似：

```
System::Void lowerMenuItem_Click(System::Object^ sender, System::EventArgs^ e)
{
::DialogResult result;
if(lottoTab->Visible)
{
lottoLimitsDialog->SetLowerEnabled();
result = lottoLimitsDialog->ShowDialog(this);
if(result == ::DialogResult::OK)
{
lottoUserMaximum = lottoLimitsDialog->UpperLimit;
lottoUserMinimum = lottoLimitsDialog->LowerLimit;
}
}
else if(euroTab->Visible)
{
euroLimitsDialog->SetLowerEnabled();
result = euroLimitsDialog->ShowDialog(this);
if(result == ::DialogResult::OK)
{
euroUserMaximum = euroLimitsDialog->UpperValuesLimit;
euroUserMinimum = euroLimitsDialog->LowerValuesLimit;
euroStarsUserMaximum = euroLimitsDialog->UpperStarsLimit;
euroStarsUserMinimum = euroLimitsDialog->LowerStarsLimit;
}
}
```

这里的逻辑与之前的处理程序函数相同。

## 实现 Help | About 菜单项

现在您了解了 MessageBox 类，这很容易。您只需在单击 Help > About 菜单项时显示一个消息框即可：

```
System::Void aboutToolStripMenuItem_Click(System::Object^ sender, System::EventArgs^ e)
{
MessageBox::Show(L"(c) Copyright Ivor Horton", L"About A Winning Application", MessageBoxButtons::OK, MessageBoxIcon::Exclamation);
}
```

## 第 21 章

当菜单项被单击时，处理程序函数会显示图 21-28 所示的消息框。

![](img/2359b0c604600c58fba3539c738a356e_1117_0.png)

图 21-28

## 处理按钮单击

单击按钮应将按钮上的值更改为新的随机值。当然，该值必须与其它按钮上的值不同，也必须与被单击按钮的值不同。最好将整个集合按排序顺序呈现；这可能会导致新值出现在不同的按钮上，但这很可能比值不按顺序更好。

处理按钮单击的过程对所有按钮都相同，因此您可以通过创建通用函数来完成工作，从而节省代码。您可以定义 Form1 类的私有函数成员，该函数为按钮数组中的给定 Button 对象生成新值：

```
// Generates a new value for button different from current button values
void SetNewValue(Button^ button, array<Button^>^ buttons,
                    int lowerLimit, int upperLimit)
{
    int index = 0;                          // Index of button in buttons

    // Array to store button values
    array<int>^ values = gcnew array<int>(buttons->Length);

    // Get values from buttons and find index for button
    for(int i = 0 ; i < values->Length ; i++)
    {
        values[i] = Int32::Parse(buttons[i]->Text);  // Get current button value

        // If current handle is same as button, save the index value
```
```
if(button == buttons[i])
    index = i;
}

int newValue = 0;                    // Store the new button value
// Check if it is different from the other button values
for(;;)                              // Loop until we get a good one
{
    newValue = random->Next(lowerLimit, upperLimit);  // Generate a value
    if(IsValid(newValue, values, values->Length))      // If it's OK...
        break;                                          // ...end the loop
    }
    values[index] = newValue;           // Store the new value at index

Array::Sort(values);                // Sort the value
for(int i = 0 ; i < values->Length ; i++)   // and set the values
    buttons[i]->Text = values[i].ToString();    // as text on the buttons
}
```

前两个函数参数是要赋新数字的按钮以及第一个按钮所属组的按钮数组。接下来的两个参数指定值的下限和上限。values 数组中存储按钮数组中按钮的当前值，第一个循环也找到按钮数组中 Button^ 句柄的索引值，该句柄是第一个参数。您需要此信息来知道 values 数组的哪个元素应被新值替换。

新值是在无限 for 循环中创建的。这是您在最初为按钮创建值时使用的相同机制。获得有效的新的值后，您将其存储在 values 数组中。然后您对 values 数组中的元素进行排序，然后将它们存储为按钮数组中按钮的 Text 属性的值。您将能够使用此函数处理所有按钮的 Click 事件。

如果尚未这样做，请双击 Lotto 选项卡上的第一个按钮以生成其 Click 事件处理程序函数。您可以通过打开按钮的 Properties 选项卡，选择 Events 按钮并更改 Click 事件的值来编辑处理程序函数的名称。按 Enter 后，代码会使用新名称进行更新。我将值更改为 lottoValue_Click。

您可以修改 Click 事件处理程序以调用刚刚添加到 Form1 类的 SetNewValue() 函数：

```
System::Void lottoValue_Click(System::Object^ sender, System::EventArgs^ e)
{
    Button^ button = safe_cast<Button^>(sender);

    // Create the array of button handles
    array<Button^>^ buttons = {lottoValue1, lottoValue2, lottoValue3,
                              lottoValue4, lottoValue5, lottoValue6};

    // Replace the value on button
    SetNewValue(button, buttons, lottoUserMinimum, lottoUserMaximum);
}
```

