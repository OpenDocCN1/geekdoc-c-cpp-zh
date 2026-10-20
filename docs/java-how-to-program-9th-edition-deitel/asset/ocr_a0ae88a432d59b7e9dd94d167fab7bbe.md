```
23 buffer.insert( 0, " " );
24 buffer.insert( 0, charArray );
25 buffer.insert( 0, " " );
26 buffer.insert( 0, charArray, 3, 3 );
27 buffer.insert( 0, " " );
28 buffer.insert( 0, booleanValue );
29 buffer.insert( 0, " " );
30 buffer.insert( 0, characterValue );
31 buffer.insert( 0, " " );
32 buffer.insert( 0, integerValue );
33 buffer.insert( 0, " " );
34 buffer.insert( 0, longValue );
35 buffer.insert( 0, " " );
36 buffer.insert( 0, floatValue );
37 buffer.insert( 0, " " );
38 buffer.insert( 0, doubleValue );
39
40 System.out.printf(
41 "buffer after inserts:\n%s\n\n", buffer.toString() );
42
43 buffer.deleteCharAt( 10 ); // delete 5 in 2.5
44 buffer.delete( 2, 6 ); // delete .333 in 33.333
45
46 System.out.printf(
47 "buffer after deletes:\n%s\n", buffer.toString() );
48 } // end main
49 } // end class StringBuilderInsertDelete
```

buffer after inserts:
33.333 2.5 10000000 7 K true def abcdef goodbye hello

buffer after deletes:
33 2. 10000000 7 K true def abcdef goodbye hello

Fig. 16.14 | StringBuilder methods insert, delete and deleteCharAt. (Part 2 of 2.)

# 16.5 Class Character

Java provides eight type-wrapper classes—Boolean, Character, Double, Float, Byte, Short, Integer and Long—that enable primitive-type values to be treated as objects. In this section, we present class Character—the type-wrapper class for primitive type char.

Most Character methods are static methods designed for convenience in processing individual char values. These methods take at least a character argument and perform either a test or a manipulation of the character. Class Character also contains a constructor that receives a char argument to initialize a Character object. Most of the methods of class Character are presented in the next three examples. For more information on class Character (and all the type-wrapper classes), see the java.lang package in the Java API documentation.

Figure 16.15 demonstrates static methods that test characters to determine whether they’re a specific character type and the static methods that perform case conversions on characters. You can enter any character and apply the methods to the character.