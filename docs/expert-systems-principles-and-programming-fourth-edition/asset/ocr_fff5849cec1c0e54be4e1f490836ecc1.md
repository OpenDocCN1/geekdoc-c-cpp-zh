it is also a class of the superclass the AKO points to. Another way of expressing this is that an AKO points from a **subclass** to a class. The link **ARE** is sometimes used for AKO where ARE are read as the ordinary word “are.”

The objects in a class have one or more **attributes** in common. Each attribute has a **value**. The combination of attribute and value is a **property**. For example, a blimp has attributes of size, weight, shape, and color. The value of the shape attribute is ellipsoidal. In other words, a blimp has the property of an ellipsoidal shape. Other types of links may also be found in semantic nets. The **IS-A** link define a value. For example, whatever aircraft the President is on is Air Force One. If the President is on a helicopter, then Air Force One IS-A helicopter. The **CAUSE** link expresses causal knowledge. For example, hot air CAUSES a balloon to rise.

Since the Goodyear Blimp is a blimp and blimps have ellipsoidal shape, it follows that the Goodyear Blimp is ellipsoidal. The duplication of one node’s characteristics by a descendant is called **inheritance**. Unless there is more specific evidence to the contrary, it is assumed that all members of a class will inherit all the properties of their superclasses. For example, balloons have a round shape. However, since the blimp class has a link pointing to the ellipsoidal shape, this takes precedence. Inheritance is a useful tool in knowledge representation because it eliminates the need to repeat common characteristics. Links and inheritance provide an efficient means of knowledge representation since many complex relationships can be shown with a few nodes and links. Later on we will discuss the object-oriented capabilities of CLIPS using its embedded language called COOL. You can write expert systems in rules, objects, or a combination of rules and objects with true multiple inheritance.

# 2.5 OBJECT-ATTRIBUTE-VALUE TRIPLES

One problem with using semantic nets is that there is no standard definition of link names. For example, some books use IS-A for both generic and individual relationships. The IS-A is then used in the sense of the ordinary words “is a” and is also used for AKO.

Another common link is HAS-A, which relates a class to a subclass. The HAS-A points opposite to the AKO and is often used to relate an object to a part of the object. For example,

```
car HAS-A engine
car HAS-A tires
car IS-A ford
```

More specifically, the IS-A relates a value to an attribute while a HAS-A relates an object to an attribute.

The three items of object, attribute, and value occur so frequently that it is possible to build a simplified semantic net using just them. An **object-attribute-value triple (OAV)**, or **triplet**, can be used to characterize all the knowledge in a semantic net and was used in the expert system MYCIN for diagnosing infectious diseases. The OAV triple representation is convenient for