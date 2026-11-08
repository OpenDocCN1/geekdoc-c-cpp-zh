```
```cpp
unique_ptr<Label> lblLastName_{new Label()};              // ...of the class
unique_ptr<Text> txtLastName_{new TextField()};
unique_ptr<Button> btnOK_{new Button{1}};
unique_ptr<Button> btnCancel_{new Button{2}};

public:
    explicit MyDialog(const string& title) : title_{title} {}
    unique_ptr<Button> showModal()
    {
        { return std::move(btnOK_); }     // Placeholder code; OK pressed
    }
    unique_ptr<MyDialog> createDialog() {
        return unique_ptr<MyDialog>{       // temporary value
            new MyDialog{"Please enter name"}};
    }
    int showDialog() {
        unique_ptr<MyDialog> dialog = createDialog();     // local variable
        unique_ptr<Button> pressed = dialog->showModal();  // return value
        return pressed->id_;
    }
int main() {
    int pressed_id = showDialog();
    if(pressed_id == 1) {
        std::cout << "Thank you for pressing OK\n";
    }
}
```
```

**Listing 20.5** `unique_ptr` as data field, return value, and local variable.

In **Listing 20.5**, I have extremely simplified a window application that displays a dialog. Users are supposed to press one of two buttons, and the program returns the pressed button as a number—but we consider windows schematically here, and in the brevity of the program no actual windows pop up. However, you will find a similar class hierarchy in most window programming interfaces.

Because all `unique_ptr` data fields belong to the `MyDialog` class (the class *owns* them), they are correctly removed when `dialog` is destroyed in `showDialog()`, along with all `unique_ptr`s. These, in turn, own their respective raw pointers and clean up their charges with `delete` in their destructor.

Something interesting happens in `createDialog()`. The return expression creates a new value—even a temp-value, essentially a variable without a name. Does this mean that at the end of the `return` statement, `unique_ptr<MyDialog>{new MyDialog{...}}` is immediately cleaned up again? Yes, it is, but not without first being “copied” for `return` to end up in the variable `dialog` in `showDialog()`. Did I say copied? Oh, no, that’s not possible! You cannot copy a `unique_ptr`. If you could copy it, there would be two `unique_ptr` instances, both wanting to manage the same raw pointer. That would not be “unique.”