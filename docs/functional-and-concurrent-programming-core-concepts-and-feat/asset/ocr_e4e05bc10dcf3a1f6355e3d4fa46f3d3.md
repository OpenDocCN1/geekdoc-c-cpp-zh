and finally the desired list of long words. These intermediate lists have to be allocated in memory, then garbage-collected, which is not free.

In Section 10.4, we discussed a possible approach to avoid this problem: Replace a pipeline of higher-order functions with a single fold. You might recall that this change did not improve code readability. In the case of longWords, it is even worse:

```
def longWords(lines: List[String], min: Int): List[String] =
  lines.foldRight(List.empty[String]) { (line, words) =>
    line.split(' ').foldRight(words) { (word, moreWords) =>
      val cleanWord = clean(word)
      if cleanWord.length >= min then cleanWord :: moreWords else moreWords
    }
  }
```

Don't bother trying to understand this function. It is here to show you that the problem can indeed be solved by using foldRight, but the resulting code is difficult to read—certainly much harder than the flatMap/map/filter variant.

A better strategy that avoids the intermediate lists is to keep using flatMap, map, and filter, but on streams instead of lists:

```
def longWords(lines: List[String], min: Int): List[String] =
  lines.to(LazyList)
    .flatMap(_.split(' '))
    .map(clean)
    .filter(_.length >= min)
    .toList
```

The initial list of lines is converted into a stream. Because streams are lazily evaluated, calls to flatMap, map, and filter do not trigger any computation, and in particular, do not create intermediate lists. The final call to toList forces an evaluation of the last stream and produces the desired list without allocating any intermediate list.

This approach is particularly popular in Java, where the Stream class implements all the necessary higher-order methods but collections like List do not. You would write the longWords function in Java as follows:

```
List<String> longWords(List<String> lines, int min) {
  return lines.stream()
    .flatMap(line -> line.replace(' ', '\n').lines())
    .map(word -> clean(word))
    .filter(word -> word.length() >= min)
    .toList();
}
```