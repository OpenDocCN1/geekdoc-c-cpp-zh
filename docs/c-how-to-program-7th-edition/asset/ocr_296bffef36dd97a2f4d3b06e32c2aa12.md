again or the program terminates. p) False. Memory addresses are displayed in hexadecimal format by default. To display addresses as long integers, the address must be cast to a long value.

+   15.3
+   
+   a) `cout << "Enter your name: ";`
+   b) `cout << uppercase;`
+   c) `cout << static_cast< void * >( myString );`
+   d) `cout << scientific;`
+   e) `cout << integerPtr;`
+   f) `cout << showbase;`
+   g) `cout << *floatPtr;`
+   h) `cout.fill( ' ' );`
+      `cout << setfill( '*' ) << setw( 10 ) << 123 << endl;`
+   i) `cout.put( 'O' ).put( 'K' );`
+   j) `cin.peek();`
+   k) `charValue = cin.get();`
+      `cin.get( charValue );`
+   l) `cin.ignore( 6 );`
+   m) `cin.read( line, 50 );`
+   n) `cin.get( name, 10, '.' );`
+      `cin.getline( name, 10, '.' );`
+   o) `cout.write( line, cin.gcount() );`
+   p) `cout << 124 << ' ' << 18.376 << ' ' << "Z" << 1000000 << " String";`
+   q) `cout << cout.precision();`
+   r) `cin >> months >> percentageRate;`
+   s) `cout << setprecision( 2 ) << 1.92 << '\t' << 1.925 << '\t' << 1.9258;`
+   t) `cout << oct << 100 << '\t' << hex << 100 << '\t' << dec << 100;`
+   u) `cout << 100 << '\t' << setbase( 8 ) << 100 << '\t' << setbase( 16 ) << 100;`
+   v) `cout << setw( 10 ) << 1234;`
+   w) `cin.get( line, 20, 'z' );`
+   x) `cout << setw( x ) << setprecision( y ) << 87.4573;`

+   15.4
+   
+   a) Error: The precedence of the << operator is higher than that of ==, which causes the statement to be evaluated improperly and also causes a compiler error.
+      Correction: Place parentheses around the expression x == y.
+   b) Error: In C++, characters are not treated as small integers, as they are in C.
+      Correction: To print the numerical value for a character in the computer's character set, the character must be cast to an integer value, as in the following:
+          `cout << static_cast< int >( 'c' );`
+   c) Error: Quote characters cannot be printed in a string unless an escape sequence is used.
+      Correction: Print the string in one of the following ways:
+          `cout << "\"A string in quotes\"";`

+   15.5
+   
+   a) 12345
+      **123
+      123
+   b) $$$$$10000
+   c) 1024.988
+   d) 0143
+      0x63
+   e) 100000
+      +100000
+   f) 4.45e-002