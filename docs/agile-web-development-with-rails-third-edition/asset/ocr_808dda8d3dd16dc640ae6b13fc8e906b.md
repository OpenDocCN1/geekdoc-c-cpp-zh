![](bbox=[0.18, 0.065, 0.835, 0.295])

Figure 12.2: XML returned by the who_bought action

Believe it or not, this is just Ruby code. It uses Jim Weirich's Builder library, which generates a well-formed XML document as a side effect of executing a program.

Within a builder template, the variable xml represents the XML object being constructed. When we invoke a method on this object (such as the call to order_list on the first line in our template), the builder emits the corresponding XML tag. If a hash is passed to one of these methods, it's used to construct the attributes to the XML tag. If we pass a string, it is used as the tag's value.

If you want to nest tags, pass a block to the outer builder method call. XML elements created inside the block will be nested inside the outer element. We use this in our example to embed a list of <order> tags inside an <order_list> and then to embed a <name> tag and an <email> tag inside each <order>.

We can test this method using a browser or from the command line. If you enter the URL into a browser, the XML will be returned. How it is displayed depends on the browser: on a Mac, Safari renders the text and ignores the tags, while Firefox shows a nicely highlighted representation of the XML (as shown in Figure 12.2). In all browsers, the View → Source option should show exactly what was sent from our application.

We can also query your application from the command line using a tool such as curl or wget.