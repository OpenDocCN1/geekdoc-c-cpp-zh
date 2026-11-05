# C# Hashtable

A hash table is a special collection that is used to store key-value items. So instead of storing just one value like the stack, array list and queue, the hash table stores 2 values. These 2 values form an element of the hash table.

Below are some example of how values of a hash table might look like.

```
{ “001” , “.Net” }
{ “002” , “.C#” }
{ “003” , “ASP.Net” }
```

Above we have 3 key value pairs. The keys of each element are 001, 002 and 003 respectively. The values of each key value pair are “.Net”, “C#” and “ASP.Net” respectively.

Let’s look at the operations available for the Hashtable collection in more detail.

+   - **Declaration of the Hashtable** – The declaration of a Hashtable is shown below. A Hashtable is created with the help of the Hashtable Data type. The “new” keyword is used to create an object of a Hashtable. The object is then assigned to the variable ht.
+   
+     `Hashtable ht = new Hashtable()`
+   - **Adding elements to the Hashtable** – The Add method is used to add an element on to the queue. The general syntax of the statement is given below
+   
+     `HashTable.add("key","value")`

Remember that each element of the hash table comprises of 2 values, one is the key, and the other is the value.

Now, let’s see this working at a code level. All of the below-mentioned code will be written to our Console application.

The code will be written to our Program.cs file. In the below program, we will write the code to see how we can use the above-mentioned methods.

For now in our example, we will just look at how we can create a hashtable , add elements to the hashtable and display them accordingly.