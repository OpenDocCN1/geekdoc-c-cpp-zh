```
string name;
if (nameField.Text != "")
{
    name = nameField.Text;
}
else
{
    throw new Exception("Missing input"); // this is a throw statement
}
```