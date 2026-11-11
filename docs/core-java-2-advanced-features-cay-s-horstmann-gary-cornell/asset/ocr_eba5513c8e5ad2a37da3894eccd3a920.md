The remainder of the code is rather technical. For each annotated method, we construct a proxy object, implementing the `ActionListener` interface, with an `actionPerformed` method that calls the annotated method. (For more information about proxies, see Volume I, Chapter 6.) The details are not important. The key observation is that the functionality of the annotations was established by the `processAnnotations` method.

Figure 8.1 shows how annotations are handled in this example.

![](bbox=[0.209, 0.31, 0.877, 0.502])

**Figure 8.1** Processing annotations at runtime

In this example, the annotations were processed at runtime. It is also possible to process them at the source level. A source code generator would then produce the code for adding the listeners. Alternatively, the annotations can be processed at the bytecode level. A bytecode editor could inject the calls to `addActionListener` into the frame constructor. This sounds complex, but libraries are available to make this task relatively straightforward. You can see an example in Section 8.7, “Bytecode Engineering,” on p. 481.

Our example was not intended as a serious tool for user interface programmers. A utility method for adding a listener could be just as convenient for the programmer as the annotation. (In fact, the `java.beans.EventHandler` class tries to do just that.) You could make the class truly useful by supplying a method that adds the event handler instead of just constructing it.

However, this example shows the mechanics of annotating a program and of analyzing the annotations. Having seen a concrete example, you are now more prepared (we hope) for the following sections that describe the annotation syntax in complete detail.