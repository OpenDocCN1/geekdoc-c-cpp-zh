same priority, 8, but because One was added before Four, it is earlier in the list.

![](bbox=[0.235, 0.105, 0.77, 0.56])

# Figure 11.4

When new documents are added to the linked list, they should be added after the last document that has the same priority. The LinkedList<Document> collection contains elements of type LinkedListNode<Document>. The class LinkedListNode<T> adds Next and Previous properties to walk from one node to the next. For referencing such elements, the List<T> is defined as List<LinkedListNode<Document>>. For fast access to the last document of every priority, the collection List<LinkedListNode> contains up to 10 elements, each referencing the last document of every priority. In the upcoming discussion, the reference to the last document of every priority is called the priority node.

Using the previous example, the Document class is extended to contain the priority, which is set with the constructor of the class (code file LinkedListSample/Document.cs):

```
public class Document
{
    public string Title { get; private set; }
    public string Content { get; private set; }
    public byte Priority { get; private set; }
}
```