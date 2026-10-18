# Input and Output Member Functions (continued)

| Form of a Function Call | Description | Header File |
|---|---|---|
| Stream_Var.put (Char_Exp); | Writes the value of the Char_Exp to the output stream Stream_Var. | fstream or iostream |
| Stream_Var.putback (Char_Exp); | Places the value of Char_Exp in the input stream Stream_Var so that that value is the next input value read from the stream. The file connected to the stream is not changed. | fstream or iostream |
| Stream_Var.precision (Int_Exp); | Specifies the number of digits output after the decimal point for floating-point values sent to the output stream Stream_Var. | fstream or iostream |
| Stream_Var.width (Int_Exp); | Sets the field width for the next value output to the stream Stream_Var. | fstream or iostream |
| Stream_Var.setf(Flag); | Sets flags for formatting output to the stream Stream_Var. See Display 6.5 for the list of possible flags. | fstream or iostream |
| Stream_Var.unsetf(Flag); | Unsets flags for formatting output to the stream Stream_Var. See Display 6.5 for the list of possible flags. | fstream or iostream |