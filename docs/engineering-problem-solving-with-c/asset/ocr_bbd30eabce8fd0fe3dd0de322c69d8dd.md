```
```cpp
for(int k=0; k<10; ++k)
{
    sensor3 >> time[k] >> motion[k];
    cout << time[k] << '\t' << motion[k] << endl;
}
//find max motion and time of occurrence
int count(0);
double maxMotion, timeOfMax;
//initialize maxMotion;
maxMotion = motion[0];
for(double m:motion)
{
    if(m > maxMotion)
    {
        maxMotion = m;
        timeOfMax = time[count];
    }
    ++count;
}
cout << "Maximum motion of " << maxMotion
     << " occurred at time " << timeOfMax << endl;
}
else
{
    cout << " Could not open file sensor3.dat..goodbye." << endl;
}
return 0;
}```
```

If the data file sensor3.dat held the set of data

| 0.0 | 1 |
| 0.1 | 1 |
| 0.2 | 2.5 |
| 0.3 | 1.7 |
| 0.4 | 2 |
| 0.5 | 2.5 |
| 0.6 | 3.5 |
| 0.7 | 1.5 |
| 0.8 | 1.5 |
| 0.9 | 1 |

the output from program chapter7_3 would be as follows:

| 0 | 1 |
| 0.1 | 1 |
| 0.2 | 2.5 |
| 0.3 | 1.7 |
| 0.4 | 2 |