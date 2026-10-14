Name value. (Note that Name is a structure, so the default constructor sets its private name field to null.)

Click here to view code image

```
sealed class PhoneBook
{
    ...
    public Name this [PhoneNumber number]
    {
        get
        {
            int i = Array.IndexOf(this.phoneNumbers, number);
            if (i != -1)
            {
                return this.names[i];
            }
            else
            {
                return new Name();
            }
        }
    }
    ...
}
```

3. Remove the comment // TODO: write 2nd indexer here and replace it with a second public read-only indexer for the PhoneBook class that returns a PhoneNumber and accepts a single Name parameter. Implement this indexer in the same way as the first one. (Again, note that PhoneNumber is a structure and therefore always has a default constructor.)

The second indexer should look like this:

Click here to view code image

```
sealed class PhoneBook
{
    ...
    public PhoneNumber this [Name name]
    {
        get
        {
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
    ...
```