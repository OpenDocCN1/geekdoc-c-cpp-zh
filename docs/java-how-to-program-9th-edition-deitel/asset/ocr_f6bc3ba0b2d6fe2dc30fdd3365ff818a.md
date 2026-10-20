```
23    super( "Simple Web Browser" );
24
25    // create enterField and register its listener
26    enterField = new JTextField( "Enter file URL here" );
27    enterField.addActionListener(
28        new ActionListener()
29    {
30        // get document specified by user
31        public void actionPerformed( ActionEvent event )
32        {
33            getThePage( event.getActionCommand() );
34        } // end method actionPerformed
35    } // end inner class
36    ); // end call to addActionListener
37
38    add( enterField, BorderLayout.NORTH );
39
40    contentsArea = new JEditorPane(); // create contentsArea
41    contentsArea.setEditable( false );
42    contentsArea.addHyperlinkListener(
43        new HyperlinkListener()
44    {
45        // if user clicked hyperlink, go to specified page
46        public void hyperlinkUpdate( HyperlinkEvent event )
47        {
48            if ( event.getEventType() ==
49                HyperlinkEvent.EventType.ACTIVATED )
50                getThePage( event.getURL().toString() );
51        } // end method hyperlinkUpdate
52    } // end inner class
53    ); // end call to addHyperlinkListener
54
55    add( new JScrollPane( contentsArea ), BorderLayout.CENTER );
56    setSize( 400, 300 ); // set size of window
57    setVisible( true ); // show window
58    } // end ReadServerFile constructor
59
60    // load document
61    private void getThePage( String location )
62    {
63    try // load document and display location
64    {
65        contentsArea.setPage( location ); // set the page
66        enterField.setText( location ); // set the text
67    } // end try
68    catch ( IOException ioException )
69    {
70        JOptionPane.showMessageDialog( this,
71            "Error retrieving specified URL", "Bad URL",
72            JOptionPane.ERROR_MESSAGE );
73    } // end catch
74    } // end method getThePage
75    } // end class ReadServerFile
```