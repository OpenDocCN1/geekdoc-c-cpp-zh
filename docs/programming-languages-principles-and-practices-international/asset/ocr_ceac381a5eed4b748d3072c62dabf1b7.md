also possible to declare task types and variables to get more than one task of a particular type or to get dynamic control over task execution. For example,

```
task type T is
  ---
end;

task body T is
  ---
begin
  ---
end T;

p,q: T;
```

declares a task type T and two tasks p and q of type T.

In addition to tasks, which are part of Ada83, Ada95 also has monitors, called protected objects, that correspond to the synchronized objects of Java. There is a similar separation of a protected type or object declaration into specification and body. For example, a protected queue type can be declared as follows:

```
protected type Queue is -- specification
  procedure enqueue (item: in ...);
  entry dequeue (item: out ...);
  function empty return boolean;
private:
  -- private data here
  size: natural;
  ---
end Queue;

protected body Queue is
  -- implementation of services here
end Queue;
```

As we see in this example, operations within a protected object are of three different kinds: functions, procedures, and entries. All three are synchronized in the Java sense, but with the following differences: Functions are not allowed to change the local state of a protected object but can be executed by any number of callers, provided that no procedures or entries are currently executing. Procedures and entries, however, can only be executed by a single caller at a time, and no functions can be executing simultaneously with a procedure or entry (this is a standard multi-reader, single-writer protocol).

The difference between a procedure and an entry in a protected object is that a procedure can always be executed (subject to the mutual exclusion rules), while an entry can only be executed under a certain condition, called the entry barrier. For example, the dequeue operation is an entry, because it can only be executed if the queue is nonempty, while an enqueue operation is a procedure, because it can always execute (assuming the queue size can be arbitrarily expanded). If a task calls an entry whose