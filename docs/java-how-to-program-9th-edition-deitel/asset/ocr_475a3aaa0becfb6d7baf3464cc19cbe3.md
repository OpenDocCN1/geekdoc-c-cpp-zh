```
176     String url = String.format( "http://localhost:8080/" +
177         "EquationGeneratorXML/resources/equation/%s/%d",
178         operation, difficulty );
179
180     // convert XML back to an Equation object
181     Equation equation = JAXB.unmarshal( url, Equation.class );
182
183     answer = equation.getResult();
184     equationJLabel.setText( equation.getLeftHandSide() + " =" );
185     checkAnswerJButton.setEnabled( true );
186 } // end try
187 catch ( Exception exception )
188 {
189     exception.printStackTrace();
190 } // end catch
191 } // end method generateJButtonActionPerformed
192
193 // obtains the mathematical operation selected by the user
194 private void operationJComboBoxItemStateChanged(
195     java.awt.event.ItemEvent evt)
196 {
197     String item = ( String ) operationJComboBox.getSelectedItem();
198
199     if ( item.equals( "Addition" ) )
200         operation = "add"; // user selected addition
201     else if ( item.equals( "Subtraction" ) )
202         operation = "subtract"; // user selected subtraction
203     else
204         operation = "multiply"; // user selected multiplication
205 } // end method operationJComboBoxItemStateChanged
206
207 // obtains the difficulty level selected by the user
208 private void levelJComboBoxItemStateChanged(
209     java.awt.event.ItemEvent evt)
210 {
211     // indices start at 0, so add 1 to get the difficulty level
212     difficulty = levelJComboBox.getSelectedIndex() + 1;
213 } // end method levelJComboBoxItemStateChanged
214
215 // main method begins execution
216 public static void main(String args[])
217 {
218     java.awt.EventQueue.invokeLater(
219         new Runnable()
220         {
221             public void run()
222             {
223                 new EquationGeneratorXMLClientJFrame().setVisible( true );
224             } // end method run
225         } // end anonymous inner class
226     ); // end call to java.awt.EventQueue.invokeLater
227 } // end main
228
```