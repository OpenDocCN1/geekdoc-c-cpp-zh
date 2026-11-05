
The code will be written to our Program.cs file. In the below program, we will write the code to see how we can use the above-mentioned methods.

In this example, we will see how a queue gets created. Next, we will see how to display the elements of the queue, and use the Count and Contains methods.

![](img/8115a2172ef67838d7fe1933fc517c4d_76_0.png)

### Code Explanation

- 1. The first step is used to declare the Queue. Here we are declaring qt as a variable to hold the elements of our Queue.
- 2. Next, we add 3 elements to our Queue. Each element is added via the “enqueue” method.
- 3. Now one thing that needs to be noted about Queues is that the elements cannot be accessed via the index position like the array list. We need to use a different approach to display the elements of the Queue. So here’s how we go about displaying the elements of a queue.
  - We first declare a temporary variable called obj. This will be used to hold each element of the Queue.
  - We then use the foreach statement to go through each element of the Queue.
  - For each Queue element, the value is assigned to the obj variable.
  - We then use the Console.WriteLine command to display the value to the console.
- 4. We are using the “Count” property to get the number of items in the Queue. This property will return a number. We then display this value to the console.
- 5. We then use the “Contains” method to see if the value of 3 is present in our Queue. This will return either a true or false value. We then display this return value to the console.

If the above code is entered properly and the program is run the following output will be displayed.

### Output

![](img/8115a2172ef67838d7fe1933fc517c4d_77_0.png)

From the output, we can clearly see that the elements of the Queue are displayed. Note that, unlike stack, in queue the first element pushed on to the queue is displayed first. The count of queue elements is also shown in the output. Also, the value of True is displayed to say that the value of 3 is defined on the queue.

Now let’s look at the remove functionality. We will see the code required to remove the first element from the queue.

```csharp
static void Main(string[] args)
{
    Queue qt = new Queue();
    qt.Enqueue(1);
    qt.Enqueue(2);
    qt.Enqueue(3);
    qt.Dequeue();
    foreach (Object obj in qt)
    {
        Console.WriteLine(obj);
    }
}
```

### Code Explanation

- 1. Here we just issue the “dequeue” method, which is used to remove an element from the queue. This method will remove the first element of the queue.

If the above code is entered properly and the program is run the following output will be displayed.

### Output

![](img/8115a2172ef67838d7fe1933fc517c4d_79_0.png)

output shows that the first element was removed from the queue

From the output, we can see that the first element which was added to the queue, which was the element 1, was removed from the queue.

## C# Hashtable

A hash table is a special collection that is used to store key-value items. So instead of storing just one value like the stack, array list and queue, the hash table stores 2 values. These 2 values form an element of the hash table.

Below are some examples of how values of a hash table might look like.

```csharp
{ "001", ".Net" }
{ "002", "C#" }
{ "003", "ASP.Net" }
```

Above we have 3 key value pairs. The keys of each element are 001, 002 and 003 respectively. The values of each key value pair are “.Net”, “C#” and “ASP.Net” respectively.

Let’s look at the operations available for the Hashtable collection in more detail.

- **Declaration of the Hashtable** – The declaration of a Hashtable is shown below. A Hashtable is created with the help of the Hashtable Data type. The “new” keyword is used to create an object of a Hashtable. The object is then assigned to the variable ht.
  
  `Hashtable ht = new Hashtable();`
- **Adding elements to the Hashtable** – The Add method is used to add an element on to the hashtable. The general syntax of the statement is given below
  
  `Hashtable.Add("key", "value");`

Remember that each element of the hash table comprises of 2 values, one is the key, and the other is the value.

Now, let’s see this working at a code level. All of the below-mentioned code will be written to our Console application.

The code will be written to our Program.cs file. In the below program, we will write the code to see how we can use the above-mentioned methods.

For now in our example, we will just look at how we can create a hashtable, add elements to the hashtable and display them accordingly.

![](img/8115a2172ef67838d7fe1933fc517c4d_81_0.png)

### Code Explanation

- 1. First, we declare the hashtable variable using the Hashtable data type by using keyword “new”. The name of the variable defined is ‘ht’.
- 2. We then add elements to the hash table using the Add method. Remember that we need to add both a key and value element when adding something to the hashtable.
- 3. There is no direct way to display the elements of a hash table.
  - In order to display the hashtable, we first need to get the list of keys (001, 002 and 003) from the hash table.
  - This is done via the ICollection interface. This is a special data type which can be used to store the keys of a hashtable collection. We then assign the keys of the hashtable collection to the variable ‘keys’.
- 4. Next for each key value, we get the associated value in the hashtable by using the statement ht[k].

If the above code is entered properly and the program is run the following output will be displayed.

### Output

![](img/8115a2172ef67838d7fe1933fc517c4d_82_0.png)

Let’s look at some more methods available for hash tables.

- **ContainsKey** - This method is used to see if a key is present in the Hashtable. Below is the general syntax of this statement. The statement will return true if the key exists, else it will return the value false.
  
  ```csharp
  Hashtable.ContainsKey(key);
  ```
- **ContainsValue** - This method is used to see if a Value is present in the Hashtable. Below is the general syntax of this statement. The statement will return true if the Value exists, else it will return the value false.
  
  ```csharp
  Hashtable.ContainsValue(value);
  ```

Let’s change the code in our Console application to showcase how we can use the “ContainsKey” and “ContainsValue” method.

```csharp
static void Main(string[] args)
{
    Hashtable ht = new Hashtable();

    ht.Add("001", ".Net");
    ht.Add("002", "C#");
    ht.Add("003", "ASP.Net");

    Console.WriteLine(ht.ContainsKey("001")); // searching for a key
    Console.WriteLine(ht.ContainsValue("C#")); // searching for a value

    Console.ReadKey();
}
```

### Code Explanation

- 1. First, we use the ContainsKey method to see if the key is present in the hashtable. This method will return true if the key is present in the hashtable. This method should return true since the key does exist in the hashtable.
- 2. We then use the ContainsValue method to see if the value is present in the hashtable. This method will return ‘true’ since the Value does exist in the hashtable.

If the above code is entered properly and the program is run the following output will be displayed.

### Output

![](img/8115a2172ef67838d7fe1933fc517c4d_84_0.png)

From the output, you can clearly see that both the key and value being searched are present in the hash table.

## Summary

- The Array List collection is used to store a group of elements. The advantage of the Array list collection is that it is dynamic in nature. You can add and remove elements on the fly to the array list collection.
- A Stack is based on the last in first out concept. The operation of adding an element to the stack is called the push operation. The operation of removing an element from the stack is called the pop operation.
- A Queue is based on the first in first out concept. The operation of adding an element to the queue is called the enqueue operation. The operation of removing an element from the queue is called the dequeue operation.
- A Hashtable is used to store elements which comprises of key-value pairs. To access the value of an element, you need to know the key of the element.
