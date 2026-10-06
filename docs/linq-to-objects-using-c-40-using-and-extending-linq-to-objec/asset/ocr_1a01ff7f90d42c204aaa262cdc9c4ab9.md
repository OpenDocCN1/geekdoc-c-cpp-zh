the user inputs either a name or phone number, and a drop-down displays recent numbers and searches the contacts held in storage for likely candidates. This technique works because of how .NET manages equality for anonymous types that are projected. The key to this technique working as expected is to ensure that the projected names for each field in the anonymous types are identical in name, case, and order. If these conditions are satisfied, the anonymous types can be operated on any of the set-based operators.

Listing 6-6 uses the sample data of contact and CallLog types introduced earlier in this book in Table 2-1 and Table 2-2 with sample partial user-entered data of Ka and 7. The Console output from this example is shown in Output 6-5.

Listing 6-6 Anonymous types with the same members can be unioned and concatenated—see Output 6-5

```
// lookup recent phone number OR contact first and last
// names to incrementally build a convenient picklist on
// partial user entry (narrow the list as data is typed)
string userEntry = "Ka";

var q = (
    // userEntry is contact name
    from contact in Contact.SampleData()
    where contact.FirstName.StartsWith(userEntry)
    || contact.LastName.StartsWith(userEntry)
    select new { Display = contact.FirstName + " " + 
    contact.LastName }).Distinct()

.Union(
    // userEntry is partial phone number
    (from call in CallLog.SampleData()
    where call.Number.Contains(userEntry)
    && call.Incoming == false
    select new { Display = call.Number }).Distinct()

);

Console.WriteLine(
    "User Entry - " + userEntry);

foreach (var item in q)
    Console.WriteLine(item.Display);
```