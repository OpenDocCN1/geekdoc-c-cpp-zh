
// Fig. 17.3: FileDemonstration.java
// File class used to obtain file and directory information.
import java.io.File;
import java.util.Scanner;

public class FileDemonstration
{
    public static void main( String[] args )
    {
        Scanner input = new Scanner( System.in );

        System.out.print( "Enter file or directory name: " );
        analyzePath( input.nextLine() );
    } // end main

    // display information about file user specifies
    public static void analyzePath( String path )
    {
        // create File object based on user input
        File name = new File( path );

        if ( name.exists() ) // if name exists, output information about it
        {
            // display file (or directory) information
            System.out.printf(
                "%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s",
                name.getName(), " exists",
                ( name.isFile() ? "is a file" : "is not a file" ),
                ( name.isDirectory() ? "is a directory" :
                "is not a directory" ),
                ( name.isAbsolute() ? "is absolute path" :
                "is not absolute path" ), "Last modified: ",
                name.lastModified(), "Length: ", name.length(),
                "Path: ", name.getPath(), "Absolute path: ",
                name.getAbsolutePath(), "Parent: ", name.getParent() );

            if ( name.isDirectory() ) // output directory listing
            {
                String[] directory = name.list();
                System.out.println( "\n\nDirectory contents:\n" );

                for ( String directoryName : directory )
                    System.out.println( directoryName );
            } // end if
        } // end outer if
        else // not file or directory, output error message
        {
            System.out.printf( "%s %s", path, "does not exist." );
        } // end else
    } // end method analyzePath
} // end class FileDemonstration

Enter file or directory name: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
jfc exists
is not a file
is a directory
is absolute path
Last modified: 1228404395024
Length: 4096
Path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
Absolute path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
Parent: E:\Program Files\Java\jdk1.6.0_11\demo\jfc

Directory contents:
CodePointIM
FileChooserDemo
Font2DTest
Java2D
Laffy
Metalworks
Notepad
SampleTree
Stylepad
SwingApplet
SwingSet
SwingSet2
SwingSet3

Enter file or directory name: C:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
README.txt exists
is not a directory
is not a file
is absolute path
Last modified: 1228404384270
Length: 7518
Path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
Absolute path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
Parent: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D

## Fig. 17.3 | File class used to obtain file and directory information. (Part 2 of 2.)

(either as a file or as a directory) on the disk. If the name does not exist, control proceeds to lines 46–49 and displays a message to the screen containing the name the user typed, followed by “does not exist.” Otherwise, the if statement (lines 22–45) executes. The program outputs the name of the file or directory (line 27), followed by the results of testing the File object with isFile (line 28), isDirectory (line 29) and isAbsolute (line 31). Next, the program displays the values returned by lastModified (line 33), length (line 33), getPath (line 34), getAbsolutePath (line 35) and getParent (line 35). If the File object represents a directory (line 37), the program obtains a list of the directory’s contents as an array of Strings by using File method list (line 39) and displays the list on the screen.

The first output of this program demonstrates a File object associated with the jfc directory from the JDK. The second output demonstrates a File object associated with the README.txt file from the Java 2D example that comes with the JDK. In both cases, we specified an absolute path on our computer.

A separator character is used to separate directories and files in the path. On a Windows computer, the separator character is a backslash (\). On a UNIX system, it’s a forward slash (/). Java processes both characters identically in a path name. For example, if we were to use the path

```
c:\Program Files\Java\jdk1.6.0_11\demo\jfc
```

which employs each separator character, Java would still process the path properly. When building Strings that represent path information, use File.separator to obtain the local computer’s proper separator character rather than explicitly using / or \. This constant returns a String consisting of one character—the proper separator for the system.

## Common Programming Error 17.1

Using \ as a directory separator rather than \\ in a string literal is a logic error. A single \ indicates that the \ followed by the next character represents an escape sequence. Use \\ to insert a \ in a string literal.

## 17.4 Sequential-Access Text Files

Next, we create and manipulate sequential-access files in which records are stored in order by the record-key field. We begin with text files, enabling the reader to quickly create and edit human-readable files. We discuss creating, writing data to, reading data from and updating sequential-access text files. We also include a credit-inquiry program that retrieves specific data from a file.

### 17.4.1 Creating a Sequential-Access Text File

Java imposes no structure on a file—notions such as records do not exist as part of the Java language. Therefore, you must structure files to meet the requirements of your applications. In the following example, we see how to impose a keyed record structure on a file.

The program in Figs. 17.4, 17.5 and 17.8 creates a simple sequential-access file that might be used in an accounts receivable system to keep track of the amounts owed to a company by its credit clients. For each client, the program obtains from the user an account number and the client’s name and balance (i.e., the amount the client owes the company for goods and services received). Each client’s data constitutes a “record” for that client. This application uses the account number as the record key—the file will be created and maintained in account-number order. The program assumes that the user enters the records in account-number order. In a comprehensive accounts receivable system (based on sequential-access files), a sorting capability would be provided so that the user could enter the records in any order. The records would then be sorted and written to the file.

### Class AccountRecord

Class AccountRecord (Fig. 17.4) encapsulates the client record information used by the examples in this chapter. AccountRecord is declared in package com.deitel.ch17 (line 3), so that it can be imported into several of this chapter’s examples for reuse. (Section 8.14 provides information on compiling and using your own packages.) Class AccountRecord contains private instance variables account, firstName, lastName and balance (lines 7–10) and set and get methods for accessing these fields. Though the set methods do not validate the data in this example, they should do so in an “industrial-strength” system.

// Fig. 17.4: AccountRecord.java
// AccountRecord class maintains information for one account.
package com.deitel.ch17; // packaged for reuse

public class AccountRecord
{
    private int account;
    private String firstName;
    private String lastName;
    private double balance;

    // no-argument constructor calls other constructor with default values
    public AccountRecord()
    {
        this( 0, "", "", 0.0 ); // call four-argument constructor
    } // end no-argument AccountRecord constructor

    // initialize a record
    public AccountRecord( int acct, String first, String last, double bal )
    {
        setAccount( acct );
        setFirstName( first );
        setLastName( last );
        setBalance( bal );
    } // end four-argument AccountRecord constructor

    // set account number
    public void setAccount( int acct )
    {
        account = acct;
    } // end method setAccount

    // get account number
    public int getAccount()
    {
        return account;
    } // end method getAccount

    // set first name
    public void setFirstName( String first )
    {
        firstName = first;
    } // end method setFirstName

    // get first name
    public String getFirstName()
    {
        return firstName;
    } // end method getFirstName
