```
```cpp
++k;
fin >> id[k] >> mph[k];
} //end while
npts = k;

//Print hurricane report.
if(max >= 74)
{
    cout << "Storms that Qualify as Hurricanes \n"
    << "Identification\t Peak Wind(mph)\t Category\n";
}
else
{
    cout << "No hurricanes in the file \n";
}
for(k=0; k<npts; ++k)
{
    if(mph[k] >= 74)
    {
        if(mph[k] == max)
        {
            cout << "\n" << id[k] << "\t" << mph[k] << "\t"
            << category(mph[k]) << endl;
        }
        else
        {
            cout << "\t" << id[k] << "\t" << mph[k] << "\t"
            << category(mph[k]) << endl;
        }
    } //end if k
} //end for
fin.close();
return 0;
}
/******************************************************************/
/* This function determines the hurricane intensity */
/* category. */

double category(double speed)
{
    //Declare variables.
    int intensity(1);

    //Determine category.
    if(speed >= 155)
    {
        intensity=5;
    }
```
```