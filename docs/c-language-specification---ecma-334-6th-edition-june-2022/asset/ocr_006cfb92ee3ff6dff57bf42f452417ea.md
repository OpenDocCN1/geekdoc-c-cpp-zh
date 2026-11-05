list of the element initializer as the argument list, and the collection initializer invokes the resulting method. Thus, the collection object shall contain an applicable instance or extension method with the name `Add` for each element initializer.

*Example:* The following class represents a contact with a name and a list of phone numbers:

```
~~~csharp
public class Contact
{
    public string Name { get; set; }
    public List<string> PhoneNumbers { get; } = new List<string>();
}
~~~
```

A List<Contact> can be created and initialized as follows:

```
~~~csharp
var contacts = new List<Contact>
{
    new Contact
    {
        Name = "Chris Smith",
        PhoneNumbers = { "206-555-0101", "425-882-8080" }
    },
    new Contact
    {
        Name = "Bob Harris",
        PhoneNumbers = { "650-555-0199" }
    }
};
~~~
```

which has the same effect as

```
~~~csharp
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8080");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist;
~~~
```

where __clist, __c1 and __c2 are temporary variables that are otherwise invisible and inaccessible.

*end example*

# 11.7.15.5 Array creation expressions

An array_creation_expression is used to create a new instance of an array_type.

```
~~~
array_creation_expression
    : 'new' non_array_type '[' expression_list ']' rank_specifier*
      array_initializer?
    | 'new' array_type array_initializer
    | 'new' rank_specifier array_initializer
    ;
~~~
```