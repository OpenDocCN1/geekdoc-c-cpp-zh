# ### 14.3.4 System.Globalization Namespace

To implement globalization in an application, include System.Globalization namespace in the application. The namespace provides classes that define culture related information such as language, country, calendars and formats.

# **CultureInfo Class**

The class provides information about a specific culture. It includes details as name of the culture, the formatting styles and calendar used.

The list of properties of **CultureInfo** class

| Property | Description |
|---|---|
| CurrentCulture | It returns the instance of the CultureInfo class representing the culture of the current thread |
| CurrentUICulture | It returns the instance of the CultureInfo class representing the culture used by the resource manager for the culture specific resource at runtime |
| Name | It returns the name of the culture in <Language code>-<Country/Region code> format |
| IsNeutralCulture | It returns a Boolean value indicating the culture represented by the CultureInfo object is a neutral culture |
| NumberFormat | It gets or sets the NumberFormatInfo object that defines the correct format for displaying numbers, currency, and percentage |

The list of methods of **CultureInfo** class

| Methods | Description |
|---|---|
| CreateSpecificCulture | It creates a CultureInfo object that represents the specific culture associated with the specific name |
| GetCultureInfo | It returns the read-only instance of the culture |
| GetCultures | It gets a list of the supported cultures filtered by the specified type |
| GetFormat | It returns the object that represents the format of the specified type |