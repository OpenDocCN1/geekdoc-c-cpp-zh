A more significant example would be to rewrite the inputAndCount function using a match.

```
def inputAndCount(base:Int,func:(Int,Int)=>Int):(Int,Int) = readLine() match {
  case "quit" =>
    (base,0)
  case n =>
    val (s,c)=inputAndCount(base,func)
    (func(s,n.toInt),c+1)
}
```

Here the call to readLine is the argument to match. This is because there is not a standard recursive argument for this function. The decision of whether or not to recurse is based on user input instead. So the user input needs to be what we match on.

# 6.6 Putting it Together

Back to the theme park. Let’s take some of the functions we wrote previously, and put them to use in a recursive function that is part of a script that we could use at the front of the park where they sell admission tickets. The recursion will let us handle multiple groups paying for admission with any number of people per group. It will then add up all the admissions costs so we can get a daily total. In addition, it will keep track of the number of groups and people that come in. The code for this makes the same assumptions we made before about groups in regards to coolers and the water park.

```
def entryCost(age:Int, cooler:Boolean, waterPark:Boolean): Double = {
  (if(age<13 || age>65) 20 else 35) +
  (if(cooler) 5 else 0) +
  (if(waterPark) 10 else 0)
}
```

```
def individualAdding(num:Int, cooler:Boolean, waterPark:Boolean): Double = {
  if(num>0) {
    println("What is the persons age?")
    val age = readInt()
    entryCost(age, cooler, waterPark)+individualAdding(num-1, false, waterPark)
  } else 0.0
}
```

```
def groupSizeCost(): (Int,Double) = {
  println("How many people are in your group?")
  val numPeople = readInt()
  println("Is the group bringing a cooler? (Y/N)")
  val cooler = readLine()=="Y"
  println("Will they be going to the water park? (Y/N)")
  val waterPark = readLine()=="Y"
  (numPeople,individualAdding(numPeople,cooler,waterPark))
}
```

```
def doAdmission(): (Int,Int,Double) = {
  println("Is there another group for the day? (Y/N)")
```