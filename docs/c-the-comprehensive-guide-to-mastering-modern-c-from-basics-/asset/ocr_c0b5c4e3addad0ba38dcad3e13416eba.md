+   • Restructure

+   • Use descriptive names

+   • Comment

Combining the first two approaches, you could perhaps break down the regex into several smaller ones, give the parts names, and then combine them.

```
// https://godbolt.org/z/TK6n4dG37
const string scoreKeyword = R("^score\s+")";
const string numberOfPoints = R(\(\d+\)");
const string forKeyword = R("^for\s+")";
const string numberOfNights = R(\(\d+\)");
const string nightsAtKeyword = R("\snights??at\s+")";
const string hotelName = R("(\*");
const regex pattern(scoreKeyword + numberOfPoints + forKeyword + numberOfNights + nightsAtKeyword + hotelName);
```

# Listing 28.15 Name parts and then combine them.

Perhaps this is more maintainable. At least this approach is recommended if parts of the expression might be used elsewhere in the program.

The third approach to commenting also works, except that C++ comments within within the expression—within the string—do not work.

Here you can use the feature that C++ directly concatenates adjacent string literals if only whitespaces remain after removing them. In this way, you can then comment parts of the expression in an almost "embedded" way.

```
// https://godbolt.org/z/MszTjE3dv
const regex pattern(R("^score")");"
```