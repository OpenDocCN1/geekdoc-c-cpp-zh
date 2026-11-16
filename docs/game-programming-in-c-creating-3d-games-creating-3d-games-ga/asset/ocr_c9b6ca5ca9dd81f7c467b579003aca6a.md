class.

To encapsulate buttons, you can declare a `Button` class, as shown in Listing 11.5. You can assume that every button has a `Text` name, and so it also needs a pointer to the `Font` that renders this text. In addition, the button has a position onscreen as well as dimensions (width and height). Finally, when the player clicks the button, some action should occur, depending on the button clicked.

To customize a button's action, `Button` uses the `std::function` class to encapsulate a callback function. This function can be a standalone function or, more likely, a lambda expression. When declaring a `Button`, the constructor takes in this function. Then, when the code detects a button click, you can call this function. This way, any arbitrary button you create for any arbitrary menu can call a corresponding arbitrary function.

# Listing 11.5 Button Declaration

Click here to view code image

```
```cpp
class Button
{

public:

// Constructor takes in a name, font,

// callback function, and position/dimensions of l

Button(const std::string& name, class Font* font,
```
```