

126
127     maxTextField.setHorizontalAlignment(
128         JTextField.CENTER );
129     maxTextField.setEditable( false );
130     navigatePanel.add( maxTextField );
131     navigatePanel.add( Box.createHorizontalStrut( 10 ) );
132
133     nextButton.setText( "Next" );
134     nextButton.setEnabled( false );
135     nextButton.addActionListener(
136         new ActionListener()
137         {
138             public void actionPerformed( ActionEvent evt )
139             {
140                 nextButtonActionPerformed( evt );
141             } // end method actionPerformed
142         } // end anonymous inner class
143     ); // end call to addActionListener
144
145     navigatePanel.add( nextButton );
146     add( navigatePanel );
147
148     displayPanel.setLayout( new GridLayout( 5, 2, 4, 4 ) );
149
150     idLabel.setText( "Address ID:" );
151     displayPanel.add( idLabel );
152
153     idTextField.setEditable( false );
154     displayPanel.add( idTextField );
155
156     firstNameLabel.setText( "First Name:" );
157     displayPanel.add( firstNameLabel );
158     displayPanel.add( firstNameTextField );
159
160     lastNameLabel.setText( "Last Name:" );
161     displayPanel.add( lastNameLabel );
162     displayPanel.add( lastNameTextField );
163
164     emailLabel.setText( "Email:" );
165     displayPanel.add( emailLabel );
166     displayPanel.add( emailTextField );
167
168     phoneLabel.setText( "Phone Number:" );
169     displayPanel.add( phoneLabel );
170     displayPanel.add( phoneTextField );
171     add( displayPanel );
172
173     queryPanel.setLayout(
174         new BoxLayout( queryPanel, BoxLayout.X_AXIS ) );
175
176     queryPanel.setBorder( BorderFactory.createTitledBorder(
177         "Find an entry by last name" ) );
178     queryLabel.setText( "Last Name:" );
179    queryPanel.add( Box.createHorizontalStrut( 5 ) );
180    queryPanel.add( queryLabel );
181    queryPanel.add( Box.createHorizontalStrut( 10 ) );
182    queryPanel.add( queryTextField );
183    queryPanel.add( Box.createHorizontalStrut( 10 ) );
184
185    queryButton.setText( "Find" );
186    queryButton.addActionListener(
187        new ActionListener()
188    {
189        public void actionPerformed( ActionEvent evt )
190        {
191            queryButtonActionPerformed( evt );
192        } // end method actionPerformed
193    } // end anonymous inner class
194    ); // end call to addActionListener
195
196    queryPanel.add( queryButton );
197    queryPanel.add( Box.createHorizontalStrut( 5 ) );
198    add( queryPanel );
199
200    browseButton.setText( "Browse All Entries" );
201    browseButton.addActionListener(
202        new ActionListener()
203    {
204        public void actionPerformed( ActionEvent evt )
205        {
206            browseButtonActionPerformed( evt );
207        } // end method actionPerformed
208    } // end anonymous inner class
209    ); // end call to addActionListener
210
211    add( browseButton );
212
213    insertButton.setText( "Insert New Entry" );
214    insertButton.addActionListener(
215        new ActionListener()
216    {
217        public void actionPerformed( ActionEvent evt )
218        {
219            insertButtonActionPerformed( evt );
220        } // end method actionPerformed
221    } // end anonymous inner class
222    ); // end call to addActionListener
223
224    add( insertButton );
225
226    addWindowListener(
227        new WindowAdapter()
228    {
229        public void windowClosing( WindowEvent evt )
230        {
231            personQueries.close(); // close database connection
285     else
286         browseButtonActionPerformed( evt );
287 } // end method queryButtonActionPerformed
288 
289 // handles call when a new value is entered in indexTextField
290 private void indexTextFieldActionPerformed( ActionEvent evt )
291 {
292     currentEntryIndex =
293         ( Integer.parseInt( indexTextField.getText() ) - 1 );
294 
295     if ( numberOfEntries != 0 && currentEntryIndex < numberOfEntries )
296     {
297         currentEntry = results.get( currentEntryIndex );
298         idTextField.setText( "" + currentEntry.getAddressID() );
299         firstNameTextField.setText( currentEntry.getFirstName() );
300         lastNameTextField.setText( currentEntry.getLastName() );
301         emailTextField.setText( currentEntry.getEmail() );
302         phoneTextField.setText( currentEntry.getPhoneNumber() );
303         maxTextField.setText( "" + numberOfEntries );
304         indexTextField.setText( "" + ( currentEntryIndex + 1 ) );
305     } // end if
306 } // end method indexTextFieldActionPerformed
307 
308 // handles call when browseButton is clicked
309 private void browseButtonActionPerformed( ActionEvent evt )
310 {
311     try
312     {
313         results = personQueries.getAllPeople();
314         numberOfEntries = results.size();
315 
316         if ( numberOfEntries != 0 )
317         {
318             currentEntryIndex = 0;
319             currentEntry = results.get( currentEntryIndex );
320             idTextField.setText( "" + currentEntry.getAddressID() );
321             firstNameTextField.setText( currentEntry.getFirstName() );
322             lastNameTextField.setText( currentEntry.getLastName() );
323             emailTextField.setText( currentEntry.getEmail() );
324             phoneTextField.setText( currentEntry.getPhoneNumber() );
325             maxTextField.setText( "" + numberOfEntries );
326             indexTextField.setText( "" + ( currentEntryIndex + 1 ) );
327             nextButton.setEnabled( true );
328             previousButton.setEnabled( true );
329         } // end if
330     } // end try
331     catch ( Exception e )
332     {
333         e.printStackTrace();
334     } // end catch
335 } // end method browseButtonActionPerformed

// handles call when insertButton is clicked
private void insertButtonActionPerformed( ActionEvent evt )
{
    int result = personQueries.addPerson( firstNameTextField.getText(),
        lastNameTextField.getText(), emailTextField.getText(),
        phoneTextField.getText() );

    if ( result == 1 )
        JOptionPane.showMessageDialog( this, "Person added!",
            "Person added", JOptionPane.PLAIN_MESSAGE );
    else
        JOptionPane.showMessageDialog( this, "Person not added!",
            "Error", JOptionPane.PLAIN_MESSAGE );

    browseButtonActionPerformed( evt );
} // end method insertButtonActionPerformed

// main method
public static void main( String args[] )
{
    new AddressBookDisplay();
} // end method main
} // end class AddressBookDisplay

a) 初始地址簿屏幕。

![](img/009e962758dcc71dbc43a493362e6dc0_1262_0.png)

b) 点击浏览所有条目后的结果。

![](img/009e962758dcc71dbc43a493362e6dc0_1262_1.png)

c) 浏览到下一条目。

![](img/009e962758dcc71dbc43a493362e6dc0_1262_2.png)

d) 查找姓氏为 Green 的条目。

![](img/009e962758dcc71dbc43a493362e6dc0_1262_3.png)

e) 添加新条目后并浏览到该条目。

![](img/009e962758dcc71dbc43a493362e6dc0_1263_0.png)

图 28.32 | 一个简单的地址簿。 （第 9 部分，共 9 部分。）

要向 AddressBook 数据库中添加新条目，用户可以在 JTextFields 中输入名字、姓氏、电子邮件和电话号码（AddressID 将自动递增），然后按下 Insert New Entry JButton。 将调用 insertButtonActionPerformed 处理程序（第 338–352 行）。 第 340–342 行调用 PersonQueries 对象上的 addPerson 方法，将新条目添加到数据库中。 第 351 行调用 browseButtonActionPerformed 以获取地址簿中更新的人员集合并相应地更新 GUI。

然后用户可以通过按下 Previous JButton 或 Next JButton 来查看不同的条目，这将分别导致调用 methods previousButtonActionPerformed（第 241–250 行）或 nextButtonActionPerformed（第 253–262 行）。 或者，用户可以在 indexTextField 中输入一个数字并按 Enter 来查看特定条目。 这将导致调用方法 indexTextFieldActionPerformed（第 290–306 行）以显示指定的记录。

## 28.12 存储过程

许多数据库管理系统可以将单个或一组 SQL 语句存储在数据库中，以便访问该数据库的程序可以调用它们。 这种命名的 SQL 语句集合称为存储过程。 JDBC 使程序能够使用实现 CallableStatement 接口的对象来调用存储过程。 CallableStatements 可以使用从 PreparedStatement 接口继承的方法接收参数。 此外，CallableStatements 可以指定输出参数，存储过程可以在其中放置返回值。 接口 CallableStatement 包括用于指定存储过程中哪些参数是输出参数的方法。 该接口还包括用于获取从存储过程返回的输出参数值的方法。

Portability Tip 28.6
尽管创建存储过程的语法在不同的数据库管理系统中有所不同，但接口 CallableStatement 为指定存储过程的输入和输出参数以及调用存储过程提供了一个统一的接口。

