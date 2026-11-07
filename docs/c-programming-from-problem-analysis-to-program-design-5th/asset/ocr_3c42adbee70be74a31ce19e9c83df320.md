```
```cpp
cout << "Program terminates." << endl;
return 1;
}
else                                      //Step 12b
{
    calculateAverage(group1, avg1);       //Step 12b.i
    calculateAverage(group2, avg2);       //Step 12b.ii
    printResult(outfile, courseId1,
                1, avg1);                 //Step 12b.iii
    printResult(outfile, courseId2,
                2, avg2);                 //Step 12b.iv
    avgGroup1 = avgGroup1 + avg1;         //Step 12b.v
    avgGroup2 = avgGroup2 + avg2;         //Step 12b.vi
    outfile << endl;
    numberOfCourses++;                    //Step 12b.vii
}

group1 >> courseId1;                      //Step 12c
group2 >> courseId2;                      //Step 12d
} //end while

if (group1 && !group2)                    //Step 13a
    cout << "Ran out of data for group 2 "
         << "before group 1." << endl;
else if (!group1 && group2)               //Step 13b
    cout << "Ran out of data for group 1 "
         << "before group 2." << endl;
else                                      //Step 13c
{
    outfile << "Avg for group 1: "
            << avgGroup1 / numberOfCourses
            << endl;
    outfile << "Avg for group 2: "
            << avgGroup2 / numberOfCourses
            << endl;
}

group1.close();                           //Step 14
group2.close();                           //Step 14
outfile.close();                          //Step 14

return 0;
}

void calculateAverage(ifstream& inp, double& courseAvg)
{
    double totalScore = 0.0;
    int numberOfStudents = 0;
    int score;
}
```
```