```
sealed class PhoneBook
{
    public PhoneNumber this [Name name]
{
        get{
            int i = Array.IndexOf(this.names, name);
            if (i != -1)
{
                return this.phoneNumbers[i];
            }
            else
{
                return new PhoneNumber();
            }
        }
    }
}
```

Notice that these overloaded indexers can coexist because the values they index are of different types, which means that their signatures are different. If the Name and PhoneNumber structures were replaced by simple strings (which they wrap), the overloads would have the same signature, and the class would not compile.

+   4. On the Build menu, select Build Solution, correct any syntax errors, and then rebuild the solution if necessary.

To call the indexers

+   1. Display the MainPage.xaml.cs file in the Code and Text Editor window and then locate the findByNameClick method.
nThis method is called when the Find By Name button is selected. This method is currently empty.
2. Replace the // TODO: comment with the code shown in bold in the following example:

Click here to view image