```
23  // call the web service with the supplied name and display the message
24  private void submitJButtonActionPerformed(
25      java.awt.event.ActionEvent evt )
26  {
27      String name = nameJTextField.getText(); // get name from JTextField
28  
29      // retrieve the welcome string from the web service
30      try
31      {
32          // the URL of the web service
33          String url = "http://localhost:8080/WelcomeRESTJSON/" +
34              "resources/welcome/" + name;
35  
36          // open URL, using a Reader to convert bytes to chars
37          InputStreamReader reader =
38              new InputStreamReader( new URL( url ).openStream() );
39  
40          // parse the JSON back into a TextMessage
41          TextMessage message =
42              new Gson().fromJson( reader, TextMessage.class );
43  
44          // display message to the user
45          JOptionPane.showMessageDialog( this, message.getMessage(),
46              "Welcome", JOptionPane.INFORMATION_MESSAGE );
47      } // end try
48      catch ( Exception exception )
49      {
50          exception.printStackTrace(); // show exception details
51      } // end catch
52  } // end method submitJButtonActionPerformed
53  
54  // main method begin execution
55  public static void main( String args[] )
56  {
57      java.awt.EventQueue.invokeLater(
58          new Runnable()
59      {
60          public void run()
61          {
62              new WelcomeRESTJSONClientJFrame().setVisible( true );
63          } // end method run
64      } // end anonymous inner class
65      ); // end call to java.awt.EventQueue.invokeLater
66  } // end main
67  
68      // Variables declaration - do not modify
69      private javax.swing.JLabel nameJLabel;
70      private javax.swing.JTextField nameJTextField;
71      private javax.swing.JButton submitJButton;
72      // End of variables declaration
73  } // end class WelcomeRESTJSONClientJFrame
74
```