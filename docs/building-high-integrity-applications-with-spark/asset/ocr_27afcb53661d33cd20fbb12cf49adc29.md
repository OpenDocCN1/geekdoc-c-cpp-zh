The first declaration in this example program defines a bounded queue with a maximum size of 100. For clarity, we chose to prefix the type Queue_Type in our declaration of the variable My_Queue even though the use clause allows us to omit the package name. After the loop enqueues thirty-six values, the program dequeues five values and displays them. After clearing the queue, it displays the size of the queue.

All that remains is to complete the body of our queue package where we implement the queue operations defined in the package specification. Here is the body of our bounded queue package:

```
    package body Bounded_Queue_V1 is

       function Full (Queue : in Queue_Type) return Boolean is
       begin
          return Queue.Count = Queue.Max_Size;
       end Full;

       function Empty (Queue : in Queue_Type) return Boolean is
       begin
          return Queue.Count = 0;
       end Empty;

       function Size (Queue : in Queue_Type) return Natural is
       begin
          return Queue.Count;
       end Size;

       function First_Element (Queue : in Queue_Type) return Element_Type is
       begin
          return Queue.Items (Queue.Front);
       end First_Element;

       function Last_Element (Queue : in Queue_Type) return Element_Type is
       begin
          return Queue.Items (Queue.Rear);
       end Last_Element;

       procedure Clear (Queue : in out Queue_Type) is
       begin
          Queue.Count := 0;
          Queue.Front := 1;
          Queue.Rear  := Queue.Max_Size;
       end Clear;
```