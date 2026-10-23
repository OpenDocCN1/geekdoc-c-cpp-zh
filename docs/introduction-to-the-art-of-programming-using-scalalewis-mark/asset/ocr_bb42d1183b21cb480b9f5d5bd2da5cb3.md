```
def buildVars(nodes:NodeSeq):mutable.Map[String,Double] = {
	mutable.Map((for(n <- nodes) yield (n \ "@name").text -> (n \ "@value").text.toDouble): _ *)
}
```

To pull the data out of the XML means that it has to get there in the first place. For this reason, we must also alter the toXML method in Drawing to include extra elements for the variables. This can be done with the following code.

```
def toXML : xml.Node =
<drawing>
  {root.toXML}
  { for(n,v) <- vars) yield (<variable name=[n] value={v.toString}/>) }
</drawing>
```

A for loop is used here to simplify the syntax of dealing with the tuples that come out of the map.

# 24.9 End of Chapter Material

# 24.9.1 Summary of Concepts

+   • The term Abstract Data Type, ADT, is used to describe a programmatic structure that has well-defined operations, but that does not specify how those operations are carried out. This concept links back to the ideas of separation of interface and implementation.

+   • A stack is a simple ADT with two basic operations, push and pop. The push operation adds an element to the top of the stack. The pop operation removes the most recently added element. This order of content removal is called Last In First Out, LIFO.

+   • A queue is another simple ADT with enqueue and dequeue operations. The enqueue adds an element to a queue while the dequeue takes out the element that has been in the queue the longest. This ordering scheme for removal of elements is called First In First Out, FIFO.

+   • Order analysis helps us understand the way in which algorithms behave as input sizes get larger. The O notation ignores constant multiples and lower-order terms. It is only really relevant when the input sizes get large.

+   • Due to their simplicity, any reasonable implementation of a stack or a queue should have operations that have an O(1) amortized cost.

+   • One way to implement that stack ADT is using an Array to store the data. Simply keep an index to the top of the stack in the Array and build up from 0. When the Array is full, it should be grown by a multiplicative factor to maintain O(1) amortized cost over copying operations.

+   • It is also possible to implement a queue with an Array. The implementation is a bit more complex because data is added at one end of the queue and removed at the other. The front and back are wrapped around when they hit the end so the Array