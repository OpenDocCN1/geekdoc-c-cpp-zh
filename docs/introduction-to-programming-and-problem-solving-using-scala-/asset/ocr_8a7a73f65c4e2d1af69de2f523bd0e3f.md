# Arrays and Lists in Scala

ND,F,1910,Mary,85
ND,F,1910,Alice,61
ND,F,1910,Margaret,61
ND,F,1910,Helen,59
ND,F,1910,Anna,58
ND,F,1910,Florence,58
ND,F,1910,Gladys,50
ND,F,1910,Mildred,50
ND,F,1910,Myrtle,48
ND,F,1910,Ruth,47

You can see that each line has five values separated by commas. Those values are the state code (which should be the same for every given file), a letter for gender, the year, the name, and number of children that gender given in that year. What we want to be able to do is read in the entire file and answer some questions about the data in it. To make things more concrete, we want to find the most common name for males and females in each.

We know what we want to do, and we know what the data looks like. Now we need to take the array and break it into pieces that we can solve. One immediate way to break the problem is to think of reading the data and finding the common names in the data as separate problems.

# 6.7.1 Reading the Data

The problem of reading a large file data can be viewed as reading one piece and doing it many times. The only way that we currently know how read this data is with readline. That will read the file as a String. Once we have that, we need to break it up on the commas and get the pieces. There is a handy method on String split that can do exactly that. It delimits to split, and returns an Array[String]. The following function takes a line of text and returns a tuple of (String, String, Int, String, Int) with the data from that. That tuple type is going to be used a lot in this code, so we will use a type declaration to give it a shorter name.

```
type NameData = (String, String, Int, String, Int)
def parseline(line:String):NameData = {
  val parts = line.split(",")
  (parts(0), parts(1), parts(2).toInt, parts(3), parts(4).toInt)
}
```

To use this, we need to read all the lines from the file and then call that function on each line. The first part of that is nicely done with fill, and the second part is a perfect application of the map method, giving us code like the following.

```
val lines = Array.fill(4358)(readline)
val data = lines.map(parseLine)
```

The 'magic number' 4358 is the number of lines in the file for North Dakota this time we was. You should replace it with the proper number for whatever file we are reading in. We refer to this as a magic number because the way it appears in the code does not really tell us much about what it is. Such things often make hard to maintain, for that reason, it is generally advised that you created named constants instead of having magic numbers in your code shown here.