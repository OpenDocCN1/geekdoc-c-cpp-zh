# 164 Introduction to Programming and Problem-Solving Using Scala

# Listing 6.2: CommonNames.scala

```
import io.StdIn.

val linesInFile = 324133 //43858
```

```
// Define shortened name for the tuple that represents each line
type NameData = (String, String, Int, Int, Int)
```

```
// This function parses a line of text from the file to a NameData
def parseLine(line:String):NameData = {
val parts = line.split(",")
(parts(0), parts(1), parts(2).toInt, parts(3), parts(4).toInt)
}
```

```
// Read the contents of the file and parse all the lines
a Array
val lines = Array.fill(linesInFile)(readLine)
val data = lines.map(parseLine)
```

```
// Function to find the most common names in aa Array
def commonNames(nameData:Array[NameData]):Array[NameData] = {
val maxTimes = nameData.map(_5).max
nameData.filter(_5==maxTimes)
}
```

```
// Find the year that data has been read
val years = data.map(_3).distinct
```

```
// Find most common female and male names
val femaleNames = years.flatMap(nd => nd._2=="F" && nd._3==year))
val maleNames = years.flatMap(nd => nd._2=="M" && nd._3==year))
commonNames(data)
```

```
// Output the results
femaleNames.forEach(println)
maleNames.forEach(println)
```

You can pick a particular file and adjust the value of linesInFile and run it to see it work.

# 6.8 End of Chapter Material

# 6.8.1 Problem Solving Approach

Despite the length of this chapter, no new valid statement types were introduced. Instead, a significant amount of flexibility was added in what you might do with the existing statement types. In particular, you can now use expressions with collection types and call methods on those collection types. You also learned that types themselves can be more complex with type parameters.