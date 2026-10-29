| FORM OF A FUNCTION CALL | DESCRIPTION | HEADER FILE |
|---|---|---|
| Stream_Var.close( ); | Disconnects the stream Stream_Var from the file it is connected to. | fstream |
| Stream_Var.bad( ); | Returns true if the stream Stream_Var is corrupted. | fstream or iostream |
| Stream_Var.eof( ); | Returns true if the program has attempted to read beyond the last character in the file connected to the input stream Stream_Var. Otherwise, it returns false. | fstream or iostream |
| Stream_Var.get( Char_Variable ); | Reads one character from the input stream Stream_Var and sets the Char_Variable equal to this character. Does not skip over whitespace. | fstream or iostream |
| Stream_Var.getline( String_Var, Max_Characters +1 ); | One line of input from the stream Stream_Var is read and the resulting string is placed in String_Var. If the line is more than Max_Characters long, only the first Max_Characters are read. The declared size of the String_Var should be Max_Characters +1 or larger. | fstream or iostream |
| Stream_Var.peek( ); | Reads one character from the input stream Stream_Var and returns that character. The character read is not removed from the input stream; the next read will read the same character. | fstream or iostream |
| Stream_Var.put( Char_Exp ); | Writes the value of the Char_Exp to the output stream Stream_Var. | fstream or iostream |
| Stream_Var.putback( Char_Exp ); | Places the value of Char_Exp in the input stream Stream_Var so that that value is the next input value read from the stream. The file connected to the stream is not changed. | fstream or iostream |
| Stream_Var.precision( Int_Exp ); | Specifies the number of digits output after the decimal point for floating-point values sent to the output stream Stream_Var. | fstream or iostream |
| Stream_Var.width( Int_Exp ); | Sets the field width for the next value output to the stream Stream_Var. | fstream or iostream |