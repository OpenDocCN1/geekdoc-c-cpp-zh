# Why Python?

environment or users. Operating systems, such as Windows, macOS and such are usually a combination of C++, C#, assembly and some form of visual-based language. Games generally use C++ whilst web pages can use a plethora of available languages such as HTML, Java, Python and so on.

More general-purpose programming is used to create programs, apps, software or whatever else you want to call them. They’re widely used across all hardware platforms and suit virtually every conceivable application. Some operate faster than others and some are easier to learn and use than others. Python is one such general-purpose language.

Python is what’s known as a High-Level Language, in that it ‘talks’ to the hardware and operating system using a variety of arrays, variables, objects, arithmetic, subroutines, loops and countless more interactions. Whilst it’s not as streamlined as a Low-Level Language, which can deal directly with memory addresses, call stacks and registers, its benefit is that it’s universally accessible and easy to learn.

```
//file: Invoke.java
import java.lang.reflect.*;

class Invoke {
public static void main( String [] args ) {
try {
Class c = Class.forName( args[0] );
Method m = c.getMethod( args[1], new class
[] { } );
Object ret = m.invoke( null, null );
System.out.println(
"Invoked static method: " + args[1]
+ " of class: " + args[0]
+ " with no args\nResults: " + ret );
} catch ( ClassNotFoundException e ) {
// Class.forName() can’t find the class
} catch ( NoSuchMethodException e2 ) {
// that method doesn’t exist
} catch ( IllegalAccessException e3 ) {
// we don’t have permission to invoke that method
} catch ( InvocationTargetException e4 ) {
// an exception occured while invoking that method
System.out.println(
"Method threw an: " + e4.
getTargetException( ) );
}
}
}
```

Java is a powerful language that's used in web pages, set-top boxes, TVs and even cars.

![](bbox=[0.12, 0.62, 0.5, 0.89])

Python was created over twenty six years ago and has evolved to become an ideal beginner’s language for learning how to program a computer. It’s perfect for the hobbyist, enthusiast, student, teacher and those who simply need to create their own unique interaction between either themselves or a piece of external hardware and the computer itself.

Python is free to download, install and use and is available for Linux, Windows, macOS, MS-DOS, OS/2, BeOS, IBM i-series machines, and even RISC OS. It has been voted one of the top five programming languages in the world and is continually evolving ahead of the hardware and Internet development curve.

So to answer the question: why python? Simply put, it’s free, easy to learn, exceptionally powerful, universally accepted, effective and a superb learning and educational tool.

```
40 LET PY=15
70 FOR W=1 TO 10
71 CLS
75 LET BY=INT (RND*28)
80 LET BX=0
90 FOR D=1 TO 20
100 PRINT AT PX,PY;" U "
110 PRINT AT BX,BY;"O"
120 IF INKEY$="P" THEN LET PY=P
Y+1
130 IF INKEY$="O" THEN LET PY=P
Y-1
135 FOR N=1 TO 100: NEXT N
140 IF PY<2 THEN LET PY=2
150 IF PY>27 THEN LET PY=27
180 LET BX=BX+1
185 PRINT AT BX-1,BY;" "
190 NEXT D
200 IF (BY-1)=PY THEN LET S=S+1
210 PRINT AT 10,10;"score=";S
220 FOR V=1 TO 1000: NEXT V
300 NEXT W
0 OK, 0:1
```

BASIC was once the starter language that early 8-bit home computer users learned.

```
print(HANGMAN[0])
attempts = len(HANGMAN) - 1

while (attempts >= 0 and "-" in word_guessed):
print("You have {} attempts remaining".format(attempts))
joined_word = "-".join(word_guessed)
print(joined_word)

try:
player_guess = str(input("Please select a letter between A-Z" + "\n ")).
except: # check valid input
print("That is not valid input. Please try again.")
continue
else:
if not player_guess.isalpha(): # check the input is a letter. Also checks a
print("That is not a letter. Please try again.")
continue
elif len(player_guess) > 1: # check the input is only one letter
print("That is more than one letter. Please try again.")
continue
elif player_guess in guessed_letters: # check it letter hasn't been guessed
print("You have already guessed that letter. Please try again.")
continue
else:
pass

guessed_letters.append(player_guess)

for letter in range(len(chosen_word)):
if player_guess == chosen_word[letter]:
word_guessed[letter] = player_guess # replace all letters in the chosen

if player_guess not in chosen_word:
```

Python is a more modern take on BASIC, it's easy to learn and makes for an ideal beginner's programming language.