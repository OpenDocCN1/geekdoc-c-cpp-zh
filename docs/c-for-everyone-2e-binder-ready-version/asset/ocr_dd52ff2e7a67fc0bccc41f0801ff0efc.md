A derived class can inherit a function from the base class, or it can override it by providing another implementation.

Consider the display function of the ChoiceQuestion class. It needs to override the base-class display function in order to show the choices for the answer. Specifically, the derived-class function needs to

+   - Display the question text.
+   - Display the answer choices.

The second part is easy because the answer choices are a data member of the derived class.

```
```cpp
void ChoiceQuestion::display() const
{
   // Display the question text
   ...
   // Display the answer choices
   for (int i = 0; i < choices.size(); i++)
   {
      cout << i + 1 << ": " << choices[i] << endl;
   }
}
```
```

But how do you get the question text? You can't access the text member of the base class directly because it is private.

Instead, you can call the display function of the base class.

```
```cpp
void ChoiceQuestion::display() const
{
   // Display the question text
   display(); // Invokes implicit parameter.display()
   // Display the answer choices
   ...
}
```
```

However, this won't quite work. Because the implicit parameter of ChoiceQuestion::display is of type ChoiceQuestion, and there is a function named display in the ChoiceQuestion class, that function will be called—but that is just the function you are currently writing! The function would call itself over and over.

To display the question text, you must be more specific about which function named display you want to call. You want Question::display:

```
```cpp
void ChoiceQuestion::display() const
{
   // Display the question text
   Question::display(); // OK
   // Display the answer choices
   ...
}
```
```

Use BaseClass::function notation to explicitly call a base-class function.

When you override a function, you usually want to extend the functionality of the base-class version. Therefore, you often need to invoke the base-class version before extending it. To invoke it, you need to use the BaseClass::function notation. However, you have no obligation to call the base-class function. Occasionally, a derived class overrides a base-class function and specifies an entirely different functionality.

Here is the complete program that displays a plain Question object and a ChoiceQuestion object. (The definition of the Question class, which you have already seen, is placed into question.h, and the implementation is in question.cpp.) This example shows how you can use inheritance to form a more specialized class from a base class.