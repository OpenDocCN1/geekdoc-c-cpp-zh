# Arrays and Lists in Scala

more generally useful. As you might recall from chapter 4, the best functions are the ones we can use in many situations. At this point, you might not reuse your functions, but it is good to keep that in mind so that we become nature later on. Here is the code for such a function:

```
def commonName(nameData:Array[NameData]):Array[NameData] = {
  val maxTimes = nameData.map(_.5).max
  nameData.filter(_.5 == maxTimes)
}
```

This function uses a map to get the name frequencies. What is that the .5 is doing as the frequency was the 5th column in the data and the 5th of the tuple. Then it calls max to get that largest frequency. The function ends by calling filter as we did not care about ties, and we only wanted one name with the maximum frequency, this could have been done more efficiently using reduceLeft as shown here:

```
def commonName(nameData:Array[NameData]):NameData = {
  nameData.reduceLeft((nd1,nd2) => if (nd1.5 > nd2.5) nd1 else nd2)
}
```

This is written, but will result in an array that has the largest frequency. Changing the > to >= or swapping the nd1 and nd2 in the comparison will result in the first of them instead of the last. We want to find all of them, so we will stick with the first version.

The task of finding all the years in the data file is fairly simple. You could look in the file and see what years are present, but we can easily get that from the data using a single line.

```
val years = data.map(_.3).distinct
```

This line uses map to pull out all the years, then a call to distinct to remove all the duplicate entries.

Once we have the years, another line can give us the most common female or male names. Here is the line giving the common female names.

```
val femaleNames = years.flatMap(year => 
commonNames(data.filter(_.2=="F" && _.3==year)))
```

This code does flatMap across all the years and for each year it calls our commonNames function that has been filtered to only females in the data.¹³ To understand why flatMap is used, we need to think about the variety of the expressions in this code. The commonNames function result in an Array[NameData]. Also, the year is an Array[Int]. If we used a regular map instead of a flatMap, the results would be an Array[Array[NameData]], where each subarray was a different year. There could be times when you want this, but in this case, we do not need it, and it is a bit harder to work with. So, we use flatMap to flatten that Array[Array[NameData]] to just an Array[NameData].

We can add a similar line for males along with some lines to print those final results, and we get a complete script that looks like following:

> ¹³There is a more efficient way to do this using a method called groupBy. We have not covered that method because it uses a type called Map that will not be introduced in this volume.