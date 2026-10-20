```
31      super( "Look and Feel Demo" );
32
33      // get installed look-and-feel information
34      looks = UIManager.getInstalledLookAndFeels();
35      lookNames = new String[ looks.length ];
36
37      // get names of installed look-and-feels
38      for ( int i = 0; i < looks.length; i++ )
39          lookNames[ i ] = looks[ i ].getName();
40
41      JPanel northPanel = new JPanel(); // create north panel
42      northPanel.setLayout( new GridLayout( 3, 1, 0, 5 ) );
43
44      label = new JLabel( "This is a " + lookNames[0] + " look-and-feel",
45          SwingConstants.CENTER ); // create label
46      northPanel.add( label ); // add label to panel
47
48      button = new JButton( "JButton" ); // create button
49      northPanel.add( button ); // add button to panel
50
51      comboBox = new JComboBox( lookNames ); // create combobox
52      northPanel.add( comboBox ); // add combobox to panel
53
54      // create array for radio buttons
55      radio = new JRadioButton[ looks.length ];
56
57      JPanel southPanel = new JPanel(); // create south panel
58
59      // use a GridLayout with 3 buttons in each row
60      int rows = (int) Math.ceil( radio.length / 3.0 );
61      southPanel.setLayout( new GridLayout( rows, 3 ) );
62
63      group = new ButtonGroup(); // button group for looks-and-feels
64      ItemHandler handler = new ItemHandler(); // look-and-feel handler
65
66      for ( int count = 0; count < radio.length; count++ )
67      {
68          radio[ count ] = new JRadioButton( lookNames[ count ] );
69          radio[ count ].addItemListener( handler ); // add handler
70          group.add( radio[ count ] ); // add radio button to group
71          southPanel.add( radio[ count ] ); // add radio button to panel
72      } // end for
73
74      add( northPanel, BorderLayout.NORTH ); // add north panel
75      add( southPanel, BorderLayout.SOUTH ); // add south panel
76
77      radio[ 0 ].setSelected( true ); // set default selection
78      } // end LookAndFeelFrame constructor
79
80      // use UIManager to change look-and-feel of GUI
81      private void changeTheLookAndFeel( int value )
82      {
```