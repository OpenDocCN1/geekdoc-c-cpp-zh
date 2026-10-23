```
scala> doThreeTimes(y=>y+1,1)
scala> doThreeTimes(y=>y+2,1)
scala> doThreeTimes(a=>a-5,100)
scala> doThreeTimes(_+1,1)
scala> doThreeTimes(_*2,1)
scala> def incChar(c:Char,offset:Int) = (c+offset).toChar
scala> incChar('a',1)
scala> incChar('a',2)
scala> incChar('z',-3)
scala> def tnp1(n:Int):(Int,Int) = {
  val odd = n%2
  (n/2*(1-odd),(3*n-1)*odd)
}
scala> odd
scala> var name = ""
scala> def introduction {
  println("What is your name?")
  name = readLine()
  println("Hello "+name)
}
scala> name
```

# 5.9.4 Exercises

1. What would be the types of the parameters and result of functions that do the following tasks. (Note that you are not supposed to write the functions, just say what their types are.)

+   - Tell you how many words are in a person’s name.
+   - Take a person’s name as normally written and give it back in “last, first” format.
+   - Take three words and return the TLA (Three Letter Acronym) for them.
+   - Take ten points in 2-space (x-y coordinates) and return how many are in the unit circle.
+   - Take a number and tell how many distinct prime factors it has.
+   - Take a number and tell has many positive factors it has.
+   - Take a value in Fahrenheit and give back the equivalent in Celsius.
+   - Take a value in Fahrenheit and give back the equivalent in Celsius and Kelvin.

2. Write functions that return a Boolean for the different parts of exercise 1 (p.85).

3. Write a function that takes a String parameter and returns a Boolean telling if the argument is a palindrome.

4. Write a function for the solution to exercise 5 (p.86).

5. Write a function for the solution to exercise 6 (p.86).

6. Write a function for the solution to exercise 7 (p.86).

7. Write a function for the solution to exercise 8 (p.86).