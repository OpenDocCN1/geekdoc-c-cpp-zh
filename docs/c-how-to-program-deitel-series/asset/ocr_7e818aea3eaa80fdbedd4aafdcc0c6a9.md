```
using namespace std;

int main()
{
   string string1( "noon is 12 pm; midnight is not." );
   int location;

   // find "is" at location 5 and 24
   cout << "\nOriginal string:\n" << string1
      << "\n\n(find) \"is\" was found at: " << string1.find( "is" )
      << "\n(rfind) \"is\" was found at: " << string1.rfind( "is" );

   // find 'o' at location 1
   location = string1.find_first_of( "isop" );
   cout << "\n\n(find_first_of) found 'o' from the group \"isop\" at: " << location;

   // find 'o' at location 28
   location = string1.find_last_of( "isop" );
   cout << "\n\n(find_last_of) found 'o' from the group \"isop\" at: " << location;

   // find '1' at location 8
   location = string1.find_first_not_of( "noi spm" );
   cout << "\n\n(find_first_not_of) '" << string1[ location ]
      << "' is not contained in \"noi spm\" and was found at: "
      << location;

   // find ';' at location 13
   location = string1.find_first_not_of( "12noi spm" );
   cout << "\n\n(find_first_not_of) '" << string1[ location ]
      << "' is not contained in \"12noi spm\" and was found at: "
      << location;

   // search for characters not in string1
   location = string1.find_first_not_of(
      "noon is 12 pm; midnight is not." );
   cout << "\n\n(find_first_not_of(\"noon is 12 pm; midnight is not.\")"
      << " returned: " << location << endl;
} // end main
```

```
Original string:
noon is 12 pm; midnight is not.

(find) "is" was found at: 5
(rfind) "is" was found at: 24

(find_first_of) found 'o' from the group "isop" at: 1

(find_last_of) found 'o' from the group "isop" at: 28

(find_first_not_of) '1' is not contained in "noi spm" and was found at: 8

(find_first_not_of) ';' is not contained in "12noi spm" and was found at: 13

(find_first_not_of("noon is 12 pm; midnight is not.") returned: -1
```

Fig. 21.6  |  Demonstrating the string find member functions. (Part 2 of 2.)