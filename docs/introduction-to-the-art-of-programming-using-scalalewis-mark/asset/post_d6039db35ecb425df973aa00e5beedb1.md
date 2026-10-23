
This is what is happening to cause our error, and it happens when zero test or assignment grades or only one quiz grade have been entered.

If we have no test or assignment grade, the normal average will return 0.0/0, as the sum is the Double 0.0 and the length is the Int 0. If the list of quiz grades only has one element, then that one is the minimum. So the function returns (x-x)/(1-1) where x is the one grade as a Double. Clearly that is going to be a NaN. So how do we fix this? We need to make the average and the averageDropMin functions a bit smarter so that they have special cases in the instances when they should not do division. We can do this by putting if expressions in both.

```
def average(nums:Double*):Double =
    if(nums.isEmpty) 0 else nums.sum/nums.length
```

```
def averageDropMin(nums:Double*):Double =
    if(nums.isEmpty || nums.tail.isEmpty) 0 else
    (nums.sum-nums.min)/(nums.length-1)
```

If you use these versions of the functions things should work well.

Now to the functional alternative. The imperative version uses three var declarations outside of the function. These declarations can be seen by anything in the script that follows them. We typically refer to this as the GLOBAL SCOPE. For small scripts this might not be a problem, but you do not want to get into the habit of making things global. Anything that is global in a large program can be messed up by any line of code, making it very hard to track down certain types of errors. It is better to have our variables declared in a LOCAL SCOPE, inside of a function.

If we simply declare the variables inside of mainGrades, it will not work because when you make a recursive call, you get new versions of all of the local variables. Instead, we want to pass the three lists into the function as arguments. The arguments to a function act just like local val declarations except that the value is provided by the calling code. This new version will not include any var declarations, nor will it have any mutable values as everything is stored in immutable Lists. So other than the printing, it is completely functional. Here is what such a function might look like.

```
def mainGrades(tests:List[Double],assignments:List[Double],
    quizzes:List[Double]) {
printMenu
readInt() match {
    case 1 =>
        println("Enter a test grade.")
        mainGrades(readDouble() :: tests,assignments,quizzes)
    case 2 =>
        println("Enter a quiz grade.")
        mainGrades(tests,assignments,readDouble() :: quizzes)
    case 3 =>
        println("Enter an assignment grade.")
        mainGrades(tests,readDouble() :: assignments,quizzes)
    case 4 =>
        println("The average is "+courseAverage(tests,assignments,quizzes))
        mainGrades(tests,assignments,quizzes)
    case 5 =>
    case _ =>
        println("Unknown option. Try again.")
        mainGrades(tests,assignments,quizzes)
    }
}
```

Instead of mutating values, this version passes the newly built List into the recursive call where it is a completely new argument value for the next level down in the recursion. The options that do not change the Lists simply pass through the same values.

## 7.12 End of Chapter Material

### 7.12.1 Problem-Solving Approach

Despite the length of this chapter, no new valid statement types were introduced. Instead, a significant amount of flexibility was added in what you might do with the existing statement types. In particular, you can now use expressions with collection types and call methods on those collection types. You also learned that types themselves can be more complex with type parameters. You can make functions that take variable numbers of arguments and you can pass arguments into functions using pass-by-name.

### 7.12.2 Summary of Concepts

- Arrays and Lists are collections that allow us to store multiple values under a single name. They are sequences, meaning that the values have an order and each one is associated with an integer index. Indexes start at zero.
- Both can be created in a number of ways.
  - `Array(e1,e2,e3,...)` or `List(e1,e2,e3,...)` to make short collections where you provide all the values.
  - `new Array[Type](num)` will make an Array of the specified type with the specified number of elements. All elements will have a default value. This is the least common usage in Scala.
  - Use the `::` operator with Lists to append elements to the front and make a new List. Use `Nil` to represent an empty List.
  - `Array.fill(num)(byNameExpression)` will make an Array of the specified size with values coming from repeated execution of the specified expression. This will also work for Lists.
  - `Array.tabulate(num)(functionOnInt)` will make an Array with num elements with values that come from evaluating the function and passing it the index. Often function literals are used here. This will also work with List.
- Arrays have a fixed size and are mutable. Access and mutate using an index in parentheses: `arr(i)`.
- Lists are completely immutable, but you can efficiently add to the front to make new Lists. Can be accessed with an index, but using head and tail is typically more efficient.
- The Scala collections, including Array and List, have lots of methods you can call on to do things.
- There are quite a few basic methods that take normal values for arguments and give you back values, parts of collections, of locations where things occur.
- The real power of collections is found in the higher-order methods. The primary ones you will use are `map`, `filter`, and `foreach`.
- There are a handful of methods that give you back various pieces of collections, including combinatorial possibilities such as permutations and combinations.
- You can make the last parameter of a function accept a variable number of arguments, `var args`, by putting an asterisk after the type. The name given to that parameter functions as a sequence. To pass a real sequence into a function in place of a `var args` parameter, follow it with `: _*` to tell Scala you want that sequence as a `*` argument of some type.
- When two variables refer to the same object in memory we call them aliases.
- Mutable objects can cause problems with aliases because changes to the object can be made using any of the aliases and they will be reflected in all of them.
- By default, arguments in Scala are passed by-value. The value of the reference is passed into the function. This automatically makes an alias of the object. If you want to protect a mutable object from unintended changes when it is passed to a function you need to make a defensive copy.
- Scala also allows pass-by-name parameters. Instead of passing a value, these pass a chunk of code called a thunk that is evaluated every time the parameter is used.

### 7.12.3 Self-Directed Study

Enter the following statements into the REPL and see what they do. Try some variations to make sure you understand what is going on. Some of these are intended to fail. You should understand why.

```
scala> val arr = Array(1, 2, 3)
scala> arr(0)
scala> arr(1)
scala> arr(0) = 5
scala> arr.mkString(" ")
scala> val lst = List(2, 3, 5, 7, 11, 13, 17)
scala> lst.head
scala> lst.tail
scala> val bigArr = new Array[String](100)
scala> bigArr(0) = "A string"
scala> bigArr(1) = "Another string"
scala> bigArr(0).length
scala> bigArr(1).length
scala> val lst2 = 1 :: 2 :: 3 :: 4 :: 5 :: Nil
scala> lst.zip(lst2)
scala> lst.zipWithIndex
scala> val arr3 = Array.fill(5)(readLine())
scala> val lst3 = List.tabulate(20)(i => i*i)
scala> def printList(lst: List[Int]) = lst match {
  case h :: t =>
    println(h)
    printList(t)
case Nil =>
}
scala> printList(lst3)
scala> lst3.mkString(" ")
scala> lst3.map(i => math.sqrt(i))
scala> arr3.map(s => s.length)
scala> bigArr.filter(s => s!=null)
scala> arr.permutations.foreach(println)
scala> lst.sliding(4)
scala> def printWords(copies:Int,words:String*) {
         words.foreach(w => println(copies*w))
       }
scala> printWords(3,"Hi")
scala> printWords(2,"This","is","a","test")
scala> val numWords = lst.map(_.toString)
scala> printWords(4,numWords)
scala> printWords(4,numWords:_*)
scala> val arrAlias = arr
scala> arrAlias.mkString(" ")
scala> arr.mkString(" ")
scala> arrAlias(0) == 42
scala> arr.mkString(" ")
scala> def alterArray(a:Array[Int]) {
         a(0) = 99
         a(1) = 98
         a(2) = 97
       }
scala> alterArray(arr)
scala> arr.mkString(" ")
scala> def getIndex[A](index:Int,a:Array[A]):Option[A] = {
         if(index<a.length) Some(a(index)) else None
       }
scala> getIndex(1,arr)
scala> getIndex(4,arr)
scala> lst.find(_ == 5)
scala> lst.find(_ == 9)
scala> def recursiveWhile(cond: =>Boolean)(body: =>Unit) {
         if(cond) {
           body
           recursiveWhile(cond)(body)
         }
       }
scala> var i=0
scala> recursiveWhile(i<10) {
         println(i)
         i += 1
       }
```

### 7.12.4 Exercises

- 1. Think of as many ways as you can to make an `Array[Int]` that has the values 1-10 in it. Write them all to test that they work. The first two should be easy. If you work you can get at least three others knowing what has been covered so far.
