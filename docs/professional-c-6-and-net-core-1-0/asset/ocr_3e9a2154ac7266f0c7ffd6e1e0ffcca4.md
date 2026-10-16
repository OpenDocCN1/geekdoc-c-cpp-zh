|  | the data is only `init` loaded from the source; `OneWay` updates from the source to the target. With `TwoWay` binding, changes from the WPF elements are written back to the source. `OneWayToSource` means that the data is never read but always written from the target to the source. |
| Converter | Use this property to specify a converter class that converts the data for the UI and back. The converter class must implement the interface `IValueConverter`, which defines the methods `Convert` and `ConvertBack`. You can pass parameters to the converter methods with the `ConverterParameter` property. The converter can be culture-sensitive; and the culture can be set with the `ConverterCulture` property. |
| FallbackValue | Use this property to define a default value that is used if binding doesn’t return a value. |
| ValidationRules | Using this property, you can define a collection of `ValidationRule` objects that are checked before the source is updated from the WPF target elements. The class `ExceptionValidationRule` is derived from the class `ValidationRule` and checks for exceptions. |
| Delay | This property is new with WPF 4.5. It enables you to specify an amount of time to wait before the binding source is updated. This can be used in scenarios where you want to give the user some time to enter more characters before starting a validation. |

# Simple Object Binding

To bind to CLR objects, with the .NET classes you just have to define properties, as shown in the `Book` class example and the properties `Title`, `Publisher`, `Isbn`, and `Authors`. This class is in the `Models` folder of the `BooksDemoLib` project (code file `BooksDemoLib/Models/Book.cs`).

```
using System.Collections.Generic;

namespace BooksDemo.Models
{
    public class Book
    {
        public Book(string title, string publisher, string isbn,
                    params string[] authors)
        {
            Title = title;
            Publisher = publisher;
            Isbn = isbn;
            Authors = authors;
        }
        public Book()
            : this("unknown","unknown","unknown")
        {
        }
    }
```