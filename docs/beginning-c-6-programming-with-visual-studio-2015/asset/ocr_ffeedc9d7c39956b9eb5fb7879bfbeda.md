```
<ProgressBar.RenderTransform>
<TransformGroup>
<ScaleTransform/>
<SkewTransform/>
<RotateTransform Angle="-36.973"/>
<TranslateTransform/>
</TransformGroup>
</ProgressBar.RenderTransform>
</ProgressBar>
</Grid>
</Window>
```

# CHAPTER 15 SOLUTIONS

# Exercise 1

Solution:

+   1. Create a new class with the name ComputerSkillValueConverter like this:

```
using Ch13CardLib;
using System;
using System.Windows.Data;

namespace KarliCards_Gui
{
    [ValueConversion(typeof(ComputerSkillLevel), typeof(bool))]
    public class ComputerSkillValueConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, System.Globalization.CultureInfo culture)
        {
            string helper = parameter as string;
            if (string.IsNullOrWhiteSpace(helper))
                return false;

            ComputerSkillLevel skillLevel = (ComputerSkillLevel)value;
            return (skillLevel.ToString() == helper);
        }

        public object ConvertBack(object value, Type targetType, object parameter, System.Globalization.CultureInfo culture)
        {
            string parameterString = parameter as string;
            if (parameterString == null)
                return ComputerSkillLevel.Dumb;

            return Enum.Parse(targetType, parameterString);
        }
    }
}
```