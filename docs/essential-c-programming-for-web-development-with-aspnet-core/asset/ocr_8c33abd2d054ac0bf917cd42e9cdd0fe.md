```
// Process the submitted data
// ...
return RedirectToAction("Success");
}
return View(model); // Redisplay the form with validation errors
}
```

The Submit action method receives a MyViewModel object, which is automatically populated with data from the form fields. The ModelState.IsValid property checks if the submitted data adheres to any validation rules defined in the model. If the data is valid, you can proceed to process it; otherwise, you can redisplay the form with validation errors.

# Data Validation: Ensuring Data Integrity

Data validation is crucial for maintaining the integrity and security of your application. It involves checking user input to ensure it conforms to expected formats, ranges, or other constraints. ASP.NET Core 3 provides built-in support for data validation using data annotation attributes on model properties.

Let's add some validation attributes to the MyViewModel class:

```
C#
public class MyViewModel
{
[Required]
public string Name { get; set; }
[Required]
[EmailAddress]
public string Email { get; set; }
```