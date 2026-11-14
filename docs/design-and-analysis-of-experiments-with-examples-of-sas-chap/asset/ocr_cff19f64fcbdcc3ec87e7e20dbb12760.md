The research goal was to determine how the proportions of the three Niagara emulsifiers affected the surface tension of the pesticide formulation. The lower the surface tension, the more likely the formulation would spread evenly on the cotton leaves.

The data analysis will first be illustrated with the ADX automated design of experiments tool. Since this specific design cannot be created easily in ADX, the SAS data step was used to read the data in Table 11.1 into the SAS data set work.form; from there, it was imported to the ADX system. Figure 11.12 shows the data in the ADX system.

# Figure 11.12 Pesticide Formulation Data in ADX

![](bbox=[0.15, 0.29, 0.85, 0.58])

Clicking first on the Design Details button followed by the Design Points tab shows a graphical representation of the design points in the simplex region. The axis points can be seen in Figure 11.13.

The SLD(3,2) design augmented by the overall centroid supports fitting special cubic model. A general strategy to follow when modeling the data from mixture experiments is to first fit the highest order model supported by the design, then try to simplify if higher order terms are insignificant. The variance of predicted values will be lower for simpler models with fewer terms.

The model can be selected in ADX by choosing the Model ▶ Change master model menus. ADX allows the user to choose the linear, quadratic, special cubic or full cubic models as defined earlier in Equations 11.4, 11.7, 11.8, and 11.9, respectively. Figure 11.14 below shows the result of fitting the Scheffe special cubic model. ADX fits the model by the method of least squares, and the same methods for checking the assumptions of the least squares fit (described in Chapter 2) can be accomplished within the ADX system. If there are replicated points, ADX automatically performs the lack of fit test as explained in Section 10.6.2. In the results shown in Figure 11.14, the $\beta_{123}$