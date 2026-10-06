```
QPointF[] points0 = new QPointF[numPoints];
QPointF[] points1 = new QPointF[numPoints];
for (int x = 0; x < numPoints; x++) {
  points0[x] = new QPointF(x, Math.random() * 100);
  points1[x] = new QPointF(x, Math.random() * 100);
}
```

The rest of the code is the same as before.

In some cases, when classes are wrapped, the generator produces code that uses QNativePointer. This type is a wrapper for C++ "value type" and works for both pointers and arrays. The file mjb_nativepointer_api.log specifies any for generated code that uses QNativePointer. The Qt Jambi documentation recommends replacing any code that uses QNativePointer and provides step-by-step instructions for how to do this.

Sometimes we will need to include additional import declarations in the .java files. This is easily achieved using the <extra-includes> tag, and is fully described in http://doc.trolltech.com/qtjambi-4.3.2_01/com/trolltech/qt/qtjambi-typesystem.html.

The Qt Jambi generator is a powerful and versatile tool for making C++/Qt classes seamlessly available to Java programmers, and makes it possible to combine the strengths of C++ and Java in a single project.