# 150 Looping Around the Iterator

# Looping Around the Iterator

Here's a piece of the code from the Main() method to demonstrate the custom LinkedList (that chunk of code is in the LinkedListContainer on this book's Web site);

```
public class Program
    public static void Main(string[] args)\    {
        // Create a container and add three elements to it.
        LinkedList l = new LinkedList();
        LinkedListNode first = l.AddObject("This is first string");
        LinkedListNode second = l.AddObject("This is second string");
        LinkedListNode third = l.AddObject("This is last string");

        // Add one at the beginning and one in the middle.
        l.AddObject(null, "Insert before the first string");
        LinkedListNode middle = l.AddObject("Insert between the second and third string");

        // You can navigate the iterator "manually.".
        Console.WriteLine("Iterate through the container manually:");
        LinkedListIteratorIterator li = (LinkedListIterator)l.GetEnumerator();
        li.Reset();
        while(li.MoveNext())\        {
            string s = li.Current;
            Console.WriteLine(s);
        }
    }
```

This code gets a LinkedListIterator and uses its MoveNext() method and Current property to iterate a linked list. Just when you thought you had mastered it, you out that C# 2.0 has simplified this process so that

+   * You don't have to call GetEnumerator() (and the results).
* You don't have to call MoveNext().
* You don't have to call Current and return its value.

+   * You can simply use foreach to iterate the collection. (C# does the rest for you under the hood — it writes the enumerator class.)

Well, to be fair, foreach works for the LinkedList class in this chapter, too. That comes from providing a GetEnumerator() method. But I still had to write the LinkedListIterator classes ourselves. The new wrinkle is that you can skip that part in your roll-own collection classes, if you choose.

Rather than implement interface methods in collection classes you write, you can provide an iterator block — and you don't have to write your own iterator class to support the collection. Iterator blocks were introduced in C# 2.0, which shipped with Visual Studio 2005.

![](bbox=[0.535, 0.946, 0.615, 0.973])