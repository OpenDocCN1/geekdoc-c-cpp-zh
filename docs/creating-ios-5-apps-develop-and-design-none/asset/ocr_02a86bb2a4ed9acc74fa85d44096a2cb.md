# # SENDING MESSAGES TO NIL

In Objective-C it is perfectly legal to send messages to nil. This often comes as a shock to people from a Java background. In Java, if you call a method on null (null and nil are identical, a pointer with a value of 0—basically a pointer that points to nothing), your application will crash. In Objective-C, the method simply returns 0 or nil (depending on the return type).

Newcomers to Objective-C often argue that this hides errors. By crashing immediately, Java prevents the program from continuing in a bad state and possibly producing faulty output or crashing inexplicably at some later point in the application. There is a grain of truth to this. However, once you accept the fact that you can send messages to nil, you can use it to produce simple, elegant algorithms.

Let’s look at one of the more common design patterns. Imagine an RSS reader that must download a hundred different feeds. First you call a method to download the XML file. Then you parse the XML. Due to potential networking problems, the first method is likely to be highly unreliable. In Java, we would need to check and make sure that we received a valid result.

```
```objectivec
XML xml = RSS.getXMLforURL(myURL);
// Make sure we have a valid xml object.
if (xml != null) {
    xml.parse();
    ...
}
```
```

In Objective-C, those checks are unnecessary. If the XML is nil, the method call simply does nothing.

```
```objectivec
XML* xml = [RSS getXMLforURL:myURL];
[xml parse];
...
```
```

Also, let’s face it, null pointers are a common source of bugs in Java applications. Java’s null pointer violates the language’s otherwise strict static typing. If you can assign it to an object variable, you should be able to treat it just like any other object. That includes calling instance methods and receiving reasonable results.