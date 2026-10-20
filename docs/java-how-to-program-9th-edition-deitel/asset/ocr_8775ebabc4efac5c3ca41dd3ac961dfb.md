window, change to the DrawTest directory, as you did in Section 23.2. Once in that folder, execute the following command:

```
jar cvf DrawTest.jar *.class
```

which creates in the current directory a JAR file named DrawTest.jar containing the applet’s .class files—DrawControls.class, DrawPanel.class and DrawTest.class. If the program had other resources, you’d simply add the file names or the folder names in which those resources are stored to the end of the preceding command. The letters cvf are command-line options to the jar command. The c option indicates that the command should create a new JAR file. The v option indicates that the command should produce verbose output so you can see the list of files and directories being included in the JAR file. The f option indicates that the next argument in the command line (DrawTest.jar) is the new JAR file’s name. Figure 23.11 shows the preceding command’s verbose output, which shows the files that were placed into the JAR.

```
added manifest
adding: DrawControls.class(in = 2611) (out= 1488)(deflated 43%)
adding: DrawPanel.class(in = 2703) (out= 1406)(deflated 47%)
adding: DrawTest.class(in = 1170) (out= 706)(deflated 39%)
```

Fig. 23.11 | Output of the jar command.

# 23.7.2 JNLP Document for the DrawTest Applet

Next, you must create a JNLP document that describes the contents of the JAR file and specifies which file in the JAR is the so-called main-class that begins the program’s execution. For an applet, the main-class is the one that extends JApplet (i.e., DrawTest in this example). For an application, the main-class is the one that contains the main method. A basic JNLP document for the DrawTest applet is shown in Fig. 23.12. We describe this document’s elements momentarily.

```
1 <?xml version="1.0" encoding="UTF-8"?>
2 <jnlp
3   codebase="PathToJNLPFile"
4   href="DrawTest.jnlp">
5 
6   <information>
7     <title>DrawTest Applet</title>
8     <vendor>Oracle Corporation</vendor>
9     <shortcut>
10      <desktop/>
11    </shortcut>
12    <offline-allowed/>
13  </information>
14 
15  <resources>
16    <java version="1.6+"/>
17    <jar href="DrawTest.jar" main="true"/>
18  </resources>
```

Fig. 23.12 | DrawTest.jnlp document for launching the DrawTest applet. (Part 1 of 2.)