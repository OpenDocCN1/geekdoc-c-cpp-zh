```
for( Object key : system.keySet() ) {
    System.out.println(
        key + "=" + system.getProperty( key.toString() )
    );
}

System.out.println();
System.out.println( "----- Some Cool Props -----" );
System.out.println( "java.version=" +
    System.getProperty( "java.version" ) );
System.out.println( "os.name=" + System.getProperty( "os.name" ) );
System.out.println( "user.country=" +
    System.getProperty( "user.country" ) );
System.out.println( "user.language=" +
    System.getProperty( "user.language" ) );
System.out.println();
System.out.println( "user.home=" + System.getProperty( "user.home" ) );
System.out.println( "user.dir=" + System.getProperty( "user.dir" ) );
System.out.println( "user.name=" + System.getProperty( "user.name" ) );
}
}
```

One of the reasons that the system properties are useful because Java includes the -D command-line flag, which lets system properties be defined on the command line. The format for the flag is -Dname=value. To set a command-line property, simply include as many -D flags as necessary. As shown in the following code snippet, when passing the flags, they cannot be placed at the very end for the command, because any text after the classname with a JAR name is passed as a string value to the main() method.

```
C:> java -Dname1=value1 -Dname2=value2 -jar CoolGame.jar
"Don't put the -D stuff here. It won't work."
```

The properties can be easily retrieved because the System class is available from anywhere. There are two methods for retrieving the property values:

```
String prop = System.getProperty( "name" );
String default = System.getProperty( "name", "default" );
```

The first method passes in only a property name, and if the property is not available, null is returned. The second method includes a default value that is returned if the property is not found. There is a catch to using properties: once they are set, they can still be overwritten. You must be careful when loading multiple property files and system properties, because the last property defined will erase previous property values.