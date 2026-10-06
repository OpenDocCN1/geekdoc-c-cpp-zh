let unsignednativeint = 76sun
let long = 12345678912345789L
let unsignedlong = 12345678912345789UL
let float32 = 42.8F
let float = 42.8

printf "int" = %d or "%A" int
printf "string" = %s or "%A" string string
printf "char" = %c or "%A" char char
printf "bool" = %b or "%A" bool bool
printf "bytearray" = "%A" bytearray

printf "hex int" = %x or "%A" hexint
printf "HEX INT" = %x or "%A" hex bigint
printf "oct int" = %o or "%A" octal octint
printf "bin int" = %b or "%A" binaryinteger binaryinteger
printf "signed byte" = "%A" signedbyte
printf "unsigned byte" = "%A" unsignedbyte

printf "small" = %s smallint
printf "small int" = %A" smallint
printf "int" = %i or "%A" integer integer
printf "uint" = %u or "%A" usignedint usignedint
printf "native int" = "%A" native int

printf "unsigned native int" = "%A" unsignednative
printf "long" = %ld or "%A" long long
printf "unsigned long" = "%A" unsignedlong
printf "float" = %f or "%A" float32 float32
printf "double" = %f or "%A" float float

# Execution result

```
int = 42
string = This is a string or "This is a string"
char = c or 'c'
bool = true or false
bytearray = [84uy; 104uy; 105uy; 115uy; 32uy; 105uy; 115uy; 107uy; 92uy; 92uy 111uy; 116uy; 112uy; 115uy; 116uy; 114uy; 105uy; 107uy; 103uy]
hex int = 34 or 52
HEX INT = 34 or 52
oct int = 42 or 34
bint int = 42 or 42
signed byte = 68uy
unsigned byte = 102uy
small int = 16s
small uint = 16us
int = 345 or 345
uint = 345 or 345u
native int = 765n
unsigned native int = 765sun
long = 123456789123456789L
unsigned long = 123456789123456789UL
float = 42.800000 or 42.7999992f
double = 42.800000 or 42.8
```

CHAPTER 1 C# and F Data Structures 13