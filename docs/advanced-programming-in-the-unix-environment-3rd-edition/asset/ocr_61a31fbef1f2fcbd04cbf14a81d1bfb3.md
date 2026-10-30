# 15.7 Message Queues

A message queue is a linked list of messages stored within the kernel and identified by a message queue identifier. We'll call the message queue just a queue and its identifier a queue ID.

> The Single UNIX Specification message-passing option includes an alternative IPC message queue interface derived from the POSIX real-time extensions. We do not discuss it in this text.

A new queue is created or an existing queue opened by msgget. New messages are added to the end of a queue by msgsnd. Every message has a positive long integer type field, a non-negative length, and the actual data bytes (corresponding to the length), all of which are specified to msgsnd when the message is added to a queue. Messages are fetched from a queue by msgrcv. We don't have to fetch the messages in a first-in, first-out order. Instead, we can fetch messages based on their type field. Each queue has the following msgid_ds structure associated with it:

```
struct msgid_ds {
    struct ipc_perm msg_perm;        /* see Section 15.6.2 */
    msgqnum_t       msg_qnum;        /* # of messages on queue */
    msglen_t        msg_qbytes;      /* max # of bytes on queue */
    pid_t           msg_lspid;       /* pid of last msgsnd() */
    pid_t           msg_lrpid;       /* pid of last msgrcv() */
    time_t          msg_stime;       /* last-msgsnd() time */
    time_t          msg_rtime;       /* last-msgrcv() time */
    time_t          msg_ctime;       /* last-change time */
    :
};
```

This structure defines the current status of the queue. The members shown are the ones defined by the Single UNIX Specification. Implementations include additional fields not covered by the standard.

| Description | Typical values |  |  |  |
|---|---|---|---|---|
|  | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
| size in bytes of largest message we can send | 16,384 | 8,192 | 16,384 | derived |
| maximum size in bytes of a particular queue (i.e., the sum of all the sizes of messages on the queue) | 2,048 | 16,384 | 2,048 | 65,536 |
| maximum number of messages queues, systemwide | 40 | derived | 40 | 128 |
| maximum number of messages, systemwide | 40 | derived | 40 | 8,192 |

Figure 15.26 System limits that affect message queues

Figure 15.26 lists the system limits that affect message queues. We show "derived" where a limit is derived from other limits. On Linux, for example, the maximum number of messages is based on the maximum number of queues and the maximum amount of data allowed on the queues. The maximum number of queues, in turn, is based on the amount of RAM installed in the system. Note that the queue maximum byte size limit further limits the maximum size of a message to be placed on a queue.