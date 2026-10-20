
```
11
12     private final int value; // current menu option
13
14     // constructor
15     MenuOption( int valueOption )
16     {
17         value = valueOption;
18     } // end MenuOptions enum constructor
19
20     // return the value of a constant
21     public int getValue()
22     {
23         return value;
24     } // end method getValue
25 } // end enum MenuOption
```

Fig. 17.11 | Enumeration for the credit-inquiry program’s menu options. (Part 2 of 2.)

## CreditInquiry Class

Figure 17.12 contains the functionality for the credit-inquiry program, and Fig. 17.13 contains the main method that executes the program. The program displays a text menu and allows the credit manager to enter one of three options to obtain credit information. Option 1 (ZERO_BALANCE) displays accounts with zero balances. Option 2 (CREDIT_BALANCE) displays accounts with credit balances. Option 3 (DEBIT_BALANCE) displays accounts with debit balances. Option 4 (END) terminates program execution.

```
1  // Fig. 17.12: CreditInquiry.java
2  // This program reads a file sequentially and displays the
3  // contents based on the type of account the user requests
4  // (credit balance, debit balance or zero balance).
5  import java.io.File;
6  import java.io.FileNotFoundException;
7  import java.lang.IllegalStateException;
8  import java.util.NoSuchElementException;
9  import java.util.Scanner;
10
11  import com.deitel.ch17.AccountRecord;
12
13  public class CreditInquiry
14  {
15      private MenuOption accountType;
16      private Scanner input;
17      private final static MenuOption[] choices = { MenuOption.ZERO_BALANCE,
18          MenuOption.CREDIT_BALANCE, MenuOption.DEBIT_BALANCE,
19          MenuOption.END };
20
21      // read records from file and display only records of appropriate type
22      private void readRecords()
23      {
24          // object to store data that will be written to file
25          AccountRecord record = new AccountRecord();
```

Fig. 17.12 | Credit-inquiry program. (Part 1 of 4.)

```
26
27    try // read records
28    {
29        // open file to read from beginning
30        input = new Scanner( new File( "clients.txt" ) );
31
32        while ( input.hasNext() ) // input the values from the file
33        {
34            record.setAccount( input.nextInt() ); // read account number
35            record.setFirstName( input.next() ); // read first name
36            record.setLastName( input.next() ); // read last name
37            record.setBalance( input.nextDouble() ); // read balance
38
39            // if proper account type, display record
40            if ( shouldDisplay( record.getBalance() ) )
41                System.out.printf( "%-10d%-12s%-12s%10.2f\n",
42                    record.getAccount(), record.getFirstName(),
43                    record.getLastName(), record.getBalance() );
44        } // end while
45    } // end try
46    catch ( NoSuchElementException elementException )
47    {
48        System.err.println( "File improperly formed." );
49        input.close();
50        System.exit( 1 );
51    } // end catch
52    catch ( IllegalStateException stateException )
53    {
54        System.err.println( "Error reading from file." );
55        System.exit( 1 );
56    } // end catch
57    catch ( FileNotFoundException fileNotFoundException )
58    {
59        System.err.println( "File cannot be found." );
60        System.exit( 1 );
61    } // end catch
62    finally
63    {
64        if ( input != null )
65            input.close(); // close the Scanner and the file
66    } // end finally
67    } // end method readRecords
68
69    // use record type to determine if record should be displayed
70    private boolean shouldDisplay( double balance )
71    {
72        if ( ( accountType == MenuOption.CREDIT_BALANCE )
73            && ( balance < 0 ) )
74            return true;
75
76        else if ( ( accountType == MenuOption.DEBIT_BALANCE )
77            && ( balance > 0 ) )
78            return true;
```

```
else if ( ( accountType == MenuOption.ZERO_BALANCE )
    && ( balance == 0 ) )
    return true;

return false;
} // end method shouldDisplay

// obtain request from user
private MenuOption getRequest()
{
    Scanner textIn = new Scanner( System.in );
    int request = 1;

    // display request options
    System.out.printf( "\n%s\n%s\n%s\n%s\n%s\n",
        "Enter request", " 1 - List accounts with zero balances",
        " 2 - List accounts with credit balances",
        " 3 - List accounts with debit balances", " 4 - End of run" );

    try // attempt to input menu choice
    {
        do // input user request
        {
            System.out.print( "\n? " );
            request = textIn.nextInt();
        } while ( ( request < 1 ) || ( request > 4 ) );
    } // end try
    catch ( NoSuchElementException elementException )
    {
        System.err.println( "Invalid input." );
        System.exit( 1 );
    } // end catch

    return choices[ request - 1 ]; // return enum value for option
} // end method getRequest

public void processRequests()
{
    // get user's request (e.g., zero, credit or debit balance)
    accountType = getRequest();

    while ( accountType != MenuOption.END )
    {
        switch ( accountType )
        {
            case ZERO_BALANCE:
                System.out.println( "\nAccounts with zero balances:\n" );
                break;
            case CREDIT_BALANCE:
                System.out.println( "\nAccounts with credit balances:\n" );
                break;
```

```
131        case DEBIT_BALANCE:
132            System.out.println( "\nAccounts with debit balances:\n" );
133            break;
134        } // end switch
135
136        readRecords();
137        accountType = getRequest();
138    } // end while
139    } // end method processRequests
140 } // end class CreditInquiry
```

Fig. 17.12 | Credit-inquiry program. (Part 4 of 4.)

```
1 // Fig. 17.13: CreditInquiryTest.java
2 // This program tests class CreditInquiry.
3
4 public class CreditInquiryTest
5 {
6     public static void main( String[] args )
7     {
8         CreditInquiry application = new CreditInquiry();
9         application.processRequests();
10    } // end main
11 } // end class CreditInquiryTest
```

Fig. 17.13 | Testing the CreditInquiry class.

```
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run

? 1

Accounts with zero balances:
300        Pam        White              0.00

Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run

? 2

Accounts with credit balances:
200        Steve      Doe               -345.67
400        Sam        Stone             -42.16
```

Fig. 17.14 | Sample output of the credit-inquiry program in Fig. 17.13. (Part 1 of 2.)

```
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run

? 3

Accounts with debit balances:
100    Bob    Jones    24.98
500    Sue    Rich    224.62

? 4
```

Fig. 17.14 | Sample output of the credit-inquiry program in Fig. 17.13. (Part 2 of 2.)

The record information is collected by reading through the file and determining if each record satisfies the criteria for the selected account type. Method processRequests (lines 116–139 of Fig. 17.12) calls method getRequest to display the menu options (line 119), translates the number typed by the user into a MenuOption and stores the result in MenuOption variable accountType. Lines 121–138 loop until the user specifies that the program should terminate. Lines 123–134 display a header for the current set of records to be output to the screen. Line 136 calls method readRecords (lines 22–67), which loops through the file and reads every record.

Line 30 of method readRecords opens the file for reading with a Scanner. The file will be opened for reading with a new Scanner object each time this method is called, so that we can again read from the beginning of the file. Lines 34–37 read a record. Line 40 calls method shouldDisplay (lines 70–85) to determine whether the current record satisfies the account type requested. If shouldDisplay returns true, the program displays the account information. When the end-of-file marker is reached, the loop terminates and line 65 calls the Scanner’s close method to close the Scanner and the file. Notice that this occurs in a finally block, which will execute whether or not the file was successfully read. Once all the records have been read, control returns to method processRequests and getRequest is again called (line 137) to retrieve the user’s next menu option. Figure 17.13 contains method main, and calls method processRequests in line 9.

## 17.4.4 Updating Sequential-Access Files

The data in many sequential files cannot be modified without the risk of destroying other data in the file. For example, if the name “White” needs to be changed to “Worthington,” the old name cannot simply be overwritten, because the new name requires more space. The record for White was written to the file as

```
300 Pam White 0.00
```

If the record is rewritten beginning at the same location in the file using the new name, the record will be

```
300 Pam Worthington 0.00
```

The new record is larger (has more characters) than the original record. The characters beyond the second “o” in “Worthington” will overwrite the beginning of the next sequential
