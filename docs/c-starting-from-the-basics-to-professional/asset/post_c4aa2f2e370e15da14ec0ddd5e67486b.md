
The compiler will object to this string literal because the raw literal appears to be terminated somewhere halfway already, right after `(a - b`. But if escaping is not an option—any backslash characters would simply be copied into the raw literal as is—how else can you make it clear to the compiler that the string literal should include this first `)` sequence, as well as the next one after `(b - a`? The answer is that the delimiters that mark the start and end of a raw string literal are flexible. You can use any delimiter of the form `"char_sequence(` to mark the beginning of the literal, as long as you mark the end with a matching sequence `)char_sequence"`. Here's an example:

```
R"*(The answer is "(a - b)" not "(b - a)")*"
```

This is now a valid raw string literal. You can basically choose any `char_sequence` you want, as long as you use the same sequence at both ends:

```
R"=Fa-la-la-la-la(The answer is "(a - b)" not "(b - a)")=Fa-la-la-la-la="
```

The only limitations are that `char_sequence` must not be longer than 16 characters and may not contain any parentheses, spaces, control characters, or backslash characters.

## Summary

In this chapter, you learned how you can use the string type that's defined in the Standard Library. The string type is much easier and safer to use than C-style strings, so it should be your first choice when you need to process character strings.

The following are the important points from this chapter:

- The `std::string` type stores a character string.
- Like `std::vector<char>`, it is a dynamic array—meaning it will allocate more memory when necessary.
- Internally, the terminating null character is still present in the array managed by a `std::string` object, but only for compatibility with legacy and/or C functions. As a user of `std::string`, you normally do not need to know that it even exists. All string functionality transparently deals with this legacy character for you.
- You can store string objects in an array or, better still, in a sequence container such as a `vector`.
- You can access and modify individual characters in a string object using an index between square brackets. Index values for characters in a string object start at 0.
- You can use the `+` operator to concatenate a string object with a string literal, a character, or another string object.
- If you want to concatenate a value of one of the fundamental numeric types, such as for instance an int or a double, you must first convert the numeric value into a string. Your easiest—though least flexible—option for this is the `std::to_string()` function template defined in the `<string>` module.
- Objects of type string have functions to search, modify, and extract substrings.
- The `<string>` module offers functions such as `std::stoi()` and `std::stod()` to convert strings to values of numeric types such as int and double.
- Objects of type `wstring` contain strings of characters of type `wchar_t`.
- Objects of type `uNstring` contain strings of characters of type `charN_t`, for an `N` equal to 8, 16, or 32.

## Exercises

The following exercises enable you to try what you've learned in this chapter. If you get stuck, look back over the chapter for help. If you're still stuck after that, you can download the solutions from the Apress website (www.apress.com/source-code), but that really should be a last resort.

- **Exercise 7-1.** Write a program that reads and stores the first names of any number of students, along with their grades. Calculate and output the average grade and output the names and grades of all the students in a table with the name and grade for three students on each line.
- **Exercise 7-2.** Write a program that reads text entered over an arbitrary number of lines. Find and record each unique word that appears in the text and record the number of occurrences of each word. Output the words and their occurrence counts. Words and counts should align in columns. The words should align to the left; the counts to the right. There should be three words per row in your table.
- **Exercise 7-3.** Write a program that reads a text string of arbitrary length from the keyboard and prompts for entry of a word that is to be found in the string. The program should find and replace all occurrences of this word, regardless of case, by as many asterisks as there are characters in the word. It should then output the new string. Only whole words are to be replaced. For example, if the string is “Our house is at your disposal.” and the word that is to be found is “our”, then the resultant string should be as follows: "**** house is at your disposal." and not "**** house is at y*** disposal.".
- **Exercise 7-4.** Write a program that prompts for the input of two words and determines whether one is an anagram of the other. An anagram of a word is formed by rearranging its letters, using each of the original letters precisely once. For instance, listen and silent are anagrams of one another, but listens and silent are not.
- **Exercise 7-5.** Generalize the program of Exercise 7-4 such that it ignores spaces when deciding whether two strings are anagrams. With this generalized definition, funeral and real fun are considered anagrams, as are eleven plus two and twelve plus one, and desperation and a rope ends it.
- **Exercise 7-6.** Write a program that reads a text string of arbitrary length from the keyboard followed by a string containing one or more letters. Output a list of all the whole words in the text that begin with any of the letters, uppercase or lowercase.
- **Exercise 7-7.** Create a program that reads an arbitrarily long sequence of integer numbers typed by the user into a single string object. The numbers of this sequence are to be separated by spaces and terminated by a # character. The user may or may not press Enter between two consecutive numbers. Next, extract all numbers from the string one by one.
- **Exercise 7-8.** A tautogram is a body of text in which all words start with the same letter. In English, an example would be “Truly automatic trim triumphant, trumpeting thrills to trounce terrible travesties.” Ask the user for a string, and verify whether it is a tautogram (ignoring casing). If it is, output also the letter by which each word starts.

  Note: True tautograms are truly tough to throw together, so perhaps you can bend the rules a bit? Maybe allow words to start with a few different letters, such as “a,” “to,” “is,” “are,” etc., or only require a certain percentage of words to begin with the same letter? Have some fun with it!
- **Exercise 7-9.** Extend your solution to Exercise 7-8 to remove all occurrences of the tautogram’s beginning letter (ignoring casing). You could do it the easy way (remember the Standard Library function you can use to accomplish this?), but perhaps it's more interesting to do it the hard way and write the complete code yourself?

## CHAPTER 8

## Defining Functions

Segmenting a program into manageable chunks of code is fundamental to programming in every language. A function is a basic building block in C++ programs. So far, every example has had one function, `main()`, and has typically used functions from the Standard Library. This chapter is all about defining your own functions with names that you choose.

In this chapter, you will learn

- What a function is and why you should segment your programs into functions
- How to declare and define functions
- How data is passed to a function and how a function can return a value
- What the difference is between “pass-by-value” and “pass-by-reference” and how to choose between both mechanisms
- What the best way is to pass strings to a function
- How to specify default values for function parameters
- What the preferred way is to return a function’s output in modern C++
- How using `const` as a qualifier for a parameter type affects the operation of a function
- The effect of defining a variable as `static` within a function
- How to create multiple functions that have the same name but different parameters—a mechanism you’ll come to know as function overloading
- What recursion is and how to apply it to implement elegant algorithms

### Segmenting Your Programs

All the programs you have written so far have consisted of just one function, `main()`. A real-world C++ application consists of many functions, each of which provides a distinct well-defined capability. Execution starts in `main()`, which must be defined in the global namespace. `main()` calls other functions, each of which may call other functions, and so on. The functions other than `main()` can be defined in a namespace that you create.

When one function calls another that calls another that calls another, you have a situation where several functions are in action concurrently. Each that has called another that has not yet returned will be waiting for the function that was called to end. Obviously something must keep track of from where in memory each function call was made and where execution should continue when a function returns. This information
