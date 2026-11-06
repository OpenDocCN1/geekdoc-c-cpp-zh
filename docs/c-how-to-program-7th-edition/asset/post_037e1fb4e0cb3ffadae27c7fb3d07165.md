
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

Fig. 17.15 | Bank account program. (Part 4 of 6.)

### Section 17.5 Reading Data from a Sequential File

- Files store data so it may be retrieved for processing when needed.
- Creating an ifstream object opens a file for input. The ifstream constructor can receive the file-name and the file open mode as arguments.
- Open a file for input only if the file’s contents should not be modified.
- Objects of class ifstream are opened for input by default.
- An ifstream object can be created without opening a specific file; a file can be attached to it later.
- To retrieve data sequentially from a file, programs normally start reading from the beginning of the file and read all the data consecutively until the desired data is found.
- Both istream and ostream provide member functions for repositioning the file-position pointer. These member functions are seekg (“seek get”) for istream and seekp (“seek put”) for ostream. Each istream object has a “get pointer,” which indicates the byte number in the file from which the next input is to occur, and each ostream object has a “put pointer,” which indicates the byte number in the file at which the next output should be placed.
- The argument to seekg normally is a long integer. A second argument can be specified to indicate the seek direction, which can be ios::beg (the default) for positioning relative to the beginning of a stream, ios::cur for positioning relative to the current position in a stream or ios::end for positioning relative to the end of a stream.
- The file-position pointer is an integer value that specifies the location in the file as a number of bytes from the file’s starting location (i.e., the offset from the beginning of the file).
- Member functions tellg and tellp are provided to return the current locations of the “get” and “put” pointers, respectively.

### Section 17.6 Updating Sequential Files

- Data that is formatted and written to a sequential file cannot be modified without the risk of destroying other data in the file. The problem is that records can vary in size.

### Section 17.7 Random-Access Files

- Sequential files are inappropriate for instant-access applications, in which a particular record must be located immediately.
- Instant access is made possible with random-access files. Individual records of a random-access file can be accessed directly (and quickly) without having to search other records.
- The easiest method to format files for random access is to require that all records in a file be of the same fixed length. Using same-size, fixed-length records makes it easy for a program to calculate (as a function of the record size and the record key) the exact location of any record relative to the beginning of the file.
- Data can be inserted into a random-access file without destroying other data in the file.
- Data stored previously can be updated or deleted without rewriting the entire file.

### Section 17.8 Creating a Random-Access File

- The ostream member function write outputs a fixed number of bytes, beginning at a specific location in memory, to the specified stream. Function write writes the data at the location in the file specified by the “put” file-position pointer.

**17.3**

```c++
a) ifstream inOldMaster("oldmast.dat", ios::in );
b) fstream inTransaction ("trans.dat", ios::in );
c) ofstream outNewMaster ("newmast.dat", ios::out );
d) inOldMaster >> accountNumber >> name >> currentBalance;
e) inTransaction >> accountNum >> dollarAmount;
f) outNewMaster << accountNum << name << currentBalance;
```

**17.4**

a) *Error:* The file `payables.dat` has not been opened before the attempt is made to output data to the stream.

*Correction:* Use `ofstream` function `open` to open `payables.dat` for output.

b) *Error:* The incorrect stream object is being used to read a record from the file named `payables.dat`.

*Correction:* Use stream object `inPayable` to refer to `payables.dat`.

c) *Error:* The file’s contents are discarded because the file is opened for output (`ios::out`).

*Correction:* To add data to the file, open the file either for updating (`ios::ate`) or for appending (`ios::app`).

## Exercises

**17.5** Fill in the blanks in each of the following:

a) Computers store large amounts of data on secondary storage devices as ________.
b) A(n) ________ is composed of several fields.
c) To facilitate the retrieval of specific records from a file, one field in each record is chosen as a(n) ________.
d) The vast majority of information stored in computer systems is stored in ________ files.
e) A group of related characters that conveys meaning is called a(n) ________.
f) The standard stream objects declared by header `<iostream>` are ________, ________, ________ and ________.
g) `ostream` member function ________ outputs a character to the specified stream.
h) `ostream` member function ________ is generally used to write data to a randomly accessed file.
i) `istream` member function ________ repositions the file-position pointer in a file.

**17.6** State which of the following are *true* and which are *false*. If *false*, explain why.

a) The impressive functions performed by computers essentially involve the manipulation of zeros and ones.
b) People prefer to manipulate bits instead of characters and fields because bits are more compact.
c) People specify programs and data items as characters; computers then manipulate and process these characters as groups of zeros and ones.
d) A person’s 5-digit zip code is an example of a numeric field.
e) A person’s street address is generally considered to be an alphabetic field in computer applications.
f) Data items represented in computers form a data hierarchy in which data items become larger and more complex as we progress from fields to characters to bits, etc.
g) A record key identifies a record as belonging to a particular field.
h) Most organizations store all information in a single file to facilitate computer processing.
i) When a program creates a file, the file is automatically retained by the computer for future reference; i.e., files are said to be persistent.

**17.7** *(File Matching)* Exercise 17.3 asked you to write a series of single statements. Actually, these statements form the core of an important type of file-processing program, namely, a file-matching program. In commercial data processing, it’s common to have several files in each application.
