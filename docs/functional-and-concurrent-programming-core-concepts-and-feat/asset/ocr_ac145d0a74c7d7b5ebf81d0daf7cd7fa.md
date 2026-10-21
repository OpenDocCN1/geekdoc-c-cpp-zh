Keep in mind that on an empty structure, exists is always false and forall is always true:

```
Some("foo").exists(_.endsWith("o")) // true
Some("foo").forall(_.endsWith("o")) // true
Some("bar").exists(_.endsWith("o")) // false
Some("bar").forall(_.endsWith("o")) // false

None.exists((proj: Project) => proj.id == 12345L) // false
None.forall((proj: Project) => proj.id == 12345L) // true   <- BE CAREFUL HERE!
```

The last case is the one most likely to trip up a careless developer.

Functions exists and forall only tell you if some or all the elements have the desired property. In scenarios that require knowing more precisely how many values satisfy a condition, you can rely on function count instead:

```
temps.count(_ > 90) // 3
```

If the list temps represents temperatures over time, you can use count to calculate how many times the temperature increased:

```
val ups = temps.sliding(2).count(pair => pair(1) > pair(0)) // 2
```

The expression temps.sliding(2) produces a sliding window of two successive temperatures: 88 and 91, 91 and 78, 78 and 69, etc. Value ups counts how many of those pairs have a second number larger than the first, which is two (88 to 91 and 69 to 100).

When the number of values that satisfy a given property is not enough information and you need the values themselves, use filter:

```
temps.filter(_ > 75) // List(88, 91, 78, 100, 98)
```

Scala also has a method filterNot that reverses its test. To separate values with and without a desired property, use partition to produce both collections, usually in a more efficient single traversal than a call to filter followed by a call to filterNot:

```
temps.filterNot(_ > 75) // List(69, 70)
temps.partition(_ > 75) // (List(88, 91, 78, 100, 98), List(69, 70))
```

The previous implementation of quick-sort in Listing 7.20 can be simplified by replacing the user-defined function splitPivot with a call to partition: