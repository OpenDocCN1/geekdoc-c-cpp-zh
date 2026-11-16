# Dictionaries

A dictionary, or data dictionary, is where the lookup table of bad words exists. The options here are endless; the application might already have a database system or filesystem in place, probably using some sort of relational or token lookup. The goal is to have a consistent, easy-to-manage data source that can store all the designated "bad words" in one place.

If constructing from scratch, a good place to start is XML files. For the uninitiated, XML is a form of information identification, assigning tokens to data that can quickly be searched and referenced. A good reference for XML can be found at the O'Reilly Network's XML.com [Oreilly01].

# Parsers

Having a dictionary to store the bad words is only a start. The more resource-intensive part involves searching through the data dictionary for matches against a string. While most C/C++ programmers and Java programmers will be familiar with string manipulation, parsing can be slow and turn into a bottleneck for the game if not implemented carefully.

Again, this is a subsystem that may already be in place with many existing game engines. Parsing through a data source is useful in many other areas of a game besides this one feature. When building a new engine with XML in mind, however, Xerces is a good place to start [Xerces01]. The Xerces library is an open source C++ library that allows very fast searching through XML file sources.

# Filtering

So far, the game will have a lookup dictionary for bad words and strings, and a parser to actively go through and root out any violations against this dictionary. The next step is to filter the text and either block it or change it accordingly. However, the method used in the game is dependent on the specific design in mind, as there are several different ways to filter the violating strings.

# Search-and-Replace, Predetermined Strings

The first filtering method is to do a search-and-replace operation on the string, with a predetermined string. This involves setting up a second word or list of words that act as suitable replacements. An example predetermined string might be:

```
char szReplacementText[] = "[censored]"
```

In this case, the bad word would be replaced with [censored]. To add variety in a place where there might be many violations, you might loop through a list of 10 or 20 variations, such as banned, blocked, and not allowed.