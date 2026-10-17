```
echo "Please enter an odd! \n";
$failure = true;
}
} while ($failure == true);
}
```

```
//display elements backwards
for ($i = ELEMENTS - 1; $i >= 0; $i--) {
    echo $odds[$i], "\t";
}
?>
```

# ## 37.3 Finding Minimum and Maximum Values in Arrays

This is the third and last time that this subject is raked up in this book. The first time was in Section 4 (Decision Control Structures) and the second time was in Section 5 (Loop Control Structures). So, there is not much left to discuss except that when you want to find the minimum or maximum value of an array that already contains some values, you needn't worry about the initial values of variables $min or $max because you can just assign to them the value of the first element of the array!

# ### Exercise 37.3-1 Which Depth is the Greatest?

Design a flowchart and write the corresponding PHP script that lets the user enter the depths of 20 lakes and then displays the depth of the deepest one.

# ### Solution

After the user enters the depths of the 20 lakes in the array $depths, the initial value of variable $max can be set as the value of the first element of array $depths, that is $depths[0]. The script can then search for any value greater than this. The final solution is quite simple and is presented next without further explanation.