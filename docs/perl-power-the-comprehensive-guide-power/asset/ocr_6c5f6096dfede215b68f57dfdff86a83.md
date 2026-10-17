```
```perl
print "\n Adding $Nation . . . ";
#Capitalize the letter
substr($Nation, 1, 1, "E"); #capitalize the second letter
#Add the changed spelling to the new array
@NationArrayWithE = (@NationArrayWithE, $Nation);
}
}
print "\n E: @NationArrayWithE";
```
```

In the lines associated with comment #1, you create two arrays containing the names of nations. One list contains the names of nations that begin with the letter “B.” The other array contains the names of nations that begin with the letter “L.” To add items to the arrays, you repeatedly make use of the list function to add scalars to the two arrays. At comment #2, you then concatenate the two basic arrays, again employing the list function. The resulting array (@NationArrayAll) contains all of the nations.

With the lines trailing comment #3, you create a foreach statement and visit each element in the @NationArrayAll array. As you iterate through the array, you place the elements in a scalar ($Nation) and then submit this scalar to the substr() function to discover the identity of the letter that occupies its second index. This letter you assign to a scalar ($Letter).

At comment #4, you repeat the basic activities performed in association with comment #3, but this time you employ a selection statement to filter the names of nations based on the second letter of their spellings. Additionally, you supply the substr() function with the scalar containing the nation’s name ($Nation) to capitalize the second letter. After capitalizing the second letter, you then employ the list function to add the name of the nation to yet another array, @NationArrayWithE. The finale arrives when you print this final list. Figure 6.5 illustrates the output of Listing06_04.

![](bbox=[0.181, 0.672, 0.594, 0.861])

**Figure 6.5** Selection of elements from arrays allows you to examine and transform them.