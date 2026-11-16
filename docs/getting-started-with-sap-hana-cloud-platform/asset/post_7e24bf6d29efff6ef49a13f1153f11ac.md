
${sap.cloud.sdk.version} property we used to obtain the target version of the Java EE 6 API. By not hard-coding this value, we can easily pass our project off to other developers who might need to configure a different version matrix.

Normally, you can adjust your user settings by editing the settings.xml file contained in the .m2 subfolder of your home directory. You can verify the exact path from within the Eclipse Preferences by expanding Maven • User Settings. From here, browse to the settings.xml file specified in the User Settings input field. Custom properties can be added by adding XML markup underneath the settings/profiles/profile/properties element in the XML.

Once all of the requisite project dependencies are defined, we can trigger a build from within Eclipse by right-clicking on the pom.xml file and choosing the Run As • Maven Install menu option, as shown in Figure 4.45.

![](img/cf7012644082c115a2181376d9b7486d_160_0.png)

Figure 4.45 Triggering a Maven Build in Eclipse

When you run this for the first time, you'll notice in the Console output that Maven carries out quite a few steps up front to pre-fetch needed plug-ins, libraries, and the like. Again, the great thing about Maven is that it's (generally) able to do all of this on its own.

### Using Maven from the Command Line

For admin types who prefer to run Maven from the command line, the build process essentially consists of two steps:

- 1. First, the admin needs to download the project folder from some source code repository (e.g., Git) to his or her local machine.
- 2. Once the source code is downloaded, the build can be kicked off by opening up a command prompt, navigating to the project folder, and entering the command mvn install, as shown in Figure 4.46. This, of course, assumes that some version of Maven has been installed on the user's local machine.

![](img/cf7012644082c115a2181376d9b7486d_161_0.png)

Figure 4.46 Running a Maven Build from the Command Line

## 4.4.2 Working with Apache Ant

Before Apache Maven came into prominence, the de facto build tool in the Java community was *Apache Ant*. To a large degree, Ant is a Java-based version of the popular make tool used to perform builds in the C/C++ communities. That is, Ant provides a runtime environment for executing build scripts.

In this section, we'll take a brief look at how such build scripts are constructed and how they're used to automate builds. For more information on the Apache Ant project, we would point you in the direction of the project documentation online at *http://ant.apache.org/*.

### Understanding the Ant Build Model

Unlike Maven, Ant makes no real assumptions about how a project is structured or how it is to be built. Instead, it provides us with an empty canvas that we can use to define each and every detail of a build: where source code is extracted from, how we invoke the Java compiler, how a Java archive file is built, and so on. Such details are specified in an XML build file called build.xml.

Listing 4.11 contains an example Ant build file that is used to build our sample project. Even if the exact syntax of the build file is new, you can generally gather what's going on in the file based on the descriptive XML element names. First, we specify various build properties, then we have a series of *targets*, which are basically executable steps within an Ant build file. Using the `depends` attribute of the `<target>` element, we can daisy-chain steps together to define the build sequence—for example, clean, then `init`, followed by `compile`, and then finally `dist`.

```
<project name="Example4_01" default="dist" basedir=".">
<!-- Set global properties for this build -->
<property environment="env" />
<property name="src.dir" location="src" />
<property name="classes.dir"
location="WebContent/WEB-INF/classes" />
<property name="lib.dir" location="WebContent/WEB-INF/lib" />
<property name="war.dir" location="WebContent" />
<property name="cloud.host" value="hanatrial.ondemand.com" />
<property name="app.name" value="example401" />

<path id="class.path">
<fileset dir="${env.HCP_SDK_HOME}/repository/plugins">
<include name="**/*.jar" />
</fileset>
<fileset dir="${lib.dir}">
<include name="**/*.jar" />
</fileset>
</path>

<target name="init" depends="clean">
<tstamp/>
<mkdir dir="${classes.dir}" />
</target>

<target name="compile" depends="init"
description="Compile the source files">
<!-- Compile the java code from ${src} -->
<javac srcdir="${src.dir}" destdir="${classes.dir}">
<classpath refid="class.path" />
</javac>
</target>

<target name="dist" depends="compile"
description="Generate the WAR file">
<!-- Create the WAR file -->
<jar jarfile="${ant.project.name}.war"
basedir="${war.dir}" />
</target>

<target name="clean" description="Clean up previous builds">
<!-- Cleanup prior builds -->
<delete dir="${classes.dir}" />
</target>
...
</project>
```

Listing 4.11 An Example Ant Build File

The targets themselves are defined using a series of Ant tasks that carry out the steps needed to perform a particular build task. Looking at the excerpt contained in Listing 4.11, you can see that we're using a number of standard Ant tasks to add and remove directories, compile Java code, and build the final WAR file. Ant provides most of the major tasks you would need for a typical build out of the box. However, if you need a more customized task, then you can either create your own or utilize the exec task to call out to an external program or script.

When working with SAP HCP application builds, this task provides us with the hooks we need to invoke Console Client commands, for example.

As you play around with Ant, you'll find that it's generally possible to define a basic template for the build.xml file that merely has to be tweaked a bit each time you reuse it (e.g., different project names, different archive files, etc.). Such a copy-and-paste approach might not be quite as convenient as Maven, but it sure beats having to rewrite the build script from scratch each time out.

### Triggering Builds

Much like we observed with Maven, Ant builds can be triggered from within the Eclipse IDE or via the command line. Within Eclipse, you can trigger a build by right-clicking on your build.xml file and selecting the Run As • Ant Build menu option. From the command line, you simply need to navigate to the directory where the build.xml file is contained and execute the ant command.

## 4.5 Continuous Integration with Jenkins

The next step in the evolution of software logistics is continuous integration (CI). As the name suggests, CI is about streamlining the integration process and avoiding the costly rework associated with integration conflicts. In effect, CI forces developers to address such conflicts up front so that integration problems get resolved well before they spiral out of control.

In practice, CI is implemented using a tool that monitors the project's source code repository (e.g., Git). Whenever changes are checked into the repository, the CI tool will react by automatically building and testing the application. If the build or test fails, then the associated developer(s) will be notified straightaway, and any integration conflicts that show up can be resolved in short order. Such instantaneous feedback ensures that the project doesn't stray too far off course over time.

In this section, we'll take a brief look at how you can implement CI within the context of your SAP HCP application development using one of the more popular CI tools in the Java development space: Jenkins.

### 4.5.1 Introducing Jenkins

Jenkins (formerly known as Hudson) is an open-source CI tool written in Java. In addition to performing the core CI tasks described earlier in this section, Jenkins also comes equipped with many value-add features, including the following:

- Integration with many code quality analysis tools
- Extensive reporting capabilities that project managers can use to track the overall health of software projects
- Integration with test tools and the capacity for performing test coverage analysis
- A robust job scheduler tool
- External integration via REST APIs

Plus, with its wide following in the software community, there's a vast number of useful plug-ins to make it easy to connect with various SCM tools, build tools, and so on. You can find out more information about these features and others via the project website at http://jenkins-ci.org. Another useful resource here is Jenkins: The Definitive Guide (Smart, O'Reilly, 2011).

### 4.5.2 Installing Jenkins on SAP HCP

For the most part, Jenkins is very easy to install and configure. Indeed, if all you're doing is performing a local installation, then you can download the appropriate installation package from the project website and be up and running in a matter of minutes. However, when it comes to installing Jenkins on SAP HCP, matters become slightly more complicated. This is because Jenkins is designed to store the various artifacts it creates at the file system level. Because we don't have access to a file system from within SAP HCP, a workaround is required to allow Jenkins to operate smoothly on SAP HCP.

Fortunately, SAP has provided just such a workaround and uploaded it to GitHub so that developers can create an SAP HCP-compatible Jenkins distribution. The solution effectively reroutes any file-based I/O to the Document Service that we'll be covering in Chapter 6. You can find more information about this project online at https://github.com/SAP/cloud-jenkins. There, in addition to the project source code, you'll also find a link to an excellent blog post on SCN written by the lead developer on the project (the great Mr. Stephan Weber).
