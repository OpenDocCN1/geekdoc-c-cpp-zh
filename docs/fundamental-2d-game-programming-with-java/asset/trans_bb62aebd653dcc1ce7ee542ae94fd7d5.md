

如果资源的完整路径是 path/to/file.txt，那么 ClassLoader 和 Class 都可以加载它。但因为 Class 还可以加载相对于自身的文件，如果路径是绝对路径，Class 需要在路径开头加上 /。

```
ClassLoader - "path/to/file.txt"
Class - "/path/to/file.txt"
```

如果 Class 的路径开头漏掉了 /，资源将找不到，因为它会相对自身查找，而不是在根目录下查找。使用 Class 时还存在另一个问题。获取类对象的常规方法是使用 getClass() 方法。这可以正常工作：

```
getClass().getResourceAsStream( "resource" );
```

然而，getClass() 方法的问题在于它始终返回最深层的子类，即使在父类中也是如此。如果最深层的子类是在不同的包中创建的，那么在父类中加载的资源将不再被找到。为了防止这种情况发生，在使用相对资源加载时，应该使用静态类。无论创建什么子类，这都有效。

```
ClassName.class.getResourceAsStream( "resource" );
```

位于 javagames.filesandres 包中的 ClasspathResources 示例演示了加载资源的不同方式。请记住创建 resources.jar 文件并手动将其添加到类路径中，以便资源在运行时可用。

```
package javagames.filesandres;

import java.io.*;

public class ClasspathResources {
	public ClasspathResources() {
	}

	public void runTest() {
		/*
		 * ClassLoader uses absolute path. There is
		 * NO '/' at the beginning of the path!
		 */
		System.out.println();
		System.out.println("**********************************");
		System.out.println("ClassLoader - Absolute Path");
		System.out.println();
		InputStream in = ClassLoader.getSystemResourceAsStream(
		        "javagames/filesandres/Test1.txt" );
		printResource( in );
		/*
		 * getClass() instead of class loader.
		 * Can be relative...
		 */
		System.out.println();
		System.out.println("**************************");
		System.out.println("getClass() - Relative path");
		System.out.println();
		in = getClass().getResourceAsStream( "Test2.txt" );
		printResource( in );
		/*
		 * getClass() can also use the absolute path,
		 * but it needs a '/' at the start of the path.
		 */
		System.out.println();
		System.out.println("**************************");
		System.out.println("getClass() - Absolute path");
		System.out.println();
		in = getClass().getResourceAsStream(
		        "/javagames/filesandres/Test3.txt" );
		printResource( in );
		/*
		 * Because getClass() always returns the subclass,
		 * if a subclass is created in another package,
		 * the relative path may not be correct.
		 * However, using an absolute path doesn't allow
		 * packages to be moved around. Use the static class,
		 * which also works in static methods.
		 */
		System.out.println();
		System.out.println("**************************");
		System.out.println("getClass() - Absolute path");
		System.out.println();
		in = ClasspathResources.class.getResourceAsStream( "Test3.txt" );
		printResource( in );
		/*
		 * Either ClassLoader or Class will return null
		 * for unknown resources
		 */
		in = getClass().getResourceAsStream( "fat/finger/mistake" );
		if (in == null ) {
		    System.out.println();
		    System.out.println( "**************************" );
		    System.out.println( "Got a null back!!" );
		}

		in = ClassLoader.getSystemResourceAsStream( "fat/finger/mistake" );
		if (in == null ) {
		    System.out.println( "Got another null back!!!" );
		}
	}

	private void printResource( InputStream in ) {
	    try {
	        InputStreamReader reader = new InputStreamReader( in );
	        BufferedReader buf = new BufferedReader( reader );
	        String line = null;
	        while ( (line = buf.readLine()) != null ) {
	            System.out.println(line);
	        }
	    } catch ( IOException e ) {
	        e.printStackTrace();
	    } finally {
	        try {
	            in.close();
	        } catch( Exception e ) { }
	    }
	}

	public static void main( String[] args ) {
	    new ClasspathResources().runTest();
	}
}
```

## 创建资源加载器实用程序

虽然从 JAR 文件内部加载资源对于已部署的应用程序很棒，但在开发过程中却很糟糕。如果每次资源文件发生更改，都必须创建新的 JAR 文件并将其添加到类路径中才能测试更改，那么开发速度将非常慢。幸运的是，在开发过程中处理从类路径加载资源有很多方法：

- 将 JAR 文件添加到类路径。不仅每次更改都要不断重新构建和部署新 JAR 很麻烦，JAR 内部的任何资源都无法更改。

- 将资源文件夹添加到类路径。这更好，但资源文件夹和 JAR 文件的文件夹结构必须匹配。此外，我使用过这种方法，但在设置新项目时忘记添加文件夹，导致难以排查问题。

- 同时从文件系统和类路径加载资源。这需要额外的代码来尝试从两个不同的位置加载资源，但无需在项目中进行任何设置即可工作。

出于本书的目的，使用第三种选项，因为它不需要在开发环境中进行任何额外设置。

以下位于 javagames.util 包中的 ResourceLoader 类用于同时从类路径和文件系统加载资源。

```
package javagames.util;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.InputStream;

public class ResourceLoader {
    public static InputStream load(
            Class<?> clazz, String filePath, String resPath ) {
        // try the resource first
        InputStream in = null;
        if( ( resPath == null ) || resPath.isEmpty() ) {
            in = clazz.getResourceAsStream( resPath );
        }

        if( in == null ) {
            // try the file path
            try {
                in = new FileInputStream( filePath );
            } catch( FileNotFoundException e ) {
                e.printStackTrace();
            }
        }

        return in;
    }
}
```

位于 javagames.filesandres 包中的 ResourceLoaderExample 代码使用 ResourceLoader 同时从文件系统和类路径加载文件。请确保调整示例中的文件路径以匹配您系统上的文件系统。

```
package javagames.filesandres;

import java.io.*;
import javagames.util.ResourceLoader;

public class ResourceLoaderExample {
    public ResourceLoaderExample() {
    }

    public void runTest() {
        Class<?> clazz = ResourceLoaderExample.class;
        // load absolute resource
        String filePath = "not/used*";
        String resPath = "javagames/filesandres/Test1.txt";
        InputStream in = ResourceLoader.load( clazz, filePath, resPath );
        printResource( in );
        // load relative resource
        filePath = "not/used*";
        resPath = "Test2.txt";
        in = ResourceLoader.load( clazz, filePath, resPath );
        printResource( in );
        // load absolute file path
        filePath = "C:/Book/res/assets/lib/javagames/filesandres/Test3.txt*";
        resPath = "not/available*";
        in = ResourceLoader.load( clazz, filePath, resPath );
        printResource( in );
        // load relative file path
        filePath = "res/assets/lib/javagames/filesandres/Test3.txt*";
        resPath = "not/available*";
        in = ResourceLoader.load( clazz, filePath, resPath );
        printResource( in );
        // error with both is null
        filePath = "fat/finger*";
        resPath = "fat/finger/too*";
        in = ResourceLoader.load( clazz, filePath, resPath );
        printResource( in );
    }
}

private void printResource( InputStream in ) {
    try {
        InputStreamReader reader = new InputStreamReader( in );
        BufferedReader buf = new BufferedReader( reader );
        String line = null;
        while ( (line = buf.readLine()) != null ) {
            System.out.println( line );
        }
    } catch( IOException e ) {
        e.printStackTrace();
    } finally {
        try {
            in.close();
        } catch( Exception e ) {}
    }
}

public static void main( String[] args ) {
    new ResourceLoaderExample().runTest();
}
}
```

## 探索 Java 属性

Java 包含一个非常有用的类来处理简单的名称-值对属性。Properties 类可以读取包含名称-值对行的文件。Properties 类可从 System 对象获取用于系统范围的属性，但可以使用任何已创建的属性类。

```
name1=value1
name2=value2
```

位于 javagames.filesandres 包中的 PrintSystemProperties 示例打印出所有系统属性值，然后突出显示一些有用的系统属性。

```
package javagames.filesandres;
import java.util.Properties;

public class PrintSystemProperties {
    public static void main( String[] args ) {
        Properties system = System.getProperties();
    }
}
```

