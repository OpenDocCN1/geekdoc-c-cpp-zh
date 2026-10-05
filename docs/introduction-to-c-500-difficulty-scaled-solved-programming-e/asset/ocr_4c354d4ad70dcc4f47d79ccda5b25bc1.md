U.12.7 Write a program that reads the names of ten students (less than 100 characters each), stores them in a two-dimensional array, and uses the bubble sort algorithm to sort the array in alphabetical order. The program should display the array, before it ends.

U.12.8 Write a program that reads the names of ten courses (store them in a vector object) and the grades of 50 students on these courses. The program should display the names of the courses and the average grade next to them, starting with the course with the best average. In case of same average, the program should display the "tied" courses in alphabetical order. To sort the array, the bubble sort algorithm. Re-visit C.12.6 to see how to use the vector object.

U.12.9 In a music contest, 200 judges vote for the top songs of 50 songs. Write a program that reads the names of the songs (store them in a vector object) and displays the top five songs. If there is a tie in the fifth place, the program should display the "tied" songs. Vote for a song, the judge enters its entry. Each judge can vote up to five songs or less and enter the word end as a title. Assume that the judge does not vote for the same more than once. To sort the array, use the selection sort algorithm.

U.12.10 Write a program that reads the price and the book titles (less than 100 characters each) of two bookstores. Assume that the maximum number of books in each bookstore is 200. If the user enters end the insertion of books should terminate. The program should display the book titles and prices of both bookstores sorted by price descending order. There is one restriction: If a title is found in both bookstores, the program should display that title once with the price in the first bookstore.

U.12.11 Write a program that reads the names of 1000 candidates, their score, and the name of the school they accepted. The program uses vector objects to store the names of the candidates and the schools. The program should read a candidate's name and display the school, as well as the score and the names of all candidates accepted in that same school sorted by descending order. For example the user enters

```
P.Smith     2300 CIT
A.Leep      1200 LU
R.Bachir    1600 LU
B.Koong     2800 BPL
```

and then the user enters A.Leep, the program should display LU and:

```
R.Bachir    1600 LU
A.Leep      1200 LU
```

U.12.12 Suppose that 20 firms participate in a contest. Each firm rates the other firms with a grade in [1, 20]. Write a program that reads their names (less than 100 characters) and the grades each firm gives to the others. The program should check that each given grade is in [1, 20] and that it is not already given. Then, the program should calculate the total score for each firm and display the rank list in score descending order.