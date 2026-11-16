

可以使用以下内容，允许 ANT 从构建脚本中编译 Java 代码：

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

使用类路径引用，以便可以在其他地方定义许多不同的库和代码文件。

以下标记用于创建 JAR 文件：

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

请注意，可以包含 <manifest> 标记来指定主类和依赖库。<fileset> 标记指定将放入 JAR 文件的文件。destfile 属性是 <jar> 标记创建的 JAR 文件的名称和位置。

以下内容可用于对 JAR 文件进行签名：

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

signjar.keystore 在任务开始和结束时都会被删除，以确保即使在运行签名 JAR 任务时出现错误，它也会被移除。<genkey> 标记创建密钥库，<signjar> 标记使用密钥库对 JAR 文件进行签名。这些标记运行随 JDK 提供的命令行工具。

最后，以下标记可用于将文件、文件夹和其他 ZIP 文件（例如其他 Java 库）添加到已创建的 JAR 文件中。

```
<jar update="true" destfile="lib/${ant.project.name}.jar">
    <fileset dir="src"/>
    <fileset dir="res"/>
    <zipfileset src="res/gamelib.jar"/>
</jar>
```

在创建默认脚本并扩展它们以向 JAR 文件添加其他资源时，此标记非常有用。

## 构建可扩展的构建脚本

创建可用作起点的可扩展脚本是一个漫长的过程，但值得付出努力。<import> 标记用于在构建脚本中包含其他脚本。

```
<import file="toinclude.xml"/>
```

在包含的脚本顶层定义的任何属性都无法被覆盖，因此请确保在包含另一个脚本之前设置任何属性。

在通用构建脚本中将第三方库定义为属性可能会很有帮助。

```
<property name="junit.lib"
         location="${common.home}/../3rd/JUnit/junit-4.5.jar"/>
```

通用脚本中的每个默认目标都分为两个目标。例如，clean 目标定义如下：

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

请注意，clean 目标依赖于空的 project-clean 目标。这种结构允许替换默认目标，或在自定义目标之前和之后执行它。

与属性不同，目标可以被覆盖。将使用同名的最后定义的目标，而属性则使用给定的第一个值。如果三个不同的文件都定义了同一个目标，则使用最后定义的目标。要调用先前定义的目标，可以使用项目名称来引用被覆盖的目标。例如，如果名为 common 的项目定义了名为 clean 的目标，则可以始终使用 common.clean 访问该目标。

要覆盖默认的 clean 目标，请定义一个同名的新目标。

```
<project name="build">
<import file="common.xml"/>
<target name="clean">
</target>
</project>
```

前面的示例覆盖了 clean 目标，完全替换了它。如果需要定义一个在默认 clean 目标之前运行但不替换它的自定义标记，则覆盖默认 clean 标记所依赖的 <project-clean> 标记。

```
<project name="custom" default="clean">
<import file="common.xml"/>
<target name="project-clean">
<echo>Runs before default</echo>
</target>
</project>
```

前面的示例覆盖了 project-clean 标记，它将在 common clean 标记之前执行。

之前解释的项目名称语法可用于引用默认 clean 标记。此功能可用于将默认标记定义为被覆盖标记的依赖项，以便自定义标记在 common 标记之后运行。

```
<project name="custom">
    <import file="common.xml"/>
    <target name="clean" depends="common.clean">
        <echo>Runs after default</echo>
    </target>
</project>
```

此示例覆盖了 clean 目标，但由于它依赖于 common.clean 目标，自定义 clean 将在默认目标之后运行。

这三种选项使得可以以任意数量的方式扩展脚本。

- 替换目标——创建一个同名的新目标。
- 默认后自定义——使用 depends="projectname.target" 语法。
- 默认前自定义——覆盖 project-target 标记。

ANT 无法覆盖属性，因此一个简单的技巧是在目标中而不是在构建脚本顶部定义默认属性。只要在调用目标之前设置属性，就可以覆盖默认属性。

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

目标中使用的所有属性——compile.srcdir、compile.destdir、compile.debug 和 compile.classpath——在目标运行之前都不会被设置。如果包含通用脚本的构建脚本在调用任务之前定义了这些属性之一，那么在设置目标属性时，该属性将已经存在。

以下是一个可扩展构建脚本的示例，您可以将其作为构建未来游戏项目的起点。

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

