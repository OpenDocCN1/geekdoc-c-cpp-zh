```
```scala
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
```

# 7.12.4  Exercises

+   1. Think of as many ways as you can to make an `Array[Int]` that has the values 1-10 in it. Write them all to test that they work. The first two should be easy. If you work you can get at least three others knowing what has been covered so far.