
How is Maven able to achieve this? Unlike other build automation tools, the basic unit of configuration in Maven is not a build script. Instead, Maven utilizes a special XML configuration file called a Project Object Model file (or POM file). Within a POM file, our goal is to build a conceptual model of our project. Here, we can specify (among other things) the following:

- A unique identifier for the project, complete with the target version number
- Descriptive details about the project, the involved participants, and so on
- Defined dependencies to other projects or libraries

Noticeably absent here are low-level build details, such as which folder to copy source code from, compilation details, and so on.

The reason we can (generally) avoid having to specify these details is because Apache Maven subscribes to the motto of “convention over configuration.” This is to say that it’s rather opinionated about how builds are supposed to work. For example, rather than forcing developers to specify where source code resides each and every time, Maven conventionally assumes that source code resides in the SRC/MAIN directory underneath the project root folder. Of course, these rules aren’t set in stone; Maven will allow you to override such settings if you absolutely want to. However, the more we play along, the more Maven is able to intuit build details on our behalf.

Another major advantage of following convention is that it allows us to leverage a wide array of plug-ins developed within the community to perform specific tasks. Besides the more obvious compile and archive plug-ins, we can find useful plug-ins to generate project documentation, capture source code metrics, and execute unit tests. Within the SAP HCP development space, SAP provides a Maven plug-in that can be used to invoke Console Client commands from within a help build. You can view details about this plug-in online at https://help.hana.ondemand.com/mavenSite/index.html.

Ultimately, the use of Maven leads to consistency in project maintenance. Projects take on a similar look and feel, and this generally makes it easier for developers to navigate through the project artifacts and find what they’re looking for. From an administrative standpoint, Maven takes a lot of the guesswork out of project builds. Admins don’t have to manipulate build scripts, download shared libraries, or do any sort of up-front prep work, because Maven is generally able to handle these tasks on its own. Even if admins don't know anything about the project they might be building, they can generally build it in a matter of seconds by simply typing in the command `mvn install` at their command prompt.

## Working with Maven in Eclipse

Although Apache Maven is a standalone tool that can be downloaded and run from the command line, for SAP HCP development we'll generally prefer to interact with it from within the Eclipse IDE. If you followed along with the IDE installation instructions described in Chapter 2, then you should find that Maven is included with your Eclipse installation.

The Maven plug-ins in Eclipse allow you to create Maven projects in one of two ways. You can either create a Maven project from scratch or you can convert an existing project into a Maven project after the fact. Which approach you take in the course of your normal development is a matter of preference. However, because most SAP HCP tutorials are predicated on the use of the Eclipse Dynamic Web project, we thought it would be more beneficial to demonstrate how to convert existing projects since that will be the more typical scenario. The steps are as follows:

- 1. Select the project you wish to convert, right-click on it, and select the CONFIGURE • CONVERT TO MAVEN PROJECT menu option, as shown in Figure 4.42.
- 2. This will open the Create New POM dialog box shown in Figure 4.43. Here, you must enter your Maven “project coordinates” by specifying the group/artifact ID and version number. Collectively, these attributes uniquely identify your project within the Maven repository. This in turn allows other projects to create defined dependencies to your project down the line. Aside from these key attributes, you need to specify the packaging type and provide a meaningful name for your project. As you can see in Figure 4.43, we selected the packaging type WAR, because we're converting a Dynamic Web project that will ultimately generate a WAR file.
- 3. Once all of the POM details are specified, click on the Finish button to complete the project conversion process.

![](img/cf7012644082c115a2181376d9b7486d_156_0.png)

Figure 4.42 Converting an Eclipse Project to a Maven Project: Part 1

![](img/cf7012644082c115a2181376d9b7486d_156_1.png)

Figure 4.43 Converting an Eclipse Project to a Maven Project: Part 2

After the dust settles on the project conversion process, you'll notice that not much has changed from an Eclipse perspective. Indeed, the only real visible difference within the PROJECT EXPLORER view is the addition of a file called pom.xml. This is, not surprisingly, the project's POM configuration file. We'll look into the contents and purpose of this file in further detail in the next section.

## Maintaining the Maven POM File

By default, the POM file generated by Eclipse is insufficient for building the project. Indeed, as you can see in Listing 4.9, aside from some build-specific details derived via the Maven plug-in, there's not much there.

```
<project xmlns=...>
<modelVersion>4.0.0</modelVersion>
<groupId>Example4.0</groupId>
<artifactId>Example4.0</artifactId>
<version>0.0.1-SNAPSHOT</version>
<packaging>war</packaging>
<name>HCP Book :: Chapter 4 :: Example 1</name>
<build>
...
</build>
</project>
```

Listing 4.9 An Excerpt of the Generated pom.xml File

Notably absent in the generated POM file are the project dependencies. For instance, in our example, we're building a Dynamic Web project based on the Java Servlet and SLF4J APIs. In order to build our project, we need to tell Maven where to go to find the corresponding libraries.

To add these dependencies to our POM, we can either use the graphical editor provided on the Dependencies tab or key in the appropriate XML markup in the pom.xml source code. For the purposes of our demonstration, we chose the former approach, as shown in Figure 4.44. Here, in the SELECT DEPENDENCY dialog box, simply plug in the coordinates of the project or library you wish to define a dependency for, to specify the scope of the dependency (provided in this case), and click on the OK button. Listing 4.10 shows the finished product for our sample project.

![](img/cf7012644082c115a2181376d9b7486d_158_0.png)

Figure 4.44 Adding Dependencies to the POM

```
<project...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>Example04_01</groupId>
    <artifactId>Example04_01</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    ...
    <dependencies>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>2.1.7</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>com.sap.cloud</groupId>
            <artifactId>neo-javaee6-wp-api</artifactId>
            <version>${sap.cloud.sdk.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <configuration>
                    <webXml>WebContent\\WEB-INF\\web.xml</webXml>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

Listing 4.10 Revised POM File with Dependency Definitions

## Understanding the Maven Repository Concept

Looking at the POM file contained in Listing 4.10, you might be wondering where we came up with the precise group/artifact IDs and versions. Unfortunately, this is not an exact science and requires a little bit of explanation.

Historically, one of the challenges of implementing automated builds has been figuring out how to keep track of library dependencies. Developers have traditionally had to come up with clever ways of attaching library folders to their projects so that they'd be available at build time.

In keeping with the "convention over configuration" motto, Maven defines such dependencies in more abstract terms. Because every project in Maven defines within its POM a unique project ID, Maven can use these coordinates to create a library index within its global repositories. At build time, the group/artifact ID and version specified in `<dependency>` elements provide Maven with a key for fetching the specified libraries from a remote repository and seamlessly incorporating them into the build.

At configuration time, we can use this same information to scan through the Maven repositories and search for the libraries we need to specify our project dependencies. One useful site for performing such searches is www.mvnrepository.com. This site provides a flexible search engine that allows you to search for libraries using group/artifact IDs and even free-form text descriptions.

In order to increase portability even further, you can adjust your user settings file attached to your Maven installation to include custom properties, such as the
