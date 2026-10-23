

序列化其内容。这只有在所有内容都是可序列化的情况下才有效。如果你尝试在这里运行这段代码，你会发现它会抛出一个异常。

```
import java.io._

class OtherData(val id:String,val course:String)
class Student(val name:String,val grades:Array[Int],val od:OtherData) extends Serializable

object Main {
    def main(args:Array[String]) {
        val oos = new ObjectOutputStream(new FileOutputStream("fail.bin"))
        val s = new Student("John",Array(98,90),new OtherData("0123","CS2"))
        oos.writeObject(s)
        oos.close()
    }
}
```

异常的详细信息如下所示。

```
java.io.NotSerializableException: OtherData
```

这段代码的问题在于 od:OtherData 是 Student 的一个成员，但它不可序列化。因此，当序列化过程处理到 od 成员时，它就会失败。在这种情况下，只需让 OtherData 扩展 Serializable 就能很容易地修复它。在其他情况下你可能无法控制这种类型，因为你处理的可能是由其他人编写的类型，并且不可序列化。

处理不可序列化信息的一种方法是简单地不将其写入。还有其他情况下这种方法也是有效的。例如，DrawRectangle 类型保存 propPanel 变量，这样用户每次查看设置时就不会每次都新建一个图形用户界面（GUI）组件。然而，如果你保存一个 DrawRectangle，就没有必要保存与 GUI 组件相关联的所有信息。这些信息可以从其他信息中轻松重建。为了在 Scala 中实现这一点，我们使用一个注解。

注解由一个普通的名称指定，该名称前面有一个 @。注解为程序提供元信息。也就是说，这些信息供更高级别的工具使用，并不是真正属于正常程序代码的一部分。Scala 编译器的一部分是一些标准注解。你可以在 API 中通过它们以小写字母开头来识别它们。与序列化相关的两个注解是 @transient 和 @SerialVersionUID。如果你有一个类中的成员不想被序列化，只需用 @transient 对其进行注解。这里我们有这段代码已经这样做了 od。

```
import java.io._

class OtherData(val id:String,val course:String)
class Student(val name:String,
              val grades:Array[Int],
              @transient val od:OtherData) extends Serializable

object Main {
    def main(args:Array[String]) {
        val oos = new ObjectOutputStream(new FileOutputStream("pass.bin"))
        val s = new Student("John",Array(98,90),new OtherData("0123","CS2"))
```

```
oos.writeObject(s)
oos.close()

val ois = new ObjectInputStream(new FileInputStream("pass.bin"))
ois.readObject() match {
  case s2:Student => println(s2.name+" "+s2.grades+" "+s2.od)
  case _ => println("Unknown type read.")
}
ois.close()
}
```

这段代码还将对象读回并打印不同的字段。这是为了说明当你读取一个具有 transient 字段的序列化对象时会发生什么。那个字段不是序列化的一部分，所以当对象被读回时，该字段会被赋予默认值。对于 AnyRef 的任何子类型，默认值都是 null。运行这段代码会显示你，最后打印的值确实是 null。

另一个注解 @SerialVersionUID 用于为类型附加版本号。这样做是为了当你加载回一个对象时，可以将保存版本的版本号与加载版本的版本号进行比较，以确保它们相同。Java 会自动为你生成这些，但它们几乎每次类型代码更改时都会改变。这会导致保存的文件损坏，即使它们仍然可以正常工作。为了防止这种情况，你可以考虑在类型声明之前放置此注解，后跟一个数字 ID 的参数。

这对你的编程的含义是，任何 transient 的东西通常必须是一个 var 而不是一个 val。这是因为当你反序列化这样的对象时，该成员将具有一个默认值，而该默认值几乎肯定需要被更改。另一方面，使用任何 transient 成员的地方可能需要有条件代码来在它们未正确设置时初始化值。这正是我们在所做的 Drawable 类型中对 propPanel 所做的。如果该字段被频繁访问，你应该考虑使用一个仅通过方法访问的私有局部 var。这里是遵循该规则的 Student 的一个替代版本。

```
class Student(val name:String,
    val grades:Array[Int],
    @transient private var lod:OtherData) extends Serializable {
  assert(lod!=null)
  def od : OtherData = {
    if(lod==null) {
      lod = new OtherData("012345","Default")
    }
    lod
  }
}
```

你可以用代码中的这个版本替换它，你就不会在打印输出中得到 null 了。这是因为现在对 s2.od 的引用是对将会在成员 lod 未被分配时创建一个默认值的方法的调用。

## 自定义序列化

默认序列化在许多情况下都很棒。然而，对于某些类型来说，它可能非常低效。此外，可能存在你确实需要为成员存储信息的情况，即使它不可序列化。出于这个原因，可以覆盖默认实现并使用自己的自定义序列化。

要覆盖默认实现，你实现私有方法 writeObjects(oos:ObjectOutputStream) 和 readObjects(ois:ObjectInputStream)。在这两个方法中你首先要做的是分别调用 oos.defaultWriteObject() 和 ois.defaultReadObject()。这将写入或读入应属于默认序列化的一部分的所有信息。即使没有要序列化的字段，你仍然需要调用它。之后你写入或从流中读取。这里是 Student 使用这种方法的示例。

```
class Student(val name:String,
    val grades:Array[Int],
    @transient private var lod:OtherData) extends Serializable {
  assert(lod!=null)
  def od = lod
  private def writeObject(oos:ObjectOutputStream) {
    oos.defaultWriteObject()
    oos.writeUTF(od.id)
    oos.writeUTF(od.course)
  }
  private def readObject(ois:ObjectInputStream) {
    ois.defaultReadObject()
    lod = new OtherData(ois.readUTF,ois.readUTF)
  }
}
```

lod 成员仍然是一个私有 var。它必须是私有的，因为它是一个 var。它必须是一个 var，因为 readObject 中的行对其进行了赋值。外部代码通过 od 方法访问该值。请注意，在这种情况下该方法更简单，因为它不需要检查 lod 的值。

这可能看起来像一个愚蠢的例子，但找到自定义序列化的实际用途并不难。碰巧 java.awt.image.BufferedImage 类我们在第 12 章中介绍过，它不可序列化。这种类型使用得相当频繁，你可能会发现如果它能用对象写入会很有帮助。以下演示了你如何做到这一点。

```
class Painting(val name:String,
    // ...
    @transient private var lImg:BufferedImage) extends Serializable {
  assert(lImg!=null)
  def img = lImg
  private def writeObject(oos:ObjectOutputStream) {
    oos.defaultWriteObject()
    oos.writeInt(img.getWidth)
    oos.writeInt(img.getHeight)
    oos.writeInt(img.getType)
    for(i <- 0 until img.getWidth; j <- 0 until img.getHeight) {
      oos.writeInt(img.getRGB(i,j))
```

```
}
}
private def readObject(ois:ObjectInputStream) {
  ois.defaultReadObject()
  val (w,h,t) = (ois.readInt(),ois.readInt(),ois.readInt())
  lImg = new BufferedImage(w,h,t)
  for(i <- 0 until w; j <- 0 until h) {
    lImg.setRGB(i,j,ois.readInt())
  }
}
}
```

这段代码首先写入图像的宽度、高度和类型，然后跟随所有红、绿、蓝（RGB）像素值。当读取回一个对象时，首先读取前三个值，然后创建图像，然后读取图像的其余部分。

## 22.4.3.2 XML 序列化

Java 的默认序列化带有二进制格式的标准优点和限制。此外，它仅适用于在 Java 虚拟机（JVM）下运行的程序。这不仅包括 Java 和 Scala，还包括许多其他语言。它不包括所有语言。C 和 C++ 是没有 JVM 实现的语言的典型代表。还有一些情况，你不需要二进制格式的好处，而更希望 XML 的可移植性和可读性。

没有内置的方法将对象转换为 XML 或将其取回，但你可以相当容易地将这种功能添加到自己的代码中。为此，我们将对我们想要能够序列化的每个类遵循三条相当简单的规则。

- 在类中放置一个 toXML : scala.xml.Node 方法，该方法返回一个包含你想要为这些对象保存的所有信息的 XML 元素。
- 包含一个伴生对象，其中有一个 apply(node:scala.xml.Node) : Type 方法，该方法反序列化 XML 节点并返回你创建的类型的一个对象。
- 使所有被序列化的字段都成为类的参数。

如果你在类型中始终如一地这样做，当一个类型包含对另一个类型的引用时，你可以简单地在该类型上调用 toXML。⁶ 你可以使用 scala.xml.XML 中的常规方法从文件读取 XML 或将其写回文件。

## 压缩流

如果你在计算机上花费了大量时间或从互联网下载文件，很可能在某个时候你遇到过 ZIP 文件。Windows® 中的压缩文件使用这种格式。它允许你将许多文件组合成一个，并且对于某些文件，特别是存储文本数据的文件，它使它们变得更小

