declaration. However, as declarations and bodies are separate constructs, it is permitted for a SPARK subprogram body to call a subprogram with a SPARK declaration even if the body of the called subprogram is not in SPARK.

It is up to you to mark the SPARK constructs of your program as such by specifying their SPARK mode. This is done using the SPARK_Mode pragma or SPARK_Mode aspect as appropriate. The SPARK mode can be explicitly set to either On or Off. If the SPARK mode of a construct is not mentioned at all, then its value is taken from some appropriate enclosing construct. For library level units, if the SPARK mode is not specified explicitly, it is taken to have the special value Auto. We describe the effect of automatic SPARK mode in Section 7.1.3.

You may not change the SPARK mode on a fine grained basis such as between different subexpressions of a single expression or between individual statements of a subprogram. Roughly, the SPARK mode setting can only be changed on the granularity of packages or subprograms. Specifically, there are six locations for which we can specify a SPARK mode:

+   - Immediately within or before a library-level package specification
+   - Immediately within a library-level package body
+   - Immediately following the **private** keyword of a library-level package specification
+   - Immediately following the **begin** keyword of a library-level package body
+   - Immediately following a library-level subprogram specification
+   - Immediately within a library-level subprogram body

If you desire for your entire program to be SPARK, you can change the default by specifying

```
pragma SPARK_Mode (On);
```

as a *configuration pragma* to your compiler. Such pragmas are used by the compiler to control various features of the entire compilation. The mechanism by which configuration pragmas are applied and the scope over which they operate is compiler specific. Should you use a configuration pragma to turn on SPARK mode for the entire program, you can still turn it off for specific parts of your program as necessary. The configuration pragma only changes the default, it does not prohibit you from creating a program that is a mixture of SPARK and non-SPARK code.

There are several important use cases that are supported. In this section we will examine some of these cases. In the examples that follow, we explicitly specify the SPARK mode. Later we will describe some important consistency rules on the way SPARK mode must be used and the effect of not specifying a SPARK mode explicitly.