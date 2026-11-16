
You can use the following to allow ANT to compile Java code from a build script:

```
<path id="common.classpath">
<pathelement location="${basedir}/bin"/>
</path>
```

```
<javac
srcdir="${basedir}/src"
destdir="${basedir}/bin"
classpathref="common.classpath"
debug="on"
/>
```

The classpath reference is used so that many different libraries and code files can be defined elsewhere.

The following tag is used to create a JAR file:

```
<fileset id="jar.fileset" dir="bin">
<exclude name="**/Tests.class"/>
</fileset>
```

```
<jar destfile="lib/${ant.project.name}.jar">
<fileset refid="jar.fileset"/>
<manifest>
<attribute name="Main-Class" value="javagames.ant.HelloWorld"/>
<attribute name="Class-Path"
value="jar1-name jar2-name directory-name/jar3-name"/>
</manifest>
</jar>
```

Notice that you can include the <manifest> tag to specify the main class and dependent libraries. The <fileset> tag specifies which file will be placed in the JAR file. The destfile attribute is the name and location of the JAR file created by the <jar> tag.

The following can be used to sign a JAR file:

```
<delete file="signjar.keystore"/>
<genkey alias="${ant.project.name}"
validity="999999"
storepass="storepass"
keystore="signjar.keystore">
<dname>
<param name="CN" value="Tim Wright"/>
<param name="OU" value="Groovy Inc."/>
<param name="O" value="Planet Earth"/>
<param name="C" value="Milkyway"/>
</dname>
</genkey>
<signjar jar="lib/${ant.project.name}.jar"
         keystore="signjar.keystore"
         alias="${ant.project.name}"
         storepass="storepass"/>
<delete file="signjar.keystore"/>
```

The signjar.keystore is deleted both at the beginning and end of the task to make sure that it is removed even if there were errors running the sign JAR task. The <genkey> tag creates the keystore and the <signjar> tag uses the keystore to sign the JAR file. These tags run the command-line tools that come with the JDK.

Finally, the following tag can be used to add files, folders, and other ZIP files, such as other Java libraries, to an already created JAR file.

```
<jar update="true" destfile="lib/${ant.project.name}.jar">
    <fileset dir="src"/>
    <fileset dir="res"/>
    <zipfileset src="res/gamelib.jar"/>
</jar>
```

This tag is handy when creating default scripts and then extending them to add additional resources to JAR files.

## BUILDING AN EXTENDABLE BUILD SCRIPT

Creating an extendable script that can be used as a starting point is a lengthy process, but it can be worth the effort. The <import> tag is used to include other scripts in a build script.

```
<import file="toinclude.xml"/>
```

Any properties defined at the top level of the included script cannot be overridden, so be sure to set any properties before another script is included.

It can be helpful to define third-party libraries as properties in the common build script.

```
<property name="junit.lib"
         location="${common.home}/../3rd/JUnit/junit-4.5.jar"/>
```

Each default target in the common script is split into two targets. For example, the clean target is defined as follows:

```
<target name="clean" depends="project-clean">
<echo>Deleting project directory structure...</echo>
<delete dir="${common.bin}"/>
<delete dir="${common.lib}"/>
<delete dir="${common.docs}"/>
<delete dir="${common.junit}"/>
</target>
<target name="project-clean"/>
```

Notice that the clean target depends on the empty project-clean target. This structure allows for the default target to be replaced, or executed before and after a custom target.

Unlike properties, targets can be overridden. The last target defined with the same name will be used, unlike properties, which use the first value given. If three different files all define the same target, the last defined target is used. To call a previously defined target, you can use the project name to reference the overridden target. For example, if the project named common defines a target named clean, you can always access that target with the name common.clean.

To override the default clean target, define a new target with the same name.

```
<project name="build">
<import file="common.xml"/>
<target name="clean">
</target>
</project>
```

The previous example overrides the clean target, completely replacing it. If you need to define a custom tag that runs before the default clean target, but does not replace it, then override the <project-clean> tag that the default clean tag depends on.

```
<project name="custom" default="clean">
<import file="common.xml"/>
<target name="project-clean">
<echo>Runs before default</echo>
</target>
</project>
```

The previous example overrides the project-clean tag, which will be executed before the common clean tag.

The project name syntax explained previously can be used to reference the default clean tag. This feature can be used to define the default tag as a dependency to an overridden tag, so that the custom tag runs after the common one.

```
<project name="custom">
    <import file="common.xml"/>
    <target name="clean" depends="common.clean">
        <echo>Runs after default</echo>
    </target>
</project>
```

This example overrides the clean target, but since it depends on the common.clean target, the custom clean will run after the default target.

These three options make it possible to extend a script any number of ways.

- Replace a target—Create a new target with the same name.
- Custom after default—Use the depends="projectname.target" syntax.
- Custom before default—Override the project-target tag.

Overriding properties is not possible with ANT, so a simple trick is to define default properties in the target instead of at the top of the build script. As long as the properties are set before the target is called, the default properties can be overridden.

```
<target name="compile" depends="project-compile">
    <property name="compile.srcdir" value="${basedir}/src/${basedir}/test"/>
    <property name="compile.destdir" value="${basedir}/bin"/>
    <property name="compile.debug" value="on"/>
    <property name="compile.classpath" value="${common.classpath}"/>

    <echo>Compiling source code...</echo>
    <javac
        srcdir="${compile.srcdir}"
        destdir="${compile.destdir}"
        classpathref="${compile.classpath}"
        debug="${compile.debug}"
    />
</target>
```

All of the properties used in the target—compile.srcdir, compile.destdir, compile.debug, and compile.classpath—are not set until the target runs. If the build script including the common script was to define one of these properties before the task is called, that property would already exist when the target property is set.

The following is an example of an extendable build script that you can use as the starting point for building future game projects.

```
<?xml version="1.0" encoding="UTF-8"?>
<project name="common" basedir=".">
    <!-- This is the base script used for creating
    custom build scripts. -->
    <property name="common.home" file="${ant.file.common}"/>
    <property name="junit.lib"
        location="${common.home}/../3rd/JUnit/junit-4.5.jar"/>
    <property name="common.bin" value="${basedir}/bin"/>
    <property name="common.lib" value="${basedir}/lib"/>
    <property name="common.docs" value="${basedir}/docs"/>
    <property name="common.test" value="${basedir}/test"/>
    <property name="common.junit" value="${basedir}/junit"/>
    <property name="common.classpath" value="common.classpath"/>
    <path id="common.classpath">
        <pathelement location="${common.bin}"/>
    </path>
</project>
```

```
<!-- BUILD -->
------------------------------------------------------------
<!-- -->
<target name="build" description="Builds the project"
    depends="project-build, clean, init, compile, jar"/>
<target name="project-build"/>
```

```
<!-- INIT -->
------------------------------------------------------------
<!-- -->
<target name="init" depends="project-init">
    <echo>Creating project directory structure...</echo>
    <mkdir dir="${common.bin}"/>
```
