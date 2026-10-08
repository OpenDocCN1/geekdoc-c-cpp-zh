# Validation

There is a serious issue with the AcmeLibrary application — validation. When you create a new book and leave the title or ISBN information empty when clicking the Create button, you will see validation messages to the right of the invalid fields. However, when you are editing a book, something happens. If you set an invalid field value and save the book, the invalid field's value is reverted to its original value without any notification. Try to set an ISBN number longer than 13 characters, and you'll be given an exception.

It's time to deal with validation. In MVC, the model is validated according to its metadata. The model (for example, the Book) has implicit metadata such as the type and nullability of a property used during the validation. For example, the Published property of the Book class is a DateTime. So, you cannot type any kind of string from this text box representing property, only data that can be parsed as DateTime.

The implicit metadata is rarely enough for providing validation for model objects. For example, the ISBN number used in AcmeLibrary should be exactly 13 characters long, and each character can be only a decimal digit. The MVC engine is not aware of that unless you declare.

# Validation Attributes

The NET base class library has a namespace called System.ComponentModel.DataAnnotations that includes attributes you can use to define validation rules clearly. For a moment, forget that the Book class is automatically generated from the ADO.NET entity model. If you created it manually, you could decorate its properties with data annotation attributes, as shown in Listing 18

> LISTING 18-16: Data Annotation Attributes Applied for the Book class

```
public class Book
{
    public int Id { get; set; }

    [Required(ErrorMessage = "Please provide the author(s) name")
    public string Author { get; set; }

    [Required(ErrorMessage = "Please provide a title")
    public string Title { get; set; }

    [RegularExpression("*[0-9]{13}\$",
    ErrorMessage = "This must be exactly 13 digits")]
    public string ISBN { get; set; }

    public DateTime Published { get; set; }

    public string Publisher { get; set; }
}
```
```