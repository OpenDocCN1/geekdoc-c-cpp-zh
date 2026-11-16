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
```