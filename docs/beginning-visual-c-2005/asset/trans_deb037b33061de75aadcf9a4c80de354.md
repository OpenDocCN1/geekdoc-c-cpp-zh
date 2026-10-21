

将 upperValuesLimit 控件的属性值设置为 49；这是控件中初始显示的值。如果还将每个 NumericUpDown 控件的 ReadOnly 属性值设置为 True，则可防止通过键盘输入值。你在这里非常简单地使用了 NumericUpDown 控件。你可以通过设置 Increment 属性值来更改上下增量。Increment 属性的类型为 Decimal，因此你也可以将其设置为非整数值。

![](img/2359b0c604600c58fba3539c738a356e_1110_0.png)

图 21-25

你可以将下组 group box 中 ComboBox 控件的 (Name) 属性值设置为 lowerStarsLimits 和 upperStarsLimits。向 ComboBox 中输入要显示的值非常容易。单击最左侧 ComboBox 控件右上角的小箭头以显示图 21-26 所示的菜单。

![](img/2359b0c604600c58fba3539c738a356e_1110_1.png)

图 21-26

## 第 21 章

选择菜单底部 Edit Items 菜单项以显示图 21-27 所示的 String Collection Editor 对话窗口。

![](img/2359b0c604600c58fba3539c738a356e_1111_0.png)

图 21-27 显示了左侧 ComboBox 控件输入的值。对于右侧的 ComboBox 控件，可以输入从 2 到 9 的值。

ComboBox 对于此应用程序来说并不理想，因为它允许文本输入以及从列表中选择；你希望限制值仅从列表中选择。控件之所以名为 ComboBox，是因为它结合了 ListBox 控件的功能，允许从列表中选择，以及 TextBox 控件的功能，提供文本输入。

### 从对话框控件获取数据

你将以与 Lotto 限制对话框基本相同的方式从控件中获取限制值。你可以先向 EuroLimitsDialog 类添加一些新的数据成员来保存用户限制值：

```
private:
    int lowerValuesLimit;
    int upperValuesLimit;
    int lowerStarsLimit;
    int upperStarsLimit;
```

为了安全起见，最好在类构造函数中初始化这些成员：

```
EuroLimitsDialog(void)
    :lowerValuesLimit(1)
    ,upperValuesLimit(50)
    ,lowerStarsLimit(1)
    ,upperStarsLimit(9)
{
```

```
InitializeComponent();
//
//TODO: Add the constructor code here
//
}
```

你还需要在对话框类中定义一些公共属性，以便从应用程序窗口对象访问限制：

```
public:
    property int LowerValuesLimit
    {
        int get() { return lowerValuesLimit; }

        void set(int limit)
        {
            lowerValuesLimit = limit;
            lowerValuesLimits->Value = limit;        // Set as selected in NumericUpDown
        }
    }
    property int UpperValuesLimit
    {
        int get() { return upperValuesLimit; }

        void set(int limit)
        {
            upperValuesLimit = limit;
            upperValuesLimits->Value = limit;        // Set as selected in NumericUpDown
        }
    }
    property int LowerStarsLimit
    {
        int get() { return lowerStarsLimit; }

        void set(int limit)
        {
            lowerStarsLimit = limit;
            lowerStarsLimits->SelectedItem = limit;  // Set as selected in ComboBox
            lowerStarsLimits->SelectedIndex =        // Set index for selected item
                lowerStarsLimits->FindString(limit.ToString());
        }
    }

    property int UpperStarsLimit
    {
        int get() { return upperStarsLimit; }

        void set(int limit)
        {
            upperStarsLimit = limit;
            upperStarsLimits->SelectedItem = limit;  // Set as selected in ComboBox
            upperStarsLimits->SelectedIndex =        // Set index for selected item
                upperStarsLimits->FindString(limit.ToString());
        }
    }
```

## 第 21 章

每个属性的 get() 函数返回对话框类对应私有成员的值。set() 函数设置数据成员的值，并更新对话框中的控件，以便设置的值成为所选值。SelectedIndex 属性值是所选项目的索引。你使用 ComboBox 控件的 FindString() 函数设置它，该函数返回控件项目集合中首次出现参数的索引值。此位置的值在控件中初始显示。

通过在 Design 窗口中双击按钮，为 EuroLimitsDialog 类中的 OK 按钮添加 Click 事件处理程序。你不需要为 Cancel 按钮实现处理程序。你可以像这样实现 OK 按钮处理程序：

```
System::Void euroOK_Click(System::Object^ sender, System::EventArgs^ e)
{
    ::DialogResult result;

    // get the limits for values
    int valuesLower = Decimal::ToInt32(lowerValuesLimits->Value);
    int valuesUpper = Decimal::ToInt32(upperValuesLimits->Value);
    if(valuesUpper - valuesLower < 4)            // Check for an adequate range
    {
        result = MessageBox::Show(this,            // Range insufficient so
            "Upper values limit: "+valuesUpper +   // display message box
            " Lower values limit: "+ valuesLower+
            "\nUpper values limit must be at least 4 greater that the lower limit."+
            "\nTry Again.",
            "Limits Invalid",
            MessageBoxButtons::OKCancel,
            MessageBoxIcon::Error);

        if(result == ::DialogResult::OK)            // If message box OK clicked
            DialogResult = ::DialogResult::None;    // prevent dialog from closing
        else                                        // Messag box Cancel clicked
            DialogResult = ::DialogResult::Cancel;  // so close the dialog
        return;
    }

    // Get stars limits
    int starsLower = lowerStarsLimits->SelectedItem == nullptr ?
                        lowerStarsLimit :
                        Int32::Parse(lowerStarsLimits->SelectedItem->ToString());

    int starsUpper = upperStarsLimits->SelectedItem == nullptr ?
                        upperStarsLimit :
                        Int32::Parse(upperStarsLimits->SelectedItem->ToString());

    if(starsUpper - starsLower < 1)            // Check for an adequate range
    {
        result = MessageBox::Show(this,            // Range insufficient so
            "Upper stars limit: "+starsUpper +     // so display message box
            " Lower stars limit: "+ starsLower+
            "\nUpper stars limit must be at least 1 greater that the lower limit."+
            "\nTry Again.",
            "Limits Invalid",
```

```
MessageBoxButtons::OKCancel,
MessageBoxIcon::Error);
if(result == ::DialogResult::OK)                // If message box OK clicked
    DialogResult = ::DialogResult::None;          // prevent dialog from closing
else                                           // Message box Cancel clicked
    DialogResult = ::DialogResult::Cancel;       // so close the dialog
}
// Store the new limits
lowerValuesLimit = valuesLower;
upperValuesLimit = valuesUpper;
lowerStarsLimit = starsLower;
upperStarsLimit = starsUpper;
}
```

NumericUpDown 控件的 Value 属性返回类型为 Decimal 的值。要将其转换为 Int32 类型，可以将其作为参数传递给 Decimal 类中的静态 ToInt32() 函数。此函数返回的值会自动取消装箱，以便可以存储在类型为 int 的变量中。

ComboBox 控件的 SelectedItem 属性返回的值类型为 Object^，因此为了安全起见，你需要检查它是否为 null。如果为 null，则将局部变量设置为对话框对象中记录的当前值；如果不为 null，则存储 SelectedItem 属性表示的值。你不能直接存储该值，但调用对象的 ToString() 函数会生成对象的字符串表示形式，然后你可以使用 Int32 类中的静态 Parse() 函数将其转换为 int 类型。

你需要在 Form1 类中添加一个私有成员来存储新对话框的句柄：

```
private:
    EuroLimitsDialog^ euroLimitsDialog;    // Dialog to set Euromillions limits
```

你可以将以下语句添加到 Form1 类构造函数的代码末尾，以创建对话框对象并更新星号限制值的属性：

```
euroLimitsDialog = gcnew EuroLimitsDialog;
euroLimitsDialog->LowerStarsLimit = euroStarsLowerLimit;
euroLimitsDialog->UpperStarsLimit = euroStarsUpperLimit;
```

通过设置对话框对象的 LowerStarsLimit 和 UpperStarsLimit 属性，你可以确保在对话框初始显示时 ComboBox 控件显示这些值。如果未为 ComboBox 控件设置所选项目，则初始时不显示任何内容。

不要忘记在 Form1.h 中添加 EuroLimitsDialog 类定义的 #include 指令：

```
#include "EuroLimitsDialog.h"
```

### 禁用输入控件

当单击 Limits > Upper 菜单项时，你希望防止输入下限，当选择 Limits > Lower 菜单项时，你希望防止输入上限值。你可以向 EuroLimitsDialog 类添加几个成员函数来实现这一点：

