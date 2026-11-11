```
```ada
private
    BufSize : constant Integer := 100;
    Buf     : array (1..BufSize) of Integer;
    Filled  : Integer range 0..BufSize := 0;
    Next_In,
    Next_Out : Integer range 1..BufSize := 1;
end Buffer;

protected body Buffer is
    entry Deposit(Item : in Integer)
        when Filled < BufSize is
    begin
        Buf(Next_In) := Item;
        Next_In := (Next_In mod BufSize) + 1;
        Filled := Filled + 1;
    end Deposit;
    entry Fetch(Item : out Integer) when Filled > 0 is
    begin Item := Buf(Next_Out);
        Next_Out := (Next_Out mod BufSize) + 1;
        Filled := Filled - 1;
    end Fetch;
end Buffer;
```
```

# ### 13.6.5 Evaluation

Using the general message-passing model of concurrency to construct monitors is like using Ada packages to support abstract data types—both are tools that are more general than is necessary. Protected objects are a better way to provide synchronized access to shared data.

In the absence of distributed processors with independent memories, the choice between monitors and tasks with message passing as a means of implementing synchronized access to shared data in a concurrent environment is somewhat a matter of taste. However, in the case of Ada, protected objects are clearly better than tasks for supporting concurrent access to shared data. Not only is the code simpler; it is also much more efficient.

For distributed systems, message passing is a better model for concurrency, because it naturally supports the concept of separate processes executing in parallel on separate processors.

# ### 13.7 Java Threads

The concurrent units in Java are methods named run, whose code can be in concurrent execution with other such methods (of other objects) and with the main method. The process in which the run methods execute is called a thread. Java's threads are lightweight tasks, which means that they all run in the same address space. This is different from Ada tasks, which are heavyweight threads