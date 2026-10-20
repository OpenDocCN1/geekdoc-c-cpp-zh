```
25  private JTextField idField; // textfield to display player's mark
26  private JTextArea displayArea; // JTextArea to display output
27  private JPanel boardPanel; // panel for tic-tac-toe board
28  private JPanel panel2; // panel to hold board
29  private Square[][] board; // tic-tac-toe board
30  private Square currentSquare; // current square
31  private Socket connection; // connection to server
32  private Scanner input; // input from server
33  private Formatter output; // output to server
34  private String ticTacToeHost; // host name for server
35  private String myMark; // this client's mark
36  private boolean myTurn; // determines which client's turn it is
37  private final String X_MARK = "X"; // mark for first client
38  private final String O_MARK = "O"; // mark for second client
39
40  // set up user-interface and board
41  public TicTacToeClient( String host )
42  {
43      ticTacToeHost = host; // set name of server
44      displayArea = new JTextArea( 4, 30 ); // set up JTextArea
45      displayArea.setEditable( false );
46      add( new JScrollPane( displayArea ), BorderLayout.SOUTH );
47
48      boardPanel = new JPanel(); // set up panel for squares in board
49      boardPanel.setLayout( new GridLayout( 3, 3, 0, 0 ) );
50
51      board = new Square[ 3 ][ 3 ]; // create board
52
53      // loop over the rows in the board
54      for ( int row = 0; row < board.length; row++ )
55      {
56          // loop over the columns in the board
57          for ( int column = 0; column < board[ row ].length; column++ )
58          {
59              // create square
60              board[ row ][ column ] = new Square( ' ', row * 3 + column );
61              boardPanel.add( board[ row ][ column ] ); // add square
62          } // end inner for
63      } // end outer for
64
65      idField = new JTextField(); // set up textfield
66      idField.setEditable( false );
67      add( idField, BorderLayout.NORTH );
68
69      panel2 = new JPanel(); // set up panel to contain boardPanel
70      panel2.add( boardPanel, BorderLayout.CENTER ); // add board panel
71      add( panel2, BorderLayout.CENTER ); // add container panel
72
73      setSize( 300, 225 ); // set size of window
74      setVisible( true ); // show window
75
76      startClient();
77  } // end TicTacToeClient constructor
```