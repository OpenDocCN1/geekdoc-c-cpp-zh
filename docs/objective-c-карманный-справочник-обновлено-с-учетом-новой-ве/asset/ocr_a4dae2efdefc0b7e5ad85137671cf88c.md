# CHAPTER 6: Manipulating Strings

parts of the original regular expression, using the $n syntax that you’d use in regular expressions elsewhere.

# Storing Rich Text

```
NSDictionary *keyword = [[NSDictionary
dictionaryWithObject:@"keyword"
forKey:@"type"] retain];
NSMutableAttributedString *program =
MutableAttributedString new];

NSAttributedString *fragment =
[[NSAttributedString alloc]
initWithString:@"int"
attributes:keyword];
[program appendAttributedString:fragment];];
```

From: richText.m

A string is just a list of characters. Before you display a string, you generally need some other attributes. These attributes describe the typeface, the size, the alignment and underline styles, and so on.

If you are writing something that deals with structured text—for example, HTML or another form of semantic markup such as DocBook—then these attributes might be a level 1 heading, or ordered list.

Foundation provides a class for assigning arbitrary attributes to strings. The NSAttributedString class lets you attach