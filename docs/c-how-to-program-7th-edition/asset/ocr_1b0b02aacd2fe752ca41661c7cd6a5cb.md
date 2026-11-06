```
```c++
131    // update record
132    if ( client.getAccountNumber() != 0 )
133    {
134       outputLine( cout, client ); // display the record
135
136       // request user to specify transaction
137       cout << "\nEnter charge (+) or payment (-): ";
138       double transaction; // charge or payment
139       cin >> transaction;
140
141       // update record balance
142       double oldBalance = client.getBalance();
143       client.setBalance( oldBalance + transaction );
144       outputLine( cout, client ); // display the record
145
146       // move file-position pointer to correct record in file
147       updateFile.seekp( ( accountNumber - 1 ) * sizeof( ClientData ) );
148
149       // write updated record over old record in file
150       updateFile.write( reinterpret_cast< const char * >( &client ),
151          sizeof( ClientData ) );
152    } // end if
153    else // display error if account does not exist
154       cerr << "Account #" << accountNumber
155          << " has no information." << endl;
156    } // end function updateRecord
157
158    // create and insert record
159    void newRecord( fstream &insertInFile )
160    {
161       // obtain number of account to create
162       int accountNumber = getAccount( "Enter new account number" );
163
164       // move file-position pointer to correct record in file
165       insertInFile.seekg( ( accountNumber - 1 ) * sizeof( ClientData ) );
166
167       // read record from file
168       ClientData client;
169       insertInFile.read( reinterpret_cast< char * >( &client ),
170          sizeof( ClientData ) );
171
172       // create record, if record does not previously exist
173       if ( client.getAccountNumber() == 0 )
174       {
175          string lastName;
176          string firstName;
177          double balance;
178
179          // user enters last name, first name and balance
180          cout << "Enter lastname, firstname, balance? ";
181          cin >> setw( 15 ) >> lastName;
182          cin >> setw( 10 ) >> firstName;
183          cin >> balance;
```
```

Fig. 17.15 | Bank account program. (Part 4 of 6.)