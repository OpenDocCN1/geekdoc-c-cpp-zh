
# CHAPTER 9: Working with Property Lists

it isn’t.

## Using JSON

```
NSData *jsonData =
    [json dataUsingEncoding:NSUTF8StringEncoding;
     NSError *error = nil];
id object =
    [JSONSerialization JSONObjectWithData:
                               jsonData
                               options:0
                                 error: &error];
NSAssert(nil == error, @"Failed to parse JSON");
NSData *data =
    [JSONSerialization dataWithObject:object
                                 options:NSJSONWritingOptions
                                  error: &error];
NSAssert(nil == error, @"Failed to export JSON");
```

From: json.m

Over the last few years, another format that is very similar to the old-style OpenStep property lists has become popular. The *JavaScript Object Notation (JSON)* is a subset of serialized JavaScript objects, storing data but not code.

Recent versions of Cocoa include a class modeled on `PropertyListSerialization` for loading and storing JSON data. This has slightly more restrictions than the property list encoding. You can only store numbers or strings in leaf nodes, and all collections must be arrays or dictionaries.

In general, you wouldn’t use JSON for applications that live in a pure Objective-C environment. JSON is mainly useful for interoperability. There are libraries available for most platforms and languages that read and write JSON and it’s the native format for most web applications. If you write JSON data, it’s trivial for a piece of client-side JavaScript on a web page to transform it. The same is true in reverse: You can generate JSON on a web page and then use it in your Objective-C code.

The example at the start of this section shows how to convert to and from JSON. The JSON standard requires data to be in some unicode encoding. The serialization class can automatically detect the encoding, because the first two characters in a JSON stream are always ASCII. This lets it detect multibyte encodings by the placement of NULL bytes within the first four, if a byte-order mark is missing.

In this example, we pretty-print the JSON. This is mostly useful for debugging. It will automatically indent the output, for readability. This takes a tiny bit more CPU and can use a lot more space, so it’s a bad idea for data’s going to go across the network and be used by another program, but a good idea if the data is going to be edited by hand.

# CHAPTER 9: Working with Property Lists

## Storing User Defaults

```
NSUserDefaults *def = 
[NSUserDefaults standardUserDefaults];
id persistentString = 
[def stringForKey:@"example"];
NSLog(@"Old value: %@", persistentString);
if (argc > 1) 
{
    NSString *new = 
    [NSString stringWithUTF8String:
argv[1]];
    [def setObject:new
forKey:@"example"];
    [def synchronize];
}
```

From: defaults.m
The user defaults system is one of the biggest users of property lists. If you look in the ~/Library/Preferences directory, you will see a lot of property list files. These files store preferences for the current user. There is a corresponding global directory in /Library/Preferences.
Every application has its own defaults domain, typically a reverse-DNS notation string (for example com.apple.TextEdit). The NSUserDefaults class can access data from this domain.

The user defaults system will read data from a variety of sources. One of the most useful is the command line. You can specify key-value pairs as command-line arguments to any OS X application, which is incredibly useful when

Storing User Defaults 207

debugging.
The defaults system is exposed as a single dictionary, with a few convenience methods. In general, you can pretend that the user defaults object really is a persistent dictionary.

**Note:** The defaults system is comparable to the Windows registry, but with a few important differences. Both support multiple levels of keys (user, system, and network), but the defaults system hides all of this from the programmer. Although both look like tree structures, whereas the defaults system is a single database, stores data in separate files for each domain. This makes it easy to modify defaults with third-party tools and means that it scales better because you never need to read more than one or two of these files into memory at once. The downside is that operations on defaults are not transactional. Modifying the same domain from two programs simultaneously is undefined.

Unlike a dictionary, the defaults object has some convenience methods for accessing non-object types and for type-checking object types. In the current example, we send it a `-stringForKey:` message. This wraps the `-objectForKey` value: a method, but ensures that the return value is a string.

There are other convenience methods, such as `-floatForKey:` and `-setFloat:ForKey:`, which take primitive C types and wrap them in NSNumber instances before storing them in the defaults system.

The code in this example ends by sending a -synchronize message to the defaults object. This is not usually necessary. The defaults object will be periodically synchronized with the on-disk storage. In this example, however, we are not using a run loop (so timers will not work) and are exiting immediately after modifying the defaults, so our changes will never be committed to disk without this.

Running this example, you can see that the initial value is nil, because there isn't anything stored in defaults. The value passed as an argument to the short program is stored in defaults and retrieved automatically the next time it is run.

This also demonstrates using NSArgumentDomain. There are several sources for defaults, which are loaded in order and overwrite the previous ones. The last, and therefore highest priority, defaults are the arguments. Specifying an -example command-line option sets the @"example" key in defaults to whatever is passed as the argument. This does not replace the persistent value, it just overrides it in this particular run of the program. You can see that when we run the program again, without the command-line argument, the old value from the two invocations ago is used. It was committed to disk on the third run of the

```
$ ./a.out persistent
a.out[72216:903] Old value: (nil)
$ ./a.out new
a.out[72216:903] Old value: persistent
$ ./a.out -example arg store
a.out[72362:903] Old value: arg
$ ./a.out -example arg
a.out[72363:903] Old value: arg
$ ./a.out new
a.out[72363:903] Old value: store
$ plutil -convert xml1 \
~/Preferences/a.out.plist
$ cat ~/Preferences/a.out.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
EN "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>example</key>
<string>new</string>
</dict>
</plist>
```

Output from: defaults

program, but was not used on the fourth run because an argument replaced it. On the fifth run, with no argument, it is visible again. If you are writing a command-line tool, this provides a very convenient way of parsing command-line arguments. You can store default values for command-line arguments in the defaults system and have them automatically overridden by the user, without needing any parsing code.

## Storing Arbitrary Objects in User Defaults

```
NSUserDefaults *def =
[NSUserDefaults standardUserDefaults];
NSData *serialized = [def objectForKey:@"color"
];
id favoriteColor = 
[NSKeyedArchiver unarchiveObjectWithData:serialized];
if (nil == favoriteColor)
{
  favoriteColor = [NSColor blackColor];
  serialized = [NSKeyedArchiver
    archivedDataWithRootObject:favoriteColor];
  [def setObject:serialized
    forKey:@"color"];
  [def synchronize];
}
```

From: colordefault.m

Quite often, you want to store something in defaults other than the basic Foundation data types. A common example is colors. If you allow users to customize the interface in any way, you typically want their selected colors to persist between program invocations. This is easy; just
