
After collecting data from the first block, the significance of factor main effects can be determined. If there are insignificant main effects, they can be ignored and the design collapses to a factorial plus center points as shown in the bottom leg of the next stage of experimentation in Figure 13.3. If all main effects are significant, a second block of experiments is performed to create a full factorial plus center points as shown in the top leg of Figure 13.3. In the analysis of data at the second stage, a test for curvature should be performed as described in Section 10.6.1. If there is significant curvature, a third block of experiments involving central-composite-design-axial points and additional center points should be run to complete a response surface design.

## Figure 13.3 Blocked Response Surface

![](img/878b651cdbe9da3d6d22e64d64b8a54f_572_0.png)

The orthogonally blocked central composite designs, which are produced automatically by SAS ADX, can be used as illustrated in Figure 13.3 if they have at least three blocks. For example, there is a three-factor central composite design that blocks orthogonally into three blocks. The first block is the half-fraction plus center points. The second block is the mirror image half-fraction plus additional center points, and the third block is the axial points plus center points. There is a similar four-factor central composite design in three blocks. For five- and six-factor designs there are central composite designs that block into five blocks. The first four blocks consist of ¼ fractions (⅛ fractions for the six-factor design) and it may be possible to eliminate some of these blocks if not all factors are significant.

An example of using a sequence of fractional factorial, factorial, and central composite design to increase knowledge in the way shown in Figure 13.3 was illustrated in the example of producing an amino acid rich biomass from eucalyptus wood given in Section 6.4 and continued in exercise 3 of Chapter 10.

After the data is collected in the optimization stage of experimentation, general quadratic or cubic (in the case of some mixture experiments) models are fit to the resulting data, and various tools are used to explore the fitted surface and identify optimum operating conditions. Since the polynomial models used in the optimization stage are just approximations to the true relationship between the quantitative factors and the response, predictions should never be made with these models outside the region of expectation.

When more knowledge is available in the form of a theoretical model, like the compartment model described in Section 10.5 or a chemical degradation model determined from first-order kinetics in Section 10.7.4, there is no need to conduct a traditional response surface experiment. When a theoretical model is available, the parameters of this model can be estimated from data collected using custom experimental designs that are based on the form of the model and prior estimates of the parameters. Once data is collected and a theoretical model is fit, predictions or extrapolations can be made outside the experimental region.

Utilizing all the stages of experimentation shown in Figure 13.1, the state of knowledge can be advanced through a sequence of experiments as illustrated in Figure 13.4. A plan of action to gain knowledge in this way is called a sequential experimentation strategy.

![](img/878b651cdbe9da3d6d22e64d64b8a54f_573_0.png)

## 13.3 One Step Screening and Optimization

In some cases when experiments are conducted in a manufacturing facility, a pilot plant (that can only be scheduled for a limited time), in marketing research studies or engineering prototype testing (where there is a fixed deadline), the sequential experimentation strategy may not be possible. After beginning experiments, some experimental plans must be modified when an experimenter finds that factors cannot be varied independently, the chosen range for one or more factors is infeasible, or a previously unknown but highly influential factor is discovered. However, when the time allotted for experimentation is tight, rarely is it possible to start with a screening experiment and proceed with additional designs and analysis to arrive at the desired state of knowledge.

For the reasons above, the sequential experimentation strategy is sometimes abandoned in favor of a single design or set of experiments. Even so, the designs used for screening and optimization are mutually exclusive. If an experimenter can only afford to run one set of experiments, he is forced to choose between one objective or the other. If the experimenter chooses a classical response surface design, he must select a subset of the factors to work with, and he risks the possibility of missing other important factors. On the other hand, if the experimenter chooses a screening experiment to avoid missing important factors, important interactions and quadratic effects will be missed.

It would be desirable in some situations to have experimental design plans that allow for (1) screening a reasonably large number of factors to identify the important ones, and (2) refitting a model to the data in only the important factors, so that important interactions or optimum operating conditions can be determined after one set of experiments. Recent literature has shown this is possible using certain orthogonal array main effect plans.

Lawson (2003) illustrates how screening followed by estimation of interactions can be accomplished using Plackett-Burman Designs. The example in Section 6.6 illustrates how this can be accomplished. Cheng and Wu (2001) proposed a strategy for using non-regular fractions of 3k designs for simultaneous screening and response surface exploration. Lawson (2003) presents 18-, 27- and 36-run examples of these non-regular fractions and an example using Chen and Wu’s strategy with an 18-run design. Many additional non-regular fractions of 3k designs are stored in a vast catalog by SAS and can be accessed using the %mkt macros described in Section 6.7. For example, the SAS commands below search for an orthogonal array design with seven factors at three levels, and then create an 18-run design.

```
*Search for orthogonal arrays in catalog of designs;
%Mktruns(3**7)
*Find an 18 run design for 7 factors with 3 levels;
%MktDes(3**7,n=18)
*Print a randomized list of the runs;
proc print data=randomized; run;
```

The analysis of data from non-regular fractions of 3k designs, like this, is similar to the analysis of Plackett-Burman Designs as illustrated in Section 6.6.

## 13.4 Evolutionary Operation

The idea of using optimization experiments, or any experimentation for that matter, is often met with resistance in an operating manufacturing facility. In manufacturing, the key process variables thought to influence production are usually tightly controlled in order to ensure the quality of the manufactured product. Tampering or experimenting with the levels of key process variables could result in the production of off-grade or scrap product. However, the levels at which the process variables are controlled in a manufacturing process, may not be optimal. These levels may have been determined in pilot plant or laboratory experiments where conditions may differ in many ways from the actual manufacturing facility. In other cases, where the levels of key process variables were actually determined through preliminary experiments in the manufacturing facility, they may no longer be optimal due to drift over time in raw materials or environmental conditions. Therefore, although acceptable product is being produced with current process variable settings, there may be benefits in experimenting to obtain improved settings or to counteract drift over time.

Box (1957) proposed a method for finding improved settings of key process variables without upsetting production. He believed that a manufacturing process should not only produce product, but also information that can be used to improve the process over time. Data is normally collected in manufacturing facilities regarding (1) the settings of key process variables during each production run (to ensure operating procedures are being followed) and (2) measured characteristics of product (to monitor quality). While recording this information, Box suggested making small perturbations in key process variable settings from time to time according to a statistical plan like a 2^2 or 2^3 experiment. The planned changes in the key process variables would be small enough that the product output would not be degraded, yet large enough that potential process improvements could be recognized after a number of cycles through the planned settings. He called this method Evolutionary Operation or EVOP for short.

When using EVOP, the center point in a 2^2 or 2^3 design is assigned to the current operating conditions (in terms of what is believed to be the key process variables). Figure 13.5 illustrates the plan for two process variables. The five different process settings would each be run during one block of manufacturing. Running all five of these conditions completes one cycle of the EVOP.

![](img/878b651cdbe9da3d6d22e64d64b8a54f_575_0.png)

If the average measure of product characteristic is y_{ij,k} during the kth EVOP cycle at process variable settings i and j, then after two or more cycles, the
