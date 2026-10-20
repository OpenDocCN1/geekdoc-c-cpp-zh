

```
114        FibonacciNumbers application = new FibonacciNumbers();
115        application.setDefaultCloseOperation( EXIT_ON_CLOSE );
116    } // end main
117 } // end class FibonacciNumbers
```

- a) 开始在后台计算第40个斐波那契数

- b) 在第40个斐波那契数继续计算的同时，计算其他斐波那契数

  ![](img/009e962758dcc71dbc43a493362e6dc0_1138_0.png)

  ![](img/009e962758dcc71dbc43a493362e6dc0_1138_1.png)

- c) 第40个斐波那契数计算完成

  ![](img/009e962758dcc71dbc43a493362e6dc0_1138_2.png)

图26.25 | 使用SwingWorker执行长时间计算并在GUI中显示结果。（第4部分，共4部分）

第48–77行注册了goJButton的事件处理器。如果用户单击此JButton，第58行获取在numberJTextField中输入的值，并尝试将其解析为整数。第72–73行创建一个新的BackgroundCalculator对象，传入用户输入的值和用于显示计算结果的fibonacciJLabel。第74行在BackgroundCalculator上调用execute方法，将其调度到单独的工作线程中执行。execute方法不会等待BackgroundCalculator执行完毕。它会立即返回，使GUI能够在计算执行的同时继续处理其他事件。

如果用户在eventThreadJPanel中单击nextNumberJButton，则执行第86–102行注册的事件处理器。第92–95行将存储在n1和n2中的前两个斐波那契数相加，以确定序列中的下一个数，将n1和n2更新为新值，并将count加1。然后第98–99行更新GUI以显示下一个数。这些计算的代码位于actionPerformed方法中，因此它们在事件分发线程上执行。在事件分发线程中处理这样短的计算不会导致GUI无响应，这与计算大数斐波那契的递归算法不同。由于较长的斐波那契计算是使用SwingWorker在单独的工作线程中执行的，因此可以在递归计算仍在进行时获得下一个斐波那契数。

## 26.11.2 使用SwingWorker处理中间结果

我们已经展示了一个使用SwingWorker类在后台线程中执行长时间进程并在进程完成时更新GUI的示例。现在，我们展示一个在长时间进程完成之前使用中间结果更新GUI的示例。图26.26展示了类PrimeCalculator，它扩展了SwingWorker，在工作线程中计算前n个素数。除了前面示例中使用的doInBackground和done方法之外，这个类还使用了SwingWorker的publish、process和setProgress方法。在此示例中，publish方法在发现素数时将素数发送给process方法，process方法在GUI组件中显示这些素数，setProgress方法更新进度属性。稍后我们将展示如何使用该属性更新JProgressBar。

```
// Fig. 26.26: PrimeCalculator.java
// Calculates the first n primes, displaying them as they are found.
import javax.swing.JTextArea;
import javax.swing.JLabel;
import javax.swing.JButton;
import javax.swing.SwingWorker;
import java.util.Arrays;
import java.util.Random;
import java.util.List;
import java.util.concurrent.CancellationException;
import java.util.concurrent.ExecutionException;

public class PrimeCalculator extends SwingWorker< Integer, Integer >
{
    private final Random generator = new Random();
    private final JTextArea intermediateJTextArea; // displays found primes
    private final JButton getPrimesJButton;
    private final JButton cancelJButton;
    private final JLabel statusJLabel; // displays status of calculation
    private final boolean[] primes; // boolean array for finding primes

    // constructor
    public PrimeCalculator( int max, JTextArea intermediate, JLabel status,
        JButton getPrimes, JButton cancel )
    {
        intermediateJTextArea = intermediate;
        statusJLabel = status;
        getPrimesJButton = getPrimes;
        cancelJButton = cancel;
        primes = new boolean[ max ];

        // initialize all prime array values to true
        Arrays.fill( primes, true );
    } // end constructor

    // finds all primes up to max using the Sieve of Eratosthenes
    public Integer doInBackground()
    {
        int count = 0; // the number of primes found

        // starting at the third value, cycle through the array and put
        // false as the value of any greater number that is a multiple
        for ( int i = 2; i < primes.length; i++ )
        {
            if ( isCancelled() ) // if calculation has been canceled
                return count;
            else
            {
                setProgress( 100 * ( i + 1 ) / primes.length );

                try
                {
                    Thread.sleep( generator.nextInt( 5 ) );
                } // end try
                catch ( InterruptedException ex )
                {
                    statusJLabel.setText( "Worker thread interrupted" );
                    return count;
                } // end catch

                if ( primes[ i ] ) // i is prime
                {
                    publish( i ); // make i available for display in prime list
                    ++count;

                    for ( int j = i + i; j < primes.length; j += i )
                        primes[ j ] = false; // j is not prime
                } // end if
            } // end else
        } // end for

        return count;
    } // end method doInBackground

    // displays published values in primes list
    protected void process( List< Integer > publishedVals )
    {
        for ( int i = 0; i < publishedVals.size(); i++ )
            intermediateJTextArea.append( publishedVals.get( i ) + "\n" );
    } // end method process

    // code to execute when doInBackground completes
    protected void done()
    {
        getPrimesJButton.setEnabled( true ); // enable Get Primes button
        cancelJButton.setEnabled( false ); // disable Cancel button

        int numPrimes;

        try
        {
```

用户单击了Cancel按钮。如果isCancelled返回true，则doInBackground方法返回迄今为止找到的素数个数（第46行），而不完成计算。

如果计算未被取消，第49行调用setProgress更新到目前为止已遍历的数组的百分比。第53行让当前执行的线程休眠最多4毫秒。我们稍后会讨论原因。第61行测试数组primes中当前索引处的元素是否为true（因此是素数）。如果是，第63行将索引传递给publish方法，以便在GUI中作为中间结果显示，第64行递增已找到的素数个数。第66–67行将当前索引的所有倍数设置为false，以表示它们不是素数。当整个数组被遍历完毕，第72行返回找到的素数个数。

### process 方法

第76–80行声明了process方法，它在事件分发线程中执行，并从publish方法接收其参数publishedVals。在工作线程中的publish与事件分发线程中的process之间传递值是异步的；并不是每次调用publish都会调用process。自上次调用process以来发布的所有整数都会以List形式由process方法接收。第78–79行遍历此列表，并在JTextArea中显示发布的值。由于doInBackground方法中的计算进展很快，频繁发布值，对JTextArea的更新可能在事件分发线程上堆积，导致GUI变得迟缓。实际上，当搜索大量素数时，事件分发线程可能会在短时间内收到如此多的更新JTextArea的请求，以至于其事件队列耗尽内存。这就是我们让工作线程在每次调用publish之间休眠几毫秒的原因。计算速度被降低到足以让事件分发线程跟上用新素数更新JTextArea的请求，从而使GUI能够平滑更新并保持响应。

### done 方法

第83–111行定义了done方法。当计算完成或取消时，done方法启用Get Primes按钮并禁用Cancel按钮（第85–86行）。第92行从doInBackground方法获取返回值——找到的素数个数。第94–108行捕获get方法抛出的异常，并在statusJLabel中显示相应的消息。如果没有异常发生，第110行设置statusJLabel以指示找到的素数个数。

### FindPrimes 类

FindPrimes类（图26.27）显示一个JTextField，允许用户输入一个数字，一个JButton用于开始查找所有小于该数字的素数，以及一个JTextArea用于显示素数。一个JButton允许用户取消计算，一个JProgressBar指示计算的进度。FindPrimes构造函数（第32–125行）设置应用程序的GUI。

第42–94行注册getPrimesJButton的事件处理器。当用户单击此JButton时，第47–49行重置JProgressBar并清除displayPrimesJTextArea和statusJLabel。第53–63行解析JTextField中的值，如果该值不是整数，则显示错误消息。第66–68行构造一个新的PrimeCalculator对象，将用户输入的整数、用于显示素数的displayPrimesJTextArea、statusJLabel以及两个JButton作为参数传递。

