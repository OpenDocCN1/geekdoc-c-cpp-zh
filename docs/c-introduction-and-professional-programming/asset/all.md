![](Images/cover01225.jpeg)

#                   C++: Introduction and Professional Programming

FRED RAY

# Table of Contents

1 The first program1

1.1 [What is a program ??](#part0002.xhtml__TOC_250072) [             1](#part0002.xhtml__TOC_250072)

1.2 [The “Hello World” program in C3](#part0004.xhtml__TOC_250071)             

1.3 [The “Hello World” program in C++4](#part0005.xhtml__TOC_250070)             

1.4 [Internal details when programming](#part0006.xhtml__TOC_250069)[             5](#part0006.xhtml__TOC_250069)

1.5 [designations in the lecture](#part0006.xhtml__TOC_250068)[             5](#part0006.xhtml__TOC_250068)

1.6 [Newer C++ compilers](#part0007.xhtml__TOC_250067)[             6](#part0007.xhtml__TOC_250067)

2 Simple data types7

2.1 [variable](#part0008.xhtml__TOC_250066)[             7](#part0008.xhtml__TOC_250066)

2.1.1 [inflation](#part0008.xhtml__TOC_250065) [             variables7](#part0008.xhtml__TOC_250065)[](#part0008.xhtml__TOC_250065)

2.1.2 [Designation of variables](#part0009.xhtml__TOC_250064)[             8th](#part0009.xhtml__TOC_250064)

2.2 [constants](#part0010.xhtml__TOC_250063)[             9](#part0010.xhtml__TOC_250063)

2.2.1 [integer constants](#part0010.xhtml__TOC_250062)[             9](#part0010.xhtml__TOC_250062)

2.2.2 [floating point constants](#part0010.xhtml__TOC_250061)[             9](#part0010.xhtml__TOC_250061)

2.2.3 [Character constants (character constants)](#part0010.xhtml__TOC_250060)[             9](#part0010.xhtml__TOC_250060)

2.2.4 [Character string constants (string constants)9](#part0010.xhtml__TOC_250059)             

2.2.5 [Symbolic Constants (Macros)](#part0011.xhtml__TOC_250058)[             10](#part0011.xhtml__TOC_250058)

2.2.6 [Constant with variable names](#part0012.xhtml__TOC_250057)[             11](#part0012.xhtml__TOC_250057)

3 operators13

3.1 [assignment operator](#part0013.xhtml__TOC_250056)[             13](#part0013.xhtml__TOC_250056)

3.2 [Arithmetic Operators](#part0014.xhtml__TOC_250055)[             14](#part0014.xhtml__TOC_250055)

3.2.1 [un](#part0014.xhtml__TOC_250054)[             ](#part0014.xhtml__TOC_250054) [̈are](#part0014.xhtml__TOC_250054)[](#part0014.xhtml__TOC_250054)[](#part0014.xhtml__TOC_250054) [operators14             ](#part0014.xhtml__TOC_250054)

3.2.2 [I](#part0014.xhtml__TOC_250053) [̈are](#part0014.xhtml__TOC_250053)[             ](#part0014.xhtml__TOC_250053) [](#part0014.xhtml__TOC_250053) [operators14             ](#part0014.xhtml__TOC_250053)

i

iiTABLE OF CONTENTS

3.3 [comparison operators             ](#part0015.xhtml__TOC_250052)[15](#part0015.xhtml__TOC_250052)

3.4 [Logical Operators             ](#part0017.xhtml__TOC_250051)[17](#part0017.xhtml__TOC_250051)

3.5 [Bit-Oriented Operators             ](#part0017.xhtml__TOC_250050)[17](#part0017.xhtml__TOC_250050)

3.5.1 [u](#part0017.xhtml__TOC_250049)[n             ](#part0017.xhtml__TOC_250049)[¨ar](#part0017.xhtml__TOC_250049)[e](#part0017.xhtml__TOC_250049) [bit-oriented](#part0017.xhtml__TOC_250049) [e](#part0017.xhtml__TOC_250049) [operators](#part0017.xhtml__TOC_250049) [17             ](#part0017.xhtml__TOC_250049)

3.5.2 [Am             ](#part0018.xhtml__TOC_250048)[¨ar](#part0018.xhtml__TOC_250048)[e](#part0018.xhtml__TOC_250048) [bit-oriented](#part0018.xhtml__TOC_250048) [e](#part0018.xhtml__TOC_250048) [operators](#part0018.xhtml__TOC_250048) [18             ](#part0018.xhtml__TOC_250048)

3.6 [Operations with predefined functions             ](#part0019.xhtml__TOC_250047)[19](#part0019.xhtml__TOC_250047)

3.6.1 [Mathematical Functions             ](#part0019.xhtml__TOC_250046)[19](#part0019.xhtml__TOC_250046)

3.6.2 [functions             ](#part0021.xhtml__TOC_250045)[n](#part0021.xhtml__TOC_250045)[fu](#part0021.xhtml__TOC_250045)[¨](#part0021.xhtml__TOC_250045) [right](#part0021.xhtml__TOC_250045) [character strings](#part0021.xhtml__TOC_250045) [21             ](#part0021.xhtml__TOC_250045)

3.7 [Increment and decrement operators             ](#part0022.xhtml__TOC_250044)[22](#part0022.xhtml__TOC_250044)

3.7.1 [Pr             ](#part0022.xhtml__TOC_250043)[¨a](#part0022.xhtml__TOC_250043)[fixed notation](#part0022.xhtml__TOC_250043) [22             ](#part0022.xhtml__TOC_250043)

3.7.2 [postfix notation             ](#part0022.xhtml__TOC_250042)[22](#part0022.xhtml__TOC_250042)

3.8 [Compound assignments             ](#part0022.xhtml__TOC_250041)[22](#part0022.xhtml__TOC_250041)

3.9 [W             ](#part0023.xhtml__TOC_250040)[more](#part0023.xhtml__TOC_250040)[now](#part0023.xhtml__TOC_250040) [addition](#part0023.xhtml__TOC_250040) [e](#part0023.xhtml__TOC_250040) [constants](#part0023.xhtml__TOC_250040) [23             ](#part0023.xhtml__TOC_250040)

4 control structures25

4.1 [Simple instruction             ](#part0024.xhtml__TOC_250039)[25](#part0024.xhtml__TOC_250039)

4.2 [block             ](#part0024.xhtml__TOC_250038)[25](#part0024.xhtml__TOC_250038)

4.3 [branches             ](#part0026.xhtml__TOC_250037)[27](#part0026.xhtml__TOC_250037)

4.4 derightZdialing cycle              33

4.5 repellent cycle             38

4.6 Non-shedding cycle             38

4.7 [Multiway selection (switch statement)             ](#part0041.xhtml__TOC_250036)[42](#part0041.xhtml__TOC_250036)

4.8 Incededcontrolbresult             43

5 Structured data types45

5.1 fields             45

5.1.1 [One-dimensional fields             ](#part0043.xhtml__TOC_250035)[45](#part0043.xhtml__TOC_250035)

5.1.2 [Multidimensional Fields             ](#part0049.xhtml__TOC_250034)[51](#part0049.xhtml__TOC_250034)

5.2 [structures             ](#part0050.xhtml__TOC_250033)[52](#part0050.xhtml__TOC_250033)

5.3 [union             ](#part0054.xhtml__TOC_250032)[56](#part0054.xhtml__TOC_250032)

5.4 [record             ](#part0055.xhtml__TOC_250031)[choice](#part0055.xhtml__TOC_250031)[yp](#part0055.xhtml__TOC_250031) [57             ](#part0055.xhtml__TOC_250031)

5.5 [General type definitions             ](#part0056.xhtml__TOC_250030)[58](#part0056.xhtml__TOC_250030)

6 pointer59

TABLE OF CONTENTSiii

6.1 [agreement of pointers](#part0057.xhtml__TOC_250029)[             59](#part0057.xhtml__TOC_250029)

6.2 [pointer operators](#part0058.xhtml__TOC_250028)[             60](#part0058.xhtml__TOC_250028)

6.3 [Pointers and Arrays - Pointer Arithmetic61](#part0059.xhtml__TOC_250027)             

6.4 [Dynamic arrays using pointer variables62](#part0060.xhtml__TOC_250026)             

6.5 [pointers to structures](#part0065.xhtml__TOC_250025)[             67](#part0065.xhtml__TOC_250025)

6.6 [reference](#part0066.xhtml__TOC_250024)[             68](#part0066.xhtml__TOC_250024)

7 functions71

7.1 [definition and declaration](#part0068.xhtml__TOC_250023)[             71](#part0068.xhtml__TOC_250023)

7.2 [parameters](#part0070.xhtml__TOC_250022)[             b](#part0070.xhtml__TOC_250022)[result](#part0070.xhtml__TOC_250022)[73](#part0070.xhtml__TOC_250022)

7.3 [Ru](#part0071.xhtml__TOC_250021)[             ¨c](#part0071.xhtml__TOC_250021)[kg values](#part0071.xhtml__TOC_250021)[before](#part0071.xhtml__TOC_250021) [n](#part0071.xhtml__TOC_250021) [functions](#part0071.xhtml__TOC_250021) [74             ](#part0071.xhtml__TOC_250021)

7.4 [fields as parameters](#part0073.xhtml__TOC_250020)[             76](#part0073.xhtml__TOC_250020)

7.5 [Declarations and header files, libraries79](#part0076.xhtml__TOC_250019)             

7.5.1 [Example: printvec](#part0077.xhtml__TOC_250018)[             80](#part0077.xhtml__TOC_250018)

7.5.2 [Example: students](#part0079.xhtml__TOC_250017)[             82](#part0079.xhtml__TOC_250017)

7.5.3 [A simple library using student as an example83](#part0080.xhtml__TOC_250016)             

7.6 [The main program](#part0081.xhtml__TOC_250015)[             84](#part0081.xhtml__TOC_250015)

7.7 [Recursive Functions](#part0083.xhtml__TOC_250014)[             86](#part0083.xhtml__TOC_250014)

7.8 [egg](#part0083.xhtml__TOC_250013)[             n](#part0083.xhtml__TOC_250013)[big](#part0083.xhtml__TOC_250013)[bigger](#part0083.xhtml__TOC_250013)[s](#part0083.xhtml__TOC_250013) [Example:](#part0083.xhtml__TOC_250013) [bisection](#part0083.xhtml__TOC_250013) [86             ](#part0083.xhtml__TOC_250013)

8 The data type class93

8.1 [Class declaration data and methods94](#part0090.xhtml__TOC_250012)             

8.2 [The constructors](#part0090.xhtml__TOC_250011)[             94](#part0090.xhtml__TOC_250011)

8.3 [The Destroyer](#part0092.xhtml__TOC_250010)[             96](#part0092.xhtml__TOC_250010)

8.4 [The assignment operator](#part0092.xhtml__TOC_250009)[             96](#part0092.xhtml__TOC_250009)

8.5 [The print operator](#part0093.xhtml__TOC_250008)[             97](#part0093.xhtml__TOC_250008)

8.6 [data encapsulation](#part0095.xhtml__TOC_250007)[             99](#part0095.xhtml__TOC_250007)

9 File input and output103

9.1 [Copy files](#part0099.xhtml__TOC_250006)[             104](#part0099.xhtml__TOC_250006)

9.2 [Data input and output via file105](#part0100.xhtml__TOC_250005)             

9.3 [Switching input/output](#part0100.xhtml__TOC_250004)[             105](#part0100.xhtml__TOC_250004)

10 output formatting107

IVTABLE OF CONTENTS

11  tips and tricks109

11.1  [Pr             ](#part0104.xhtml__TOC_250003)[aprocessor](#part0104.xhtml__TOC_250003) [command](#part0104.xhtml__TOC_250003) [109             ](#part0104.xhtml__TOC_250003)

11.2  [timing in the program             ](#part0105.xhtml__TOC_250002)[110](#part0105.xhtml__TOC_250002)

11.3  [profiling             ](#part0106.xhtml__TOC_250001)[111](#part0106.xhtml__TOC_250001)

11.4  [debugging             ](#part0106.xhtml__TOC_250000)[111](#part0106.xhtml__TOC_250000)

Chapter 1

# The first program

## 1.1 What is a program ??

Actually, everyone already knows programs, but one often understands different contents by them.

• party manifesto↔︎ideas

• theater program↔︎scheduling

• music score↔︎strict sequence of instructions

• Windows program↔︎interactive action with the computer

programnisttheresLo¨senbeforenGave upinouchfenm computermediums ownSoftware and includes all four aspects in the above list.

Aettypicalu¨ exerciseebcomplythe followingnSentence:

![](Images/image00824.jpeg)

1

2CHAPTER 1\. THE FIRST PROGRAM

## What should I do ??

ideaim head or on paper. (What should the computer do?)

program idea

ideafu¨↓rightcomputer

processing

Formulate idea in↓ a programming language.

source filefu¨rightthe

computerandtranslation Zen

Draft. (How can the computer realize the idea?)

Edit source text/source file. (What expressions may I use?)

Compile [and link] file. (translation into processor language)

Structogram

program code

exportaudibleprogram

program↓ mcode

exportearRemarks:

Test program with different data sets

program test

1. The learning process in programming typically proceeds from the bottom up in the previous overview.

2. softwaree =exportaudiblesProgram + program code + ideas

![](Images/image00825.jpeg)

Tmore typicalOnfcomment:aberightI meant that completely differently.

![](Images/image00826.jpeg)

1.2\. THE “HELLO WORLD” PROGRAM IN C3

## 1.2 The “Hello World” program in C

idea: The simplest program that only writes a message on the screen.

![](Images/image00827.jpeg)source code  (HelloWorld.c):

• ![](Images/image00828.jpeg)Start, end of comment

![](Images/image00829.jpeg)predefined functions/Variables/ constants

• Beginning of the main program

• simple instruction

• block statementsource code inputand compile, execute programear:

0. Turn on computer, log in

Log in:

passwd:

1. Tterminalor file managerOopenand change to the working directorysel.

LINUX> cd progs

2. Enter source text in the source file, editor of your own choice.

LINUX> editHelloWorld.cor

LINUX> xemacs HelloWorld.c.

3. Compile source file. LINUX> gcc HelloWorld.c

4. programmexportear.

LINUX>a.outor LINUX>./a.outor WIN98> ./a.exe

Remarks:

![](Images/image00830.jpeg)LINUX> gcc HelloWorld.c

generated oneexportaudiblesProgram with the default name a.out .

![](Images/image00831.jpeg)casestheresexportaudibleeProgram, e.g. myprog should be called:

LINUX> gcc -o myprog HelloWorld.c LINUX> myprog

![](Images/image00832.jpeg)Tueeconcretee  command line  to the  compileistuh¨ngiGbeforemvconsiderdeten compiler.

4CHAPTER 1\. THE FIRST PROGRAM

## 1.3 The “Hello World” program in C++

![](Images/image00833.jpeg)![](Images/image00834.jpeg)Idea and structogram as in section 1.2 source code (HelloWorld.cc):

![](Images/image00835.jpeg)comment to line-

in

![](Images/image00836.jpeg)predefined classes and methods

• Beginning of the main program

• simple instruction

• block statementsource code inputU.Ni.ecompile, execute programear:

0./1\. as in § 1.2.

2. Edit source file.

LINUX> edit HelloWorld.cc

3. Compile source file.

LINUX> g++ HelloWorld.cc

4. programmexportear.  LINUX>a.outor LINUX>./a.outorWIN98> ./a.exe

Remarks:

![](Images/image00837.jpeg)ofrightC source code of HelloWorld.c can also be written in C++ andbreplacedwill:

LINUX> g++ HelloWorld.c

However, the source text line #include <stdio.h> is then absolutely necessary.

• C instructionsare a subset of the C++ instructions.

• The C comment/**/ can also be used in C++.

![](Images/image00838.jpeg)ofrightc++ how //goortnot to the syntax of C andshould therefore not be used in C programs. Otherwise there is a portability problem, ie not every C compiler can compile the source code.

Programming tip:

Esgivet(nearly)alwaysrightmehrightals oneMonequalsince one ideaim computer programto realize.

=⇒ Find your own programming style (and improve it).

1.4\. INTERNAL DETAILS WHEN PROGRAMMING5

## 1.4 Internal details when programming

derighteasy geachangesecallfto compile

LINUX> g++ -v HelloWorld.cc

generateda layoungereScreen output showing several stages of compilingrens indicates. Here are some tips on how to look at each phase to better understand the process:

a) Preprocessing:

header files(*.hh and *.h) are added to the source fileGt(+ macrodefinitions, conditional compilation)

LINUX> g++ -E HelloWorld.cc > HelloWorld.ii

The addition > HelloWorld.ii directs the screen output to the HelloWorld.ii file. This HelloWorld.ii file can be viewed with an editor and is a long C++ source code file.

b) u¨ bsubstitutein assembly code:

Here a source text file in the (processor-specific) programminglanguage assembler generated.

LINUX> g++ -S HelloWorld.cc

The resulting HelloWorld.s file can be viewed with the editor.

c) Generate object code:

Now a file is created which contains the direct control commands, ie numbers, for the processor.

LINUX> g++ -c HelloWorld.cc

The file HelloWorld.o can no longer be viewed in the normal text editor, but with

LINUX> hex HelloWorld.o

d) links:

Vbindall object files and necessary libraries for executionMr-ble program a.out .

LINUX> g++ HelloWorld.o

## 1.5 designations in the lecture

![](Images/image00839.jpeg)Commands in a command line under LINUX:

![](Images/image00840.jpeg)LINUX> g++ [-o myprog] file name.cc

![](Images/image00841.jpeg)The square brackets [ ] mark optional parts in commands, commandsor definitions. Each file name consists of the free waavailableBase name (file name) and the suffix (.cc) which identifies the file type.

6CHAPTER 1\. THE FIRST PROGRAM

• Some file types after the suffix:SuffixFileType

![](Images/image00842.jpeg)

cC source file

. HC header file (also C++), source file with predefined program modules

.cc[.cpp]C++ source code file

.hh[.hpp]C++ -Header file

. Oobject file

.aLibrary file (Library)

![](Images/image00843.jpeg)A statementhow< type>means that this placeholder must be replaced by an expression of the appropriate type.

## 1.6 Newer C++ compilers

Since the first version of this script, newer versions of the header files are available alongside the old header files, such as iostream instead of iostream.h. In some cases compilers like g++ then deliver annoying, multi-line warnings when compiling the source text on page 4\. This error message can be removed using LINUX> g++ -Wno-deprecated HelloWorld.cc

oppress¨cctwearth.

![](Images/image00844.jpeg)![](Images/image00845.jpeg)atinright(recommended) use of the new header files achanget  himselfourright  smallprogram in :

![](Images/image00846.jpeg)

![](Images/image00847.jpeg)I  wantinnscopee operator,  please refer8 do not have to write down every timeeat,henceI prefer the variant:

![](Images/image00848.jpeg)

Chapter 2

# Simple data types

## 2.1 variable

### 2.1.1 variable definition

Every meaningful program processes data in some form. This data is saved in variables.

Tueevariablei)is a symbolic representationsentation(identifier/name) fu¨rightennstorage space of data.

ii) is described by type and storage class.

iii) The contents of the variables, ie the data in the memory space, change during program execution.

General form of variable declaration:

[< storage class >] <type> <identifier1> [, identifier2] ;

TypeMemory Contentvaluesto bytes (g++)

![](Images/image00849.jpeg)

![](Images/image00850.jpeg)char1Character sign'H', 'e', 'n'

![](Images/image00851.jpeg)boolean1boolean variablefalse, true [C++ only]

![](Images/image00851.jpeg)![](Images/image00852.jpeg)internal4-32767.231

short [int]2whole Numbers-32767

![](Images/image00853.jpeg)long [int]4-32767.231

![](Images/image00851.jpeg)float4Floating point numbers 1.1, -1.56e-32

double81.1, -1.56e-32, 5.68e+287

![](Images/image00851.jpeg)![](Images/image00854.jpeg)unsigned[int]4of coursecommone  numbers32767,32769,2311

![](Images/image00855.jpeg)long long [int]8whole  Numbers231, 2631

longdouble12Floating point numbers 5.68e+287, 5.68e+420

7

Remarks:

• Character data stores exactly one ASCII or special character.

![](Images/image00856.jpeg)![](Images/image00857.jpeg)The memory requirement of types of the integer group (int) can depend on the compiler and the operating system (16/32 bit). It is therefore advisable to read the relevant compiler instructions or to determine the actual number of bytes required with the sizeof operator using sizeof( <type> ) or sizeof( <variable> ). See also the following example:

![](Images/image00858.jpeg)

![](Images/image00859.jpeg)Wirightare usually the base type int fu¨rightthe appropriate subrange of integers and unsigned int fu¨rightn / Aof thecommone  numbersvuse.theMarking unsigned can also be linkedcan be used with other integer types.

### 2.1.2 Designation of variables

![](Images/image00860.jpeg)![](Images/image00861.jpeg)![](Images/image00862.jpeg)Variable names start with letters or underscores, the following characters can also be numbers. The use of spaces and operator characters ( 3) in names is not permitted, nor are variable names allowed to be keywords of the C++ syntax (see Ref.).

![](Images/image00840.jpeg)![](Images/image00863.jpeg)![](Images/image00840.jpeg)![](Images/image00864.jpeg)C/C++ is case sensitive, ie,

ToteHosen and toteHosen are different identifiers!

![](Images/image00865.jpeg)According to the original C standard, the first 8 characters of a variable identifier are significant, ie a2345678A and a2345678B would no longer be perceived as different identifiers. Compilers now see more characters as significant (C9X standard: 63 characters).

## 2.2 constants

Most programs, including HelloWorld.cc, use unchangeable values, so-called constants, during the course of the program.

### 2.2.1 integer constants

Decimal constants (base10):100// int; 100

512L// long; 512

128053// long; 128053

octal constants(Base 8):020// int; 16

01000L// long; 512

0177// int; 127

Hexadecimal constants (base16):0x15// int; 21

0x200// int; 512

0x1ffffl// long; 131071

### 2.2.2 floating point constants

Floating point constants are always interpreted as double. Some examples infollowing:              17631.0e-78

| 1E+10 | // | 10000000000 |
| 1. | // | 1 |
| .78 | // | 0.78 |
| 0.78 |  |  |
| -.2e-3 | // | -0.0002 |
| -3.25 |  |  |

### 2.2.3 character constants(character constants)

The character constant contains the character between the two ' :

'a', 'A', '@', '1'//ASCII character ''//spaces

'_'//underline/underscore

'\''//prime sign '

'\\'//backslash character \

'\n'//new line

'\0'//Null character NUL

### 2.2.4 string constants(string constants)

Thestringincludesthecharactersbetweenthetwo              "              :

"Hello World\n"

""//empty string

"A"//String "A"

![](Images/image00866.jpeg)![](Images/image00867.jpeg)Each character string is automatically terminated with the (character) character '\0'("Hey,hererightHortinright  thongouchf!”).thererightist  'A'unequalH  "A",wmooseconsists of the characters 'A' and '\0' and thus 2 bytes for storagebOnerequired.

### 2.2.5 Symbolic Constants (Macros)

If one of the constants used in the previous sections is required more than once, a symbolic name is assigned to this constant, e.g

#defineNL'\n'

#defineN5

![](Images/image00868.jpeg)#defineHELLO"Hello  World\n"

or in general

#define<identifier> <constant>

Remarks:

![](Images/image00869.jpeg)ofrightPrëprocessrightreplaces every occurrence of in the rest of the source code

<identifier> with <constant>, ie, off

cout << HELLO;

will

cout << "Hello World\n";

![](Images/image00840.jpeg)![](Images/image00870.jpeg)u¨  usuallyironno lower-case letters are used in these identifiers because, for example, MAX AUTO is then immediately recognizable as a symbolic constant.

### 2.2.6 Constant with variable names

![](Images/image00871.jpeg)wei.ea variable declarationadditionalHwith the ending¨sselwortconst geis marked, this variable can only be initialized in the declaration part and never again afterwards, ie it acts as a constant.

![](Images/image00872.jpeg)

difference:

#defineN5Eswill no disk space fu¨rightN benorequired,since N in ge

all source code is replaced by 5.

const int N =5; Variable N is saved, the program works with it

her.

Chapter 3

# Expressione,Operators and mathematical functions

• expression¨ckeconsist of operands and operators.

• arevariables, constantsorrightexpression again¨cke.

• operators fuearnActions with operands.

## 3.1 assignment operator

The assignment operator <operand_A> = <operand_B> assigns the value of the right operand to the left operand, which must be a variable.

For example, in the result of the statement sequence

![](Images/image00873.jpeg)

the value of x is 0 and the value of y is 4\. where x, y, 0,x+4 operands, where the latter is also an expression consisting of the operands x, 4 and the operator +. Both x = 0 and y = x + 4 are expressions. First the trailing semicolon ; converts these expressions into statements to be executed!

![](Images/image00874.jpeg)Esk̈onnenalsoHmultiple assignments occur. The following three assignments are aequivalent.

13

![](Images/image00875.jpeg) 

## 3.2 arithmeticoperators

### 3.2.1 U.N ̈areoperator

atwellren operatorskickstonly one operand.

![](Images/image00876.jpeg)operatorDescriptionExample

-negation-a

### 3.2.2 I  ̈areoperators

atamaren operatorstwo operands occur. The result type of the operation ha¨ngtbeforenenn operatorsaway.

| operator | description | example |
| + | addition | b + a |
| - | subtraction | b - a |
| * | multiplication | b * a |
| / | Division (! with integer values ​​!) | b/a |
| % | remainder in integer division | b % a |

![](Images/image00877.jpeg)![](Images/image00878.jpeg)Dividing integers calculates the integer part of the division, ie 8 / 3 returns 2 as the result. However, if the result is 2.666666, at least one of the operators must be converted to a floating-point number, as can be seen in the example.

3.3. COMPARISON OPERATORS15

![](Images/image00879.jpeg)![](Images/image00880.jpeg)Concerning.inrightpriority rulenwas¨right  operators  may beouchfyoue  literaturevprovedyoueoldThe rule “point calculations before dash calculations” also applies in C/C++. Analogueto thebecome school expr¨ckein round brackets ( <expression> ) firstcalculated.

## 3.3 comparison operators

Vcomparison operatorsare bina¨reoperators. The result value is always oneInteger value, where FALSE returns 0 and TRUE returns non-zero.

| operator | description | example |
| > | bigsweeter | b > a |
| >= | bigsweetrightorrightsame | b >= 3.14 |
| < | smaller | a <b/3Ex330.cc |
| <= | Smaller or equal | b*a <= c |
| == | equal (! with floating point numbers!) | a == b |
| != | not equal (! with floating point numbers!) | a != 3.14 |

![](Images/image00881.jpeg) 

A typical error occurs when testing for equality by using instead of theequalsoperators == the assignment operator = is written. The compiler accepts both source texts, possibly (depending on the compiler) a warning is issued if the code is incorrect.

![](Images/image00882.jpeg)

in theincorrectn codekickstthe unknownwisheNebeffecton,thereßenrightWerof the variable i in the test geat thet will, woweari.e  following,correct code nonehas side effects.

![](Images/image00883.jpeg)

3.4. LOGICAL OPERATORS17

## 3.4 Logical Operators

Esgivetnowright aandn / Arenlogicaln Operator:

| operator description | example |  |
| ! logical negation | ! (3>4) | // | TRUE |  |
| U.Ni.etwo bina¨relogicale Operators: |  |
| operator | description | example |  |  |
| && | logicalAND | (3>4)&& | (3<=4) | // FALSE |
| &#124;&#124; | logical OR | (3>4) &#124;&#124; | (3<=4) | // TRUE |
|  |  |  |  |  |  |

![](Images/image00884.jpeg)Tueetruth tables fu¨rightthe logical AND and the logical OR areknown from algebra (otherwise, see literature).

![](Images/image00885.jpeg)

## 3.5 bit-orientedoperators

eggn bitis the smallest information unit with exactly two mosamen conditionfind:

![](Images/image00886.jpeg)wouldticëscht  bit set

≡ (0

≡ (0

![](Images/image00887.jpeg)false true

![](Images/image00888.jpeg)![](Images/image00889.jpeg)A byte consists of 8 bits, so a short int number is 16 bits long. WhenOperators in bit operations usually occur in integer expressions¨ckeon.

### 3.5.1 U.N¨arebit-oriented operators

![](Images/image00890.jpeg)operatorDescriptionExample

~binaovercomplement,bitwironnegationnof the operand~k

### 3.5.2 Am¨arebit-oriented operators

![](Images/image00891.jpeg)operatorDescriptionExample

&bitwise AND theoperandsk & l

| bitwiseORk | l

^bitwise exclusiveORk^l

<<Left shift bits from

<op1> by <op2> digits

>>Right shift of bits from

<op1> by <op2> digits

k<<2// = k*4

k >>2// = k/4

| Truth table:x | and | x & | and | x &#124; | and | x^y |
| 0 | 0 | 0 |  | 0 |  | 0 |
| 0 | L | 0 |  | L |  | L |
| L | 0 | 0 |  | L |  | L |
| L | L | L |  | L |  | 0 |

![](Images/image00892.jpeg)These operators are demonstrated in the following examples:

| l = 5; | // | 0..000L0L | = | 5 |
| k = 6; | // | 0..000LL0 | = | 6 |

![](Images/image00893.jpeg)

TueeBit operations are nuplusHwhen testing whether an even or odd in-terger number is available. The least significant bit can be used with integer numbers to differentiate between even and odd numbers (see also the bit representation of the numbers 5 and 6 in the above code). Therefore, if this bit is ORed with a set bit, the least significant bit remains unchanged for odd numbers. This is exploited in the following code.

![](Images/image00894.jpeg)![](Images/image00895.jpeg)

## 3.6 Operations with predefinedfunctions

### 3.6.1 Mathematicalfunctions

The header file math.h contains, among other things, the definitions of the mathematical functions and constants summarized in Table 3.1:

Rounding a real number x can be achieved with ceil(x+0.5) (ignoring the rounding rules in eg, 4.5).

Function/ConstantDescription

![](Images/image00896.jpeg)![](Images/image00897.jpeg)square(x)square rootbeforenx:√2 x (x0)

exp(x)ex

log(x)of courselocalright logarithmbeforenx:loge x (x > 0)

pow(x,y)Exponentiation (x > 0 if y is not an integer)

![](Images/image00898.jpeg)fabs(x)absolute value of x: x

![](Images/image00899.jpeg)fmod(x,y)real remainder of x/y(y = 0)

![](Images/image00900.jpeg)cell(x)n / Anextealle  numberx

![](Images/image00901.jpeg)floor(x)n / Anextealle  numberx

![](Images/image00902.jpeg)sin(x), cos(x), tan(x) trigonometric functions asin(x),acos(x)trig inverse functions (x [1, 1])assigning(x)              trig inverse function

![](Images/image00903.jpeg)

M_EEuler's number e

M_PI p

Table 3.1: Mathematical functions

![](Images/image00904.jpeg)foot¨rightyoue  Permitted¨assigsinceThe programmer is responsible for the operations, ie the domain of the arguments. Otherwise program aborẗwhichor produce nonsensical results.

![](Images/image00905.jpeg)

The functions from math.h are stored in a special mathematical library, so the compiling and linking command must take this library libm.a into account, ie

LINUX> g++ Ex361.cc [-lm]

### 3.6.2 functionsnfu¨rightcharacter strings

![](Images/image00906.jpeg)The header file string.h contains, among other things, the definitions of the following functions for strings:

![](Images/image00907.jpeg)FunctionDescription

strcat(s1,s2)Attachmentlengthnbeforen s2an s1

strcmp(s1,s2)Lexicographical comparison of strings s1 and s2 strcpy(s1,s2) Copies s2 to s1

strlen(s)Number of characters in string s ( = sizeof(s1)-1 )

strchr(s,c)Finds character c in string s

tabell3.2: Classic functions fu¨rightthongs

![](Images/image00908.jpeg)

detailsandbhethese functions (and others) ko¨nenby means of

LINUX> man 3 string LINUX> man strcmp can be obtained.

## 3.7 Increment and decrement operators

### 3.7.1 Pr¨afix notation

![](Images/image00909.jpeg)![](Images/image00910.jpeg)

### 3.7.2 postfix notation

![](Images/image00911.jpeg)![](Images/image00912.jpeg)

Pre¨-U.Ni.epostfixed notation should economicalvusedwearth,mostlytbusedone thisefu¨rightan index variable in cycles (§ 4).

## 3.8 Compound assignments

value assignmentsthe form

<lvalue> = <lvalue> <operator> <expression>

knockout¨nen to

verkurtwill.

<lvalue> <operator>= <expression>

Here <operator> ∈ {+,-,*,/,%,&,|,^,<<,>>} from § 3.2 and § 3.5 .

3.9.  OTHER USEFUL CONSTANTS 23

![](Images/image00913.jpeg)

## 3.9 Continueenow¨additionalconstants

foot¨right system dependentpendinge number ranges,Exactlyopportunitiesetc.  istyoueselectionlenrightfol-ing constants quite helpful.

![](Images/image00914.jpeg)FunctionDescription

FLT_DIGnumberlgoodvalidrightdecimals fu¨rightfloatFLT_MINSmallest representablepositive number FLT_MAX bigate,representableepositive numberFLT_EPSILON Smallest positive number with 1.0 + ε = 1.0

![](Images/image00915.jpeg)(Job advertisementfake)

DBL_howifinfu¨rightdouble

LDBL_howifinfu¨rightlong doubles

Table 3.3: A few constants from float.h

![](Images/image00916.jpeg)FunctionDescription

INT_MINSmallest representable integer number INT_MAXbigate,representableepositive integer SHRT_              howifinfu¨rightshort int

LONG_howifinfu¨rightlong int LLONG_howifinfu¨rightlong long int

Table 3.4: A few constants from limits.h

Wmoreconstants knockout¨nenunder the gabusynLinux distributions di-directly in the files /usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3/include/float.h and

/usr/include/limits.hto be checked. The corresponding header files can also be created with the command

LINUX> find /usr -name float.h -print

be searched.

Chapter 4

# control structures

## 4.1 Simple instruction

A simple statement is made up of an expression and the semicolon at the end of a statement:

<expression> ;

Examples: cout << "Hello World" << endl; i = 1 ;

## 4.2 block

The block (also compound statement) is a summary of agreements and statements using curly brackets:

{

<statement_1>

...

<statement_n>

![](Images/image00917.jpeg)}

25

Structogram:

![](Images/image00918.gif)

![](Images/image00919.jpeg)In C, the declaration part must immediately follow the beginning of the block. In C++ you canseveraleVparts of the agreementim  block  exist,  shehimeatnnowrightbefore

enrightrespective first use of the variable names. From gru¨nden derightHowever, this should not be exploited for the sake of clarity in the program.

• The closing bracket at the end of the block “}” is not followed by a semicolon.

• A block can always be used in place of a statement.

• Blo¨ckek¨onnenbanyinto each otherrightbe nested.

![](Images/image00920.jpeg)![](Images/image00921.jpeg)The variables declared in a block are only visible there, ie the variable does not exist outside the block (locality). Conversely, variables of the superordinate block can be accessed.

![](Images/image00922.jpeg)

## 4.3 branches

The general form of branching (also alternative) is

if ( <logical expression> )

<statement_A> else

<statement_B>

U.Ni.e e.gchoicetin turns in turnalsapplice.  deright else -Branchcannwignoredbecome (simple alternative).

Structogram:

![](Images/image00923.gif)

As is so often the case, a concrete problem can be programmed in various ways.

![](Images/image00924.jpeg)Example: We consider the calculation of the Heaviside function

y(x)=1x≥ 0

0x <0

![](Images/image00925.jpeg)and present four variants of implementation.

![](Images/image00926.jpeg)

Option A: simple alternative

![](Images/image00927.jpeg)

variant b: dual alternative

![](Images/image00928.jpeg)

variante c:double alternative with Blo¨ckin

![](Images/image00929.jpeg)

variant d: decision operator.

Stepping in a double alternativein each branch only one value assignment to the same variable (as in versions b) and c)), then the decision operator

![](Images/image00840.jpeg)![](Images/image00840.jpeg)<log. expression> ? <expression A> : <expression B>

![](Images/image00930.jpeg)be used.

Example: Another example is the calculation of the signum function (sign function)

![](Images/image00931.jpeg)y(x) =

1x >0

0x= 0

-1x < 0

![](Images/image00932.gif)![](Images/image00933.jpeg)and we present several variants of implementation. Structogram:

We consider two implementation variants, the framework program is identical to the framework program on page 28.

![](Images/image00934.jpeg)Option A: nesting of alternatives

varianteb:casesenright else branchnowrightouchs onewfester if-else statementbe-stands, variant a can be slightly modified.

![](Images/image00935.jpeg)

In general, such a multipath decision can be

if ( <logical expression_1> )

<statement_1>

else if ( <logical expression_2> )

<instruction_2>

...

else if ( <logical expression_(n-1)> )

<statement_(n-1)> else

<statement_n>

written, with the else branch being optional.

![](Images/image00936.jpeg)Example: Determining the minimum and maximum of two numbers to be entered.

Structogram:

![](Images/image00937.gif)

![](Images/image00938.jpeg)

![](Images/image00939.jpeg)Example: Determining the minimum of three numbers to be entered. Structogram:

![](Images/image00940.gif)

![](Images/image00941.jpeg)

## 4.4 derightZcounting cycles(for loop)

At theZacooling cyclesstands for the number of cyclesufea priori, thefracture test is done before running a cycle. The general form is

for (<expression_1>; <expression_2>; <expression_3>)

<statement>

Ambest be the zacooling cyclesan one example allowedfeeds.

![](Images/image00942.jpeg)Example:Esistthe sum of the first 5 natulocaln  numbers  tocalculate.

![](Images/image00943.jpeg)

in theabove program example, i is the running variable of Zaoil cycle,wmooseinitialized with i = 1 (<expression_1>), continued with i = i+1 (<expression_3>).  does noti.ein i<= n (<expression_2>) regarding the upper limit of the loop capacity¨ufeIs tested. Inside the loop sum = sum + i; (instruction) theactual calculation steps of the cycle. The summation variable sum must be initialized before entering the cycle.

A compact version of this summation loop (correct but very difficult to read) would be:

for (isum = 0, i = 1; i <= n; isum += i, i++)

A distinction is made between the end of an instruction “;” and the separator “,” in a list of expressions. These lists are processed from left to right.

![](Images/image00944.jpeg)The <expression_2> is always a logical expression ( 3.3-3.4) and <expression_3>

is an arithmetic expression for manipulating the run variables, e.g

i++

j = d-2 d += 2

x =x+h// float type

k =2*k// doubling

l =l/4// Quartering - be careful with integers

Structogram:

![](Images/image00945.gif)

The control variable can be a simple variableout2.1 be eg, int or

![](Images/image00946.jpeg)double .

![](Images/image00844.jpeg)![](Images/image00947.jpeg)![](Images/image00948.jpeg)Be careful when using floating point numbers (float, double) asvariable. The correct abort test may not be easy to implement there due to the internal number representation.

Structogram:

![](Images/image00949.gif)Example: It is the double sum

![](Images/image00950.jpeg)![](Images/image00951.jpeg)nkn

sum=1

i2

![](Images/image00952.jpeg)k=1 i=1

tk

=tk

k=1

![](Images/image00953.jpeg)![](Images/image00954.jpeg)was¨rightn to be entered to be calculatedto.

![](Images/image00955.jpeg)

Wmoresimple examples calculate the sum of the first even natulocalnNumbers and the Za¨hlen onecountdowns.

![](Images/image00956.jpeg)

The following examples illustrate the problem of the limited accuracy of floating-point numbers in connection with cycles and some tips on how to work around them.

![](Images/image00957.jpeg)Example: Output of the discrete nodes xi of the interval [0, 1], which is in

![](Images/image00844.jpeg)nequal subintervals, i.e.,

![](Images/image00958.jpeg)![](Images/image00959.jpeg)x= iHi=0, . . . ,nWithH=1 − 0

n

Structogram:

![](Images/image00960.gif)![](Images/image00961.jpeg)

Dafloating point numbernnowright onelimitedenumberlgoodvalidright digitsbsit,canit (mostly) happens that the last node xn is not output. Only for = 2k , k cannin our example a correct processing of the Zacooling cyclesguaranteetwearth.  selectionee are

1. ![](Images/image00962.jpeg)A¨  changeGinsabort testsinxi <= xe + h/2.0 , but xn is still in error.

for (xi = far; xi < = car + h/2.0; xi += h)

{

cout << xi << endl;

}

2. Cycle with int control variable for (i = 0; i <= n; i++)

{

xi = xa + i*h;

cout << xi << endl;

}

![](Images/image00963.jpeg)Tueecommon summation of minor and majorouterrightNumbers can also

inaccuracysidesfuear. In the example, the sum

s1 :=

n

![](Images/image00964.jpeg)![](Images/image00965.jpeg)![](Images/image00966.jpeg)i=1

1/i

2with the

![](Images/image00967.jpeg)(theoretically identical) sum

![](Images/image00968.jpeg)

2:= S1 1

![](Images/image00969.jpeg)

2for big

(65,000, 650,000)

![](Images/image00970.jpeg)

![](Images/image00971.jpeg)

![](Images/image00972.jpeg)

The numerical result in s2 is more accurate because all small numbers are there firstare added, which at s1 because of the restrictionsgoodnnumberlgoodvalidrightDigits no longer contribute to the summation kocan. At the same time is closedbnote,that the computation of 1.0/(i*i) ends in an overflow, since

i*i can no longer be represented in int numbers. On the other hand, the calculation of1.0/i/i complete¨ndiGimRange of floating point numbers.

## 4.5 Repelling cycle (while loop)

At therejecting cycle is the number of passagesufenot fixed a priorithe abort test is performed before running a cycle.

The general form is

while (<logical expression>)

<statement>

![](Images/image00973.jpeg)![](Images/image00974.jpeg)Example:  determineinnrounded upn  buildinglogarithms(Bases2)  one  a-reading number.

Structogram:

![](Images/image00975.gif)Comment:If the very first test in the rejecting cycle is FALSE, then the statement block inside the cycle is never executed (the cycle is rejected).

## 4.6 Non-rejecting cycle (do-while loop)

At thenon-rejecting cycle is the number of passagesufenot fixed a-priori, the termination test takes place after a cycle has been run through. Thus passairthe non-rejecting cycle uses the instructions inside the cycle at least once.

The general form is

of the

<statement>

while (<logical expression>) ;

![](Images/image00976.gif)Structogram:

![](Images/image00977.jpeg)Example: A character is read from the keyboard until an x

is entered.

![](Images/image00978.jpeg)

Consider weathera somewhat more demanding example, namely the Losolutioncan be determined from sin(x) = x/2 with x ∈ (0, π). For this one considers

youeEquivalent zero problem: Determine the zero x0 ∈ (0, π) of the

![](Images/image00979.jpeg)Function f(x) := sin(x)x/2 = 0 .

Analytically:No practical Losolutionegpresent.

graphicsch:The function f(x) is graphed and the LoResolution interval reduced manually (halved). This process is continued untiluntil x0 can be determined accurately enough, ie, to a predetermined number of digits.

![](Images/image00980.jpeg)![](Images/image00981.jpeg)f(x) =sin(x)-x/20.25

![](Images/image00982.jpeg)0.2

0

–0.2

0.3

0.2

0.2

0.15

–0.4

0.1

–0.6

–0.8

0.1

0.05

-1

02

–1.202

–1.4

–0.05

–1.6

Numeric: The above graphical procedure can be applied to a purely numerical

ricsVExperiencedimcomputerandbendurewearth(enright MAPLE -

![](Images/image00983.jpeg)![](Images/image00984.jpeg)![](Images/image00985.jpeg)callffsolve(sin(x)=x/2,x=0.1..3 returns as Naapproximation resultx0 = 1.895494267 ). We are developing a program to determine theZero of f (x) := sin(x) x/2 in the interval [a, b] by bisecting the interval, where it is assumed for simplification that f (a) > 0 and f (b) < 0\. The midpoint of the interval is denoted by c := (a + b)/2\. then

knockout¨nenWe ubhethe Lo¨sunGstate the following:

x0∈ [c, b]if f (c) > 0 .

![](Images/image00986.jpeg)![](Images/image00987.jpeg)x0∈ [a, c]iff(c) < 0

![](Images/image00988.jpeg)By redefining the interval limits a and b, the zero search can be reduced to the smaller (halved) interval. We demonstrate the implementation using a non-repellent cycle.

Structogram:

![](Images/image00989.gif)

The above bisection can also be realized by means of a rejecting cycle.

![](Images/image00990.gif)

![](Images/image00991.jpeg)

Since floating-point numbers only work with limited accuracy, an abort test f (c) = 0 usually results in an endless program. That's a break test like |f(c)| < ε with a given accuracy 0 < ε 1 is preferable.

![](Images/image00992.jpeg)Likent:Behindcooling cyclesn(for) which executes at least one cycleto hearknockouẗnen  as well asbyHdifferentiron end(while)to thesalso by non-rejecting cycles (do while)equivalentstexpressed¨cctwearth.thiseA¨equivalentE.g.cannbeggVuseinrightapplironingin4.8 are lost. If in a zacooling cyclesinrightAway-

![](Images/image00993.jpeg)brokent  alwaysFALSEE  resultsie.inrightloopcörphe  willNoeexecutedtouches,then istinright  appropriatedifferentiron end  cycleafterH  howbeforerightaequivalent.  Howeveristthe not deviron endcycle no longer aequivalent,there the loop körpheis also processed once in this case. See the example file Loops.cc.

## 4.7 Multiway selection (switch statement)

Tueeadditionalegselection ermpossiblet oneindividualsreactnouchf specificWgeta variable.

switch (<expression>)

{

case <const_expression_1>:

<statement_1> [break;]

...

case <const_expression_n> :

<statement_n> [break;]

default:

<statement_default>

}

![](Images/image00994.jpeg)![](Images/image00995.jpeg)Example:outputeinrightnumber¨rtrightwas¨rightthe integer inputs {1, 2, 3}.

Above switch statementkcouldealsoHwedt onemultiple vbranching(Sincee31)be implemented, however, in the switch statement, the individual

4.8.  UNCONDITIONAL PASS OF CONTROL 43

branchesexplicit andbheleave the break; statement. Withoutbreak;  will

togetherplusHenrightgo to the next branch¨rige blockprocessedruns.

## 4.8 Unconditional Tax Instructions rungsudownhille

breakThe na is immediately aborted¨chstaexteriornswitch whiledo-while, for statement.

![](Images/image00996.jpeg)continueCancellation of the current and start of the nanextncycle of a while,do-while, for loop.

goto <brand> Continuation of the program at the with

<brand> : <statement>

marked spot.

Comment :Except for break in the switch statement, the above statements should be used very sparingly (better not at all), since they run counter to structured programming and produce the dreaded spaghetti code.

in theInternship are above instructions for Lo¨sunGof exercises etc. not allowed.

Chapter 5

# Structured data types

Wirightin this chapter new Mpossiblesidesof data storageear.

![](Images/image00997.jpeg)array:

Grouping of elements of the same type.

![](Images/image00998.jpeg)Structure (struct):

Grouping of components of different types.

![](Images/image00999.jpeg)union (union):

u¨ bstorageseveral components of different types in the same memory space.

![](Images/image01000.jpeg)recordpaymentType(number)

basic dataypwedtfree wapalpablemWcrop area.

## 5.1 fields (arrays)

### 5.1.1 One-dimensional fields

Data (elements) of the same type are combined in a field. The general convention of a static field is

<type> <identifier>[dimension];

where the square brackets “[” and “]” are an essential part of the agreement. A one-dimensional array is mathematically equivalent to a vector.

45

![](Images/image01001.jpeg)![](Images/image01002.jpeg)

The square brackets are used in the declaration part of the dimension declarationx[N] and in the instruction part access to individual array elements x[3] . The field can already be initialized during the declaration:

double x[N] = {9,7,6,5,7}

![](Images/image01003.jpeg)Attention :The numbering of the array elements begins with 0\. Therefore, onlyon array elements xi, i = 0, . . . , N 1 can be accessed. Otherwise, mysterious program behavior, inexplicable miscalculations and sudden program crashes are to be expected, the cause of which is not obvious because they may only appear in remote program parts.

Typical mistake

//Typical error

{

const int N = 123;

int ij[N] , i;

...

for (i = 1; i <= N;i++)// !! WRONG!!

{

cout << ij[i] << endl;

}

}

The array elements ij1, ij2, ij3, ij4 and the meaningless value of ij5 become

spent, howevernot the very first array element ij0 .

The dimension of a static field must be known at compile time, so only constants or expressions consisting of constants can appear as a dimension.

{

const intN=5, M=1; int size;

floatx[5];//Correct

short i[N];//Correct

charc[N-M+1];//Correct

intij[size];//!! WRONG!!

}

![](Images/image01004.jpeg)![](Images/image01005.jpeg)Example: An interesting special case of the field is the character string (string). We initialize the string with the word "math" and print it out in normal type and character by character.

Tueestring ha¨ttealsoHWithchar word[L] = "math"; or

char word[] = "math";

initializetwill kcan,where in the latter case the La¨ngeof field word

ouchsthe la¨ngeenrightCharacter string constant is determined.

![](Images/image01006.jpeg)

Example: Calculation of

L2-norm of a vector, i.e.,

ǁ x  ǁL2

:=N−1 2

![](Images/image01007.jpeg)![](Images/image01008.jpeg)![](Images/image01009.jpeg)i=0

![](Images/image01010.jpeg)![](Images/image01011.jpeg)

Als small exampleserveeU.NsyoueFibonaci sequence of numbers,wmooseandbheyoue two-staged recursion

f(n): = f(n − 1) + f(n −2)n= 2, . . .

![](Images/image01012.jpeg)is defined with the initial conditions f (0) = 0, f (1) = 1\. To check, we can use Binet's or de Moivre1's formula.

![](Images/image01013.jpeg)![](Images/image01014.jpeg)![](Images/image01013.jpeg)![](Images/image01014.jpeg)![](Images/image01015.jpeg)![](Images/image01016.jpeg)   1  1+ √5 !n1 − √5 !n!

![](Images/image01017.jpeg)![](Images/image01018.jpeg)![](Images/image01019.jpeg)

![](Images/image01020.jpeg)

![](Images/image01021.jpeg)

1[http://www.ee.surrey.ac.uk/Personal/R.Knott/Fib onacci/fibFormula.html](http://www.ee.surrey.ac.uk/Personal/R.Knott/Fibonacci/fibFormula.html)

![](Images/image01022.jpeg)As a further example, the minimum and maximum of a vector are to be determined and the corresponding vector elements are to be swapped with one another (similar to pivoting). This includes the two subtasks:

a) Determine minimum and maximum (and mark the positions). Structogram:

![](Images/image01023.gif)

b) VexchangeMin/Max Entryage.  At Vectorlange0 or at identicalNo swapping is necessary for vector elements.

![](Images/image01024.gif)Structogram:

At theVexchange futouches

the obvious first idea x[kmin] = x[kmax] x[kmax] = x[kmin]

not to success. Why?

![](Images/image01025.jpeg)

### 5.1.2 Multidimensional Fields

Tueeentry¨ageenrightso farrightbconsidered1D-Folder areimSpoakbehind each otherstored (linear memory model), for example, is the row vector

as

x0x1x2x3x4

![](Images/image01026.jpeg)  double x[5];

agreed and saved as

| x0 | x1 | x2 | x3 | x4 |

where each cell is 8 bytes long.

![](Images/image01027.jpeg)A two-dimensional (static) array, for example, a matrix A with N = 4 rows and M = 3 columns

![](Images/image01028.jpeg)A00A01A02A10A11A12

AN×MA20A21A22

A30A31A32

![](Images/image01029.jpeg)![](Images/image01029.jpeg)![](Images/image01029.jpeg)can also only be stored linearly in memory, i.e.,

| A00 | A01 | A02 | A10 | A11 | A12 | A20 | A21 | A22 | A30 | A31 | A32 |

![](Images/image01030.jpeg)This results in two options for the 2D field declaration: Variant 1: As a 2D array.

doubleA[N][M];// Declaration

A[3][1] =5.0;// Initialize A(3,1)

![](Images/image01031.jpeg)Variant 2 :  As a 1D array.

doubleA[N*M]; // Declaration A[3*M+1] =5.0;// Initialize A(3,1)

Example: As an example we consider the multiplication of the matrix AN×M consisting of N = 4 rows and M = 3 columns with a row vectoruM the Lange M .  The result is a row vector f N of La¨nge N ,ie,

![](Images/image01032.jpeg)![](Images/image01033.jpeg)f:=AN×M uM .The components of f = [f0, f1, . . . , fN−1]T bcalculate

to

M−1

![](Images/image01034.jpeg)be  :=hey,j  ·  andj∀i  =0,  .  .  .  ,  N  −  1.

j=0

hoherdimensionalefolderk¨onnendeclared and used analogous to version 1will. In variant 2 double B[L,N,M]; be accessed using B[i*M*N+j*M+k].

## 5.2 structures

The structure defines a new data type which combines components of different types. The type declaration

struct <struct_identifier>

{

<data declaration>

};

allows the declaration of variables of this type

<struct_identifier> <var_identifier>;

![](Images/image01035.jpeg)![](Images/image01036.jpeg)Example:We declare a data type to store the persosimilardata of a student.

The assignmentrobbi = arni; copies the complete dataset from avariables to the other. The component firstname of the variable arni (of the type Student) is accessed via

on it.firstname

The data is saved in the form

| matriculation | sketch | Surname | First name |

awayHa¨ngiGbeforen compiler settingsor.  -optionsknockout¨nen smallerunused- teSpEicherlu¨ckin betweenenn componentsimSpoakperformn(Dateaalignmentst fu¨rightfaster data access ).

![](Images/image01037.jpeg)Tueestructure student can easily fu¨rightStudents who have several majorsprove, to be expanded.

![](Images/image01038.jpeg)

![](Images/image01039.jpeg)

![](Images/image01040.jpeg)![](Images/image01041.jpeg)Tueestructure student incl̈altalready have fields as components. On the other hand könenthiseData types can in turn be arranged into fields.

structuresnknockout¨nen in turnat thee structureddatatypesals componentscontain.

![](Images/image01042.jpeg)

In the example above, line.p2 is a variable of the Point3D type, whose data can be accessed using the . Operators can be accessed.

## 5.3 union

AlleseUnion components are on the same storage area ubhe-shown overlapping. The type declaration

union <union_identifier>

{

<data declaration>

};

allows the declaration of variables of this type

[union] <union_identifier><var_identifier>;

Components of the union are accessed like a structure.

![](Images/image01043.jpeg)![](Images/image01044.jpeg)

![](Images/image01045.jpeg)The memory requirement of aunion                                   

![](Images/image01046.jpeg)![](Images/image01047.jpeg)![](Images/image01048.jpeg)judgetafter the bigatenComponet (here sizeof(double) = 8). The union is used to store spacesaving should be reserved for experienced programmers because of the possibility of errors (ie, no

![](Images/image01049.jpeg)

5.4.  ENUM TYPE 57

## 5.4 recordpayment type

![](Images/image01050.jpeg)ofrightrecordchoiceypist  onebasicypwedtfriiwowpalpablemWcrop areathes  may beillustrated by the days of the week.

![](Images/image01051.jpeg)

| day weekday; | // | variable of enum |
| weekday = monday; | // | data init |

C++ has a predefined type bool, which takes the values ​​false and true

acceptncan.  InCla¨ßt himselfthesby definition

enum bool {false,true}

inanalogrightWiron reach,wobegg falsebyH 0U.Ni.e truebyH 1representativepresentedwhich conforms to § 2.1.1 and § 3.3.

## 5.5 General type definitions

The general type definition

typedef <type_definition> <type_identifier>

is the consequent advancement to freely definable types.

![](Images/image01052.jpeg)![](Images/image01053.jpeg)The program example below illustrates the definition of the three new types Boolean, Text and Point3D.

Interestingly, a variable of type Text is now always a character string variable with a (max.) length of 100\. Note also the initialization of the variable p. Even a constant of the type Point3d can be declared and initialized with it.

Chapter 6

# pointer

Up until now, we've always accessed variables directly, meaning it didn't care where the data was stored in memory. A new type of variable, the pointer, stores addresses considering the type of data stored there.

## 6.1 agreement of pointers

If the pointer to an object of type int is denoted by p, then

int *p;

whose declaration, or general is made by

[storage class] <type> *<identifier>;

defines a pointer to the data type <type>.

![](Images/image01054.jpeg)SOknockouẗnenyouefollowing pointer variables are defined

![](Images/image01055.jpeg)![](Images/image01056.jpeg)

## 6.2 pointer operators

derightwell¨re reference operator(address operator)

&<variable>determines the address of the variable in the operand.

derightwell¨redereference operator(access operator)

*<pointers>

![](Images/image01057.jpeg)![](Images/image01058.jpeg)allows (indirect) access to the data pointed to by the pointer. The data can be manipulated like a variable.

In the example aboveacts*pintas an int variable and accordingly all operations defined for it can be performed with it.

![](Images/image01059.jpeg)![](Images/image01060.jpeg)![](Images/image01061.jpeg)

![](Images/image01062.jpeg)![](Images/image01063.jpeg)Attention :  In the program fragment

{

double *px;

*px =3.1; // WRONG!

}

willalthough storage space fu¨rightreserves the pointer (8 bytes), but the value of px is still undefined and so the value 3.1 is converted to a dafu¨rightnotdesignated memory area written

=⇒mysterio¨seprogram stepreU.Ni.e-error.

There is a special pointer constant 0 (NULL in C) which refers to the (hexadecimal) memory address 0x0 (= nil) and which can be tested for as a pointer variable.

6.3\. POINTERS AND FIELDS - POINTER ARITHMETICS61

## 6.3 Pointers and Arrays - Pointer Arithmetic

Arrays use the linear memory model, ie an element that follows in the index is also physically stored in the immediately following memory area. This fact allows pointer variables to be interpreted as field identifiers and vice versa.

{

const int N = 10;

int f[N],*pint;// array and pointer

pint =&f[0];// init pointer

}

Field identifiers are always treated as pointers, hence the program line

identical with

pint = &f[0];

pint = f;

![](Images/image01064.jpeg)consequentialGtherefore set the expression¨ckef[1],*(f+1),*(pint+1),

![](Images/image01065.jpeg)pint[1] represents the identical access to array element f1.

|  | f0 |  | f1 |  |

![](Images/image01066.jpeg)pint

![](Images/image01067.jpeg)The address represented by (pint+1).will result in (address in pint) + sizeof(int) . In this case, int designates the data type on which thePointer pin points. Access to other array elements fi, i = 0 . . . N 1 is analogous.

The following operators are applicable to pointers:

• Comparison operators: == , != , < , > , <= , >=

• Addition + and subtraction -

![](Images/image01068.jpeg)increase++ ,decrement-- and compound operators

+= , -=

![](Images/image01069.jpeg)![](Images/image01070.jpeg)![](Images/image01071.jpeg)To demonstrate, we consider an example in which an array is first defined and initialized in a conventional way and then output using pointer operations.

## 6.4 Dynamic arrays using pointer variables

![](Images/image01072.jpeg)Until nowreferred a pointer to already provided (allocated) memory fu¨ronesimple variable, structure, field. foot¨rightHowever, a pointer can also be added to the typeorigrightSpoak areadynamicHallocatetwearth.Mr Jerezandbone usesthe new conclusion¨sselwortnew . The memory allocated in this way can be changed usingdelete to be released again.

![](Images/image01073.jpeg)

The statement px = new double[n]; allocates n*sizeof(double) bytes forenn pointer px.  danachcanntheresdynamicefeld px how one staticfeldbe treated. However, dynamic fields make better use of the existing storage space, since this can be released with the delete command and used again for other purposes.

![](Images/image01074.jpeg)danger:The above dynamic field declaration is only fu¨rightC++ goodvalid.In Cmueatnother commands are used - here are the differences.

![](Images/image01075.jpeg)C++C

#include <malloc.h>

px = newdouble[n];px = (double*) malloc(n*sizeof(double)); delete []px; free(px);

![](Images/image01076.jpeg)![](Images/image01077.jpeg)eggnbetweenone-dimensionaldynamic field latet  himself  on the one handbyH  one  one-dimensional dynamic field (analogous to variant 2 in 5.1.2) as well as by a pointer to a field of pointers. This looks like this for a matrix with n rows and m columns.

![](Images/image01078.jpeg)

First the pointer must be allocated to the line pointer, only then can the memory for the individual lines be requested. When deallocating memory, all rows must also be freed again. For the case n = 3 and m = 4, the figure shows how the data is stored in memory.

![](Images/image01079.jpeg)![](Images/image01080.jpeg)![](Images/image01081.jpeg)![](Images/image01082.jpeg)![](Images/image01083.jpeg)...

Attention:There is no guarantee that the individual rows of the matrix are arranged consecutively in memory. Thus, the storage of the dynamic 2D array differs from the storage of the static 2D array, although the syntax of the element access b[i][j] is identical. On the other hand, this matrix storage is more flexible, since the rows can also have different lengths (sparse matrices or matrices with a profile).

![](Images/image01084.jpeg)![](Images/image01085.jpeg)showrightknockouẗnenturn appear in structures or general types. Here, however, gras possibleeCare should be taken when using the dynamic fields, since fu¨rightstatic variables otherwise uncritical operations plomoreHto miraculömprogram inreceivewasearnknockoutcan.

What does the data store look like at times (A), (B) and (C)?

![](Images/image01086.gif)

• robbi does not have its own dynamic fields.

![](Images/image01087.jpeg)delete [] arni.pfirstname;

thus also releases the memory area addressed by robbi.pfirstname and thus robbi.pfirstname points to a memory area that is no longer reserved, which the program may use as it sees fit.

![](Images/image01088.jpeg)tiny = new char[5];

taket himselfennfriibecomenSpoak placeU.Ni.eandbhe writesheyn spa¨ter.

![](Images/image01089.jpeg)Under LINUX-gcc, at time (C) robbi.pfirstname points to the same address as the pointer tiny, so that the data from robbi.pfirstname can be output using

cout << robbi.pfirstname << endl;

gives the output tiny.

![](Images/image01090.jpeg)way out:

![](Images/image01091.jpeg)Eshimeatnwas¨rightrobbi own dynamic fields are allocated and the contents of the dynamic fields of arni mueatnbe copied to this. (see assignment operators and copy constructors fu¨rightclassesalso§ 11).

6.5. POINTERS TO STRUCTURES67

## 6.5 pointers to structures

![](Images/image01092.jpeg)![](Images/image01093.jpeg)We consider the structure Student ( 5.2) and define a pointer to it.

Tuee accesses(*pg).firstname and pg->firstname are vo¨lliGaequivalent.  All-thing improves the latterclearly the readability of a program, especially if the pointer represents a dynamic array of type Student. This is particularly evident when accessing array elements of firstname (ie, single characters). Access to the 0th character is via

| or | pg->firstname[0] (*pg).firstname[0] | or or | *pg->firstname*(*pg).firstname |
| and accessing the 3rd character using |
| or | pg->firstname[3] (*pg).firstname[3] | oror | *(pg->firstname+3)*((*pg).firstname+3) |
|  |  |  |  |

![](Images/image01094.jpeg)Note that pg->firstname represents a pointer to type char and the dereferencing operator * is performed before the + addition. Conjecture and test what you get when you use *pg->firstname+3.

## 6.6 reference

![](Images/image01095.jpeg)AeReference is an alias (pseudoname) fu¨righta variable and can do the samehow these are used. References (unlike pointers) do not represent an object of their own, ie no additional memory is required for them.

6.6. REFERENCE69

![](Images/image01096.jpeg)referencesnbecome houchfigureto the parameterbresultanfunctions used, they-he 7.2\. Another useful application is the reference to an array element, structure element or inner data of a complicated data structure as shown below, derived from the example on page 54.

![](Images/image01097.jpeg)![](Images/image01098.jpeg)

Chapter 7

# functions

## 7.1 definition and declaration

Purpose of a function:

![](Images/image01099.jpeg)ofsOearliern  will  oneprogram partlinothernprogram sectionsn  againinrequired.To the program andbmore evidentand more manageable toodesign, this part of the program is programmed once as a function and called up in the rest of the program with its function name.

![](Images/image01100.jpeg)Alreadycompleted functions könenwas¨rightother programs of other programmers available¨gunGare provided, analogous to the use of

pow(x,y) and strcmp(s1,s2) in§ 3.6.

In the general form of the function definition with

<storage class><type><function_name> (parameter_list)

{

<agreements>

<instructions>

}

putVagreementU.Ni.eapplice partennfunctional co¨rphethererightU.Ni.e <type> laysthe type of Ru¨cvaluefixed. The combination <function_name>and (parameter_list) uniquely identifies a function and is therefore used ascalled signature of a function. The function definition becomes fu¨righteach function exactly once benorequired.

The difference is the function declaration

<storage class><type><function_name> (parameter_list) ;

ineach source file n¨otiGwmooseyoueFunction <function_name> calls.

71

![](Images/image01101.gif)Structogram:

![](Images/image01102.jpeg)Example: We write the calculation of sgn(x) from page 29 as a function.

![](Images/image01103.jpeg)

Remarks:The sgn() function is uniquely described by its signature. thesHatfu¨rightdeclarationnU.Ni.edefinitelynbeforenfunctionsnyoue Consequences:

7.2. PARAMETER TRANSFER 73

(i) Some more (or even more) identical function declarations

double sgn(double x);

are allowed in the example above.

(ii) togetheradditioneFunction declarations with other parameter lists arebelieves, e.g.:

double sgn(double* x); double sgn(int x);

since the arguments differ from the initial definition. However, we have not yet defined these new functions.

(iii) Ae togetheradditionedeclarationn(see § 7.2)

double sgn(double& x);

is not allowed because the signature is as under (i). Therefore, the compiler cannot figure out whether the function under (iii) or the function under (i) is in the statement

y = sgn(x);

meantis.

(iv) Different functions with the same name are identified by their different parameter lists, see item (iii).

(v) derightRu¨cvalueof a function cannot be used to identify itare tightened, the declarations

double sgn(int x); int sgn(int x);

knockout¨nennottdifferencesnwearth(sameesignature)U.Ni.ethereforerightleantthecompiler from this source text.

## 7.2 parametersdownhille

When designing a program, we distinguish three types of parameters of a function:

INPUTParameter data is used in the function but not verachanges,that is, they are constant within the function.

INOUTParameter data is used in the function and verachanges.

OUTPUT parameter data are initialized in the function and, if applicableverachanges.

![](Images/image01104.jpeg)Programmatically we will not distinguish between INOUT and OUTPUT parametersdifferentiate. There are generally three Moequalsidesthe programtechnicalnPassing parameters

1. u¨ bresultenrightData of a variable (by value).

2. u¨ bresultthe address of a variable (by address)

3. u¨ bresultenrightreferencese.gouchf onevariablee(engl.  :by reference), whereby an address is transferred in a hidden manner.

Comment:

Wifuse a variable in the function as a constant¨tztwill, then shouldthey are also treated as such, ie pure INPUT parameters should always be marked as const in the parameter list. This increases security against unintentional data manipulation.

## 7.3 Rureturn valueeof functions

Each function has a function result of data type <type> . As types are allowedbe used:

• simple data types (§ 2.1.1),

• structures (§ 5.2), classes,

• pointer (§ 6.1),

• References (§ 6.6),

jedocHno fields and functions - therefor¨rightbut pointer to a field or aFunction and references to fields.

derightRu¨cvalue(function result)will with

return <result> ;

antherescalling program andbresult.  A special case are functions of the kind

void f(<parameter_list>)

fu¨rightwhich no Ru¨cvalue(voii.e =empty)is expected, so with

return ;

inthe calling program back¨cswept will.

![](Images/image01105.jpeg)![](Images/image01106.jpeg)

Wirightlook at the mpossiblesidesenrightparametersbresultam exampleenrightsgn function with variable double a .

| u¨ bresultart | parameter list | call | effect of | use | recommendation |
| x++ | (*x)++ |
| by value | double x | sgn(a) | internal | —- | INPUT | [c] |
| const double x | not allowed | —- | INPUT | C [simple data types] |
| by address | double* x | sgn(&a) | internal | internal/external | INOUT | C |
| const double* x | internal | not allowed | INPUT | C [complex data types] |
| double* const x | not allowed | internal/external | INOUT | [c] |
| by reference | double& x | sgn(a) | internal/external | —- | INOUT | C++ |
| const double& x | not allowed | —- | INPUT | C++ |
|  |  |  |  |  |  |  |

tabell7.1: Mpossiblesidesenrightparametersbresult

The ”by-reference” variant double &const x is rejected by the compiler and the ”by-address” variant const double* const x , ie,Pointers and data you¨fenlocally not verachangetwearth,istpractically meaningless.

![](Images/image01107.jpeg)![](Images/image01108.jpeg)

examplesfu¨rightFunction results:

floatf1(...) float number [struct] studentf2(...) structure student int*f3(...) Pointer to int number

[struct] Students*f4(...) Pointer to Structure Student

internal(*f5(...)) []Pointer to array of int numbers

internal(*f6(...)) ()Pointer to a function that has the result type int

Remarks:

AefunctionnrepresentfseveraleRu¨cdelivery instructions return[<result>]; besit,eg, one in each branch of an alternative. However, this is no longer clean structured programming.

![](Images/image01109.jpeg)= Each function should have exactly one return statement at the end of the function bodybsit(Defaulti.ewas¨righttheresInternship).

## 7.4 fields as parameters

Staticefields ko¨nenanalogous to their declaration as function parameters ubresultwearth.  HoweversmueatnAllesedimensions,except the honextndimension, to be known at compile time.

![](Images/image01110.jpeg)As a first example, we consider the output of a (static or dynamic) 1D field, ie, a vector x of length n.

7.4\. FIELDS AS PARAMETERS77

Structogram:

![](Images/image01111.gif)![](Images/image01112.jpeg)

AlsnnextsLet's consider the output of a 2D static array, ie, aMatrix with MCOL columns and NROW rows. The number of columns must be defined as a global constant here, otherwise the following function cannot be compiled.

![](Images/image01113.jpeg)

![](Images/image01114.jpeg)Unfortunately  k̈onnen  weatheryouefunctionn  PrintMat_fixnowrightwas¨right  static2D Folder(Matrices)apply, and then only fu¨rightthose with NCOL=3 columns - yesa matrix double aa[7][9] can no longer be output with this function. However, we can interpret the 2D field as a 1D field of length NROW*MCOL and thus generalize the function in such a way that any static 2D fields and dynamic 1D fields that can be interpreted as 2D fields (as in version 2 on page 52) can be handed over.

![](Images/image01115.jpeg)

Since the PrintMat function expects a 1D array (i.e. a pointer), from the static2D Feld a one pointerouchfyoue first rowenrightmotherxandbresultwearth. Therefore, a[0] appears in the corresponding call line.

## 7.5 Declarations and header files, libraries

Normally, the source code of a computer program is composedconsists of (substantially) more than one source text file. With it functions, data structures (and global constants, variables) and macros from other source text files

(name.cc)usedtwearthkcan,busedmomnheader files(name.hh, name.h) which the declarations fu¨rightcontain the source text file name.cc.

### 7.5.1 Example: printvec

![](Images/image01116.jpeg)![](Images/image01117.jpeg)We want to use the PrintVec and PrintMat functions programmed in 7.4 in another code (ie, main program). First we copy the definitions of the two functions (and everything else that is needed for compiling) into the new file printvec.cc.

![](Images/image01118.jpeg)

The file printvec.cc is now compiled (without linking it!)

LINUX> g++ -c printvec.cc

![](Images/image01119.jpeg)whereby the object file printvec.o is created. The main program in

![](Images/image01120.jpeg)Ex751-old.cc bOnebusytwellrightthe declarations of the two functions.

Compiling the main file

LINUX> g++ -c Ex751-old.cc

creates the object file Ex751-old.o which has to be linked with the other object file to the finished program a.out

LINUX> g++ Ex751-old.o printvec.o

satofficialscompile and link latetcan also be expressed in a command line¨ckin

LINUX> g++ Ex751-old.cc printvec.cc

whereby some compilers expect the main() main program in the first source text file (here Ex751-old.cc).

![](Images/image01121.jpeg)Tueedeclarationsnimmain programmwas¨rightyouefunctionsnouchsprintvec.cc scream-We use the header file printvec.hh

![](Images/image01122.jpeg)

U.Ni.e weather substituteenndeclaration partlimmain programmbyHyouebeforenPrePer-processor instruction

![](Images/image01123.jpeg)#include "printvec.hh"

![](Images/image01124.jpeg)which automatically inserts the content of printvec.hh before compiling Ex751.cc.

Tueeanfuapproxchen" " around the file name indicates that the hea-derfile printvec.hh in the same directoryhow to find the source file Ex751.cc.

The command

LINUX> g++ Ex751.cc printvec.cc

in turn generates the program a.out.

![](Images/image00840.jpeg)![](Images/image01125.jpeg)

### 7.5.2 Example: students

![](Images/image00863.jpeg)![](Images/image01126.jpeg)![](Images/image01127.jpeg)Wirightknockouẗnenalso self-defined data structures, eg the data structuresSave Student, Student Mult from 5.2 and Student2 from 6.4 and global constants in a header file student.hh.

![](Images/image01128.jpeg)

The new function Copy Student2 is defined in student.cc, where the function corpheouchsEx643-correct.cc copyt would.

![](Images/image01129.jpeg)

![](Images/image00863.jpeg)![](Images/image01130.jpeg)Since the Student2 structure is used, the header file student.hh must also be included in student.cc. The new Copy Student2 function can now be used in the main program Ex752.cc to copy a structure. Of course, the main program needs the header file student.hh for this.

The command

LINUX> g++ Ex752.cc student.cc

finally creates the program a.out.

### 7.5.3 A simple library using student as an example

umthe repeated compiling togetheradditionalrightSource files and the ones with themLibraries are used to avoid possibly long lists of object files when linking. At the same time, libraries have the advantage that you can make your compiled functions (along with the header files) available to others in a compact form without having to reveal your programming secrets (intellectual property). This is demonstrated using the (very simple) example from §7.5.2.

• Generate the object file student.o (compile)

LINUX> g++ -c student.cc

![](Images/image01131.jpeg)Generating/updating the library libstud.a (archiving) from/with the object file student.o. The library identifier stud is freely selectable.

LINUX> ar r libstud.a student.o

TueeArchiving options (here, only r) ko¨nenwith the usedcompilers vary.

![](Images/image01132.jpeg)![](Images/image01133.jpeg)Compile the main program and link with the library from the current directory

LINUX> g++ Ex752.cc -L. -lstud

The following steps are necessary to compile and link the program without using a library.

![](Images/image01134.jpeg)g++ -c student.cc

−−−−−−−−−−−→

g++ -c Ex752.cc

student.o

![](Images/image01135.jpeg)g++ Ex752.o student.o

−−−−−−−−−−−−−−→

Ex752.cc−−−−−−−−−−→Ex752.o

awayku¨rzeni.eis also modaily:

![](Images/image01136.jpeg)Ex752.cc, student.ccg++ Ex752.cc student.cc

When using the libstud.a library, the process is as follows

![](Images/image01137.jpeg)student.ccg++ -c

student.cc

g++ -c

student.o −a−right−right−−left−b−St−and−i.e−.a→

libstud.a

![](Images/image01138.jpeg)g++ Ex752.o

![](Images/image01139.jpeg)−−−−−−−−→

Ex752.cc

−E−x−75−2−c→c

Ex752.o

-L. -lstud

wowsbeggalready existing library in turn abkurtwearthcan:

![](Images/image01140.jpeg)Ex752.cc, libstud.ag++ Ex752.cc -L. -lstud

a.out

## 7.6 The main program

Tueesyntax used so far fu¨rightthe main program

Main()

{

...

}

is always used by the compilerasint main()

{

...

return 0;

}

understood, since for functions without type specification theType int used as default willwedtthe standard ru¨cvalue 0A Ru¨cvalue 0bedeu-tes that the main program was processed without errors.

The program processing can be stopped at any time, also in functions, with the instruction exit(<int_value>); be aborted. The value <int_value> is then the return value of the program and can be used for error diagnosis.

![](Images/image01141.jpeg)

TheresThe program above breaks off when n < 0hrunGimmediately from andreturns error code 10\. The exit statement can also be used in fun()will.

As with other functions, the main program can also be called with parameters, but in

int main(int argc, char* argv[])

the parameter list (more precisely, the types of parameters) prescribed, where

• argv[0] the program name and

![](Images/image01142.jpeg)argv[1] . . . argv[argc-1] the arguments when calling the program as character stringsandbresult.

7.6. THE MAIN PROGRAM85

• Esgilt always argc≥1,i.eathe program name always ubresultwill.

![](Images/image01143.jpeg)![](Images/image01144.jpeg)

Tueefunctionn atoi(char*) (= ASCII to int) converts the ubdevoted Sign-concatenate to an integer and is declared in stdlib.h. By means of the analogfunctionn atod(char*) latet himself one float numberas parameters andbresult. After compiling and linking, the program can a.out using

LINUX> a.out

or.

LINUX> a.out 5

be started. In the formercase the value of n is read from the keyboard,imsecond case, the value 5 from the command line ubtaken andn assigned. An elegant, and real C++-Lsolution,regarding the handover

of command line parameters can be found in [Str00, pp.126].

## 7.7 Recursive Functions

![](Images/image01145.jpeg)![](Images/image01146.jpeg)functionsnknockouẗneninC/C++ can be called recursively.

![](Images/image01147.jpeg)![](Images/image01148.jpeg)Example: The power to be realized.

xkwith x ∈

, k∈

can also as

k=x·  xk−1k >01k= 0

## 7.8 eggnbigoutersExample: Bisection

![](Images/image01149.jpeg)The example on page 39 was about determining the zero of f (x) := sin(x) x/2 in the interval (a,b), with a = 0 and b = 1\. Provided that f (a) > 0 > f (b) this problem can be solved (for continuous functions) using bisection. The bisection algorithm essentially consists of the steps for each interval [a, b].

(i) c := (a + b)/2

(ii) is|f(c)| close enough to 0 ?

(iii) Inwhich interval haelevenemußi.eHsearch further ?

thesist one classicrecursion,wobeggpunkt(iii)youen / Anexterecursionn initiatesU.Ni.ePoint (ii) is intended to guarantee the cancellation of the recursion. Formally knockoutcanweatherthesput it like that¨cken:

x0 := Bisect(a, b, ε) :=

c :=(a + b)/2if |f (c)| < ε

Bisect(c, b, ε)else if f (c) > 0

Bisect(b, c, e)otherwise,casesf(c) < 0

Structogram:

![](Images/image01150.gif)

thesgives the function definition fu¨rightBisect() which with

![](Images/image01151.jpeg)x0 = Bisect(a,b,1e-6);

calledn willU.Ni.eto version 1 of the bisection program futouches

![](Images/image01152.jpeg)

To make the program a bit more flexible, we will fix the in Bisect1()

programmed function f(x) by the global function

![](Images/image01153.jpeg)

substitute. at the same timeiGknockoutcouldnwe replace the function parameter eps with a globalReplace constant EPS with bale, resulting in version 2.

![](Images/image01154.jpeg)Tueeflexibility¨atthe bisection function läßtcontinue to riseheynby entering the function f(x) to be evaluated as a variable in the parameter list ubresult.A functionnas a parameter/argument is always used as a pointer ubresult,ie,  a functionas an argument, like the declaration fu¨rightf6 built on page 76being. Specifically, this means:

double (*func)(double) is a pointer to a function func with a

double variablesalsargumentsnU.Ni.edouble as the type of the Ru¨creciprocal. This allows us the function declaration and definition of Bisect3()

![](Images/image01155.jpeg)

The fourth argument (eps) in the Bisect3() parameter list is optionalArgument which is not used when calling the functionbresultwearthgot to. In this case, the default value specified in the function declaration is automatically assigned to this optional argument. In our case, the call would be in the main program

x0 = Bisect3(f,a,b,1e-12)

youeRecursion at |f (c)| < ε := 10−12 cancel, waduring

x0 = Bisect3(f,a,b)

![](Images/image01156.jpeg)![](Images/image01157.jpeg)beautifulbegg|f(c)| < ε := 10−6 stops. We could now add another function

declare and define, and call the bisection algorithm in version 3\. with it:

![](Images/image01158.jpeg)x0 = Bisect3(g,a,b,1e-12)

Comment:Da weatherourealsargumentsnin Bisect3andbdevotedfunctionn funcis a pure INPUT parameter, we should mark it with const. However, the correct labeling of the first argument is in Bisect3

double Bisect3(double (* const func)(double), const double a, const double b, const double eps=1e-6);

a bit confusing at the beginning.

![](Images/image01159.jpeg)![](Images/image01160.jpeg)ourrightProgram works satisfactorily fu¨rightf (x) = sin(x) x/2 and yieldsfootrightthe input parameters a = 1 and b = 2 the correct solution x0 = 1.89549, the same for a = 0 and b = 2, however, the (trivial) solution x0 = 0 is not found here because a = 0 is entered would. With the inputs a = 0, b = 1 or a = 1, b = 0.1 (x0 := 0 [a, b]) the program aborts after a while with a segmentation fault, since the recursion does not abort and at some point the fu The memory (stack) reserved for function calls is no longer sufficient.

![](Images/image01161.jpeg)knockouẗnenwe secure our program in such a way that, for example, the existing zerox0  =  0  as well asin[0,  1]to thesin  [1, 0.1] is found? Which cases can occur with regard to the function values ​​f (a) and f (b) (preliminary assumption: a < b)?

(i) f (a)>0 > f(b) (ie, f(a) > 0 and f(b) < 0), e.g., a = 1, b = 2

=⇒ Standard case in Bisect3().

(ii) f(a) > 0 and f(b) > 0, e.g., a = 0.5, b = 1.5, respectively

![](Images/image01162.jpeg)f(a) < 0 and f (b) < 0, eg, a=1,  b= 0.5

![](Images/image01163.jpeg)possibly nonezero=cancel.

(Esk¨onnenThere may be zeros in the interval, which we do not find with the bisection method ko¨nen!)

![](Images/image01164.jpeg)(iii)f (a) = 0 or f (b) = 0, better |f (a)| < ε etc.

or=⇒

=aor b are the zero,

aand b are a zero.

(iv) f(a) < 0 < f(b), e.g. a = −1, b = 0.1

Swap a andb=⇒ Case (i).

(v) a =b=⇒ included in (ii) and (iii).

b < a=⇒fuMrton (i) or (iv).

![](Images/image01165.jpeg)thisecase distinction fuMrtus to the following structural diagram andversion 4.

Structogram:

![](Images/image01166.gif)

![](Images/image01167.jpeg)![](Images/image01168.jpeg)To thescroendnFinally we define further functions in the program h(x) = 3 ex, t(x) = 1 x2, ask the user which math. function fu¨rthe root search is to be used and calculate the root(s) in the given interval. This selection can easily be implemented with a switch statement and leads to version 5 of the program.

![](Images/image01169.jpeg)Comment:The three functions Bisect[1-3]() differ in their parameter lists. Therefore all three functions can be used under the name Bisect(), since their signatures differ and thus the compiler knows exactly which Bisect() function should be used.

Chapter 8

# The data type class (class)

![](Images/image01170.jpeg)![](Images/image01171.jpeg)ofrightdatayp  student2ouchs6.4 incl.̈altdynamicedata structuresnthrough whichInitialization and copying of the corresponding variables must be specially implemented each time (see also 7.5.2). A great advantage, among many others, of the class concept in C++ is that data structures with dynamic components can also be handled in the main program like simple data types. Of course, this requires some preliminary work.

![](Images/image01172.jpeg)Ae  class(class) is a data type with associatedothernmethodn  (functions) and willsimilarHcreated in a structure and can be used analogously.The methods of a class always have access to the data of this class.

![](Images/image01173.jpeg)![](Images/image01174.jpeg)Starting from the structure Student2 we derive a class Students. We save all declarations of the class in the header file studenten.hh and all definitions in studenten.cc. A modified variant with regard to the pointer initialization can be found in the studs.hh and studs.cc files.

![](Images/image01175.jpeg)

![](Images/image01176.jpeg)

93

## 8.1 Class declaration data and methods

![](Images/image01177.jpeg)Here is the declaration of the Students class with the absolutely necessary methods.

TueelistedhonorednmethodnLet's look at them in the order given.

## 8.2 The constructors

Constructors are used for the initial initialization of data in a class. In general, a class should have at least the following constructors.

• Definition of the default constructor (no arguments)

8.2. THE CONSTRUCTORS95

![](Images/image01178.jpeg)

In the construction student :: denotes the scope operator

::the acces¨rigksinceenrightMethod Students() on class Students

and is part of the signature of this method (function). The default constructor is used in the main program with students robbi;

called up automatically, so that all data from robbi is initialized with 0 or the zero pointer.

• ![](Images/image01179.jpeg)Definition of a parameter constructor

With the parameter constructor, a variable of type Students

declared, defined and initialized at the same time. Students arni("Arni","Black",812,7981579); It would also be possible:

![](Images/image01180.jpeg)

parameter constructorsnknockout¨nencontain optional parameters whoseStandard values ​​are already specified in the declaration (Page 94). Thus, a variable definition of the students type would also be about students arni("Arni","Schwarz");

goodvalid.

• Definition of the copy constructor

![](Images/image01181.jpeg)

The copy constructor allows definition in terms of another variable of the same class, as in

students mike(arni);

## 8.3 The Destroyer

![](Images/image01182.jpeg)Every  classbsitsexactlyand  adestructor,which when leaving the Guvalid-range of a variable (end of block, end of function) is called automatically. The main task of the destructor is mostly to free dynamic memory of the class.

## 8.4 The assignment operator

Constructors always access uninitialized data. To assign the data of arni to the already initialized (with default values) variable robbi, ie, robbi = arni; , an assignment operator has to be defined,

8.5\. THE PRINT OPERATOR97

wmooseessentially from the functional co¨rpseriouslycomposed of destructor and copy constructor. However, here is before uberpuovens,whether the right side of the assignment (ubdevotedvariable)nottidenticalH to thelinkinpageof assignment (this) is.

![](Images/image01183.jpeg)

Wsuppurationeari.ebe here on the keyword overloading of operators in theLiterature [SK98, §16], [Str00, $11] referenced.

## 8.5 The print operator

eggnnot absolutely necessary, but right nowadditionalrightoperator is the print operator fu¨righta class, which the data output using

cout << robbi <<endl;

ermosamen target.

![](Images/image01184.jpeg)The declaration in students.hh

allows, thanks to the friend identifier, to use the Students class to define a new method of the ostream class (declared in iostream.h). The definition is then:

![](Images/image01185.jpeg)

![](Images/image01186.jpeg)![](Images/image01187.jpeg)![](Images/image01188.jpeg)Wellrightk̈onnenwe use the example Ex643-correct.cc (or Ex752.cc) from 6.4much easier to write and extend.

The command line

LINUX> g++ Ex851.cc students.cc

generatedtheresexportaudibleeProgram.

## 8.6 data encapsulation

The data in studentshave been classified as public, meaning anyone can access this data, as with mike.pfirstname . To protect this data from unwantedaccess to schu¨tzenand possibly nachtra the data layout¨glicH

at then tokcan,capsuletmomnyouedatenso into the class that they only ubheaccess methods are available. The relatedequaleClassification is by the syllogism¨sselwortprivate specified. So that achanget himselfthe declarationpart of the class students in

![](Images/image01189.jpeg)//students2.hh #include <iostream.h>

class students

{

// Data in students are private now!! private:

long int register; int skz;

char *pname, *pfirstname;

//Methods in students public:

//constructors, Destructor, Access operator

...

// Output operator

friend ostream & operator<<(ostream & s, const students & orig);

// methods to access the private data

//Methods for data manipulation in students void SetFirstName(const char firstname[]);

void SetName(const char name[]);

void SetMatrikel(const longinternalmat_nr); void SetSKZ(constintskz_nr);

//Methods that don't manipulate data in students const long int& GetMatrikel() const;

const int& GetSKZ() const; const char* GetFirstName() const; const char* GetName() const;

![](Images/image01190.jpeg)![](Images/image01191.jpeg)};

There are two const declarations in the above methods. A const at the end of the declaration line indicates that the data in Student will not be modified by the corresponding method, eg, GetSKZ. The const at the beginning of the line belongs to the result type and indicates that the data referred to with the reference int& must not be changed. This ensures that the data cannot be manipulated unintentionally using pointers or references.

The access methods are defined as follows:

![](Images/image01192.jpeg)![](Images/image01193.jpeg)

![](Images/image01194.jpeg)![](Images/image01195.jpeg)thisenew access methods könen  howfollowtto be used:

Some access functions, eg SetSKZ and GetSKZ, are so short that a function call is actually not worthwhile because of the effort involved in passing the parameters. In this case, the declaration and definition of a method are linked in the header file, and the method/function is defined inline. These inline lines replace the function call each time.

![](Images/image01196.jpeg)![](Images/image01197.jpeg)

Chapter 9

# File input and output

The objects cin and cout used for I/O are (in iostream.h)predefined variables of class type stream. In order to read from or write to files, new stream variables are now created, namely of the type ifstream for the input and of the type ofstream for the output. The file name is transferred when the variable is created (C++ constructor).

103

![](Images/image01198.jpeg)

## 9.1 Copy files

![](Images/image01199.jpeg)![](Images/image01200.jpeg)The following program copies an input file to an output file, but without spaces, tabs, line breaks.

On the other hand, if you want to copy the file identically, you have to read in and out character by character. The get and put methods from the corresponding stream classes are used for this.

![](Images/image01201.jpeg)

9.2\. DATA INPUT AND OUTPUT VIA FILE105

## 9.2 Data input and output via file

![](Images/image01202.jpeg)![](Images/image00844.jpeg)![](Images/image01203.jpeg)Data input and output via file and terminal can be used in combination.

## 9.3 Switching input/output

![](Images/image00844.jpeg)![](Images/image01204.jpeg)sometimeslis a problemabhabusysSwitching between file IO and terminal IO wu¨desswheor nnecessary.Unfortunately, in this case you have tolike to work on the types istream and ostream.

![](Images/image01205.gif)

![](Images/image01206.jpeg)

![](Images/image01207.jpeg)![](Images/image00844.jpeg)![](Images/image00844.jpeg)![](Images/image01208.jpeg)Aevery comfortable Monequalsinceof switching the input/output usingCommand line parameters can be found in the examples.

# output formatting

Tueeoutputeandbhestreamings(<<)cannvmostformattwearth.  Ae smallA selection of formatting is given here, more on this in the literature.

![](Images/image01209.jpeg)We use thosevariablesdouble da = 1.0/3.0, db = 21./2,

dc = 1234.56789;

![](Images/image01210.jpeg)Standard output:

cout << da << endl << db << endl << dc << endl << endl;

![](Images/image01211.jpeg)mehrightgoodvalideDigits (here 12) in the output:

cout.precision(12); c out << ...

![](Images/image01212.jpeg)Fixed number (here 6) of decimal places: cout.precision(6); cout.setf(ios::fixed, ios::floatfield); c out << ...

![](Images/image01213.jpeg)Output with exponent: cout.setf(ios::scientific, ios::floatfield); c out << ...

![](Images/image01214.jpeg)Ru¨ckputouchfstandard editionand:cout.setf(0, ios::floatfield); c out << ...

![](Images/image01215.jpeg)alignmentG(right-hand¨end)U.N.i.eWildcard (16 characters):cout.setf(ios::right, ios::adjustfield); cout.width(16);

cout << da << endl; cout.width(16); cout << db << endl; cout.width(16); cout << dc << endl;

107

108CHAPTER 10\. OUTPUT FORMATTING

Aegeneral Lo¨sunGusing standard manipulators is in [Str00,

§ 1.4.6.2, pp.679].

![](Images/image01216.jpeg)Hexadecimal output of integers: cout.setf(ios::hex, ios::basefield); cout << "127 = " << 127 << endl;

# tips and tricks

## 11.1Praprocessor commands

Wirightalready know the Praprocessor appice

#include <math.h>

![](Images/image01217.jpeg)![](Images/image01218.jpeg)which inserts the content of the file math.h at the appropriate place in the source file before the actual compilation. Similarly, certain parts of the source code can be included or ignored when compiling, depending on the dependency of the test (analogous to an alternative as in 4.3) which is carried out with a preprocessor variable.

variablenensPreprocessorswearthby means of

#define MY_DEBUG

definetand we k¨onnenalsoHtesting,whether they are defined:

#ifdef MY_DEBUG

cout << "In debug mode" << endl; #endif

Analog can with

#ifndef MY_DEBUG#define MY_DEBUG #endif

![](Images/image01219.jpeg)zunächsttestedtwearth,whether the variable MY_DEBUG has already been defined. If not, then it is defined now. This technique will haufigurebusedaroundto prevent the declarations of a header file from being included more than once in the same source text.

![](Images/image01220.jpeg)

109

OnerightPreprocessor variablencannalsoH onebe assigned value

#define SEE_PI 5

wmoosethen in Praprocessor tests(orrightin the program as a constant)can be used:

#if (SEE_PI==5)

cout << " PI = " << M_PI << endl; #else

// empty or statements #endif

AeHouchfrightenedapplendingbexistsinenright allocation oneWfirst to onePrePer-processor variable if not already defined

#ifndef M_PI

#define M_PI 3.14159 #endif

Deswfesterknockout¨nenmacrosdefined with parameters

MAX(x,y) (x>y ? x #define : y)

and used in the source code.

cout << MAX(1.456 , a) << endl;

mehrightandbhePraprocessorcommandistetc.  in[God98th]U.Ni.e[Str00,$A.11] toFind.

## 11.2 timing in the program

![](Images/image01221.jpeg)To theperimeterGbeforen  C++giveHHoursn  somefunctions,wmoose  it  allowyoue  runningto determine the time of certain program sections (or the entire code). The corresponding declarations are provided in the header file time.h.

![](Images/image01222.jpeg)

11.3. PROFILING111

Esknockout¨nenany number of time measurements can be made in the program (at some pointbut these in turn slow down the program!). Each of these time measurements needs a start and an end, but the times of different measurements can be accumulated (by simply adding them up).

![](Images/image01223.jpeg)In the Ex1121.cc file, the function value of a polynomial of degree 20 at the

![](Images/image01224.jpeg)positione  x  ie,  s  =  Σ20 a.k  ·xk,bcalculated.Tuee21Coefficients ak and the value x

are provided in the file input.1121. The function value is calculated in two mathematically identical ways in the program. Variant 1 uses the pow function, while variant 2 calculates the value of xk by continuous multiplication.

The different runtime behavior (cause !?) can now be proven by time measurement and improved by progressively activating compiler options for program optimization, e.g

LINUX>g++ Ex1121.ccLINUX>g++ -O Ex1121.ccLINUX>g++ -O3 Ex1121.cc                                         

LINUX>g++ -O3 -ffast-math Ex1121.ccThe program is started by usingLINUX>a.out < input.1121             

## 11.3 profiling

of courselicHkcouldeone in a program the time measurement in each functionwrite to determine the runtime behavior of the functions and methods. However, this is not necessary since many development environments already provide tools for performance analysis, ie profiling. At a minimum, the time spent in the functions and the number of function calls are output (often graphically). Sometimes this can be resolved down to single lines of source code. In addition to the professional (and fee-based) profiling and debugging tools, simple (and free) commands for this are also available under LINUX/UNIX.

LINUX>g++ -pg Jacobi.cc matvec.ccLINUX>a.out

LINUX>gprof -b a.out > outLINUX>less out

The compiler switch -pg accommodates some additional functions in the program so that the runtime behavior can be analyzed by gprof after the program run. The last command (can also be an editor) displays the redirected output of this analysis on the screen.

## 11.4 debugging

It is often necessary to follow the program flow step by step and, if necessary, to have variable values ​​etc. output for control purposes. Next

enrightalways working, but annoyingend,method

...

cout << "AA" << variable << endl;

...

cout << "BB" << variable << endl;

...

areOften professional debugging tools are availableavailable.  Here is one again(free) program under LINUX presented.

LINUX> g++ -g Ex1121.cc

LINUX> ddd a.out &

The handling of the various debuggers differs greatly. With the ddd debugger, the input file can be specified with set args < input.1121 and the test run is started with run, which is stopped at previously set break points. There, the program can be followed step by step using the source code.

# bibliography

[Cap01] Derek Capper. Introducing C++ for Scientists, Engineers and Mathematicians. Springer, 2001.

[CF88]MatthewsClauss and Gu¨ntherightfisherman. Programming with C. VerlagTechnique, 1988.

[Cor93]microsoft corp Get in the right wayin C++. Microsoft Press, 1993\. [Dav00]  Stephen R Davis. C++ furightdummies.  boarding school Thomson Publ.,

Bonn/Albany/Attenkirchen, 2nd edition, 2000.

[Erl99]HelmutErlenkotter.  CprogramnbeforenAbeginningan.  Rowohlt,1999[God98] Edward Gode. ANSI C++: short & good. O'Reilly, 1998.

[Her00]dietrightHerrmann. C++ fu¨rightnaturalist.  Addison-Wesley,Bonn, 4th edition, 2000.

[Her01]Dietmar Herrmann. Effective programming in C and C++. vieweg,

5th edition, 2001.

[HT03]Andrew Huntand David Thomas. The Pragmatic Programmer.

Hanser textbook, 2003.

[Jos94]Nicolai Josuttis. Object-oriented programming in C++: from the class to the class library. Addison-Wesley, Bonn/Paris/Reading,

3.  edition, 1994.

[KPP02] Ulla Kirch-Prinz and Peter Prinz. Everything about object-oriented programming. Galileo Press, 2002.

[KPP03]Ulla Kirch-Prinz and Peter Prinz. C++ furightC programmer.  GalileoPress, Oct. 2003.

[Mey97] Scott Meyers. Programming C++ more effectively. Addison-Wesley, 1997.

[Mey98] Scott Meyers. Programming effectively in C++. Addison-Wesley, 3rd, updated edition, 1998.

[OT93] Andrew Oram and SteveTalbott. Managing projects with make.

O'Reilly, 1993.

113

114BIBLIOGRAPHY

[SB95] Gregory Satir and Doug Brown. C++: The Core Language. O'Reilly, 1995.

[SK98] Martin Schader and Stefan Kuhlins.  Programming in C++. RowohltVieweg, 5th revised edition, 1998.

[Str00]Bjarne Stroustrup. The C++ programming language. Addison-Wesley,

4.  updated edition, 2000.

[Str03]Thomas Strasser. Programming with style. A systematic introduction.  dpunkt, 2003.

# index

#define, 109

#if, 110

#ifdef, 109

#ifndef, 109

#include, 109

abort test, 41

rejecting cycle, 38

abort test, 38

alternative, 27

Instruction, 3, 4, 25

argc, 84

argv[], 84

array, see field assembler, 5

atod(), 85

atoi(), 85

onzaestyp,45, 57

Expression, 13 edition

cost, 103

Files, 103

formatting, 107

new line, 9

char, 7

class, 93-101

data encapsulation, 99

declaration, 94 method

seeMethod, 93

compile, 20

conditional, 109

g++,4-6, 83, 111, 112

gcc, 3

debugging, 112

delete, 62

do-while loop, see non-rejecting cycle

double, 7

Notepad, 3 input

cin, 103

Files, 103

Decision operator, 29 enum, see enumeration type

|  | false, 15, 17, 57 |
| Library, 5, 6, 20, 80, 83 |  | field, 45 |
| update, 83 |  | declaration, 46 |
| generate, 83 |  | Dimensions, 46 |
| left, 83 |  | dynamic, 62–66, 78 |
| binalogarithm,38 |  | allocate, 62 |
| Bisection, 40 |  | deallocate,64 |
| (, 86 |  | one-dimensional, 45, 62 |
| ), 91 |  | field elements, 46 |
| bit, 17 |  | initialization, 46 |
| blocks, 3, 4, 25 |  | multidimensional, 51, 63 |
| beginning, 25 |  | Numbering, 46 |
| end, 25 |  | static, 45–52, 77 |
| Location ̈t,26 |  | Dimensions, 46 |
| boolean, 7, 57 |  | String, 47 |
| break, 43 |  | Fibonacci, 49 |
| bytes, 17 | 115 | find |
|  |  |  |

116INDEX

Unix command 23

float, 7

float.h, 23, 37, 51

![](Images/image00844.jpeg)FLT DIG, 23

![](Images/image00844.jpeg)FLT EPSILON, 23, 37

![](Images/image00844.jpeg)FLT MAX, 23, 51

![](Images/image00844.jpeg)FLT MIN, 23

for loop, please refer Zaoil cycleFunction, 71–91

Define, 71

Declaration, 71, 80

functional co¨rphe,71

in-line, 101

parameters, see parameter return value,see function

on result recursively, see recursion signature, 71–73

function result,74

void, 74

Floating point number, 9, 14, 15

u¨ brun,37

Accuracy, 36, 41

running variable, 35

Header file, 3-6, 80, 101

in-line, 101

Heaviside, 28

if-then-else, see alternative inline, 101

int, 7

comment

C, 3, 4

C++, 4

Constant, 9–11

characters, 9

floating point number, 9

global, 88

integer, 9

mathematical, 20

thong, 9

symbolic, 10

running variable, 34

floating point number, 35

limits.h, 23

![](Images/image00844.jpeg)INT MAX, 23

![](Images/image00844.jpeg)INT MIN, 23

Left, 5, 20, 83

macro, 10

main(), 3, 4, 84

math.h, 20

acos(), 20

salted(), 20

atan(), 20

cell(), 20, 37

body(), 20

exp(), 20

fabs(), 20

floor(), 20

fmod(), 20

log(), 20

![](Images/image00844.jpeg)ME, 20

![](Images/image00844.jpeg)MPI, 20

pow(), 20

sin(), 20

sqrt(), 20

tan(), 20

Matrix, 52, 63, 64, 77, 78

Multiple choice, 42

method, 93

copy constructor, 95

Define, 101

declaration, 101

destructor, 96

in-line, 101

parameter constructor, 95

print operator, 97

Default constructor, 94

assignment operator, 97methods

access methods, 100

new, 62

non-shedding cycle, 38

abort test, 38

zeros, 39

object code, 5

object file, 6

operands, 13

operator, 13

arithmetic,14

bit-oriented, 17

more logical, 17

comparison operator, 15parameter

INDEX117

by address, 75

by reference, 75

by value, 75

const, 75

Field, 76

function, 88

main(), 84

Matrix, 77, 78

optional argument, 89

Vector, 76 pointers, see pointers

Preprocessor,5,10,109

Profiling, 111 program

exportear,3, 4

Source file, 6, 80

compile, 3, 4, 83

edit, 3, 4 source text, see source file

reference, 68

recursion, 86

abort test, 86

function, 86

Segmentation fault, 90

Signum, 29, 72

sizeof(),8 memory

allocate, 62

deallocate,64

Segmentation fault, 90

string.h, 21

strcat(), 21

strchr(), 21

strcmp(), 21

strcpy(), 21

strlen(), 21 struct, see Structure Structure, 45, 52-55

in structures, 54

Pointer up, 67

Pointer in, 65

college student, 82

library, 83

Class, 94

structure, 53

Student2, 65, 82

suffix, 6

switch

Multiple choice, 42

time.h

clock(), 110

![](Images/image00844.jpeg)![](Images/image00844.jpeg)CLOCKS PER SEC, 110

true, 15, 17, 57

union, 45, 56

using namespace, 6

variable, 7–8

storage class, 7

type, 7

Vector, 45, 76

Branches, see alternative void, 74

truth table, 18

while loop,please refermore dismissivecycle

Zaoil cycle,33

abort test, 35

hands, 59–69

address operator, 60

Arithmetic, 61

on structure, 67

declaration, 59

Dereference operator, 60

in structure, 65

Null pointer, 60

reference operator, 60

undefined, 60

access operator, 60

assignment operator,16