```
```cpp
// Ask a basic question
Question q1;
q1.set_text("Who was the inventor of C++?");
q1.set_answer("Bjarne Stroustrup");

q1.display();
cout << "Your answer: ";
getline(cin, response);
cout << q1.check_answer(response) << endl;

// Ask a choice question

ChoiceQuestion q2;
q2.set_text("In which country was the inventor of C++ born?");
q2.add_choice("Australia", false);
q2.add_choice("Denmark", true);
q2.add_choice("Korea", false);
q2.add_choice("United States", false);

q2.display();
cout << "Your answer: ";
getline(cin, response);
cout << q2.check_answer(response) << endl;

return 0;
}
```
```

# Program Run

```
```
Who was the inventor of C++?
Your answer: Bjarne Stroustrup
true
In which country was the inventor of C++ born?
1: Australia
2: Denmark
3: Korea
4: United States
Your answer: 2
true
```
```

![](bbox=[0.079, 0.671, 0.226, 0.759])

**11.** What is wrong with the following implementation of the display function?

```
```cpp
void ChoiceQuestion::display() const
{
    cout << text << endl;
    for (int i = 0; i < choices.size(); i++)
    {
        cout << i + 1 << ": " << choices[i] << endl;
    }
}
```
```

**12.** What is wrong with the following implementation of the display function?

```
```cpp
void ChoiceQuestion::display() const
{
    this->display();
    for (int i = 0; i < choices.size(); i++)
    {
```
```