
```cpp
104  // copy all records from record file into text file
105  while ( !readFromFile.eof() )
106  {
107     // write single record to text file
108     if ( client.getAccountNumber() != 0 ) // skip empty records
109        outputLine( cout, client );
110
111     // read next record from record file
112     readFromFile.read( reinterpret_cast< char * >( &client ),
113        sizeof( ClientData ) );
114  } // end while
115} // end function createTextFile
116
117// update balance in record
118void updateRecord( fstream &updateFile )
119{
120
121   // obtain number of account to update
122   int accountNumber = getAccount( "Enter account to update" );
123
124   // move file-position pointer to correct record in file
125   updateFile.seekp( ( accountNumber - 1 ) * sizeof( ClientData ) );
126
127   // read first record from file
128   ClientData client;
129   updateFile.read( reinterpret_cast< char * >( &client ),
130      sizeof( ClientData ) );
131
132   // update record
133   if ( client.getAccountNumber() != 0 )
134   {
135      outputLine( cout, client ); // display the record
136
137      // request user to specify transaction
138      cout << "\nEnter charge (+) or payment (-): ";
139      double transaction; // charge or payment
140      cin >> transaction;
141
142      // update record balance
143      double oldBalance = client.getBalance();
144      client.setBalance( oldBalance + transaction );
145      outputLine( cout, client ); // display the record
146
147      // move file-position pointer to correct record in file
148      updateFile.seekp( ( accountNumber - 1 ) * sizeof( ClientData ) );
149
150      // write updated record over old record in file
151      updateFile.write( reinterpret_cast< char * >( &client ),
152         sizeof( ClientData ) );
153   } // end if
154   else // display error if account does not exist
155      cerr << "Account #" << accountNumber
156           << " has no information." << endl;
157} // end function updateRecord

// create and insert record
void newRecord( fstream &insertInFile )
{
   // obtain number of account to create
   int accountNumber = getAccount( "Enter new account number" );

   // move file-position pointer to correct record in file
   insertInFile.seekg( ( accountNumber - 1 ) * sizeof( ClientData ) );

   // read record from file
   ClientData client;
   insertInFile.read( reinterpret_cast< char * >( &client ),
                      sizeof( ClientData ) );

   // create record, if record does not previously exist
   if ( client.getAccountNumber() == 0 )
   {
      string lastName;
      string firstName;
      double balance;

      // user enters last name, first name and balance
      cout << "Enter lastname, firstname, balance\n? ";
      cin >> setw( 15 ) >> lastName;
      cin >> setw( 10 ) >> firstName;
      cin >> balance;

      // use values to populate account values
      client.setLastName( lastName );
      client.setFirstName( firstName );
      client.setBalance( balance );
      client.setAccountNumber( accountNumber );

      // move file-position pointer to correct record in file
      insertInFile.seekp( ( accountNumber - 1 ) * sizeof( ClientData ) );

      // insert record in file
      insertInFile.write( reinterpret_cast< const char * >( &client ),
                          sizeof( ClientData ) );
   } // end if
   else // display error if account already exists
      cerr << "Account " << accountNumber
           << " already contains information." << endl;
} // end function newRecord

// delete an existing record
void deleteRecord( fstream &deleteFromFile )
{
   // obtain number of account to delete
   int accountNumber = getAccount( "Enter account to delete" );

// move file-position pointer to correct record in file
deleteFromFile.seekp( ( accountNumber - 1 ) * sizeof( ClientData ) );

// read record from file
ClientData client;
deleteFromFile.read( reinterpret_cast< char * >( &client ),
   sizeof( ClientData ) );

// delete record, if record exists in file
if ( client.getAccountNumber() != 0 )
{
   ClientData blankClient; // create blank record

   // move file-position pointer to correct record in file
   deleteFromFile.seekp( ( accountNumber - 1 ) *
      sizeof( ClientData ) );

   // replace existing record with blank record
   deleteFromFile.write(
      reinterpret_cast< const char * >( &blankClient ),
      sizeof( ClientData ) );

   cout << "Account " << accountNumber << " deleted.\n";
} // end if
else // display error if record does not exist
   cerr << "Account #" << accountNumber << " is empty.\n";
} // end function deleteRecord

// display single record
void outputLine( ostream &output, const ClientData &record )
{
   output << left << setw( 10 ) << record.getAccountNumber()
      << setw( 16 ) << record.getLastName()
      << setw( 11 ) << record.getFirstName()
      << setw( 10 ) << setprecision( 2 ) << right << fixed
      << showpoint << record.getBalance() << endl;
} // end function outputLine

// obtain account-number value from user
int getAccount( const char * const prompt )
{
   int accountNumber;

   // obtain account-number value
   do
   {
      cout << prompt << " (1 - 100): ";
      cin >> accountNumber;
   } while ( accountNumber < 1 || accountNumber > 100 );

   return accountNumber;
} // end function getAccount
```

*图 17.14 | 银行账户程序。（第 3 部分，共 5 部分。）*

*图 17.14 | 银行账户程序。（第 4 部分，共 5 部分。）*

*图 17.14 | 银行账户程序。（第 5 部分，共 5 部分。）*

该程序有五个选项（选项 5 用于终止程序）。选项 1 调用函数 createTextFile，将所有账户信息以格式化列表形式存储到名为 print.txt 的文本文件中，以便打印。函数 createTextFile（第 80–115 行）接收一个 fstream 对象作为参数，用于从 credit.dat 文件输入数据。函数 createTextFile 调用 istream 成员函数 read（第 101–102 行），并使用图 17.13 的顺序文件访问技术从 credit.dat 输入数据。第 17.9 节讨论的函数 outputLine 将数据输出到文件 print.txt。注意，createTextFile 使用 istream 成员函数 seekg（第 97 行）确保文件位置指针位于文件开头。选择选项 1 后，print.txt 文件包含

| 账户 | 姓氏 | 名 | 余额 |
|---:|---|---|---:|
| 29 | Brown | Nancy | -24.54 |
| 33 | Dunn | Stacey | 314.33 |
| 37 | Barker | Doug | 0.00 |
| 88 | Smith | Dave | 258.34 |
| 96 | Stone | Sam | 34.98 |

选项 2 调用 updateRecord（第 118–156 行）来更新账户。该函数只更新已存在的记录，因此函数首先判断指定记录是否为空。第 128–129 行使用 istream 成员函数 read 将数据读入对象 client。然后第 132 行将 client 对象的 getAccountNumber 返回值与零比较，以判断记录是否包含信息。如果该值为零，第 154–155 行打印错误消息，指出该记录为空。如果记录包含信息，第 134 行使用函数 outputLine 显示该记录，第 139 行输入交易金额，第 142–151 行计算新余额并将记录重写到文件中。选项 2 的典型输出为

```
Enter account to update (1 - 100): 37
37        Barker             Doug              0.00

Enter charge (+) or payment (-): +87.99
37        Barker             Doug              87.99
```

选项 3 调用函数 newRecord（第 159–201 行）向文件添加新账户。如果用户输入的账号对应已存在的账户，newRecord 会显示错误消息，指出该账户已存在（第 199–200 行）。该函数以与图 17.11 的程序相同的方式添加新账户。选项 3 的典型输出为

```
Enter new account number (1 - 100): 22
Enter lastname, firstname, balance
? Johnston Sarah 247.45
```

选项 4 调用函数 deleteRecord（第 204–235 行）从文件中删除记录。第 207 行提示用户输入账号。只有已存在的记录才能被删除，因此，如果指定账户为空，第 234 行会显示错误消息。如果账户存在，第 227–229 行通过复制一条空记录（空白-
