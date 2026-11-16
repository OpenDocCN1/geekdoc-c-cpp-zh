
```java
@Override
protected void processInput( float delta ) {
    super.processInput( delta );

    while( keyboard.processEvent() ) {
        if( keyboard.keyDownOnce( KeyEvent.VK_UP ) ) {
            appSleep += Math.min( appSleep * 2, 1000L );
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_DOWN ) ) {
            appSleep -= Math.min( appSleep / 2, 1000L );
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_ESCAPE ) ) {
            spacesCount = 0;
        }
        if( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
            spacesCount++;
        }
        processTypedChar();
    }
}
```

The up and down arrows adjust the frame rate to test that keypresses are not missed. The number of spacebar presses is counted, and the Escape key resets the spacebar count. The processTypedChar() method handles the typed keys. Because all typed characters are processed in this method, including keys that do not need to be displayed, such as Backspace and Enter, it is necessary to handle them. The addCharacter() and removeCharacter() methods are responsible for updating the text that is typed to the screen. The updateObjects() method is responsible for controlling the blinking cursor at the end of the text. Notice, at the end of the processTypedChar() method, that the cursor blinking is reset. This keeps the cursor from blinking while text is being typed.

```java
drawCursor = true;
blink = 0.0f;
```

The render() method draws the usual directions, along with a count of the spacebar presses. This count can be used to verify that no keyboard presses are missed. The typed text is drawn below the instructions using the Utility class. Finally, the blinking cursor is drawn.

```java
package javagames.text;
import java.awt.*;
import java.awt.event.KeyEvent;
import java.util.ArrayList;
import javagames.util.*;

public class SafeKeyboardInputExample extends SafeKeyboardFramework {
    private int spacesCount;
    private float blink;
    private boolean drawCursor;
    private ArrayList<String> strings = new ArrayList<String>();

    public SafeKeyboardInputExample() {
        appSleep = 10L;
        appTitle = "Safe Keyboard Input Example";
        strings.add( "" );
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );
        while( keyboard.processEvent() ) {
            if( keyboard.keyDownOnce( KeyEvent.VK_UP ) ) {
                appSleep += Math.min( appSleep * 2, 1000L );
            }
            if( keyboard.keyDownOnce( KeyEvent.VK_DOWN ) ) {
                appSleep -= Math.min( appSleep / 2, 1000L );
            }
            if( keyboard.keyDownOnce( KeyEvent.VK_ESCAPE ) ) {
                spacesCount = 0;
            }
            if( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
                spacesCount++;
            }
            processTypedChar();
        }
    }

    private void processTypedChar() {
        Character typedChar = keyboard.getKeyTyped();
        if( typedChar != null ) {
            if( Character.isISOControl( typedChar ) ) {
                if( KeyEvent.VK_BACK_SPACE == typedChar ) {
                    removeCharacter();
                }
                if (KeyEvent.VK_ENTER == typedChar ) {
                    strings.add( "" );
                }
                else {
                    addCharacter( typedChar );
                }
            }
        }
        drawCursor = true;
        blink = 0.0f;
    }

    private void addCharacter( Character c ) {
        strings.add( strings.remove( strings.size() - 1 ) + c );
    }

    private void removeCharacter() {
        String line = strings.remove( strings.size() - 1 );
        if ( line.isEmpty() ) {
            strings.add( line.substring( 0, line.length() - 1 ) );
        }

        if ( strings.isEmpty() ) {
            strings.add( "" );
        }
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );

        blink += delta;
        if ( blink > 0.5f ) {
            blink = -0.5f;
            drawCursor = !drawCursor;
        }
    }

    @Override
    protected void render( Graphics g ) {
        super.render( g );

        textPos = Utility.drawString( g, 20, textPos,
            "",
            "Sleep Value: " + appSleep,
            "Space Count: " + spacesCount,
            "Press Up to increase sleep",
            "Press Down to decrease sleep",
            "Press ESC to clear spaces count"
        );
        textPos = Utility.drawString( g, 20, textPos, strings );
        if ( drawCursor ) {
            FontMetrics fm = g.getFontMetrics();
            int height = fm.getAscent() + fm.getDescent() + fm.getLeading();
            int y = textPos - height;
            int x = 20 + fm.stringWidth( strings.get( strings.size() - 1 ) );
            g.drawString( " .", x, y + fm.getAscent() );
        }
    }
    public static void main( String[] args ) {
        launchApp( new SafeKeyboardInputExample() );
    }
}
```

## RESOURCES AND FURTHER READING

“Working with Text APIs,” 1995, http://docs.oracle.com/javase/tutorial/2d/text/index.html.

“Fonts and Text Layout,” 2011, http://docs.oracle.com/javase/6/docs/technotes/guides/2d/spec/j2d-fonts.html#wp73059.

## CHAPTER 12

![](img/588a4cda8f2acae94a7e1987bf99400d_365_0.png)

## THREADS

Threads can add complexity to software. They are very complicated and easy to get wrong. Bugs, deadlocks, and race conditions can be difficult to find, and the simple act of logging or stepping through the code can change the timing enough so the bugs no longer happen. It has been said that threads can solve any problem except too many threads. Although I would prefer to never need them, because they are so complex, there are some situations where threads are the best solution.

> **Tip**
> 
> Deadlocks can occur when two parts of the program are waiting for the other to finish. For example, if thread A is waiting for thread B to finish a task, but thread B is waiting for thread A to finish a task, both threads will wait forever.
> 
> A race condition occurs when two threads are both updating a resource at the same time. If that resource is not protected so that only one thread can have access at a time, both threads will try to update the variable simultaneously. These two threads are racing to update the data, and depending on which one gets there first, the results can produce bugs that are very hard to find.

There is no way to teach everything you need to understand threads in a single chapter. Entire books exist on the subject and some of these don't even cover everything. So, if you have never done any thread programming, check out the resources at the end of the chapter.

Since the very first chapter, you have been using threads to create a custom game loop that runs apart from Swing's event dispatch thread. However, there are many more classes available in the language, which makes multithreaded programming easier.

## USING THE CALLABLE TASK WITH THREADS

There exists an ExecutorService interface that can process Callable tasks and return Future objects. Two really cool features that make Callable objects different from Runnable objects are that Callable objects can return a result, and they can capture and rethrow exceptions inside other threads. This is possible by using a Future object. The Callable interface is as follows:

```java
public interface Callable<V> {
    V call() throws Exception;
}
```

The ExecutorService contains a submit method, which executes a Callable task and returns a Future object.

```java
public interface ExecutorService extends Executor {
    <T> Future<T> submit(Callable<T> task );
}
```

The Future object returned from the executor has a get() method that will block until the Callable task has finished. It will return the result that was returned from the Callable method. If the call() method threw an exception, that exception will be rethrown so the software can handle the error in the current thread.

The CallableTaskExample, located in the javagames.threads package, is a simple program to demonstrate using the ExecutorService to execute Callable tasks. It also demonstrates using the Future objects to get the results and exceptions from the tasks. The CallableTaskExample implements the Callable<Boolean> interface. Notice that the call() method returns a Boolean result. The task sleeps for a few milliseconds, returns true or false, and even throws an exception when the random sleep time is zero. The main() method uses the Executors class to create a new cached thread pool:

```java
ExecutorService exec = Executors.newCachedThreadPool();
```

The cached thread pool creates a new thread for each task, but keeps those threads around for a little while before destroying them. If other tasks are submitted, the cached threads are reused. Notice how the get() method from the Future object will not return until the Callable task is finished; it rethrows any exceptions thrown by the Callable task.

The thread pool is shut down with the shutdown() method. It uses the awaitTermination() method to block until all the threads in the thread pool have finished.
