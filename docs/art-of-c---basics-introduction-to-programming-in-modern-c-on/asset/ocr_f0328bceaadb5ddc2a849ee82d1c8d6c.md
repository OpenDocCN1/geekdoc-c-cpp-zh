birth-date/Birthdate.cs

```
```csharp
namespace Example;

static class BirthDate {
    internal static string Weekday(DateTime date) =>
        Enum.GetName(date.DayOfWeek) ?? "";
    internal static int AgeInDays(DateTime date) => (DateTime.Now -
        date).Days;
    internal static (int, int) AgeInHours(DateTime date) {
        var age = DateTime.Now - date;
        return ((int)age.TotalHours, age.Minutes);
    }
}
```
```

# # MD5 Hash