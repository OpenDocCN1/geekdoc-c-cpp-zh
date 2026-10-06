As an example, the following simple query returns the last element in the integer array, writing the number 2 to the Console window:

```
int[] nums = new int[] { 5, 3, 4, 2 };
int last = nums.Last();
Console.WriteLine(last);
```

# Return the Same Type as the Source-IEnumerable<TSource>

The most basic projection type returns a filtered and ordered subset of the original source items. This projection is achieved by specifying the range variable as the argument after the select keyword. The following example returns an IEnumerable<Contact>, with the type Contact being inferred from the element type of the source collection:

```
List<Contact> contacts = Contact.SampleData();
IEnumerable<Contact> q = from c in contacts
select c;
```

A more appropriate query would filter the results and order them in some convenient fashion. You are still returning a collection of the same type, but the number of elements and their order will be different.

```
List<Contact> contacts = Contact.SampleData();
IEnumerable<Contact> q = from c in contacts
where c.State == "WA"
orderby c.LastName, 
c.FirstName ascending
select c;
```

# Return a Different Type Than the Source-IEnumerable<TAnyType>

Any type can be projected as part of the select clause, not just the source type. The target type can be any available type that could otherwise be