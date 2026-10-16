```
if q = q.next then
   q := null;
else
   q.next := q.next.next;
   q := q.next;
end if;
end dequeue;

function emptyq return Boolean is
begin
   return q = null;
end emptyq;

begin
   q := null;
end Queues;
```

Note that this allows us to write initialization code internally within the package body (the last three lines of the above code), which is executed on “elaboration,” or allocation time (at the beginning of execution). This eliminates the need for user-supplied code to initialize a queue, and so there is no createq procedure.

Normally this would imply that there can only be one queue in a client, since otherwise the entire code must be replicated (try this using a C++ namespace—see Exercise 11.28). This results from the static nature of most module mechanisms (including those of Ada and ML). In Ada, however, the generic package mechanism offers a convenient way to obtain several different queues (even for the same stored type) by using multiple instantiations of the same generic package:

```
with Ada.Text_IO; use Ada.Text_IO;
with Ada.Integer_Text_IO;
use Ada.Integer_Text_IO;
with Queues;

procedure Quser is

package Queue1 is new Queues(Integer);
package Queue2 is new Queues(Integer);

begin
   Queue1.enqueue(3);
   Queue1.enqueue(4);
   Queue2.enqueue(1);
   Queue2.enqueue(2);
   put(Queue1.frontq); -- prints 3
```