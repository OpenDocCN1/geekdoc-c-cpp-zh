![](bbox=[0.18, 0.1, 0.75, 0.78])

# FIGURE 10-4

The heart of the solution is the PriorityDocumentManager class. This class is very easy to use. With the public interface of this class, new Document elements can be added to the linked list, the first document can be retrieved, and for testing purposes it also has a method to display all elements of the collection as they are linked in the list.

The class PriorityDocumentManager contains two collections. The collection of type LinkedList<Document> contains all documents. The collection of type List<LinkedListNode<Document>> contains references of up to 10 elements that are entry points for adding new documents with a specific priority. Both collection variables are initialized with the constructor of the class PriorityDocumentManager. The list collection is also initialized with null:

```
public class PriorityDocumentManager
{
    private readonly LinkedList<Document> documentList;
```