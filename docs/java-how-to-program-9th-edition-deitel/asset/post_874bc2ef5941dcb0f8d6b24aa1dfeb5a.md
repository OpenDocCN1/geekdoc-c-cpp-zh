
```
6      public static void main( String[] args )
7      {
8          CreateTextFile application = new CreateTextFile();
9
10         application.openFile();
11         application.addRecords();
12         application.closeFile();
13     } // end main
14 } // end class CreateTextFileTest
```

To terminate input, type the end-of-file indicator when you are prompted to enter input.
On UNIX/Linux/Mac OS X type <ctrl> d then press Enter
On Windows type <ctrl> z then press Enter

Enter account number (> 0), first name, last name and balance.
? 100 Bob Jones 24.98
Enter account number (> 0), first name, last name and balance.
? 200 Steve Doe -345.67
Enter account number (> 0), first name, last name and balance.
? 300 Pam White 0.00
Enter account number (> 0), first name, last name and balance.
? 400 Sam Stone -42.16
Enter account number (> 0), first name, last name and balance.
? 500 Sue Rich 224.62
Enter account number (> 0), first name, last name and balance.
? ^Z

Fig. 17.7 | Testing the CreateTextFile class. (Part 2 of 2.)

| Sample data |  |  |  |
|---|---|---|---|
| 100 | Bob | Jones | 24.98 |
| 200 | Steve | Doe | -345.67 |
| 300 | Pam | White | 0.00 |
| 400 | Sam | Stone | -42.16 |
| 500 | Sue | Rich | 224.62 |

Fig. 17.8 | Sample data for the program in Figs. 17.5–17.7.

## 17.4.2 Reading Data from a Sequential-Access Text File

Data is stored in files so that it may be retrieved for processing when needed. Section 17.4.1 demonstrated how to create a file for sequential access. This section shows how to read data sequentially from a text file. We demonstrate how class Scanner can be used to input data from a file rather than the keyboard.

The application in Figs. 17.9 and 17.10 reads records from the file "clients.txt" created by the application of Section 17.4.1 and displays the record contents. Line 13 of Fig. 17.9 declares a Scanner that will be used to retrieve input from the file.

// Fig. 17.9: ReadTextFile.java
// This program reads a text file and displays each record.
import java.io.File;
import java.io.FileNotFoundException;
import java.lang.IllegalStateException;
import java.util.NoSuchElementException;
import java.util.Scanner;

import com.deitel.ch17.AccountRecord;

public class ReadTextFile
{
    private Scanner input;

    // enable user to open file
    public void openFile()
    {
        try
        {
            input = new Scanner( new File( "clients.txt" ) );
        } // end try
        catch ( FileNotFoundException fileNotFoundException )
        {
            System.err.println( "Error opening file." );
            System.exit( 1 );
        } // end catch
    } // end method openFile

    // read record from file
    public void readRecords()
    {
        // object to be written to screen
        AccountRecord record = new AccountRecord();

        System.out.printf( "% -10s%-12s%-12s%10s\n", "Account",
            "First Name", "Last Name", "Balance" );

        try // read records from file using Scanner object
        {
            while ( input.hasNext() )
            {
                record.setAccount( input.nextInt() ); // read account number
                record.setFirstName( input.next() ); // read first name
                record.setLastName( input.next() ); // read last name
                record.setBalance( input.nextDouble() ); // read balance

                // display record contents
                System.out.printf( "% -10d%-12s%-12s%10.2f\n",
                    record.getAccount(), record.getFirstName(),
                    record.getLastName(), record.getBalance() );
            } // end while
        } // end try
```
53      catch ( NoSuchElementException elementException )
54      {
55          System.err.println( "File improperly formed." );
56          input.close();
57          System.exit( 1 );
58      } // end catch
59      catch ( IllegalStateException stateException )
60      {
61          System.err.println( "Error reading from file." );
62          System.exit( 1 );
63      } // end catch
64      } // end method readRecords

      // close file and terminate application
      public void closeFile()
      {
          if ( input != null )
              input.close(); // close file
      } // end method closeFile
  } // end class ReadTextFile

# Fig. 17.9 | Sequential file reading using a Scanner. (Part 2 of 2.)

```
1  // Fig. 17.10: ReadTextFileTest.java
2  // Testing the ReadTextFile class.
3
4  public class ReadTextFileTest
5  {
6      public static void main( String[] args )
7      {
8          ReadTextFile application = new ReadTextFile();
9
10         application.openFile();
11         application.readRecords();
12         application.closeFile();
13     } // end main
14  } // end class ReadTextFileTest
```

| Account | First Name | Last Name | Balance |
|---|---|---|---|
| 100 | Bob | Jones | 24.98 |
| 200 | Steve | Doe | -345.67 |
| 300 | Pam | White | 0.00 |
| 400 | Sam | Stone | -42.16 |
| 500 | Sue | Rich | 224.62 |

# Fig. 17.10 | Testing the ReadTextFile class.

Method openFile (lines 16–27) opens the file for reading by instantiating a Scanner object in line 20. We pass a File object to the constructor, which specifies that the Scanner object will read from the file "clients.txt" located in the directory from which the application executes. If the file cannot be found, a FileNotFoundException occurs. The exception is handled in lines 22–26.

Method readRecords (lines 30–64) reads and displays records from the file. Line 33 creates AccountRecord object record to store the current record’s information. Lines 35–36 display headers for the columns in the application’s output. Lines 40–51 read data from the file until the end-of-file marker is reached (in which case, method hasNext will return false at line 40). Lines 42–45 use Scanner methods nextInt, next and nextDouble to input an int (the account number), two Strings (the first and last names) and a double value (the balance). Each record is one line of data in the file. The values are stored in object record. If the information in the file is not properly formed (e.g., there’s a last name where there should be a balance), a NoSuchElementException occurs when the record is input. This exception is handled in lines 53–58. If the Scanner was closed before the data was input, an IllegalStateException occurs (handled in lines 59–63). If no exceptions occur, the record’s information is displayed on the screen (lines 48–50). Note in the format string in line 48 that the account number, first name and last name are left justified, while the balance is right justified and output with two digits of precision. Each iteration of the loop inputs one line of text from the text file, which represents one record.

Lines 67–71 define method closeFile, which closes the Scanner. Method main is defined in Fig. 17.10 in lines 6–13. Line 8 creates a ReadTextFile object, which is then used to open, add records to and close the file (lines 10–12).

## 17.4.3 Case Study: A Credit-Inquiry Program

To retrieve data sequentially from a file, programs start from the beginning of the file and read all the data consecutively until the desired information is found. It might be necessary to process the file sequentially several times (from the beginning of the file) during the execution of a program. Class Scanner does not allow repositioning to the beginning of the file. If it’s necessary to read the file again, the program must close the file and reopen it.

The program in Figs. 17.11–17.13 allows a credit manager to obtain lists of customers with zero balances (i.e., customers who do not owe any money), customers with credit balances (i.e., customers to whom the company owes money) and customers with debit balances (i.e., customers who owe the company money for goods and services received). A credit balance is a negative amount, a debit balance a positive amount.

### MenuOption Enumeration

We begin by creating an enum type (Fig. 17.11) to define the different menu options the user will have. The options and their values are listed in lines 7–10. Method getValue (lines 19–22) retrieves the value of a specific enum constant.

```
1  // Fig. 17.11: MenuOption.java
2  // Enumeration for the credit-inquiry program's options.
3
4  public enum MenuOption
5  {
6      // declare contents of enum type
7      ZERO_BALANCE( 1 ),
8      CREDIT_BALANCE( 2 ),
9      DEBIT_BALANCE( 3 ),
10     END( 4 );
```

Fig. 17.11 | Enumeration for the credit-inquiry program’s menu options. (Part 1 of 2.)
