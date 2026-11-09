# CHAPTER TWENTY

![](bbox=[0.06, 0.12, 0.44, 0.25])

Figure 20-7: User interface for the Test Scores application

Output: average score or highest score
Processing: one-dimensional array of scores (module-level)
            number of array elements (module-level)
            array subscript
            total scores accumulator (start at 0)
Input: scores

Algorithm for the Enter Test Scores button:
1. repeat for array subscripts from 0 through the number of array elements - 1 in increments of 1:
        enter a score
        store the score in the current array element
   end repeat
2. clear the label control that displays the average score or highest score

Algorithm for the Average Score button:
1. assign 0 to the total scores accumulator
2. repeat for array subscripts from 0 through the number of array elements - 1 in increments of 1:
        add the contents of the current array element to the total scores accumulator
   end repeat
3. calculate the average score by dividing the total scores accumulator by the number of array elements
4. display the average score

Algorithm for the Highest Score button:
1. assign the contents of the first array element as the highest score
2. repeat for array subscripts from 1 through the number of array elements - 1 in increments of 1:
        if the contents of the current array element is greater than the highest score, do this:
            assign the contents of the current array element as the highest score
        end if
   end repeat
3. display the highest score

Figure 20-8: Planning information for the Test Scores application