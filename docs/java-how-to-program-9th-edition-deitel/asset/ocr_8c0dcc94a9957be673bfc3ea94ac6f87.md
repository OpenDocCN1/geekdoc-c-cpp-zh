where PathToJnlpJarFile includes both the path and the file name jnlp.jar. For example, on our Windows Vista computer, the PathToJnlpJarFile is

```
"C:\Program Files\Java\jdk1.6.0_11\sample\jnlp\servlet\jnlp.jar"
```

# Packaging the Applet for Use with Java Web Start

To package the applet for use with Java Web Start, you must create a JAR file that contains the applet’s code and the jnlp.jar file. To do so, use the command

```
jar cvf LoadImageAndScale.jar *.class PathToJnlpJarFile
```

where PathToJnlpJarFile includes both the path and the file name jnlp.jar. This will place all the .class files for the applet and a copy of the jnlp.jar file in the new JAR file LoadImageAndScale.jar.

# JNLP Document for LoadImageAndScale Applet

The JNLP document in Fig. 24.2 is similar to the one introduced in Fig. 23.12. The only new feature in this document is that the resources element (lines 10–14) contains a second jar element (line 13) that references the jnlp.jar file, which is embedded in the file LoadImageAndScale.jar.

```
1 <?xml version="1.0" encoding="UTF-8"?>
2 <jnlp codebase="file:." href="LoadImageAndScale.jnlp">
3 
4   <information>
5     <title>LoadImageAndScale Applet</title>
6     <vendor>Deitel</vendor>
7     <offline-allowed/>
8   </information>
9 
10  <resources>
11    <java version="1.6+"/>
12    <jar href="LoadImageAndScale.jar" main="true"/>
13    <jar href="jnlp.jar"/>
14  </resources>
15 
16  <applet-desc
17    name="LoadImageAndScale"
18    main-class="LoadImageAndScale"
19    width="400"
20    height="300">
21  </applet-desc>
22 </jnlp>
```

Fig. 24.2 | JNLP document for the LoadImageAndScale applet.

# Making the Applet Draggable Outside the Browser Window

The HTML document in Fig. 24.3 loads the applet into a web browser. In this example, we use an applet element to specify the applet’s class and provide two param elements between the applet element’s tags. The first (line 4) specifies that this applet should be draggable. That is, the user can hold the Alt key and use the mouse to drag the applet outside the browser window. The applet will then continue executing, even if the browser is