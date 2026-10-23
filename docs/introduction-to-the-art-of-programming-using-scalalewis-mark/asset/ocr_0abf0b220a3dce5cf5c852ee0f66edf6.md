# 16.1.4.5 The update Method

Having an apply method is sufficient for many situations. For example, it is all that is needed for immutable collections. It is also all we will want for our CourseSection class given how we have written it. However, it is not sufficient if you want to do something like an assignment into an Array. Basically, it looks things up, it does not change things. To do this, you use the update method. When Scala sees an expression like this

```
obj(args) = e
```

it converts it to a call of the form

```
obj.update(args,e)
```

So you can get assignments for indexing by simply implementing the proper update methods.

# 16.1.4.6 Overloading Methods

Methods can be overloaded. This means that you can have two different methods that have the same name as long as they take different numbers of arguments or different types of arguments. The ability to overload methods can come in handy, but it is something that you do not want to abuse as it can make it difficult for readers to understand what is going on or even make code ambiguous so that it does not compile. In the case of special methods, which have to have a particular name, overloading is the only way to make it so that you can get the desired functionality with different types.

To understand this, consider that you have a class that represents a grid of numbers, perhaps for a spreadsheet. This is a situation where it makes sense to use the apply method to get values out. However, there are several ways to refer to cells in a spreadsheet. The most obvious approach in a program would be to pass two Ints for the row and column. However, when you run a spreadsheet program it is common to refer to cells using letters for the column and numbers for the row. You might want to allow these to be passed in a String and an Int (e.g., "C", 13) or just a String (e.g., "C13"). With overloading you could write three different apply methods and update methods as shown here.

```
class Spreadsheet(rows:Int, columns:Int) {
  private val data = Array.fill(rows,columns)(0.0)

  def apply(c:Int, r:Int) : Double = data(r)(c)

  def update(c:Int, r:Int, v:Double) = data(r)(c)=v

  def apply(c:String, r:Int) : Double = data(r)(calcColumn(c))

  def update(c:String, r:Int, v:Double) = data(r)(calcColumn(c))=v

  def apply(cell:String) : Double = {
    val (c,r) = cell.partition(_.isLetter)
    data(r.toInt)(calcColumn(c))
  }

  def update(cell:String, v:Double) = {
    val (c,r) = cell.partition(_.isLetter)
    data(r.toInt)(calcColumn(c))=v
  }
}
```