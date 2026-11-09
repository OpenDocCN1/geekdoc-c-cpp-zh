# Creating fetch requests

To read data, create a fetch request and pass it to the managed context. Fetch requests can be complex, and the code interface isn’t intuitive, but in outline, there isn’t any more to searching than creating a request, setting its parameters, passing it to the context, and reading the results.

Sample code is shown below:

```
NSEntityDescription *albumEntity
= [NSEntityDescription entityForName:@"Album"
inManagedObjectContext:managedObjectContext];
NSFetchRequest *theRequest = [[NSFetchRequest alloc] init];
[theRequest setEntity:albumEntity];
returnArray = [managedObjectContext
    executeFetchRequest:theRequest error:&error];
```

In the context of your model, this code runs the simplest possible search. returnArray returns a list of all Album entities in the context; that is, a list of all albums. You can then process the array to further extract values from it.

# Using predicates

To narrow the search, you can add a predicate to the search request:

```
NSPredicate *thePredicate =
[NSPredicate predicateWithFormat:@"Name == 'An Album Name'"];

[theRequest setPredicate:thePredicate];
//Run the search...
```

The predicate syntax is complex, but recognizably similar to regex matching, which it’s based on. predicateWithFormat: allows substitutions with the usual withFormat: options. Use this to search strings and other values dynamically.

```
NSPredicate *thePredicate =
[NSPredicate predicateWithFormat:@"Name == %@", aString];
```

Table 14.3 shows some other examples. For more information about predicate programming, see the Predicates Programming Guide in the Cocoa documentation.