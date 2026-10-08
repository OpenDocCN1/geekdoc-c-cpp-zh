# CHAPTER 9: Working with Property Lists

# Storing User Defaults

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
arv[1]];
    [def setObject:new
forKey:@"example"];
    [def synchronize];
}
```

From: defaults.m
The user defaults system is one of the biggest users of property lists. If you look in the ~/Library/Preferences directory, you will see a lot of property list files. These files store preferences for the current user. There is a corresponding global directory in /Library/Preferences.
Every application has its own defaults domain, typically a reverse-DNS notation string (for example com.apple.TextEdit). The NSUserDefaults class can access data from this domain.

The user defaults system will read data from a variety of sources. One of the most useful is the command line. You can specify key-value pairs as command-line arguments to any OS X application, which is incredibly useful when