+   - 12.12.2 Using const to Protect an Array from a Function 397
+   - 12.12.3 Returning a Pointer to an Array 397
+   - 12.13 Array of Pointers 398
+   - 12.14 sort_selection2.c: Sorted View of Array Using Array of Pointers 398
+   - 12.15 Pointer to a Pointer 399
+   - 12.16 Pointers and Two-Dimensional Arrays 402
+   - 12.17 The Generic or Void Pointer 404
+   - 12.18 Using the const Qualifier with Pointers 406

# # CHAPTER 13 Strings 412

+   - 13.1 String Basics 412
+   - 13.2 Declaring and Initializing a String 413
+     - 13.2.1 Using an Array to Declare a String 413
+     - 13.2.2 When an Array Is Declared But Not Initialized 413
+     - 13.2.3 Using a Pointer to Declare a String 414
+     - 13.2.4 When an Array of Characters Is Not a String 415
+   - 13.3 intro2strings.c: Declaring and Initializing Strings 415
+   - 13.4 Handling Lines as Strings 417
+     - 13.4.1 Using gets/puts: The Unsafe Way 417
+     - 13.4.2 gets_puts.c: A Program Using gets and puts 417
+     - 13.4.3 Using fgets/fputs: The Safe Way 418
+     - 13.4.4 fgets_fputs.c: A Program Using fgets and fputs 419
+   - 13.5 The sscanf and sprintf Functions 420
+     - 13.5.1 sscanf: Formatted Input from a String 420
+     - 13.5.2 sprintf: Formatted Output to a String 421
+     - 13.5.3 validate_pan.c: Using sscanf and sprintf to Validate Data 421
+   - 13.6 Using Pointers for String Manipulation 422
+   - 13.7 Common String-Handling Programs 423
+     - 13.7.1 string_palindrome.c: Program to Check a Palindrome 423
+     - 13.7.2 count_words.c: Counting Number of Words in a String 424
+     - 13.7.3 sort_characters.c: Sorting Characters in a String 425
+   - 13.8 Developing String-Handling Functions 426
+     - 13.8.1 my_strlen: Function to Evaluate Length of a String 426
+     - 13.8.2 reverse_string: Function to Reverse a String 427
+     - 13.8.3 my_strcpy: Function to Copy a String 427
+     - 13.8.4 my_strcat: Function to Concatenate Two Strings 427
+     - 13.8.5 string_manipulation.c: Invoking All Four Functions from main 428
+     - 13.8.6 substr.c: Program Using a Function to Extract a Substring 429
+   - 13.9 Standard String-Handling Functions 430
+     - 13.9.1 The strlen Function 430
+     - 13.9.2 The strcpy Function 430
+     - 13.9.3 The strcat Function 431
+     - 13.9.4 The strcmp Function 431