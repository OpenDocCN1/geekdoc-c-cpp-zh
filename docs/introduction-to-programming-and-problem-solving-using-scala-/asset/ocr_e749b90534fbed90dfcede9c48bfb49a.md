# 7.12.3 Self-Directed Study

Enter the following statements in the REPL and see what they do. Try some variations to make you understand what is going on. Some of these are intended to fail.
understand why.

```
scala val arr = Array(1, 2, 3)
scala arr(0)
scala arr(1)
scala arr(0) = 5
scala arr.mkString("")
scala val lst = List(2, 3, 5, 7, 11, 13, 17)
scala lst.head
scala lst.tail
scala val bigArr = new Array[String](100)
scala bigArr(0) = "A string"
scala bigArr(1) = "Another string"
scala bigArr(0).length
scala bigArr(2).length
scala lst2 = 1 : 2 :: 3 : 4 : 5 : Nil
scala lst.zip(lst2)
scala lst.zipWithIndex
scala val arr3 = Array.fill(5)(readLine())
scala val lst3 = List.tabulate(20)(i => i*i)
scala def printList(lst:List[Int]) = lst match {
case h::
println(h)
printList(h)
case Nil =>
}
scala scala printList(lst3)
scala lst3.mkString("")
scala lst3.map(i => math.sqrt(i))
scala arr3.map(s => s.length)
scala bigArr.permutations.foreach(println)
scala arr.permutations.foreach(s=>s!=null)
scala lst.sliding(4)
scala def printWords(copies:Int,String:*) {
words.foreach(w => println(copies*w))
}
scala scala printWords(3,"Hi")
scala scala printWords(2,"This","is","a","test")
scala val numWords = lst1.map(_toString)
scala scala printWords(4,numWords)
scala scala printWords(4,numWords::*)
scala val arrAliases = arr
scala arrAliases.mkString("")
scala arrAliases.mkString("")
scala arrAliases(0) = 42
scala arrAliases.mkString("")
scala scala def alterArray(a:Array[Int]) {
a(0) = 99
a(1) = 95
a(2) = 97
}
scala scala alterArray(arr)
```