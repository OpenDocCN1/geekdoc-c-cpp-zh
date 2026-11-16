
If the full path to the resource is path/to/file.txt, then both ClassLoader and Class can load it. But because Class can also load files relative to itself, Class needs a / at the beginning of the path if the path is absolute.

```
ClassLoader - "path/to/file.txt"
Class - "/path/to/file.txt"
```

If the / is left off the beginning path for the Class, the resource will not be found because it will look relative to itself instead of at the root directory. There is another problem when Class is used. The normal way to get the class object is to use the getClass() method. This can work just fine:

```
getClass().getResourceAsStream( "resource" );
```

However, the problem with the getClass() method is that it will always return the deepest child class, even in the parent class. If the deepest subclass is created in a different package, then the resource loaded in the parent will no longer be found. To prevent this from happening, the static class should be used when relative resource loading is used. This will work no matter what subclasses are created.

```
ClassName.class.getResourceAsStream( "resource" );
```

The ClasspathResources example, located in the javagames.filesandres package, demonstrates the different ways to load a resource. Remember to create the resources.jar file and manually add it to the classpath so the resources are available at runtime.

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

## MAKING A RESOURCE LOADER UTILITY

Although loading resources from inside JAR files is great for a deployed application, it is terrible during the development process. If every time there is a change in resource files, and a new JAR file must be created and added to the classpath before the change can be testing, development must be very slow. Luckily, there are many ways to deal with loading resources from the classpath during development:

- Add the JAR file to the classpath. Not only is it a pain to keep rebuilding and deploying a new JAR every time changes are made, any resources inside the JAR cannot be changed.

- Add the resources folder to the classpath. This is better, but the folder structure of the resource folder and the JAR file must match. Also, I have used this method but forgotten to add the folder when setting up a new project and had trouble figuring out the problem.

- Load resources from both the file system and the classpath. This requires extra code to try loading the resource from two different places, but there is no setup required in the project to make it work.

For the purposes of this book, the third option is used because it doesn't require any additional setup in the development environment.

The following ResourceLoader class, located in the javagames.util package, is used to load resources from both the classpath and the file system.

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

The ResourceLoaderExample code, located in the javagames.filesandres package, uses the ResourceLoader to load files from both the file system and the classpath. Make sure to adjust the file paths in the example to match the file system on your system.

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

## EXPLORING JAVA PROPERTIES

Java contains a very helpful class for dealing with simple name-value pair properties. The Properties class can read in a file containing lines with name-value pairs. The Properties class is available from the System object for system-wide properties, but any property class that has been created can be used.

```
name1=value1
name2=value2
```

The PrintSystemProperties example, located in the javagames.filesandres package, prints out all the system property values and then highlights some useful system properties.

```
package javagames.filesandres;
import java.util.Properties;

public class PrintSystemProperties {
    public static void main( String[] args ) {
        Properties system = System.getProperties();
    }
}
```
