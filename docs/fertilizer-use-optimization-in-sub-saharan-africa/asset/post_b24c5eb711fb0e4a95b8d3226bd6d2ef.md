
![](img/279f2242dca113ddfb6220d3a162ffff_71_0.png)

Figure 6.3: Net return from fertilizer use in the Derived Savanna Transitional Zone of Ghana. Less profitable and unprofitable nutrient applications were excluded from the figure. This graphic is dependent on grain values and fertilizer use costs. Grain and tuber values used were: 0.75, 1.52, 1.22, 2.78, 1.77 and 0.20 for maize, sorghum, rice, groundnut, soybean and cassava respectively. Fertilizer use costs were: urea = 100; TSP = 150; KCl = 150 and ZnSO4 = GH¢ 600 per 50 kg.

6.2 with a large yield increase with increasing N at low rates, a lower rate of yield increase at higher N rates, until yield reaches a plateau with no more yield increase. This tells us that the net returns to low rates of nitrogen application are greater than with higher rates. Such response curves are typical for most crops and nutrients and are essential to determining the profitability of fertilizer use. These show that the financially constrained farmer will make more profit on a limited amount of fertilizer by applying at lower nutrient rates to more land than by applying higher rates over less land.

GH¢ 20/ha (x-axis) of K applied to cassava with an expected net return of approximately GH¢ 1230/ha (y-axis). When the same amount (GH¢ 20) is invested in P applied to groundnut (on x-axis), the expected mean net return is approximately GH¢ 950 (on the y-axis) to farmers in the Derived Transitional Zone. The peak of the curves is the point of maximum profit per hectare for that nutrient applied to that crop. When slopes decline, profit is declining. The financially constrained farmer wants first to take advantage of the most profitable crop-nutrient combinations for crops in the cropping system. Making decisions in consideration of these curves for the amount of nutrient to apply to each crop is, however, very complex. Not only the agronomy of the responses to applied nutrients of the different crops of interest to farmers, but also the farmer's land allocation to different crops, the value of the commodity, the costs of fertilizer use and the money available for fertilizer use need to be considered in optimizing fertilizer use for high profit. Therefore, fertilizer optimization tools were developed using Excel Solver® (Frontline Systems Inc.) that use complex mathematics to integrate economic and agronomic information, but which are easy to use (https://agronomy.unl.edu).

## 6.7 Fertilizer use optimization tools (FOT) for Ghana

Fertilizer Optimization Tools (FOTs) were developed to integrate the economic and agronomic aspects of the farmer's situation with the crop nutrient response functions determined from field research trials through complex calculations involving linear optimization here.

Fertilizer use optimization as mentioned here refers to maximizing profit from fertilizer use, including profit per hectare for the farmer with adequate finance and also profit on the small investment in fertilizer use by the financially constrained farmer. These easy to use tools were designed to make decisions to maximize profits from fertilizer use.

The FOTs were developed for four zones in Ghana as shown in the FOT input screen (Figure 6.4) for the Derived Savanna Transitional Zone. It considers high and low potential maize, cassava, upland and lowland rice, groundnut and soybean. To use the FOT, the Excel add-in Solver needs to be activated and macros need to be enabled; see the step-by-step instructions in the 'Help and Instructions' worksheet of the FOTs and more detailed instructions (Extension Materials and FOT Manual) are available at http://agronomy.unl.edu/OFRA.

Once Solver has been activated and macros enabled, the user enters the land areas in hectares 'Area Planted, ha' for each crop to be planted. The expected on-farm value of the commodity considering the expected value of that kept for home consumption and that to be marketed is entered 'Expected Grain Value/kg'. If a crop is not planted, '0' is entered for hectares. Next, the cost of using available fertilizers are entered considering the purchase price, and transport and application costs under 'Cost/50 kg bag'; if the fertilizer is not available, '0' is entered for the cost. An optional fertilizer can be added under the KCl row with the nutrient concentrations. Finally, the amount of money that the farmer has for fertilizer use is entered 'Budget Constraint'; in the example, GH¢ 500 is entered, an affordable budget for many smallholders. A left click on 'Optimize' runs the optimization.

The FOT output is in three tables (Figure 6.5). The upper table 'Application rate - kg/ha' gives the recommended fertilizer rates for each crop. Some recommended rates are less than 20 kg/ha and too low for feasible application; that fertilizer or money can be allocated by the user to another fertilizer application. Total fertilizer amounts recommended are 256 kg/ha of urea, 33 kg/ha of TSP, 0 kg/ha DAP as this was not selected in the Input screen, 56 kg/ha of KCl, and just 6 kg of NPK which was generally not economically competitive with the single nutrient fertilizers.

The next table 'Expected Average Effects per ha' addresses expected average yield increases and net return per acre due to the recommended fertilizer use (Figure 6.5). This table indicates the relative profitability associated with fertilizer applied to the different crops; in the table the most profitable fertilizer use is with cassava suggesting that the farmer may want to increase area planted to cassava; this high profit potential with cassava is consistent with information in Figure 6.3.

The third table 'Total Expected Net Returns to Fertilizer' is an average estimate, adjusted for land allocated to each crop, but expecting that the net returns will be more in some years and less in other years. These results can only be expected if the farmer adheres to good agronomic practices of variety selection, planting and control of weeds, disease and pests.

Crop options are to a large extent determined by physiographic and climatic conditions, such as with sorghum and cowpea generally in drier areas and maize and beans in more humid areas. The choice of crops is done by the farmer considering crop suitability, home consumption needs, local market opportunities, credit availability and market access.

The FOTs help the farmers make decisions to maximize profit from fertilizer use. The FOTs can be used in decision making at district level so as to ensure the fertilizers that are most cost effective for the farmer are adequately available on a timely basis. For example, the results in Figure 6.5 indicate the strong need for timely availability of urea but also that TSP and KCl supply should have priority over supply of NPK.

![](img/279f2242dca113ddfb6220d3a162ffff_73_0.png)

## AEZ Derived Savanna/Transitional

Producer Name: xxx
Prepared By:
Date Prepared: August 3, 2016

| Crop | Area Planted (Ha)* | Expected Grain Value/kg † |
|---|---|---|
| Maize HP>3t | 1 | 0.75 |
| Maize LP<3t | 0.5 | 0.75 |
| Cassava | 0.5 | 0.2 |
| Rice upland | 0.5 | 1.22 |
| Rice lowland | 0.5 | 1.22 |
| Groundnut | 1 | 2.71 |
| Soybean | 0.3 | 1.77 |
| Total | 4.3 | |

| Fertilizer Product | N | P2O5 | K2O | Zn | Costs/50 kg bag †† |
|---|---|---|---|---|---|
| Urea | 46% | 0% | 0% | 0% | 100 |
| Triple super phosphate, TSP | 0% | 46% | 0% | 0% | 150 |
| Diammonium phosphate, DAP | 18% | 46% | 0% | 0% | 0 |
| Muriate of potash, KCl | 0% | 0% | 60% | 0% | 150 |
| NPK | 15% | 15% | 15% | 0% | 120 |

| Amount available to invest in fertilizer |
|---|
| 500 |

Figure 6.4: Input data options for the computer generated FOT.

| Crop | Area | TSP | DAP | KCl | NPK |
|---|---|---|---|---|---|
| Maize HP>3t | 45 | 9 | 0 | 0 | 0 |
| Maize LP<3t | 0 | 0 | 0 | 7 | 0 |
| Cassava | 87 | 0 | 0 | 20 | 6 |
| Rice upland | 60 | 0 | 0 | 19 | 0 |
| Rice lowland | 35 | 0 | 0 | 5 | 0 |
| Groundnut | 0 | 24 | 0 | 5 | 0 |
| Soybean | 0 | 0 | 0 | 0 | 0 |
| Total fertilizer needed | 151 | 33 | 0 | 30 | 3 |

| Crop | Yield Increases | Net Returns |
|---|---|---|
| Maize HP>3t | 916 | 571 |
| Maize LP<3t | 177 | 112 |
| Cassava | 14,952 | 2,740 |
| Rice upland | 1,800 | 1,961 |
| Rice lowland | 739 | 816 |
| Groundnut | 297 | 717 |
| Soybean | 0 | 0 |

| Total net returns to investment in fertilizer |
|---|
| 4,101 |

Figure 6.5: Output after optimizing the tool showing fertilizers needed and the expected returns.
