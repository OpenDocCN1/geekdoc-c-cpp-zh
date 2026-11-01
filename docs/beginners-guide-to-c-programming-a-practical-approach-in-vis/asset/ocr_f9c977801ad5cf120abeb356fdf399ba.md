7. Since the name of our class is ShowText, its constructor method(s) should also be named as ShowText. Let's declare two different constructor methods. One of them will take a single string parameter while the other will take two. In the first constructor, we will display a message box showing the passed string while the second constructor will show the concatenated string made of its parameters in a message box. We can declare these constructor methods as follows:

```
public class ShowText
{
    public string memberString1, memberString2;

    public ShowText(string passedString1)
    {
        memberString1 = passedString1;
        MessageBox.Show(memberString1);
    }

    public ShowText(string passedString1, string passedString2)
    {
        memberString1 = passedString1;
        memberString2 = passedString2;
        MessageBox.Show(memberString1+ " - " + memberString2);
    }
}
```

Code 12.17

+   - Our class has two member variables named memberString1 and memberString2. These variables are not initialized during declaration.
+   - In the first constructor method, the passed string is assigned to the first member variable memberString1 and then shown in a message box.
+   - In the second constructor method, two string variables are passed and then these are assigned to memberString1 and memberString2. Then they are shown in a message box together with a hyphen between them.
+   - Remember that constructor methods are executed only once when an object is created using them. Therefore either of these message boxes