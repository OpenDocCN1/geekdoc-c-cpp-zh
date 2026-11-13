```
}
}
}
printf("Total comparisons made: %d" , comparisons); return index;
}

void display(){ int i;
printf("\n");
 // navigate through all items for(i = 0;i<MAX;i++){
 printf("%d ",intArray[i]); }
 printf("\n"); }

main(){
printf("Input Array: "); display();
printline(50);

//find location of 1 int location = find(55);
// if element was found
if(location != -1)
printf("\nElement found at location: %d" ,(location+1)); else
printf("\nElement not found.");
}
```

If we compile and run the above program, it will produce the following result -

```
Input Array: [ 1 2 3 4 6 7 9 11 12 14 15 16 17 19 33 34 43 45 55 66 ]
======================================================
Comparison 1
lowerBound : 0, intArray[0] = 1
upperBound : 19, intArray[19] = 66
Comparison 2
lowerBound : 10, intArray[10] = 15
upperBound : 19, intArray[19] = 66
Comparison 3
lowerBound : 15, intArray[15] = 34
upperBound : 19, intArray[19] = 66
Comparison 4
lowerBound : 18, intArray[18] = 55
upperBound : 19, intArray[19] = 66
Total comparisons made: 4
Element found at location: 19
```