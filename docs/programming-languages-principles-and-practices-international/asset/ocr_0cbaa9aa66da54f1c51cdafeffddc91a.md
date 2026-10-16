```
```java
(58)    public void run() {
(59)        while (!Thread.currentThread().isInterrupted())
(60)        {
(61)            char c = buffer.get();
(62)            System.out.print(c);
(63)        }
(64)        while(buffer.more()) // clean-up
(65)        {
(66)            char c = buffer.get();
(67)            System.out.print(c);
(68)        }
(69)    }
(70) }

(71) class Producer implements Runnable{
(72)    private final Buffer buffer;
(73)    private final InputStreamReader in
(74)        = new InputStreamReader(System.in);

(75)    public Producer(Buffer b) { buffer = b; }

(76)    public void run() {
(77)        try {
(78)            while (!Thread.currentThread().isInterrupted()) {
(79)                int c = in.read();
(80)                if (c == -1) break; // -1 is end of file
(81)                buffer.put((char)c);
(82)            }
(83)        }
(84)        catch (IOException e) { }
(85)    }
(86) }
```
```

The main program creates a buffer of five characters, a reader (the producer) for the buffer and a writer (the consumer) that prints characters. Two threads are created, one for the producer and one for the consumer (so that three threads in all exist for this program, including the main thread). The main thread then waits for the reader to finish (line 12), and then interrupts the writer (line 13). (Since **join** can, like **wait**, generate **InterruptedException**, we must also handle this exception.)

The bounded buffer class itself uses an array to hold the characters, along with two indices that traverse the array in a circular fashion, keeping track of the last positions where insertions and removals took place (this is a standard implementation technique discussed in many data structures books). Both the **put** (insert) and **get** (remove) operations are synchronized to ensure mutual exclusion. The **put** operation delays a thread if the buffer is full (line 30), while the **get** operation delays a thread if the