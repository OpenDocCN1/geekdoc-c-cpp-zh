lambda operator, o False. When specifying a lambda parameter's type and/or when a lambda
more than one parameter, you must enclose the parameter list in parentheses. (p) True.

# # Exercises

# ## 21.3 (Collections Terminology) Describe each of the following:

+   - a) ICollection
- b) Array
- c) IList
- d) load factor
- e) hash-table collision
- f) space/time trade-off in hashing
- g) dictionary

# ## 21.4 (Enumerator Members) Explain briefly the operation of each of the following enumerator-related methods:

+   - a) GetEnumerator
- b) Current
- c) MoveNext

# ## 21.5 (IDictionary<K,V> Methods and Properties) Explain briefly the operation of each of the fol-lowing methods and properties of interface IDictionary<K,V>, which both Dictionary and Sort-edDictionary implement:

+   - a) Add
- b) Keys
- c) Values
- d) ContainsKey

# ## 21.6 (LinkedList without Duplicates) Write an app that reads a series of first names and stores them in a LinkedList. Do not store duplicate names. Allow the user to search for a first name.

# ## 21.7 (Summarizing Counts with SortedDictionary) Modify the app in 21.4 to count the number of occurrences of each name rather than each word. For example, the example "HELLO THERE" contains two Hs, three Es, two Ls, one O, one T and one R. Display the results.

(Dictionary of Colors) Use SortedDictionary to create a reusable class for choosing from the predefined colors in class Color (in the System.Drawing namespace). The names of the colors should be used as keys, and the Color objects should be used as values. Place this class in a class library that can be referenced from any C#. Use your new class in a Windows app that allows the user to select a color, then change the background color of the Form.

(Duplicate Words in a Sentence) Write an app that determines and displays the number of duplicate words in a sentence. Treat uppercase and lowercase the letters as same. Ignore punctuation.

(Using a List) Write an app that inserts 25 random integers from 0 to 100 into an order of class List. The app should calculate the sum of the elements and the floating-point average of the elements. Use loops to help perform calculations.

(Reversing a LinkedList) Write an app that creates a LinkedList object of 10 characters, creates a second list containing a copy of the file, but in reverse order. Do not call LinkedList method Reverse.

(Prime Numbers and Prime Factorization) Write an app that takes a whole-number from a user and determines whether it's prime. If the number is not prime, display the unique prime factors of the number (using a List<int> to store the factors). Remember that a prime number's factors are only 1 and the prime itself. Every number that's not prime has a unique prime factorization. For example, consider the number 54. The prime factors of 54 are 2, 3, 3 and 3. When