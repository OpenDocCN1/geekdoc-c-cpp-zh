![](bbox=[0.19, 0.06, 0.81, 0.44])

# Figure 30.17

Of course, you can also create a control template and use a data template from within.

# Styling a ListView

Changing a style of a button or a label is a simple task, such as changing the style of an element that contains a list of elements. For example, how about changing a ListView? Again, this list control has behavior and a look. It can display a list of elements, and you can select one or more elements from the list. For the behavior, the ListView class defines methods, properties, and events. The look of the ListView is separate from its behavior. It has a default look, but you can change this look by creating a template.

To fill a ListView with some items, the class CountryRepository returns a list of a few countries that will be displayed (code file Models[WPF|UWP]/CountryRepository.cs):

```
public sealed class CountryRepository
{
    private static IEnumerable<Country> s_countries;

    public IEnumerable<Country> GetCountries() =>
        s_countries ?? (s_countries = new List<Country>
        {
            new Country { Name="Austria", ImagePath ="Images/Austria.bmp" },
            new Country { Name="Germany", ImagePath ="Images/Germany.bmp" },
```