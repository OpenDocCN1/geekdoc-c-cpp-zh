# Reference Variables 407

```
void file_it(ostream & os, double fo, const double fe[], int n)
{
    ios_base::flags initial;
    initial = os.setf(ios_base::fixed); // save initial formatting state
    os.precision(0);
    os << "Focal length of objective: " << fo << " mm\n";n    os.setf(ios::showpoint);
    os.precision(1);
    os.width(12);
    os << "f.1 eyepiece";
    os.width(15);
    os << "magnification" << endl;
    for (int i = 0; i < n; i++)
    {
        os.width(12);
        os << fe[i];
        os.width(15);
        os << int (fo/fe[i] + 0.5) << endl;
    }
    os.setf(initial); // restore initial formatting state
}
```

Here is a sample run of the program in Listing 8.8:

Enter the focal length of your telescope objective in mm: 1800
Enter the focal lengths, in mm, of 5 eyepieces:
Eyepiece #1: 30
Eyepiece #2: 19
Eyepiece #3: 14
Eyepiece #4: 8.8
Eyepiece #5: 7.5
Focal length of objective: 1800 mm
f.1 eyepiece magnification

```
30.0 60
19.0 95
14.0 129
8.8 205
7.5 240
```

Done

The following line writes the eyepiece data to the file ep-data.txt:

```
file_it(fout, objective, eps, LIMIT);
```

And this line writes the identical information in the identical format to the screen:

```
file_it(cout, objective, eps, LIMIT);
```