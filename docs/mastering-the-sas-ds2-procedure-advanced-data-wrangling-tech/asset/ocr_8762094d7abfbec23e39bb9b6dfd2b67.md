# 5.5.2 Matrix Package Example

Our motor pool is getting ready to place the order for the fluids required for this year's maintenance on our vehicle fleet. The data set crsour_fleet contains information about the vehicles in the fleet:

Figure 5.14: Data Contained in crsour_fleet Data Set

| Obs | Make | Model | BodyType | Year | Inventory | Oil | Cooling | Transmission | Differential |
|---|---|---|---|---|---|---|---|---||}{
| 1 | Ford | F550 | Pickup Truck | 2015 | 24 | 7.0 | 26.7 | | 17.5 | 5.9 |
| 2 | Ford | Expedition | Full size SUV | 2015 | 12 | 6.0 | 18.5 | | 13.1 | 3.6 |
| 3 | Dodge | Ram Proaster 3500 | Cargo Van | 2015 | 20 | 6.0 | 10.6 | | 9.0 | 4.8 |
| 4 | GMC | Yukon XL | Full size SUV | 2015 | 12 | 8.0 | 17.4 | | 11.4 | 5.5 |
| 5 | Smart | For Two | Mini | 2015 | 144 | 3.6 | 4.5 | | 2.5 | 0.0 |
| 6 | Land Rover | Range Rover | Full size SUV | 2010 | 48 | 6.5 | 16.0 | | 10.5 | 1.5 |

To start, we create a matrix with six rows and four columns that represents the fluid capacities of all vehicles and a second matrix with one row and six columns that represents the inventory of each type of vehicle. The next step is to multiply these two matrices. The result is a matrix of one row and four columns containing the total volume of each fluid required for this year's maintenance.

# 5.5.2.1 Getting data into out of Matrices

Because it is easier to transfer data into and out of matrix package using arrays, for each matrix we create, we create a corresponding array or variable. We'll use the RUN method to load the capacity matrix and the vehicle inventory. Then, in the TERM method, we'll load the vehicle inventory into the unit's matrix, do the multiplication, and transfer the results out all values to the volume's array, round up to the nearest whole unit, and output the result set.

```
proc ds2;
title1 'Fluids required for this year''s maintenance:';
title2 'All volumes in gallons:';
data;
* The Matrices *
* Six vehicle types, 4 capacities each */
dcl package matrix m_caps(6,4);
* How many of each type get maintenance */
dcl package matrix m_units(1,6);
* Total amount of each fluid to buy */
dcl package matrix m_fluid_reg(1,4);
* The Arrays /
* 4 capacities each vehicle */
vararray double a[4] Oil Cooling Transmission Differential;
* How many of each type get maintenance */
dcl double a_units[1] Inventory;
* Total amount of each fluid to buy */
vararray double a_vals[4] Oil Cooling Transmission Differential;
keep Oil Cooling Transmission Differential;
```