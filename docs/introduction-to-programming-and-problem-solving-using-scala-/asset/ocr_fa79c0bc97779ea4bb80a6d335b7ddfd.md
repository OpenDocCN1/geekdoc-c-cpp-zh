# Scala Basics

43

```
addString   head      r takeWhile
aggregate headOption reduce to
apply         indexOf reduceLeft toArray
asInstanceOf  indexOfSlice reduceLeftOption toBoolean
canEqual      where reduceOption toBuffer
capitalize    indices reduceRight toByte
collect       init reduceRightOption toDouble
collectFirst  inits replaceAllLiterally toFloat
combinations  intersect isDefinedAt repr toIndexedSeq
compare       isEmpty reverse reverseIterator toInt
compareTo     isInstanceOf reverseMap toIterator
contains      slice isTraversableAgain sameElements toList
copyToArray  length scan toLong
copyToBuffer  count scanLeft toMap
corresponds  lastOfIndex scanRight toSeq
count        lastOfSlice segmentLength toShort
diff         lastOfIndex size toStream
drop         lengthComplete sliding toTraversable
dropRight    lines sortBy toVector
ends        linesWithIterator sortWith union
exists       linesWithSeparators sorted updated
filter       map split withFilter
filterNot    maxBy splitAt zip
flatMap      min startsWith zipAll
fold         min stringPrefix zipWithIndex
```

Going through all these methods is beyond the scope of this chapter, but it is beneficial to see examples of some of them. To do this, let us consider a situation where we have a person's name written as "first, last". We wish to build a new string that has the same name in the format "last, first". To do this, we must first find where the space is, then get the parts of the original string before and after the space. Once we have done that, we can simply put the pieces back together in the reverse order with a comma between.

To find the location of the space, we will use indexOf. This method gives us a numeric index for the first occurrence of a particular character or substring in a string.

```
scala> val name = "Mark Lewis"
name: String = Mark Lewis
```

```
scala> val spaceIndex = name.indexOf(" ")
spaceIndex: Int = 4
```

The index of 4 is not 5, because the indexes in strings, and everything else except tuples, start at 0. So if the 'M' is 0, the 'a' is at 1, etc.

Now that we know where the space is, we need to get the parts of the string before and after it. That can be accomplished using the substring method

```
scala> val first = name.substring(0,spaceIndex)
first: String = Mark
```

```
scala> val last = name.substring(spaceIndex+1)
```