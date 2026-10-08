# CHAPTER 9: Working with Property Lists

store everything that the newer formats support. With OS X, Apple introduced an XML and a binary property list format. The XML format is incredibly verbose, but has the advantage that it can be parsed by other XML-compatible tools and can be embedded in other XML documents.

The binary representation is very fast to parse and very dense but, being binary, is not human-readable.

Some libraries for other languages can handle property lists. The WINGS library in WindowMaker can read and write them, as can a library included with NetBSD. Apple’s Core Foundation framework, and its open-source CFLite library, can also use them from C code.

# Storing Collections in Property Lists

```
NSArray array = [NSArray arrayWithObjects:
@"array", @"containing", @"string",n@"objects", nil];
[array writeToFile:@"example.plist" atomically:
NO];
MutableArray *cycle = [array mutableCopy];
[cycle addObject:cycle];
[cycle writeToFile:@"failure.plist" atomically:
NO];
```

From: writeeplist.m

The array and dictionary classes implement a