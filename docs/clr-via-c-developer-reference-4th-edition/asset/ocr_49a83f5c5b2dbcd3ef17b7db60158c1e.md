The System.Globalization.CultureInfo type is one of the very few types defined in the FCL that implements IFormatProvider interface. If you want to format a string for, say, Vietnam, you'd construct a CultureInfo object and pass it as ToString's Format parameter. The following code obtains a string representation of a Decimal numeric value formatted as currency appropriate for Vietnam.

Decimal price = 123.54M;
String s = price.ToString("C", new CultureInfo("vi-VN"));
MessageBox.Show(s);

![](bbox=[0.118, 0.241, 0.335, 0.429])

FIGURE 14-5 Numeric value formatted correctly to represent Vietnamese currency.

Internally, Decimal's ToString method senses that the formatProvider argument is not null and calls the object's GetFormat method as follows.

NumberInfo nfi = (NumberInfo)
formatProvider.GetFormat(typeof(NumberInfo));

This is how ToString requests the appropriate number-formatting information from the (CultureInfo) object. Number types (such as Decimal) request only number-formatting information. Other types (such as DateTime) call GetFormat like the following.

DateTimeInfo dtfi = (DateTimeInfo)
formatProvider.GetFormat(typeof(DateTimeInfo));

Actually, because Format's parameter can identify any type, the method is flexible enough to allow any type of format information to be requested. The types in the .NET framework call GetFormat, requesting only number or date information; in the future, other kinds of formatting information could be requested.

By the way, if you want to obtain a string for an object that isn't formatted for any culture, you should call System.Globalization.CultureInfo's static InvariantCulture property and pass the object returned as ToString's Format parameter.

Decimal price = 123.54M;
String s = price.ToString("C", CultureInfo.InvariantCulture);
MessageBox.Show(s);