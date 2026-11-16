```
messageCount++;
System.out.println("Received: " + msg);
if (msg == Message.POISON_PILL ) {
break;
}
}
return new Integer( messageCount );
}
}
```

```
enum Message {
MESSAGE_ONE,
MESSAGE_TWO,
MESSAGE_THREE,
POISON_PILL; // Quit :
}
```

```
private ExecutorService exec;
private BlockingQueue<Message> queue;

public BlockingQueueExample() {
exec = Executors.newCachedThreadPool();
queue = new LinkedBlockingQueue<BlockingQueueExample.Message>();
}
```

```
public void runTest() {
int numberOfMessages = 100;
int sleep = 100;
System.out.println( "Messages Sent: " + numberOfMessages );
exec.submit( new Producer( numberOfMessages, sleep ) );
// sleep a little
sleep( 2000 ); // two seconds..
try {
// Start the consumer much later, but that's ok!
Future<Integer> consumer = exec.submit( new Consumer() );
try {
System.out.println( "Messages Processed: " + consumer.get() );
} catch( ExecutionException ex ) {
}
catch( InterruptedException ex ) {
}
} finally {
try {
exec.shutdown();
exec.awaitTermination( 10, TimeUnit.SECONDS );
```