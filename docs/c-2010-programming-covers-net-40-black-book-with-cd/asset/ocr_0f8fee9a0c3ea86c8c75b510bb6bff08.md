You need to flush the cache to write the data to AD, as shown in the following code snippet:

```
user.CommitChanges();
```

# Modifying the Active Data Objects

To modify the values of the properties of AD objects, you can use various methods, such as Add(), Remove(), and RemoveAt(). The Add() method is used to add new values to a property; while the Remove() and RemoveAt() methods are used remove specific values from a property. You can also clear the value of a property by using the PropertyValueCollection.Clear() method.

The following code snippet shows how the properties—company and department—of user Steve can be modified:

```
DirectoryEntry entry = new DirectoryEntry("LDAP://192.168.1.95");

string a = null;
entry.Path = "LDAP://192.168.1.95/CN=" + a + ",CN=Users,DC=sql, DC=local";
entry.Username = "administrator@sql.local";
entry.Password = "kogenta321";
if (entry.Properties.Contains("company"))
{
    entry.Properties["company"][0] = textBox3.Text;
}
else
{
    entry.Properties["company"].Add(textBox3.Text);
}
if (entry.Properties.Contains("department"))
{
    entry.Properties["department"][0] = textBox4.Text;
}
else
{
    entry.Properties["department"].Add(textBox4.Text);
}
entry.CommitChanges();
```

# Searching Active Directory for Objects

The DirectorySearcher class is used to search object values in AD. To search object values, you need to define four important parts in the constructor of DirectorySearcher class, which are as follows:

+   - SearchRoot
+   - Filter
+   - PropertiesToLoad
+   - SearchScope

Let’s discuss these parts one by one.

# SearchRoot

The SearchRoot part in the constructor of DirectorySearcher class specifies the base node from where the search should begin. The default node is the root domain. The SearchRoot class starts searching from this domain. The SearchRoot class is used along with the Path property of the DirectoryEntry object.

# Filter

The Filter part defines the criteria for searching objects in AD. The string identifying the filter should be enclosed in parentheses. A search filter contains name, operator, and value. You can also use the <=, =, >=, &, and | operators while writing the search expressions in a search filter.