> > **TIP:** To see the rounds, run the `javac` command with the `-XprintRounds` flag:

```
    Round 1:
        input files: {rect.Point, rect.Rectangle,
            rect.SourceLevelAnnotationDemo}
        annotations: [sourceAnnotations.ToString]
        last round: false
    Round 2:
        input files: {sourceAnnotations.ToStrings}
        annotations: []
        last round: false
    Round 3:
        input files: {}
        annotations: []
        last round: true
```

This example demonstrates how tools can harvest source file annotations to produce other files. The generated files don't have to be source files. Annotation processors may choose to generate XML descriptors, property files, shell scripts, HTML documentation, and so on.

> > **NOTE:** Some people have suggested using annotations to remove an even bigger drudgery. Wouldn't it be nice if trivial getters and setters were generated automatically? For example, the annotation

```
    @Property private String title;
```

> > could produce the methods

```
    public String getTitle() { return title; }
    public void setTitle(String title) { this.title = title; }
```

> > However, those methods need to be added to the same class. This requires editing a source file, not just generating another file, and is beyond the capabilities of annotation processors. It would be possible to build another tool for this purpose, but such a tool would go beyond the mission of annotations. An annotation is intended as a description *about* a code item, not a directive for adding or changing code.

# ## 8.7 Bytecode Engineering

You have seen how annotations can be processed at runtime or at the source code level. There is a third possibility: processing at the bytecode level. Unless annotations are removed at the source level, they are present in the class