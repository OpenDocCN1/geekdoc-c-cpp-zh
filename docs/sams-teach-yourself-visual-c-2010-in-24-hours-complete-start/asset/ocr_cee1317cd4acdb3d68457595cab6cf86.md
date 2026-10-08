3. Run the application by pressing Ctrl+F5. The output should look similar to Figure 12.4.

![](bbox=[0.28, 0.178, 0.63, 0.442])

# **FIGURE 12.4**

Grouping data

# # Joining Data

LINQ also enables you to combine multiple data sources by joining them together on one or more common fields. Joining data is important for queries against data sources where their relationship cannot be followed directly. Unlike SQL, which supports joins using many different operators, join operations in LINQ are based on the equality of their keys.

Expanding on the earlier examples that used only the `Contact` class, you need at least two classes to perform join operations. The `Contact` class is shown again in Listing 12.9, along with a new `JournalEntry` class. Continue the assumption that the contacts list has been populated as a result of calling `GetContacts` and that the journal list has been populated as a result of calling `GetJournalEntries`.

# ## LISTING 12.9 The Contact and JournalEntry Classes

```
```csharp
class Contact
{
  public int Id { get; set; }
  public string Company { get; set; }
  public string LastName { get; set; }
  public string FirstName { get; set; }
  public string Address { get; set; }
  public string City { get; set; }
  public string StateProvince { get; set; }
}
```
```