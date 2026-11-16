ANT_HOME\bin folder to the system path allows the ANT tool to be run from the command line. The ANT tool should also be integrated with most common IDEs, so feel free to use that environment.

The JAVA_HOME environment variable should point to the JDK so that ANT has access to the Java tools needed to compile source code. The online documentation for installing ANT will be the most correct and up-to-date, so it is recommended that you use that documentation as an installation guide. See the resources at the end of the chapter for more information.

# UNDERSTANDING THE FORMAT OF A BUILD SCRIPT

The build script has several tags. There's the project tag, which is the root tag for any build script. This tag has a name and optional basedir and default target attributes.

```
<project name="name" basedir="." default="default">
</project>
```

There are also target tags. A build script contains one or more targets, which is one step in the build process. Targets contain a name, a description, and an optional depends attribute, which is a comma-separated list of all the targets this target depends on. Before a target is run, all of its dependencies are run. Dependent targets run only once, regardless of the number of times they are referenced.

```
<target name="target-name" description="target description"
depends="list, separated, with, commas">
</target>
```

ANT scripts also contain properties. Properties have a name and either a value or location. If the location attribute is used, the location is converted to a valid file path. Properties, once defined, cannot be overridden. No matter how many times a property is defined, it will only ever have the first value it is set to. This is the cause of many issues when importing multiple build scripts.

```
<property name="name1" value="value1"/>
<property name="name2" location="location/one"/>
```

Properties are useful because they can be referenced by surrounding the property name with a dollar sign and curly braces. ${property.name} is expanded at runtime to the value of the property with the name property.name. This expansion can even happen inside xml attributes. ANT provides access to all the Java system properties with the same dollar sign syntax. ${os.name} expands to the same value as System.getProperty("os.name").