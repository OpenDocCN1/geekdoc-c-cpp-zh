Each chapter starts with an introduction, which is followed by one or more sections consisting of a heading and one or more paragraphs, images, tables, or notes.

However, in one common case you can't define the rules to be as flexible as you might like. Whenever an element can contain text, there are only two valid cases. Either the element contains nothing but text, such as

```
```xml
<!ELEMENT name (#PCDATA)>
```
```

or the element contains *any combination of text and tags in any order*, such as

```
```xml
<!ELEMENT para (#PCDATA|em|strong|code)*>
```
```

It is not legal to specify any other types of rules that contain #PCDATA. For example, the following is illegal:

```
```xml
<!ELEMENT captionedImage (image, #PCDATA)>
```
```

You have to rewrite such a rule, either by introducing another `caption` element or by allowing any combination of `image` elements and text.

This restriction simplifies the job of the XML parser when parsing *mixed content* (a mixture of tags and text). Since you lose some control by allowing mixed content, it is best to design DTDs so that all elements contain either other elements or nothing but text.

> **NOTE:** Actually, it isn't quite true that you can specify arbitrary regular expressions of elements in a DTD rule. An XML parser may reject certain complex rule sets that lead to nondeterministic parsing. For example, a regular expression `((x,y)|(x,z))` is nondeterministic. When the parser sees `x`, it doesn't know which of the two alternatives to take.This expression can be rewritten in a deterministic form as `(x,(y|z))`. However, some expressions can't be reformulated, such as `((x,y)*|x?)`. The parser in the Java XML library gives no warnings when presented with an ambiguous DTD; it simply picks the first matching alternative when parsing, which causes it to reject some correct inputs. The parser is well within its rights to do so because the XML standard allows a parser to assume that the DTD is unambiguous.
> 
> In practice, this isn't an issue over which you should lose sleep, because most DTDs are so simple that you will never run into ambiguity problems.