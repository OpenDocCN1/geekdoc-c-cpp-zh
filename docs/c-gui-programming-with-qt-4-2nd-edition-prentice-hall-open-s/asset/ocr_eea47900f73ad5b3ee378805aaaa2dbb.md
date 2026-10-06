The key to influencing the generator works is what we put in the XML file we give it. For example, if we have multiple inheritance in C++, one straightforward way to handle this in Qt Jambi is to identify just one of the classes as an "object type" or "value type" in the system, and identify all the others as "interface types".

It is also possible to provide more natural method signatures. For example, instead of using an ArrayList<QPointF> to pass the points for a curve, it would be nicer to pass a QPoint array. This involves hiding the original C++ method and replacing it with a Java method that accepts a QPoint[] and calls the original C++ method behind the scenes. We can achieve this by modifying the jambiplotter.xml file. We originally declared the C++ Plotter type with an entry like this:

```
<object-type name="Plotter" />
```

We will replace the preceding line with a more sophisticated version:

```
<object-type name="Plotter">
  <modify-function
    signature=setCurveData(int,constVector&lt;QPointF&gt;&amp;)
    access modifier="private" />
    <rename to="setCurveData_private />
  </modify-function>
  <inject-code>
    public final void setCurveData(int id, com.trolltech.qt.core.QPoint points[]) {
      setCurveData_private(id, java.util.Arrays.asList(points));
    }
  </inject-code>
</object-type>
```

In the <modify-function> element, we rename the C++ setCurveData() method to setCurveData_private() and change its access specifier to private, thereby preventing access to it from outside the class's own methods. Notice that we must escape XML's special characters '<', '>', and '&' in the signature attribute.

In the <inject-code> element, we implement a custom setCurveData() method in Java. This method accepts a QPointF[] argument and simply calls the private setCurveData_private() method, converting the array to the list that the C++ method expects.