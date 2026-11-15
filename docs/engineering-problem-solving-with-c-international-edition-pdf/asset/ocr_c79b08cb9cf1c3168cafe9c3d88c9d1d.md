```
//Get filename and open file
cout << " Enter name of input file: ";
cin >> filename;
fin.open(filename.c_str());
if(fin.fail())
{
    cerr << " Could not open the file " << filename
         << " Goodbye." << endl;
    exit(1);
}
//Read header from input file
getline(fin,header);
//Read first line of input data
int i = 0;
fin >>> i = 0; >>> month >>> day >>> hour
fin >>> minute >>> waveHeights[i];
//Echo header
cout << header << endl;
//Print starting date and time.
cout << " Starting time: " << endl << year
     << setw(3) << month << setw(3) << day
     << setw(3) << hour << setw(3) << minute << endl;
//Read remaining lines of input
//Order wavelength in descending order
int pos;
for(int i=1; i<SAMPLE_SIZE; ++i)
{
    fin >>> year >>> month >>> day >>> hour
        >>> minute >>> newVal;
    //Find ordered position
    pos = 0; //start at top
    while(pos < i && newVal < waveHeights[pos])
    {
        ++pos;
    }
    if(pos == i)
    {
        //newVal belongs at end of array
        waveHeights[i] = newVal;
    }
    else
    {
        //Insert newVal at midpoint in array
        //Move values down to make room
        for(int k=i; k>pos; --k)
```