the sender has crashed or an error has occurred in the sender’s algorithm. For this case, the receiver process can include an after clause to time out the receive operation. Its form is:

```
receive
    Pattern1 [ when Guard1 ] ->
        Expressions1
    Pattern2 [ when Guard2 ] ->
        Expressions2
    ...
    after Time ->
        Expressions
end
```

The Time variable stands for the maximum number of milliseconds that the receive operation must wait for a message, after which control proceeds to the Expressions, which are executed. This feature can be used to define a sleep function, which essentially suspends the calling process for a given amount of time:

```
sleep(Time) ->
    receive
    after Time ->
        true
    end
```

The Erlang programmer also must be aware of the manner in which messages are scheduled for a process. Each process is associated with a mailbox, a queue-like data structure. When another process sends a message, it goes at the end of the receiver process’s mailbox. The process’s receive operation attempts to match the message at the front of its mailbox to one of its patterns. If a match occurs, the message is removed from the mailbox, discarded, and the expressions in the clause are executed. If no match occurs, the message is removed from the mailbox and put at the rear of the process’s save queue. The next message in the mailbox is then tried, and so forth, until the mailbox becomes empty. If that happens, the process itself is suspended, until a new message arrives in the mailbox, at which point, the process itself is rescheduled for execution to examine this message. If a message is matched, all of the messages in the saved queue are transferred to the mailbox in their original order. The same transfer of messages from saved queue to mailbox is carried out if a timeout due to an after clause occurs.

Our final example defines a function flush_mailbox, which empties the mailbox of a process.

```
flush_mailbox() ->
    receive
        _Any ->
            flush_mailbox()
    after 0 ->
        true
    end
```