

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

上下箭头调整帧率，以测试按键是否被遗漏。空格键按下的次数会被计数，Escape 键会重置空格键计数。processTypedChar() 方法处理输入的按键。由于所有输入的字符都在此方法中处理，包括不需要显示的按键（如 Backspace 和 Enter），因此有必要对它们进行处理。addCharacter() 和 removeCharacter() 方法负责更新输入到屏幕上的文本。updateObjects() 方法负责控制文本末尾的闪烁光标。请注意，在 processTypedChar() 方法末尾，光标闪烁会被重置。这样可以防止在输入文本时光标闪烁。

```java
drawCursor = true;
blink = 0.0f;
```

render() 方法绘制常规说明，以及空格键按下的次数。此计数可用于验证没有遗漏任何键盘按键。输入的文本使用 Utility 类绘制在说明下方。最后，绘制闪烁光标。

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

## 资源与进一步阅读

“使用文本 API，” 1995，http://docs.oracle.com/javase/tutorial/2d/text/index.html.

“字体和文本布局，” 2011，http://docs.oracle.com/javase/6/docs/technotes/guides/2d/spec/j2d-fonts.html#wp73059.

## 第 12 章

![](img/588a4cda8f2acae94a7e1987bf99400d_365_0.png)

## 线程

线程会为软件增加复杂性。它们非常复杂，而且容易出错。bug、死锁和竞争条件可能很难找到，仅仅记录日志或单步调试代码这一简单动作，就足以改变时序，导致 bug 不再发生。有句名言说，线程可以解决任何问题，除了线程太多的问题。虽然我宁愿永远不需要它们，因为它们太复杂了，但在某些情况下，线程是最佳解决方案。

> **提示**
> 
> 当程序的两个部分都在等待对方完成时，可能会发生死锁。例如，如果线程 A 正在等待线程 B 完成任务，而线程 B 正在等待线程 A 完成任务，那么两个线程将永远等待下去。
> 
> 当两个线程同时更新同一资源时，就会发生竞争条件。如果该资源没有受到保护，以至于同一时间只能有一个线程访问，那么两个线程都会尝试同时更新变量。这两个线程在竞争更新数据，具体结果取决于哪个线程先完成，可能会产生非常难以查找的 bug。

无法在一个章节中讲解你理解线程所需的一切。关于这个主题存在整本书，而且其中一些书甚至也没有涵盖所有内容。因此，如果你从未进行过线程编程，请查看本章末尾的资源。

自第一章以来，你一直在使用线程来创建与 Swing 事件分派线程分离运行的自定义游戏循环。然而，该语言中还有更多可用的类，这使得多线程编程更加容易。

## 将可调用任务与线程一起使用

存在一个 ExecutorService 接口，可以处理 Callable 任务并返回 Future 对象。Callable 对象与 Runnable 对象不同的两个非常酷的特性是：Callable 对象可以返回结果，并且可以捕获并在其他线程中重新抛出异常。这是通过使用 Future 对象实现的。Callable 接口如下：

```java
public interface Callable<V> {
    V call() throws Exception;
}
```

ExecutorService 包含一个 submit 方法，用于执行 Callable 任务并返回 Future 对象。

```java
public interface ExecutorService extends Executor {
    <T> Future<T> submit(Callable<T> task );
}
```

执行器返回的 Future 对象具有一个 get() 方法，该方法会阻塞直到 Callable 任务完成。它将返回 Callable 方法返回的结果。如果 call() 方法抛出了异常，该异常将被重新抛出，以便软件可以在当前线程中处理错误。

CallableTaskExample 位于 javagames.threads 包中，是一个简单的程序，用于演示使用 ExecutorService 执行 Callable 任务。它还演示了如何使用 Future 对象获取任务的结果和异常。CallableTaskExample 实现了 Callable<Boolean> 接口。请注意，call() 方法返回一个 Boolean 结果。该任务休眠几毫秒，返回 true 或 false，并且在随机休眠时间为零时甚至会抛出异常。main() 方法使用 Executors 类创建一个新的缓存线程池：

```java
ExecutorService exec = Executors.newCachedThreadPool();
```

缓存线程池为每个任务创建一个新线程，但在销毁它们之前会保留一小段时间。如果提交了其他任务，则会重用缓存的线程。请注意，Future 对象的 get() 方法在 Callable 任务完成之前不会返回；它会重新抛出 Callable 任务抛出的任何异常。

线程池使用 shutdown() 方法关闭。它使用 awaitTermination() 方法阻塞，直到线程池中的所有线程都完成。

