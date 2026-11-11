+   1. while(true) //use break to exit loop;
+   2. {
+   3. cin>>i/or getline(ifstream, string);
+   4. If(cin.eof()){  //If it’s EOF
+   5. cout<<"EOF _ encountered"<<endl
+   6. //break;
+   7. }
+   8. If(cin.fail()) //deal with Invalide input
+   9. {
+   10. cin.clear(); //Important. clear state and buffer
+   11. while(cin.get()!='\n') //get rid rest of line,
+   12. continue ;
+   13. cout<<"please _ input _ a _ number"<<endl;
+   14. continue;
+   15. }
+   16. ... // input is right.do some useful things.
+   17. }

+   - In the previous example, why do we need to distinguish eof and fail? When fail happen, maybe there are invalid character in buffer. After clean the buffer, I can continue to read input from input buffer. Three methods to clean invalid character in the buffer.

```
```
cin.clear();   //Important. clear state and buffer
while(cin.get()!='\n')
continue ;    // method 1
while(!issapce(cin.get()))
continue; //method 2
basic_istream& ignore(streamsize _Count = 1, \
int_type _Delim = traits_type::eof()); //method 3
cin.ignore(5, 'a');
```
```