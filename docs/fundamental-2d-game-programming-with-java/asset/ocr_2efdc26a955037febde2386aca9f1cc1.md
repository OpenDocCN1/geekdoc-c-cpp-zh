Each default target in the common script is split into two targets. For example, the clean target is defined as follows:

```
<target name="clean" depends="project-clean">
<echo>Deleting project directory structure...</echo>
<delete dir="${common.bin}"/>
<delete dir="${common.lib}"/>
<delete dir="${common.docs}"/>
<delete dir="${common.juni}"/>
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
<include file="common.xml"/>
<target name="project-clean">
<echo>Runs before default</echo>
</target>
</project>
```