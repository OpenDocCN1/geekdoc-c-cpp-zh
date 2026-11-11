+   - Pattern.CANON_EQ: Take canonical equivalence of Unicode characters into account. For example, u followed by ¨ (diaeresis) matches ü.

The last two flags cannot be specified inside a regular expression.

If you want to match elements in a collection or stream, turn the pattern into a predicate:

```
```
Stream<String> strings = . . .;
Stream<String> result = strings.filter(pattern.asPredicate());
```
```

The result contains all strings that match the regular expression.

If the regular expression contains groups, the Matcher object can reveal the group boundaries. The methods

```
```
int start(int groupIndex)
int end(int groupIndex)
```
```

yield the starting index and the past-the-end index of a particular group.

You can simply extract the matched string by calling

```
```
String group(int groupIndex)
```
```

Group 0 is the entire input; the group index for the first actual group is 1. Call the groupCount method to get the total group count. For named groups, use the methods

```
```
int start(String groupName)
int end(String groupName)
String group(String groupName)
```
```

Nested groups are ordered by the opening parentheses. For example, given the pattern

```
```
(([1-9]|1[0-2]):([0-5][0-9]))([ap]m)
```
```

and the input

```
```
11:59am
```
```

the matcher reports the following groups

| Group Index | Start | End | String |
| --- | --- | --- | --- |
| 0 | 0 | 7 | 11:59am |
| 1 | 0 | 5 | 11:59 |
| 2 | 0 | 2 | 11 |
| 3 | 3 | 5 | 59 |