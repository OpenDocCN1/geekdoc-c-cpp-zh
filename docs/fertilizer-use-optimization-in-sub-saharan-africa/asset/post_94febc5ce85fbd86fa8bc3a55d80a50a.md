
## Foreword

Low soil fertility costs Africa's farmers US$4 billion a year in reduced yields. This usually results in low incomes and poor livelihoods. Part of the problem is that fertilizer use in the continent is only about 12 kg/ha/yr.

Africa's smallholder farmers are mostly very poor and have little financial ability to invest in inputs such as fertilizer. However, they are generally responsive to perceived high profit opportunities with little risk. The key to increased fertilizer use is to improve the profitability of its use with little risk. Achieving this gives farmers the opportunity to reduce the severity of their financial constraints and to gradually improve their crop management.

Fertilizer recommendations are available for some crops in most African countries, but too often these are decades-old blanket recommendations that cover large regions or even whole countries, are not well supported by field research and are more oriented to achieving high yields rather than high farmer profits.

The AGRA-funded project 'Developing and fine-tuning fertilizer recommendations within an integrated soil fertility management framework', abbreviated as the Optimizing Fertilizer Recommendations in Africa (OFRA), was implemented to develop the basis for fertilizer use optimization, that is, more profitable fertilizer use.

Through OFRA, national research institutes of 13 sub-Saharan African countries partnered together, and with CABI and the University of Nebraska-Lincoln, to develop the field research-based information needed for fertilizer use optimization decisions. Results of past research and OFRA-supported research were compiled and systematically analysed. This was applied to determine crop nutrient response functions for the important food crops in each of 67 agro-ecological zones (AEZ) or recommendation domains across the 13 countries. When several response functions for an AEZ are considered, it becomes apparent that profit potential varies according to which nutrient is applied to which crop and the rate of application. Therefore, especially for financially constrained farmers, the crop-nutrient-rate choices are very important to maximizing profitability. The choice of fertilizer types may include blends but maximizing profit potential requires adequate availability of single- (such as urea and triple superphosphate) and multi-nutrient, compound fertilizers (such as diammonium phosphate and potassium chloride).

Country teams integrated the crop nutrient response functions into decision tools that use linear programming to determine recommendations specific to a farmer's context intended to maximize profit from fertilizer use (see Chapter 1 and country chapters 4–16). These decision tools are called OFRA Fertilizer Optimization Tools (FOT); computer versions are available and also paper versions for use when a computer is not available. The FOT considers the farmer's financial ability, choice of crops and land allocation, crop values and fertilizer costs to determine the crop-nutrient-rate choices expected to maximize farmer profit from fertilizer use.

Sharing of research results across countries was enhanced with the development of the GIS tool called the OFRA Inference Tool. This tool uses GIS layers for soil properties of Africa Soil Information Service (AfSIS) and climatic properties, elevation, latitude and crops of HarvestChoice in geo-transfer of research results within and across countries between areas of similar growing conditions (see Chapter 2).

Fertilizer use optimization is within the framework of integrated soil fertility management with recommended fertilizer rates adjusted according to soil property information and the use of complementary practices (see Chapter 3).

Much early progress in enabling fertilizer use optimization with farmers and their advisors has been made, but this still requires a tremendous effort with much stakeholder support. Many more government and non-government extension staff and input retailers need to be trained in advising farmers in fertilizer use optimization. Farmers need training in the use of the paper FOTs to make fertilizer use choices according to the 4Rs (right type, rate, time and method of nutrient application) of nutrient stewardship and with proper calibration of application). Extension training resources have been developed and applied and many advisors have been trained. This is addressed in Chapter 17 with lessons learned for more effective progress in the future. AGRA is delighted with the success of the OFRA partnership of 13 countries in:

- developing a strong database of crop nutrient responses while recognizing that more research is needed to address secondary and micro nutrients, intercropping and rotations, and otherwise fine-tuning existing information,
- providing computer and paper FOTs for 67 recommendation domains,
- effectively applying GIS in sharing research results across recommendation domains and countries,
- capturing in the 17 chapters of this book a great deal of information applicable to fertilizer use optimization within integrated soil fertility management framework, and
- training many extension staff and other stakeholders, realizing that much more of this is needed to achieve fertilizer use optimization throughout sub-Saharan Africa.

**Rebbie Harawa,**
Interim Head, Farmers' Solution Program,
Alliance for a Green Revolution in Africa

**Bashir Jama Adan,**
Divisional Manager, Islamic Development Bank (and
previously Head, Soil Health Program, Alliance for a
Green Revolution in Africa)

## 1. Fertilizer Use Optimization: Principles and Approach

Kayuki C. Kaizzi¹ kckaizzi@gmail.com, Mohammed Beshir Mohammed² and Maman Nour³
¹ National Agricultural Research Laboratories, P.O. Box 7065, Kampala, Uganda
² Arba Minch University, P.O. Box 21, Ethiopia
³ Institut National de Recherche Agronomique du Niger, BP 240 Maradi, Niger

### 1.1 Introduction

Soils in sub-Saharan African (SSA) are degraded with low nutrient availability. This is partly a result of erosion, leaching and depletion through clearing and cultivation of the land with minimal use of external sources of nutrients (Stoorvogel et al., 1993; Bekunda et al., 1997). The rate of soil fertility decline depends on soil erosion, nutrient removal in harvests, the rate at which nutrients are returned to the soil through the use of both [inorganic] fertilizer and organic manures, and the rate of mineralization of soil mineral and organic matter nutrients.

Optimization of fertilizer use by smallholders refers in this chapter to the maximization of net returns on the farmers' investment achieved through the best choice of crop-nutrient-rate combinations. Making decisions on choice of crop to fertilize and the amount of each nutrient to apply, however, is very complex. Crop responses to applied nutrients needs to be considered in addition to the farmer's land allocation to different crops, the value of the produce, the costs of fertilizer use and the money available for fertilizer use.

The economic consequences of soil fertility nutrient depletion are great with reduced farm production and food security. Economic growth is slowed at community, regional and national levels by reduced agricultural productivity and its economic multiplier effects. Lower farm employment and increased poverty may drive migration to urban areas where infrastructure and employment opportunities are inadequate (Homer-Dixon et al., 1993).

Fertilizer use in SSA countries is low, partly because farmers do not recognize adequate profit opportunity with acceptable risk. Unfortunately, most countries have blanket fertilizer use recommendations that too often fail to consider farmers' profit potential. Farmers who are financially well off can afford to apply fertilizers on all their farmland to maximize profit per hectare. Smallholders often have some financial ability to use fertilizer, but need high returns on their small investment. The high returns will often reduce the financial constraint, enabling them to invest more in fertilizer use in following seasons. Smallholders have a high opportunity cost for their money and a benefit-cost ratio of two within a six to 12 month period is often not sufficient to justify an investment; alternative use of the limited financial capacity may give better returns or better meet urgent needs.

### 1.2 What is optimization?

Optimization is the process of identifying solutions that minimize or maximize a function's value, where the function represents the investment required for the desired benefit (Kumar 2013). All optimization problems are constrained due to resource scarcity or costs, and the maximizing or minimizing some objective function is always subject to one or more constraints.

Two common techniques of optimization are linear programming (LP) and non-linear programming. Linear programming is applied when the objective function f (the function that should be maximized or minimized) is linear and the constraints (resource limitations) are specified using only linear equalities and inequalities. Non-linear programming is applied when the objective function, the constraints, or both contain non-linear components. Other optimization techniques include integer stochastic programming, dynamic programming, hill climbing and simulated annealing (Kumar 2013).

Linear programming solves optimization problems where all the constraints as well as the objectives are expressed as a linear function using decision or activity variables and finite objective functions. The decision or activity variables refer to activities which are in competition with other variables for limited resources. For example, fertilizer purchase by a
