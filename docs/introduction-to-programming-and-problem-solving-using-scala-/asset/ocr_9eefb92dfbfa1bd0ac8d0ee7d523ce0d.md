```
<course name="CSCI 1320">
  <student name="Quinn" name="Bender">
    <quizzes>98 100</quizzes>
    <tests>94</tests>
    <assignments>100</assignments>
  </student>
  <student name="Jason" name="Hughes">
    <quizzes>85 78</quizzes>
    <tests>67</tests>
    <assignments>20</assignments>
  </student>
</course>
```

Here all grades of the same type have been given as contents of elements with the proper names. This makes things much shorter and does not significantly increase the difficulty of parsing the grades. It does remove the flexibility of attaching additional information with each grade as the comments.

An alternate approach would be to not use attributes at all and store all the information in sub-elements. Doing that, one of the students might like the following:

```
<student>
  <fname>Jason</fname>
  <name>Hughes</name>
  <quiz><grade>85</grade></quiz>
  <quiz><grade>78</grade></quiz>
  <test><grade>67</grade></test>
  <assignment>
    <grade>20</grade>
    <comment>Code didn't compile.</comment>
  </assignment>
</student>
```

There is no definitive answer for which of these two styles you should use. What can be said definitively that attributes must be unique and generally have short text. You should not try to use attributes for things that would span multiple lines or need multiple values that would be challenging to break apart. A possible rule of thumb to follow is that anywhere you only have a single value that is, you should represent as an attribute. Anything that has multiple values or is long should be in sub-elements.

# 14.2 XML in Scala

XML is not part of the normal first semester in computer science, but Scala makes it so easy that there is no reason not to. To see this, simply go to the REPL and type in valid XML.

```
scala <tag>Some XML.</tag>
res0: scala.xml.Elem = <tag>Some XML.</tag>
```

The Scala language has a built-in XML parser that allows you to write XML directly into your code. You can see that the type of this expression is scala.xml.Elem.