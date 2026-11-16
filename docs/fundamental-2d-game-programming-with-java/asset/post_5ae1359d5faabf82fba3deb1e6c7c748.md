
```java
package javagames.threads;

import java.util.Random;
import java.util.concurrent.*;

public class CallableTaskExample implements Callable<Boolean> {

    @Override
    public Boolean call() throws Exception {
        // simulate some stupid long task and maybe fail...
        Random rand = new Random();
        int seconds = rand.nextInt( 6 );
        if ( seconds == 0 ) {
            // pretend there was an error
            throw new RuntimeException( "I love the new thread stuff!!! :)" );
        }

        try {
            Thread.sleep( seconds * 100 );
        } catch( InterruptedException e ) { }
        // even = true, odd = false
        return seconds % 2 == 0;
    }

    public static void main( String[] args ) {
        ExecutorService exec = Executors.newCachedThreadPool();
        try {
            for ( int i = 0; i < 50; ++i ) {
                try {
                    Future<Boolean> result =
                        exec.submit( new CallableTaskExample() );
                    Boolean success = result.get();
                    System.out.println( "Result: " + success );
                } catch( ExecutionException ex ) {
                    Throwable throwable = ex.getCause();
                    System.out.println( "Error: " + throwable.getMessage() );
                } catch( InterruptedException e ) {
                    System.out.println( "Awesome! Thread was canceled" );
                    e.printStackTrace();
                }
            }
        } finally {
            try {
                exec.shutdown();
                exec.awaitTermination( 10, TimeUnit.SECONDS );
                System.out.println("Threadpool Shutdown :");
            } catch( InterruptedException e ) {
                // at this point, just give up...
                e.printStackTrace();
                System.exit( -1 );
            }
        }
    }
}
```

## USING THREADS TO LOAD FILES

The FileLoadingExample, as shown in Figure 12.1 and located in the javagames.threads package, uses the Callable, Future, and ExecutorService objects to simulate loading a bunch of files. There are three different thread pools that can be used to simulate loading the 100 files. One is a single threaded executor, another has a maximum of 32 threads, and the last is an unlimited cached thread pool.

![](img/588a4cda8f2acae94a7e1987bf99400d_368_0.png)

Figure 12.1
File Loading Example.
© 2014 Timothy Wright.

The initialize() method creates all three thread pools and creates 100 callable tasks that simulate loading 100 files. The processInput() method submits each task to the different thread pools. If you press 1, the single threaded pool is used. The 2 key uses the thread pool with a maximum of 32 threads. The 3 key uses the unlimited cached thread pool.

The updateObjects() method loops through the list of Future tasks and removes any completed tasks. The render() method displays the usual directions and the percentage of tasks complete. The terminate() method shuts down each thread pool before the application shuts down.

Although threads can make some tasks more complicated, this is an example of a task that is suited for threads.

```java
package javagames.threads;

import java.awt.Graphics;
import java.awt.event.KeyEvent;
import java.util.*;
import java.util.concurrent.*;
import javagames.util.*;

public class FileLoadingExample extends SimpleFramework {
    private static final int NUMBER_OF_FILES = 100;
    private ExecutorService singleThread;
    private ExecutorService thirtyTwoThreads;
    private ExecutorService unlimitedThreads;

    private boolean loading = false;
    private List<Callable<Boolean>> fileTasks;
    private List<Future<Boolean>> fileResults;

    public FileLoadingExample() {
        appWidth = 640;
        appHeight = 480;
        appSleep = 1L;
        appTitle = "File Loading Example";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    @Override
    protected void initialize() {
        super.initialize();
        singleThread = Executors.newSingleThreadExecutor();
        thirtyTwoThreads = Executors.newFixedThreadPool( 32 );
        unlimitedThreads = Executors.newCachedThreadPool();
        fileTasks = new ArrayList<Callable<Boolean>>();
        for( int i = 0; i < NUMBER_OF_FILES; ++i ) {
            final int taskNumber = i;
            fileTasks.add( new Callable<Boolean>() {
                @Override
                public Boolean call() throws Exception {
                    try {
                        // pretend to load a file
                        // just sleep a little
                        Thread.sleep( new Random().nextInt(750) );
                        System.out.println( "Task: " + taskNumber );
                    } catch ( InterruptedException ex ) { }
                    return Boolean.TRUE;
                }
            });
        }
        fileResults = new ArrayList<Future<Boolean>>();
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );
        if( keyboard.keyDownOnce( KeyEvent.VK_1 ) ) {
            if( !loading ) {
                for( Callable<Boolean> task : fileTasks ) {
                    fileResults.add( singleThread.submit( task ) );
                }
            }
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_2 ) ) {
            if( !loading ) {
                for( Callable<Boolean> task : fileTasks ) {
                    fileResults.add( thirtyTwoThreads.submit( task ) );
                }
            }
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_3 ) ) {
            if( !loading ) {
                for( Callable<Boolean> task : fileTasks ) {
                    fileResults.add( unlimitedThreads.submit( task ) );
                }
            }
        }
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );
        Iterator<Future<Boolean>> it = fileResults.iterator();
        while( it.hasNext() ) {
            Future<Boolean> next = it.next();
            if( next.isDone() ) {
                try {
                    if(next.get()) {
                        it.remove();
                    }
                } catch(ExecutionException ex) {
                    ex.printStackTrace();
                } catch(InterruptedException ex) {
                    ex.printStackTrace();
                }
            }
        }
        loading = !fileResults.isEmpty();
    }

    @Override
    protected void render(Graphics g) {
        super.render(g);
        textPos = Utility.drawString(g, 20, textPos,
            "",
            "Press the number key to start loading files",
            "(1) Thread",
            "(2) 32 Threads",
            "(3) Unlimited Threads",
            ""
        );
        double percentComplete =
            (NUMBER_OF_FILES - fileResults.size()) / (double)NUMBER_OF_FILES;
        String fileProgress =
            String.format("File Progress: %f%%", 100.0 * percentComplete);
        textPos = Utility.drawString(g, 20, textPos, fileProgress);
    }

    @Override
    protected void terminate() {
        super.terminate();
        shutdownExecutor(singleThread);
        shutdownExecutor(thirtyTwoThreads);
        shutdownExecutor(unlimitedThreads);
    }

    private void shutdownExecutor(ExecutorService exec) {
        try {
            exec.shutdown();
            exec.awaitTermination(10, TimeUnit.SECONDS);
            System.out.println("Executor Shutdown!!!");
        } catch (InterruptedException e) { }
    }

    public static void main(String[] args) {
        launchApp(new FileLoadingExample());
    }
}
```

## USING THE FAKEHARDWARE CLASS FOR TESTING

Next, you are going to create a FakeHardware class, located in the javagames.threads package, to pretend to use some hardware. Do not be confused by the name. Any task that takes a long time to complete—such as really long file loading, complicated artificial intelligence calculations, or network communication—can benefit from this kind of non-blocking design. In the next chapter, this same idea is needed to make the sound classes work, so hang in there. If these examples do not make sense, there are many more in the next chapter.

The FakeHardware class is a non-blocking class. Each of the following methods returns immediately, performing the task later in another thread:

- turnOn()
- turnOff()
- start()
- stop()

The FakeHardwareListener callback is used to notify interested objects when the non-blocking methods have completed.

```java
package javagames.threads;

import javagames.threads.FakeHardware.FakeHardwareEvent;

public interface FakeHardwareListener {
    public void event( FakeHardware source, FakeHardwareEvent event );
}
```

The FakeHardwareEvent is an enum with four events:

```java
public enum FakeHardwareEvent {
    START,
    STOP,
    ON,
    OFF;
}
```
