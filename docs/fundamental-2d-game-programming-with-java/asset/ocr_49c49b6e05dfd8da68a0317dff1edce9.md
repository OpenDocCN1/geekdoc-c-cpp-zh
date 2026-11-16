```
private int roll( int value, int min, int max ) {
if ( value < min )
return max;
if ( value > max )
return min;
return value;
}
private int getSelectedIndex( int row, int col ) {
return row * colCount + col;
}
@Override
protected AttractState getState() {
return new HighScore();
}
@Override
protected boolean shouldChangeState() {
return finished;
}
}
```

# CREATING A BUILD SCRIPT

Finally, the last file you need is a build script. This file imports the common.xml base script developed in Chapter 14, "Deployment with ANT." The common.classpath and jar.mainclass properties are both set before the common file is imported. Once the default JAR is created, the sound, images, and XML folders are added to the JAR so all of the resources are available from inside the JAR file, and the game consists of just that single file.

```
<?xml version="1.0" encoding="UTF-8"?>
<project name="complete-game" default="default">
<description>
Building Space Rocks
</description>
<property name="common.classpath" value="custom.classpath"/>
<property name="jar.mainclass"
value="javagames.completegame.CompleteGame"/>
<import file="res/assets/xml/common.xml"/>
<path id="custom.classpath">
<pathelement location="${basedir}/bin"/>
</path>
```