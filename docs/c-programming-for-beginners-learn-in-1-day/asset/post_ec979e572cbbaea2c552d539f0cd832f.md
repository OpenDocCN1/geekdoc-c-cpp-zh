
![](img/8115a2172ef67838d7fe1933fc517c4d_67_0.png)

### Code Explanation:-

- 1. The first step is used to declare our Array List. Here we are declaring a1 as a variable to hold the elements of our array list.
- 2. We then use the add keyword to add the number 1 , the String “Example” and the Boolean value ‘true’ to the array list.
- 3. We then use the Console.WriteLine method to display the value of each array lists element to the console. You will notice that just like arrays, we can access the elements via their index positions. So to access the first position of the Array List, we use the [0] index position. And so on and so forth.

If the above code is entered properly and the program is run the following output will be displayed.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_67_1.png)

From the output, you can clearly see that all of the elements from the array list are sent to the console.

Let’s look at some more methods which are available as part of the ArrayList.

- - **Count** – This method is used to get the number of items in the ArrayList collection. Below is the general syntax of this statement. ArrayList.Count() –
This method will return the number of elements that the array list contains.

- - **Contains** - This method is used to see if an element is present in the ArrayList collection. Below is the general syntax of this statement  
  `ArrayList.Contains(element)` – This method will return true if the element is present in the list, else it will return false.

- - **RemoveAt** - This method is used to remove an element at a specific position in the ArrayList collection. Below is the general syntax of this statement

`ArrayList.RemoveAt(index)` – This method will remove an element from a specific position of the Array List.

Now let’s see this working at a code level. All of the below-mentioned code will be written to our Console application. The code will be written to our Program.cs file.

In the below program, we will write the code to see how we can use the above-mentioned methods.

![](img/8115a2172ef67838d7fe1933fc517c4d_68_0.png)

### Code Explanation:-

- 1. So the first property we are seeing is the Count property. We are getting the Count property of the array list a1 and then writing it to the Console.
- 2. In the second part, we are using the Contains method to see if the arraylist a1 contains the element 2. We then write the result to the Console via the Writeline command.
- 3. Finally to showcase the Remove element method, we are performing the below steps,
  - a. First, we write the value of the element at Index position 1 of the array list to the console.
  - b. Then we remove the element at Index position 1 of the array list.
- c. Finally, we again write the value of the element at Index position 1 of the array list to the console. This set of steps will give a fair idea whether the remove method will work as it should be.

If the above code is entered properly and the program is run the following output will be displayed.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_69_0.png)

Why the last value is true?

If you see the sequence of events , the element Example is removed from the array because this is at position 1. Position 1 of the array then gets replaced by what was in position 2 earlier which the value ‘true’

## C# Stack

The stack is a special case collection which represents a last in first out (LIFO) concept. To first understand LIFO, let’s take an example. Imagine a stack of books with each book kept on top of each other.

The concept of last in first out in the case of books means that only the top most book can be removed from the stack of books. It is not possible to remove a book from between, because then that would disturb the setting of the stack.

Hence in C#, the stack also works in the same way. Elements are added to the stack, one on the top of each other. The process of adding an element to the stack is called a push operation. To remove an element from a stack, you can also remove the top most element of the stack. This operation is known as pop.

Let’s look at the operations available for the Stack collection in more detail.

- - **Declaration of the stack** – A stack is created with the help of the Stack Data type. The keyword “new” is used to create an object of a Stack. The object is then assigned to the variable st. `Stack st = new Stack()`
- - **Adding elements to the stack** – The push method is used to add an element onto the stack. The general syntax of the statement is given below. `Stack.push(element)`
- - **Removing elements from the stack** – The pop method is used to remove an element from the stack. The pop operation will return the topmost element of the stack. The general syntax of the statement is given below `Stack.pop()`
- - **Count** – This property is used to get the number of items in the Stack. Below is the general syntax of this statement. `Stack.Count`
- - **Contains** - This method is used to see if an element is present in the Stack. Below is the general syntax of this statement. The statement will return true if the element exists, else it will return the value false. `Stack.Contains(element)`

Now let’s see this working at a code level. All of the below-mentioned code will be written to our Console application. The code will be written to our Program.cs file. In the below program, we will write the code to see how we can use the above-mentioned methods.

In this example, we will see

- - How a stack gets created.
- - How to display the elements of the stack , and use the Count and Contains methods.

![](img/8115a2172ef67838d7fe1933fc517c4d_71_0.png)

### Code Explanation:-

- 1. The first step is used to declare the Stack. Here we are declaring “st” as a variable to hold the elements of our stack.
- 2. Next, we add 3 elements to our stack. Each element is added via the Push method.
- 3. Now since the stack elements cannot be accessed via the index position like the array list, we need to use a different approach to display the elements of the stack. The Object (obj) is a temporary variable, which is declared for holding each element of the stack. We then use the foreach statement to go through each element of the stack. For each stack element, the value is assigned to the obj variable. We then use the Console.Writeline command to display the value to the console.
- 4. We are using the Count property (**st.count**) to get the number of items in the stack. This property will return a number. We then display this value to the
console.
- 5. We then use the Contains method to see if the value of 3 is present in our stack. This will return either a true or false value. We then display this return value to the console.

If the above code is entered properly and the program is run the following output will be displayed.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_72_0.png)

From the output, we can clearly see that the elements of the stack are displayed. Also, the value of True is displayed to say that the value of 3 is defined on the stack.

Note: You have noticed that the last element pushed onto the stack is displayed first. This is the topmost element of the stack. The count of stack elements is also shown in the output.

Now let’s look at the “remove” functionality. We will see the code required to remove the topmost element from the stack.

![](img/8115a2172ef67838d7fe1933fc517c4d_73_0.png)

### Code Explanation:-

- 1. Here we just issue the pop method which is used to remove an element from the stack.

If the above code is entered properly and the program is run, the following output will be displayed.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_74_0.png)

output shows that the element 3 was popped from the stack

We can see that the element 3 was removed from the stack.

## C# Queue

The Queue is a special case collection which represents a first in first out concept. Imagine a queue of people waiting for the bus. Normally, the first person who enters the queue will be the first person to enter the bus. Similarly, the last person to enter the queue will be the last person to enter into the bus. Elements are added to the stack, one on the top of each other.

The process of adding an element to the queue is the enqueue operation. To remove an element from a queue, you can use the dequeue operation. The operation in queues are similar to stack we saw previously.

Let’s look at the operations available for the Queue collection in more detail.

- - **Declaration of the Queue** – The declaration of a Queue is provided below. A Queue is created with the help of the Queue Data type. The “new” keyword is used to create an object of a Queue. The object is then assigned to the variable qt.
- - **Adding elements to the Queue** – The enqueue method is used to add an element onto the queue. The general syntax of the statement is given below.
- - **Removing elements from the queue** – The dequeue method is used to remove an element from the queue. The dequeue operation will return the last element of the queue. The general syntax of the statement is given below
- - **Count** – This property is used to get the number of items in the queue. Below is the general syntax of this statement.
- - **Contains** - This method is used to see if an element is present in the Queue. Below is the general syntax of this statement. The statement will return true if the element exists, else it will return the value false.

```
Queue qt = new Queue()
```

```
Queue.enqueue(element)
```

```
Queue.pop()
```

```
Queue.Count
```

```
Queue.Contains(element)
```

Now, let’s see this working at a code level. All of the below-mentioned code will be written to our Console application.
