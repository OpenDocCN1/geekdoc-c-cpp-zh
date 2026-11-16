
FakeHardware 类包含使用 Collections.synchronizedList() 方法创建的监听器。监听器列表在添加和删除项目时是线程安全的。只要列表迭代在 synchronized 块中受到保护，它在多线程中使用也是安全的。

fireEvent() 方法会通知所有监听器已完成的事件：

```java
private void fireEvent(FakeHardwareEvent event) {
    synchronized( listeners ) {
        for( FakeHardwareListener listener : listeners ) {
            listener.event( this, event );
        }
    }
}
```

setStart() 方法存在一个问题。一旦事件发送，它就会调用 runTask() 方法。该方法不能完全同步，否则在任务运行期间，其他任何 synchronized 块都无法被调用。然而，由于该方法的编码方式，它不是线程安全的。如果在 synchronized 块之后但下一次布尔检查之前停止了硬件，任务将永远不会运行，STOP 事件也永远不会发送。这是故意为之，模拟了下一章中声音类的类似错误。与其修复代码，不如在类不是线程安全的情况下，也以线程安全的方式使用该类。

请注意，所有非阻塞方法都会生成一个新线程来完成任务，然后立即返回。任务实际上是在另一个线程中发生的，然后触发监听器以通知观察者任务已完成。

```java
package javagames.threads;
import java.util.*;
```

```java
/*
 * This will simulate some fake hardware.
 */
public class FakeHardware {
    private static final int SLEEP_MIN = 100;
    private static final int SLEEP_MAX = 500;
    public enum FakeHardwareEvent {
        START,
        STOP,
        ON,
        OFF;
    }

    private volatile boolean on = false;
    private volatile boolean running = false;
    private String name;

    private List<FakeHardwareListener> listeners =
        Collections.synchronizedList(new ArrayList<FakeHardwareListener>());

    public FakeHardware( String name ) {
        this.name = name;
    }

    public boolean addListener( FakeHardwareListener listener ) {
        return listeners.add( listener );
    }

    public boolean isOn() {
        return on;
    }

    public boolean isRunning() {
        return running;
    }

    private void sleep() {
        int rand = new Random().nextInt( SLEEP_MAX - SLEEP_MIN + 1 );
        sleep( rand + SLEEP_MIN );
    }

    private void sleep( int ms ) {
        try {
            Thread.sleep( ms );
        } catch( InterruptedException ex ) {
        }
    }

    public void turnOn() {
        new Thread( new Runnable() {
            public void run() {
                sleep();
                setOn();
            }
        }).start();
    }

    public void turnOff() {
        new Thread( new Runnable() {
            public void run() {
                sleep();
                setOff();
            }
        }).start();
    }

    public void start( final int timeMS, final int slices ) {
        new Thread( new Runnable() {
            public void run() {
                sleep();
                setStart( timeMS, slices );
            }
        }).start();
    }

    public void stop() {
        new Thread( new Runnable() {
            public void run() {
                sleep();
                setStop();
            }
        }).start();
    }

    private synchronized void setOn() {
        if ( on ) {
            on = true;
            fireEvent( FakeHardwareEvent.ON );
        }
    }

    private synchronized void setOff() {
        if ( on ) {
            setStop();
            on = false;
            fireEvent( FakeHardwareEvent.OFF );
        }
    }

    /*
     * There is a problem with this method.
     * If the lock running is set to false after the lock
     * is released but before the next if statement,
     * the task will never run...
     *
     * Let's pretend this Hardware driver doesn't work well,
     * even though that NEVER happens :)
     */

    private void setStart( int timeMS, int slices ) {
        synchronized( this ) {
            if( on && running ) {
                running = true;
                fireEvent( FakeHardwareEvent.START );
            }
        }

        if( running ) {
            runTask( timeMS, slices );
            running = false;
            fireEvent( FakeHardwareEvent.STOP );
        }
    }

    private synchronized void setStop() {
        if( running ) {
            running = false;
            // don't send the event
            // not actually done yet :)
        }
    }

    private void runTask( int timeMS, int slices ) {
        int sleep = timeMS / slices;
        for( int i = 0; i < slices; ++i ) {
            if( !running ) {
                return;
            }
            System.out.println( name + "[" + (i+1) + "/" + slices + "]" );
            sleep( sleep );
        }
    }

    private void fireEvent( FakeHardwareEvent event ) {
        synchronized( listeners ) {
            for( FakeHardwareListener listener : listeners ) {
                listener.event( this, event );
            }
        }
    }
}
```

## 使用 WAIT/NOTIFY 方法

FakeHardware 类是使用线程和回调监听器来创建非阻塞类并通知事件完成的绝佳示例。但有时有必要为非阻塞类创建阻塞版本。wait() 和 notify() 方法非常适合这种情况。

每个对象都有一个 wait() 方法，只要在该对象上持有 synchronized 锁，它就会阻塞，直到收到唤醒通知。

```java
synchronized(object) {
    while(conditionNotTrue()) {
        object.wait();
    }
}
```

wait() 方法会阻塞，直到另一个线程获取对象锁并通知所有在该对象上等待的线程。有必要使用 while 循环来检查条件，因为 wait() 方法在某些情况下可能会在没有任何类唤醒等待线程的情况下从 wait() 方法中醒来。仅仅因为 wait() 方法返回了，并不意味着条件一定为真。要唤醒等待线程，使用 notifyAll() 方法：

```java
synchronized(object) {
    object.notifyAll();
}
```

这一切之所以有效，是因为当调用 wait() 方法时，锁会被释放，这样其他感兴趣的类才能获取锁。通过请求非阻塞类执行某个操作并等待回调被触发，可以用阻塞版本包装非阻塞类。位于 javagames.threads 包中的 WaitNotifyExample 是一个简单程序，它使用 FakeHardware 类，结合 wait() 和 notifyAll() 方法，阻塞直到每个操作完成。

```java
package javagames.threads;
import javagames.threads.FakeHardware.FakeHardwareEvent;

public class WaitNotifyExample implements FakeHardwareListener {
    public WaitNotifyExample() {
    }

    public void runTest() throws Exception {
        FakeHardware hardware = new FakeHardware( "name" );
        hardware.addListener( this );
        synchronized( this ) {
            hardware.turnOn();
            while(!hardware.isOn()) {
                wait();
            }
        }
        System.out.println("Hardware is on!");
        synchronized( this ) {
            hardware.start( 1000, 4 );
            while( !hardware.isRunning() ) {
                wait();
            }
        }
        System.out.println( "Hardware is running" );
        synchronized( this ) {
            while( hardware.isRunning() ) {
                wait();
            }
        }
        System.out.println( "Hardware has stopped!" );
        synchronized( this ) {
            hardware.turnOff();
            while( hardware.isOn() ) {
                wait();
            }
        }
    }
    @Override
    public synchronized void event(
        FakeHardware source, FakeHardwareEvent event ) {
        System.out.println( "Got Event: " + event );
        notifyAll();
    }
    public static void main( String[] args ) throws Exception {
        new WaitNotifyExample().runTest();
    }
}
```

## 在游戏循环中使用线程

位于 javagames.threads 包中的 BlockingHardware 类是一个用阻塞版本包装 FakeHardware 类的类。然而，它不使用 wait/notify 方法，而是使用 Lock 和 Condition 类，这些类属于并发库。学习这些类是件好事，因为它们提供了 wait/notify 方法所没有的一些功能。请注意，锁对象提供用于通知的条件对象。这些对象的创建方式如下：

```java
Lock lock = new ReentrantLock();
Condition cond = lock.newCondition();
```

要等待对象，请调用条件的 await() 方法。Lock 类具有 lock() 和 unlock() 方法，用于获取和释放锁。使用 try/finally 块来确保锁始终被释放。

```java
lock.lock();
try {
    while( conditionNotTrue() ) {
        cond.await();
    }
} finally {
    lock.unlock();
}
```

要通知等待线程，请使用 signalAll() 方法：

```java
lock.lock();
try {
    cond.signalAll();
} finally {
    lock.unlock();
}
```

此时，你可能会好奇，为什么有人会使用这些类，而不是所有对象都可用的更简单的 wait/notify 方法。原因是 Lock/Condition 对象具有许多方法，允许更大的灵活性。例如，wait/notify 模式使用 synchronized 块。

```java
synchronized( object ) {
    // do stuff here
}
```

该代码会阻塞，直到获取锁，即使等待永远。然而，Lock 对象有其他可用于获取锁的方法，如下：

- tryLock()—该方法会尝试获取锁，如果获取成功则返回 true。不过，它不会阻塞；如果未获取锁，则返回 false。
- tryLock( long, TimeUnit )—该方法可以接受超时值，并在设定的时间后放弃尝试获取锁。

