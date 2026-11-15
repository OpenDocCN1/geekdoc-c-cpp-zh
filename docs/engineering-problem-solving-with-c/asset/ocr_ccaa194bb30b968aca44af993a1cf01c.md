```
calculateAverages:
for i=0,numberOfSamples
for j=0,numberOfPlants
sum[j] = sum[j] + sampleData[i].getPlantCount[j]
for j=0,numberOfPlants
average[j] = sum[j]/numberOfPlants;
reportBelowAverage:
for i=0,numberOfSamples
first=true
for j=0,numberOfPlants
if (sample[i].plantCount[j]<average[j])
if (first is true)
print latitude, longitude, elevation
first=false
print plant name
print (1 - plantCount[j]/average[j])*100
```

Our structure chart and pseudocode provide enough detail to develop a C++ solution. Create a new project in Xcode by selecting New->Project... from the File menu at the top left of the main Xcode window. For this solution, we will select Application under OS X and Command Line Tool, as illustrated in the new project window below.

![](bbox=[0.235, 0.52, 0.805, 0.785])

New Project Window

Select Next, provide a name and location in the following window and create your new project.

Recall from Section 2.4 that Xcode creates a main.cpp for a new application. We will select main.cpp from the left side of the project window to display its content in the editor as shown below.