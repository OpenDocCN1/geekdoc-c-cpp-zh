
// Fig 26.27: FindPrimes.java
// Using a SwingWorker to display prime numbers and update a JProgressBar
// while the prime numbers are being calculated.
import javax.swing.JFrame;
import javax.swing.JTextField;
import javax.swing.JTextArea;
import javax.swing.JButton;
import javax.swing.JProgressBar;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.ScrollPaneConstants;
import java.awt.BorderLayout;
import java.awt.GridLayout;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.util.concurrent.ExecutionException;
import java.beans.PropertyChangeListener;
import java.beans.PropertyChangeEvent;

public class FindPrimes extends JFrame
{
    private final JTextField highestPrimeJTextField = new JTextField();
    private final JButton getPrimesJButton = new JButton("Get Primes");
    private final JTextArea displayPrimesJTextArea = new JTextArea();
    private final JButton cancelJButton = new JButton("Cancel");
    private final JProgressBar progressJProgressBar = new JProgressBar();
    private final JLabel statusJLabel = new JLabel();
    private PrimeCalculator calculator;

    // constructor
    public FindPrimes()
    {
        super("Finding Primes with SwingWorker");
        setLayout(new BorderLayout());

        // initialize panel to get a number from the user
        JPanel northJPanel = new JPanel();
        northJPanel.add(new JLabel("Find primes less than: "));
        highestPrimeJTextField.setColumns(5);
        northJPanel.add(highestPrimeJTextField);
        getPrimesJButton.addActionListener(
            new ActionListener()
            {
                public void actionPerformed(ActionEvent e)
                {
                    progressJProgressBar.setValue(0); // reset JProgressBar
                    displayPrimesJTextArea.setText(""); // clear JTextArea
                    statusJLabel.setText(""); // clear JLabel

                    int number; // search for primes up through this value
52
53     try
54     {
55         // get user input
56         number = Integer.parseInt(
57             highestPrimeJTextField.getText() );
58     } // end try
59     catch ( NumberFormatException ex )
60     {
61         statusJLabel.setText( "Enter an integer." );
62         return;
63     } // end catch
64
65     // construct a new PrimeCalculator object
66     calculator = new PrimeCalculator( number,
67         displayPrimesJTextArea, statusJLabel, getPrimesJButton,
68         cancelJButton );
69
70     // listen for progress bar property changes
71     calculator.addPropertyChangeListener(
72         new PropertyChangeListener()
73         {
74             public void propertyChange( PropertyChangeEvent e )
75             {
76                 // if the changed property is progress,
77                 // update the progress bar
78                 if( e.getPropertyName().equals( "progress" ) )
79                 {
80                     int newValue = ( Integer ) e.getNewValue();
81                     progressJProgressBar.setValue( newValue );
82                 } // end if
83             } // end method propertyChange
84         } // end anonymous inner class
85     ); // end call to addPropertyChangeListener
86
87     // disable Get Primes button and enable Cancel button
88     getPrimesJButton.setEnabled( false );
89     cancelJButton.setEnabled( true );
90
91     calculator.execute(); // execute the PrimeCalculator object
92     } // end method ActionPerformed
93     } // end anonymous inner class
94 ); // end call to addActionListener
95     northJPanel.add( getPrimesJButton );

    // add a scrollable JTextArea to display results of calculation
    displayPrimesJTextArea.setEditable( false );
    add( new JScrollPane( displayPrimesJTextArea,
        ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS,
        ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER ) );

Fig. 26.27 | Using a SwingWorker to display prime numbers and update a JProgressBar while the prime numbers are being calculated. (Part 2 of 3.)

103    // initialize a panel to display cancelJButton,
104    // progressJProgressBar, and statusJLabel
105    JPanel southJPanel = new JPanel( new GridLayout( 1, 3, 10, 10 ) );
106    cancelJButton.setEnabled( false );
107    cancelJButton.addActionListener(
108        new ActionListener()
109    {
110        public void actionPerformed( ActionEvent e )
111        {
112            calculator.cancel( true ); // cancel the calculation
113        } // end method ActionPerformed
114    } // end anonymous inner class
115    ); // end call to addActionListener
116    southJPanel.add( cancelJButton );
117    progressJProgressBar.setStringPainted( true );
118    southJPanel.add( progressJProgressBar );
119    southJPanel.add( statusJLabel );

120    add( northJPanel, BorderLayout.NORTH );
121    add( southJPanel, BorderLayout.SOUTH );
122    setSize( 350, 300 );
123    setVisible( true );
125    } // end constructor

    // main method begins program execution
    public static void main( String[] args )
    {
        FindPrimes application = new FindPrimes();
        application.setDefaultCloseOperation( EXIT_ON_CLOSE );
    } // end main
} // end class FindPrimes

![](img/009e962758dcc71dbc43a493362e6dc0_1145_0.png)

Fig. 26.27 | Using a SwingWorker to display prime numbers and update a JProgressBar while the prime numbers are being calculated. (Part 3 of 3.)

Lines 71–85 register a PropertyChangeListener for the PrimeCalculator object. PropertyChangeListener is an interface from package java.beans that defines a single method, propertyChange. Every time method setProgress is invoked on a PrimeCalculator, the PrimeCalculator generates a PropertyChangeEvent to indicate that the progress property has changed. Method propertyChange listens for these events. Line 78 tests whether a given PropertyChangeEvent indicates a change to the progress property. If so, line 80 gets the new value of the property and line 81 updates the JProgressBar with the new progress property value.

The Get Primes JButton is disabled (line 88) so only one calculation that updates the GUI can execute at a time, and the Cancel JButton enabled (line 89) to allow the user to stop the computation before it completes. Line 91 executes the PrimesCalculator to begin finding primes. If the user clicks the cancel JButton, the event handler registered to lines 107–115 calls PrimeCalculator’s method cancel (line 112), which is inherited from class SwingWorker, and the calculation returns early. The argument true to method cancel indicates that the thread performing the task should be interrupted in an attempt to cancel the task.

## 26.12 Interfaces Callable and Future

Interface Runnable provides only the most basic functionality for multithreaded programming. In fact, this interface has several limitations. Suppose a Runnable encounters a problem and tries to throw a checked exception. The run method is not declared to throw any exceptions, so the problem must be handled within the Runnable—the exception cannot be passed to the calling thread. Now suppose a Runnable is performing a long calculation and the application wants to retrieve the result of that calculation. The run method cannot return a value, so the application must use shared data to pass the value back to the calling thread. This also involves the overhead of synchronizing access to the data. The developers of the concurrency APIs recognized these limitations and created a new interface to fix them. The Callable interface (of package java.util.concurrent) declares a single method named call. This interface is designed to be similar to the Runnable interface—allowing an action to be performed concurrently in a separate thread—but the call method allows the thread to return a value or to throw a checked exception.

An application that creates a Callable likely wants to run it concurrently with other Runnables and Callables. The ExecutorService interface provides method submit, which will execute a Callable passed in as its argument. The submit method returns an object of type Future (of package java.util.concurrent), which is an interface that represents the executing Callable. The Future interface declares method get to return the result of the Callable and provides other methods to manage a Callable’s execution.

## 26.13 Java SE 7: Fork/Join Framework

Java SE 7’s concurrency APIs include the new fork/join framework, which programmers parallelize algorithms. The framework is beyond the scope of this book. Experts tell us that most Java programmers will benefit by this framework being used “behind the scenes” in the Java API and other third party libraries.

The fork/join framework is particularly well suited to divide-and-conquer-style algorithms, such as the merge sort that we implemented in Section 19.3.3. Recall that the recursive algorithm sorts an array by splitting it into two equal-sized subarrays, sorting each subarray, then merging them into one larger array. Each subarray is sorted by performing the same algorithm on the subarray. For algorithms like merge sort, the fork/join frame-
