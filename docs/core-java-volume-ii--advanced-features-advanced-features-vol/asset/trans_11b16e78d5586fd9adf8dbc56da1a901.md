
```java
public static void main(String[] args) throws ReflectiveOperationException
{
    var belgium = new Country("Belgium", 30510);
    var analyzer = new ObjectAnalyzer();
    System.out.println(analyzer.toString(belgium));
}
```

现在编译这两个模块和演示程序：

```bash
javac com.horstmann.util/module-info.java \
    com.horstmann.util/com/horstmann/util/ObjectAnalyzer.java
javac -p com.horstmann.openpkg/module-info.java \
    v2ch09.openpkg/com/horstmann/places/*.java
java -p v2ch09.openpkg:com.horstmann.util -m v2ch09.openpkg/com.horstmann.places.Demo
```

程序将因异常而失败：

```text
Exception in thread "main" java.lang.reflect.InaccessibleObjectException:
    Unable to make field private java.lang.String com.horstmann.places.Country.name
accessible: module v2ch09.openpkg does not "opens com.horstmann.places" to module
com.horstmann.util
```

当然，在纯粹的理论上，违背封装并窥探对象的私有成员是不对的。但对象关系映射或XML/JSON绑定这类机制非常普遍，模块系统必须支持它们。

使用`opens`关键字，模块可以*打开*一个包，从而允许对给定包中所有类的实例进行反射访问。下面就是我们的模块需要做的：

```java
module v2ch09.openpkg
{
    requires com.horstmann.util;
    opens com.horstmann.places;
}
```

经过这个修改，`ObjectAnalyzer` 就能正确工作。

模块可以被声明为`open`，例如：

```java
open module v2ch09.openpkg
{
    requires com.horstmann.util;
}
```

开放模块在运行时授予对其所有包的访问权限，就像所有包都被声明为`exports`和`opens`一样。然而，在编译时只能访问显式导出的包。开放模块将模块系统的编译时安全性与经典的宽松运行时行为结合在了一起。

回顾卷I第5章，JAR文件除了类文件和清单外，还可以包含*文件资源*，这些资源可以使用`Class.getResourceAsStream`方法加载，现在也可以使用`Module.getResourceAsStream`。如果资源存储在模块中与某个包匹配的目录中，那么该包必须向调用者开放。其他目录中的资源以及类文件和清单，任何人都可以读取。

**注意：** 举一个更实际的例子，我们可以将`Country`对象转换为XML或JSON。Java 9和10包含了用于XML转换的`java.xml.bind`模块。该模块已从Java 11中移除（连同`java.activation`、`java.corba`、`java.transaction`、`java.xml.ws`和`java.xml.ws.annotation`模块）。这些模块包含的包也是Jakarta EE（以前称为Java EE）规范的一部分，该规范中的API比Java SE中的更全面。如果JDK中存在冲突的包，企业应用服务器就无法模块化。不幸的是，在本书写作时，还没有XML绑定的模块化替代品。

不过，如果从源代码构建，JSON-B实现会提供模块化JAR文件。希望在你读到本文时，这些JAR文件能出现在Maven Central中。将JAR文件放到模块路径上，然后运行`com.horstmann.places.Demo2`程序。当`com.horstmann.places`包被开放时，转换为JSON的操作就会成功。

**注意：** 未来的库可能会使用*变量句柄*而非反射来读写字段。`VarHandle`类似于`Field`。你可以使用它来读取或写入某个特定类的任意实例的特定字段。然而，要获得`VarHandle`，库代码需要一个`Lookup`对象：

```java
public Object getFieldValue(Object obj, String fieldName, Lookup lookup)
        throws NoSuchFieldException, IllegalAccessException
{
    Class<?> cl = obj.getClass();
    Field field = cl.getDeclaredField(fieldName);
    VarHandle handle = MethodHandles.privateLookupIn(cl, lookup)
            .unreflectVarHandle(field);
    return handle.get(obj);
}
```

只要`Lookup`对象是在有权访问该字段的模块中生成的，这种做法就有效。模块中的某个方法只需调用`MethodHandles.lookup()`，该方法会生成一个封装调用者访问权限的对象。这样，一个模块就可以授予另一个模块访问私有成员的权限。实际问题是如何以最少的麻烦授予这些权限。

### 9.8 自动模块

现在你已经知道如何使用Java平台模块系统了。如果从全新项目开始，自己编写所有代码，你可以设计模块、声明模块依赖，并将应用程序打包为模块化JAR文件。

然而，这是一种极其罕见的情况。几乎所有项目都依赖第三方库。当然，你可以等到所有库的提供者将它们变成模块，然后再对自己的代码进行模块化。

但如果你不想等待呢？Java平台模块系统提供了两种机制，用于跨越当前前模块化世界与完全模块化应用之间的鸿沟：*自动模块*和*未命名模块*。

为了迁移，你可以将任何JAR文件变成模块，只需将它放到模块路径中的某个目录而不是类路径中。模块路径上没有`module-info.class`的JAR文件被称为*自动模块*。自动模块具有以下属性：

- 1. 该模块隐式包含`requires`子句，要求所有其他模块。
- 2. 它的所有包都被导出和开放。
- 3. 如果JAR文件清单`META-INF/MANIFEST.MF`中有键为`Automatic-Module-Name`的条目，则该条目的值将成为模块名称。
- 4. 否则，模块名称从JAR文件名获取，去掉末尾的版本号，并将非字母数字字符序列替换为点。

前两条规则意味着，自动模块中的包的行为方式与它们在类路径上时相同。使用模块路径的原因是为了其他模块的利益，使它们能够表达对此模块的依赖。

例如，假设你正在实现一个处理CSV文件并使用Apache Commons CSV库的模块。你希望在`module-info.java`文件中表明你的模块依赖于Apache Commons CSV。

如果将`commons-csv-1.5.jar`放到模块路径中，那么你的模块就可以引用这个模块。它的名称是`commons.csv`，因为尾部的版本号`-1.5`被移除，非字母数字字符`-`被替换为点。

这个名字可能是一个可接受的模块名，因为Commons CSV广为人知，其他人不太可能尝试将同一名称用于不同的模块。但更好的是，这个JAR文件的维护者能尽快同意保留一个反向DNS名称，最好是顶层包名`org.apache.commons.csv`作为模块名。他们只需在JAR内的`META-INF/MANIFEST.MF`文件中添加一行`Automatic-Module-Name: org.apache.commons.csv`。最终，希望他们能通过添加带有保留模块名的`module-info.java`将JAR文件变为真正的模块——所有使用该名称引用CSV模块的其他模块将继续正常工作。

**注意：** 通向模块化的迁移计划是一场伟大的社会实验，没有人知道它是否会以好的结果告终。在将第三方JAR放入模块路径之前，请检查它们是否为模块化；如果不是，检查它们的清单是否有模块名。如果没有，你仍然可以将JAR变成自动模块，但要准备好稍后更新模块名。

在本书写作时，Commons CSV JAR文件的1.5版本既没有模块描述符，也没有自动模块名。尽管如此，它在模块路径上也能正常工作。你可以从 https://commons.apache.org/proper/commons-csv 下载该库。解压缩并将`commons-csv-1.5.jar`文件放入`v2ch09.automod`模块的目录中。该模块包含一个简单的程序，用于读取带有国家数据的CSV文件：

```java
package com.horstmann.places;

import java.io.*;
import org.apache.commons.csv.*;

public class CSVDemo
{
   public static void main(String[] args) throws IOException
   {
      var in = new FileReader("countries.csv");
      Iterable<CSVRecord> records = CSVFormat.EXCEL.withDelimiter(';')
            .withHeader().parse(in);
      for (CSVRecord record : records)
      {
         String name = record.get("Name");
         double area = Double.parseDouble(record.get("Area"));
         System.out.println(name + " has area " + area);
      }
   }
}
```
