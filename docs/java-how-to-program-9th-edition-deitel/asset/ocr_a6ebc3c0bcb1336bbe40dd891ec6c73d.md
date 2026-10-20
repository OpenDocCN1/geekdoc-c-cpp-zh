```
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
120
121    add( northJPanel, BorderLayout.NORTH );
122    add( southJPanel, BorderLayout.SOUTH );
123    setSize( 350, 300 );
124    setVisible( true );
125    } // end constructor
126
127    // main method begins program execution
128    public static void main( String[] args )
129    {
130        FindPrimes application = new FindPrimes();
131        application.setDefaultCloseOperation( EXIT_ON_CLOSE );
132    } // end main
133    } // end class FindPrimes
```

![](bbox=[0.13, 0.6, 0.87, 0.82])

Fig. 26.27 | Using a SwingWorker to display prime numbers and update a JProgressBar while the prime numbers are being calculated. (Part 3 of 3.)

Lines 71–85 register a PropertyChangeListener for the PrimeCalculator object. PropertyChangeListener is an interface from package java.beans that defines a single method, propertyChange. Every time method setProgress is invoked on a PrimeCalcu-