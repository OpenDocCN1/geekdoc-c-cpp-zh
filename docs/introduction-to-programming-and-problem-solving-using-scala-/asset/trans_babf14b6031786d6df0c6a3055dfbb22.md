

mkString - 可以带零、一个或三个参数调用。它根据元素的字符串表示构建一个单一的长字符串。如果没有提供任何参数，则元素之间将无任何内容。如果指定了一个参数，它应该是一个用于分隔元素的字符串。如果指定了三个参数，中间的那个是分隔符，第一个和最后一个是放在元素之前和之后的字符串。

```
scala = lst.mkString
res55: String = 746391
```

```
scala = lst.mkString(" ")
res56: String = 7; 6; 3; 9; 1
```

```
scala = lst.mkString("[", ", "]")
res57: String = "[7, 4, 6, 3, 9]"
```

patch - 这一强大的方法允许你生成新的序列，这些序列是从原始序列中移除并插入的。它接受三个参数：开始补丁的索引、要放入补丁的元素、以及要用补丁替换的元素数量。如果替换项为空集合，它将简单地移除指定数量的元素。如果给定的元素为 0，则它仅会在给定位置插入新元素。

```
scala = lst.patch(3,Nil,2)
res58: List[Int] = List(7, 4, 6, 1)
```

```
scala = lst.patch(3,List(10,11,12),0)
res59: List[Int] = List(7, 4, 6, 10, 11, 12, 3, 9, 1)
```

```
scala = lst.patch(3,List(10,11,12),3)
res60: List[Int] = List(7, 4, 6, 10, 11, 12)
```

reverse - 接受参数并按反序产生一个新的集合。

```
scala = lst.reverse
res61: List[Int] = List(1, 9, 3, 6, 7)
```

toArray - 不接受参数，并根据当前集合中的元素创建一个指定类型的新集合。

```
scala = lst.toArray
res62: Array[Int] = Array(7, 4, 6, 3, 9)
```

zip(that:Iterable[B]) - 接受另一个集合作为参数，并产生一个元组集合，其中第一个元素来自此集合，第二个元素来自传入的集合。结果的为两者中较短的一个。

```
scala = lst.zip(lst.reverse)
res63: List[(Int, Int)] = List((7,1), (4,9), (6,3), (3,6), (9,4), (1,7))
```

```
scala = lst.zip(Array(1, 2, 3, 4))
res64: List[(Int, Int)] = List((7,1), (4,2), (6,3), (3,4))
```

# Scala 中的数组和列表

- zipIndex – 接受参数并产生一个新的元组集合，其中第一个是集合中的元素，第二个是它的索引。

```
scala> lst.zipIndex
res65: List[(Int,Int)] = List((7,0), (4,1), (6,2), (3,3), (9,4), (1,5))
```

上述列出的方法适用于任何类型的序列。因此，它们可以适用于 List[Int]、List[String] 或 Array[Double]。有少数方法对元素类型有特殊要求（需要某些操作），这些是 min、sum 和 product。min 和 max 方法适用于可以排序的类型。它们包含了 Int 和 Double，还包括许多其他类型，而这些类型中 sum 和 product 方法要求集合是数值类型。我们可以像这里这样直接调用 sum 或 product 方法。

```
scala> lst.sum
res66: Int = 30
```

```
scala> lst.product
res67: Int = 45
```

值必须是数值类型的限制意味着你不能使用 + 来连接它们。对于 List[String] 或 Array[String]，你应该使用 mkString 来连接这些值。

## 6.5.2 高阶方法

虽然你可能觉得这里展示的方法列表很长，且并赋予了我们许多能力，但所有这些方法都是通过为参数添加普通值来实现的。就像我们的第一个方法一样，通过添加一些抽象并使它们成为高阶方法，它们可以变得强大。下面列出了许多属于 List 或 Array 中的类型 B 的方法。再次，这些示例使用了 val lst = List(7,4,6,3,9)。

- count(p:(A)=>Boolean) – 接受一个作用于元素并返回布尔值的函数。返回集合中所有返回 true 的元素数量。

```
scala> lst.count(_ > 5)
res68: Int = 3
```

- dropWhile(p:(A)=>Boolean) – 产生一个新的集合，包含从第一个返回 false 的元素开始的所有元素。

```
scala> lst.dropWhile(_ < 3)
res69: List[Int] = List(3, 9, 1)
```

# 编程与问题解决简介

- exists(p:(A)=>Boolean) - 接受一个作用于元素并返回布尔值的函数。如果集合中某个元素使函数结果为 true，则其值为 true。

```
scala lst.exists(_ 5 == 0)
res70: Boolean = true
```

- filter(p:(A)=>Boolean) - 接受一个作用于元素并返回布尔值的函数。产生一个包含所有使函数返回 true 的元素的新集合。

```
scala lst.filter(_ < 5)
res72: List[Int] = List(3, 9, 1)
```

```
scala lst.filter(x > 4)
res73: List[Int] = List(7, 4, 6)
```

- filterNot(p:(A)=>Boolean) - 接受一个作用于元素并返回布尔值的函数。产生一个包含所有使函数返回 false 的元素的新集合。

```
scala lst.filterNot(_ < 5)
res75: List[Int] = List(7, 6)
```

```
scala lst.filterNot(_ > 7)
res76: List[Int] = List(3, 9, 1)
```

- flatMap(f:(A)=>Seq[B]) - 接受一个作用于元素并返回集合的函数。从所有函数返回的集合中构建一个新的集合。

```
scala lst.flatMap(n => if (n<6) n else Nil)
res78: List[Int] = List(7, 4, 6, 3, 9)
```

```
scala val str = "test"
scala lst.flatMap(str.take)
res79: List[Char] = List(t, e, s, t)
```

- forAll(p:(A)=>Boolean) - 接受一个作用于元素并返回布尔值的函数。如果集合中所有元素使函数结果为 true，则其值为 true。传入 flatMap 的返回类型实际上比 Seq[B] 更通用，但差别并不大。

```
scala lst.forall(_ > 2)
res80: Boolean = false
```

```
scala lst.forall(_ < 10)
res81: Boolean = true
```

- foreach(f:(A)=>Unit) – 接受一个作用于元素并应用于集合中所有元素的函数。返回类型为 Unit。此方法用于副作用。

```
scala lst.foreach(n=>println(n))
14
8
18
2
```

- indexWhere(p:(A)=>Boolean) - 接受一个作用于元素并返回布尔值的函数。返回第一个使函数返回 true 的元素的索引值。

```
scala lst.indexWhere(_ 2 == 0)
res82: Int = 1
```

```
scala lst.indexWhere(_ > 7)
res83: Int = 4
```

- lastIndexWhere(p:(A)=>Boolean) – 接受一个作用于元素并返回布尔值的函数。返回最后一个使函数返回 true 的元素的索引值。

```
scala lst.lastIndexWhere(_ 2 == 0)
res84: Int = 2
```

- map(f:(A)=>B) – 接受一个作用于元素并产生结果的函数。产生一个包含将函数应用于集合所有内容后的结果的新集合。

```
scala lst.map(_ + 1)
res85: List[Int] = List(8, 5, 7, 4, 10, 2)
```

```
scala lst.map(_ * 2)
res86: List[Int] = List(14, 8, 12, 6, 18, 2)
```

```
scala lst.map(i => i * i)
res87: List[Int] = List(49, 16, 36, 9, 81, 1)
```

