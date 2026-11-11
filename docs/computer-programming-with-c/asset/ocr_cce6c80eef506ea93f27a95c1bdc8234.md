Once the value of variable n is known, we can then take only the required number of Book objects as input from the user and store them in first n-locations of the array, whereas the remaining part of the array can still continue to hold junk values. For example, if user inputs the value of variable n as 5, this means that the user wishes to store data about 5 books in the computer memory. Hence, we will now start taking the details of 5 books as input from the user, such that the details of the first Book object entered by the user are stored in b[0] (first location of the array), the details of the second Book object entered by the user are stored in b[1] and so on. Hence, the last Book object will be stored in b[4]. The remaining part of the array, which is the elements from position 5 to position 99 will still continue to hold junk values.

The id, title, author, and price of the n book objects to be stored as the first n-elements of the array can be taken as input from the user by using the following for loop:

```
```c
for(i=0;i<=n-1;i++)
{
    scanf("%d%s%s%s%f",&b[i].id,b[i].title,b[i].author,&b[i].price);
}
```
```

User may input the book details in any order of price and hence we now need to sort the input data in ascending order of price obtained by each book. Let us assume that the user inputs unordered data which is as follows:

| Object of structure book | Data entered by the user (id, title, author, and price) |
|---|---|
| b[0] | (1, "C++", "Kunal", 900) |
| b[1] | (2, "Java", "Jack", 800) |
| b[2] | (3, "Fortran", "Jill", 990) |
| b[3] | (4, "Basic", "Tom", 950) |
| b[4] | (5, "Cobol", "Jazz", 400) |

Figure 9.17 gives the set of for loops required to sort an array in ascending or descending order. These loops have been explained in detail in Chapter 6, Section 6.2.5 so we will not repeat that explanation here.

For simplifying the explanation, we will refer the element at lower index as a Book object above in the array and the element at higher index as a Book object below in the array.

![](bbox=[0.244, 0.705, 0.771, 0.892])

**Figure 9.17:** for loops required for sorting the array