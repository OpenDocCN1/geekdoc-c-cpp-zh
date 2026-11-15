```
longitude = 0.0;
elevation = 0.0;
}
void VegetationSample::inputSampleData(istream& in)
{
    in >> latitude >> longitude >> elevation;
    for(int i = 0; i < MAXPLANTS; ++i)()
    in >> plantCounts[i];
    }
}
```

VegetationSample has enough functionality to be useful in our solution. The solution requires several tasks. We must open the data file, input the header, input the sample data, calculate averages, and report locations with below average plant populations. A structure chart for our solution is provided in Figure 7.7.

![](bbox=[0.22, 0.38, 0.8, 0.65])

Pseudocode is provided below for the four modules referenced by main. The remaining three modules represent methods defined in VegetationMap.

```
getHeader: input stationCode, sampleDate, sampleRadius
for i = 0, numberOfPlants
    input plantName[i]
getData: input numberofSamples
if (numberofSamples > MAX) exit
for (i = 0, numberOfSamples
    input sampleData[i]
```