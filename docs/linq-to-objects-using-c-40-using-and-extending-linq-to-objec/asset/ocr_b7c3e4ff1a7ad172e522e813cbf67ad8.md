# Listing 2-12 Query joins two collections based on the phone number—see Output 2-7.
Notice the use of the temporary anonymous type.

```
List<Contact> contacts = Contact.SampleData();
List<CallLog> callLog = CallLog.SampleData();
```

```
var q = from call in callLog
  join contact in contacts on
      call.Number equals contact.Phone
  select new {
      contact.FirstName,
      contact.LastName,
      call.When,
      call.Duration
  };

foreach (var c in q)
  Console.WriteLine(
      "{0} - {1} ({2}min)",
      c.When.ToString("ddMM HH:mm"), c.FirstName,
      c.LastName, c.Duration);
```

# Output 2-7

07Aug 08:12 - Barney Gottshall (2min)
07Aug 09:23 - Ariel Hazelgrove (15min)
07Aug 10:5 - Mack Kamph (1min)

08Jul 14:37 - Armando Valdes (13min)
08May 15:23 - Chance Lard (16min)
08Jun 17:12 - Mack Kamph (24min)

To demonstrate the full power of LINQ to Objects query functionality, the query shown in Listing 2-13 summarizes the data from two in-memory collections by using joins, groups, and also aggregate operators in the select clause. The final output of this query is shown in Output 2-8.