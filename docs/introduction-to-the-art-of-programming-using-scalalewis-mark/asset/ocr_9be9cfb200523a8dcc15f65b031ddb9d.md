```
```
def apply(p: DrawTransform, data: xml.Node) = {
  val ret = new DrawTransform(p, TransformType((data\"@type\").text.toInt),
    (data\"@values\").text.split(\":\").map(_.toDouble))
  data.child.filter(cxml => cxml match {
    case e: xml.Elem => true
    case _ => false
  }).map(cxml => makeDrawable(ret, cxml)).foreach(ret.addChild)
  ret
}
```
```

The Enumeration for the type of transformation was moved into the companion object to eliminate problems it might cause with serialization. The `subnodes` member is left out of the argument list because when we deserialize a transform, the `Drawables` under it need to have it as their parent. For this reason, we have to instantiate a complete transform that does not yet have children, then make the children and add them to the transform. This is all handled by methods in the companion object. Lastly, the `drawing_=` method implemented here not only sets the local value, it also recursively sets the values on all the subnodes.

With these changes in place, you now have the ability to make whatever drawings you wish and save them off in one of three styles, then load them back in. In practice you would likely choose between the binary serialization and XML serialization methods as few applications would need to support both.

# 22.6 End of Chapter Material

# 22.6.1 Summary of Concepts

+   - The `java.io` package contains quite a few useful types. There are four extended type hierarchies rooted in `InputStream`, `OutputStream`, `Reader`, and `Writer`. The first two have operations for reading and writing bytes. The second two operate on characters. We previously saw how to use `scala.io.Source` and `java.io.PrintWriter` for text access so this chapter focuses mainly on the two stream hierarchies.
+   - The `InputStream` and `OutputStream` classes are both abstract. Their subtypes come in two general forms, those that actually specify a source or sink for reading or writing, and those that modify the manner or functionality of reading and writing. The `FileInputStream` and `FileOutputStream` are of the former types. They provide stream behaviors attached to files.
+   - Exceptions are a way of dealing with unexpected conditions or other errors in code. When something goes wrong, an exception can be thrown. It is then up to the code that called the function where the error occurred to figure out what to do about it.
+     - Exception handling is done through the `try-catch` expression. Code that might fail is put in a `try` block. The `catch` partial function has cases for the different exceptions the coder knows how to handle at that point.
+     - When an exception is thrown, it immediately begins to pop up the call stack