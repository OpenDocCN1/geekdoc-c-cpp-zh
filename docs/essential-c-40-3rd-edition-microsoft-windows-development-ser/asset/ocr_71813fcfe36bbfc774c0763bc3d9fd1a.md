# TABLE 3.1: Control Flow Statements (Continued)

| Statement | General Syntax Structure | Example |
| :--- | :--- | :--- |
| do while statement | do embedded-statement while(boolean-expression); | do { System.Console.WriteLine( "Enter name :"); input = System.Console.ReadLine(); } while(input != "exit"); |
| for statement | for(for-initializer; boolean-expression; for-iterator embedded-statement | for (int count = 1; count <= 10; count++) { System.Console.WriteLine( "count = {0}", count); } |
| Foreach statement | foreach(type identifier in expression) embedded-statement | foreach (char letter in email) { if(!insideDomain) { if (letter == '@') { insideDomain = true; continue; } System.Console.Write( letter); } } |
| continue statement | continue; | |