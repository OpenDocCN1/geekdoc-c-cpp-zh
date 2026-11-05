# ANALYZE THE PROBLEM

Review the problem specification in Figure 12–21 to ensure that you understand the problem definition. Values for the location, including location name, state, and mile marker number are entered. The depths at low and high tide are also input into the application. Four separate days of low and high tidal water values are entered by the user. The FrmWaterDepth class is created as the user interface. It displays a number of text boxes that are used to enter values into the application. These values are used to instantiate the ShoalArea class.

Output consists of displaying the location entered and the calculated averages for the water depths at low and high tide. An overall average is calculated using all of the water values entered. The data members for the ShoalArea class are shown in Table 12–4.

# DATA

Table 12–4 lists the data field members needed for the ShoalArea class.

# TABLE 12-4  ShoalArea class data fields

| Data description | Type | Identifier |
|---|---|---|
| Location (town) | `string` | location |
| State | `string` | state |
| Mile number | `double` | mileMarker |
| Low tide depth | `double[]` | lowTideDepth |
| High tide depth | `double[]` | hiTideDepth |

# DESIGN A SOLUTION

The desired output is to produce a message showing the location of the shoal area and data describing the current condition of the reported problem. In Chapter 13, you will be introduced to file-handling techniques. This application will be revisited to illustrate how the records could be stored in a file for later retrieval. Figure 12–22 shows a prototype of the form that will be used for input. As the prototype shows, four different days of water depths are entered by the user along with information relating to the location.