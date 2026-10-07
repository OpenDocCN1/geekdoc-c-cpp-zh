

![](img/f4ec2665c3484c528370923aeb5cb99f_367_0.png)

## 7.6 结论

目前的剂量发现实践往往不尽人意：许多剂量发现研究的设计并不合理（剂量过少、剂量范围过窄、样本量不足等），且从这些研究中得出的推断不够准确，导致药物开发中产生不理想的严重后果（例如：III 期失败率高、批准后需要更改标签等）。

在此，我们描述了一种用于分析剂量发现研究的统一策略，包括选择一个或多个剂量进入进一步开发。所提的方法结合了多重比较和建模方法的优点，由一个多阶段程序组成。在第一阶段，使用多重比较方法进行剂量-效应检验，以识别与一组候选模型相对应的具有统计学意义的差异。如果在第一阶段建立了剂量-效应信号，则使用最佳模型进行剂量-效应和目标剂量估计。我们通过对真实数据和模拟数据的分析，展示并评估了结合统计学显著性和临床相关性的不同基于模型的剂量选择方法。

所提方法的 MCP 部分被认为能将族性错误率（FWER）维持在名义水平，在单调剂量-效应设置下其效能与标准趋势检验相当，在非单调场景下表现更好（前提是候选模型足够足够）。与传统的多重比较剂量发现方法相比，这种新方法的明显优势在于通过使用建模技术增加了搜索和识别未来药物开发合适剂量的灵活性。文献中已经研究并探讨了所提方法的几种变体。

与传统的基于 ANOVA 的两对多重比较相比，MCP-Mod 的优势在于能够在设计中允许更多剂量，而不需要大幅增加患者人数。在 ANOVA 类型方法中，仅使用相应剂量的信息来估计剂量-效应，这意味着当每个剂量处需要固定的 MCP 精度时，所需的样本量很大取决于所研究的剂量。通过使用建模技术，MCP-Mod 允许我们跨剂量水平进行信息插值，总样本量将不再强烈依赖于研究的剂量数量。使用更多剂量的可能性通常会导致信息丰富的剂量发现设计，并为 II 期结束时的决策提供更好的依据。

MCP-Mod 可适用于广泛的参数模型，超越标准 ANOVA 模型中正态分布终点的设置。例如，响应变量可能是计数、二分或事件时间变量，而不是呈特定分布。对于广义 MCP-Mod，只需要获得剂量处的响应估计值以及相关的协方差矩阵。在 SAS 中，可以使用不同的方法来产生这些估计。`proc glmix` 可能是最通用的过程，因此推荐用于大多数情况。另一个优势是它能产生适当的多重性 p 值。然后可以使用提供的 proc 代码执行 Mod 步骤，该代码非常灵活，且不依赖终点的底层分布。当然，其他过程如 `proc nlin` 或 `proc mixed` 可用于 Mod 步骤。此外，最终分析通常需要对相关的协变量（如地区、年龄等）进行调整，患者的测量值通常随时间记录（需要使用纵向模型），且患者可能接受多种治疗（如交叉或不完全区设计）。在本章中，我们通过两个真实数据集说明了如何在实践中使用 MCP-Mod 方法。此外，我们还提供了相关的 SAS 代码，使感兴趣的读者能够在许多实际相关的情况中实施并执行 MCP-Mod 方法。实现 MCP 的另一种可能性是通过 DoseFinding R 包 [11]，该包包含了用于剂量发现研究设计和分析的广泛功能。商业软件软件包 ADDPLAN-DF 包含了使用 MCP-Mod 设计剂量发现研究的广泛工具 [12]。此外，Cytel 开发了 PROC MCPMOD 作为 SAS 的插件，专注于使用 MCP-Mod 进行剂量发现研究的分析。

## 参考文献

- 1. Bornkamp B, Brest F, Dmitrienko A, Enas G, Gaydos B, Hsu CH, Koenig F, Krams M, Liu Q, Neuenschwander B, Parke T, Pinheiro J, Roy A, Sax R, & Shen F. (2007). Innovative approaches to designing and analyzing adaptive dose-ranging trials (with discussion). Journal of Biopharmaceutical Statistics 17: 965-995.
- 2. Bretz F, Pinheiro J & Branson M. (2005). Combining multiple comparisons and modeling techniques in dose-response studies. Biometrics 61: 738-748.
- 3. European Medicines Agency. (2014). Qualification opinion of MCP-Mod as an efficient statistical methodology for model-based design and analysis of Phase II dose-finding studies under model uncertainty. Available at: http://www.ema.europa.eu/docs/en_GB/document_library/Regulat
- 4. Pinheiro J, Bornkamp B, Glim E & Bretz F. (2014). Multiple comparisons and modeling for dose finding using general parametric models. Statistics in Medicine 33: 1646-1661.
- 5. Thomas N, Sweeney K & Somayaji V. (2014). Meta-analysis of clinical response in a large drug development portfolio. Statistics in Biopharmaceutical Research 6: 302-317.
- 6. Pinheiro J, Bornkamp B & Bretz F. (2006). Design and analysis of dose finding studies combining multiple comparisons and modeling procedures. Journal of Biopharmaceutical Statistics 16: 639-656.
- 7. European Medicines Agency. (2015). Report from Dose Finding Workshop. Available at: http://www.ema.europa.eu/docs/en_GB/document_library/Report/2
- 8. Dette H, Bretz F, Pepelyhev A & Pinheiro JC. (2008). Optimal designs for dose finding studies. Journal of the American Statistical Association 103: 1225-1237.
- 9. Bretz F, Dette H & Pinheiro J. (2010). Practical considerations for optimal designs in clinical dose finding studies. Statistics in Medicine 29: 731-742.
- 10. Atkinson A, Donev A & Tobias R. (2007). Optimum Experimental Design with SAS. Oxford, UK: Oxford University.
- 11. Bornkamp B, Pinheiro J & Bretz F. (2014). DoseFinding, version 0.9-12. Available at CRAN.R-project.org.
- 12. ADDPLAN DF. (2013). Adaptive Designs – Plans 3.1. Available at www.addplan.com.
- 13. Tukey JW, Ciminera & Heys JF. (1985). Testing effect of a drug using multiple doses. Biometrics 41: 295-301.
- 14. Thomas N. (2006). Dose-response signal using a sigmoid Emax model in phase II. Journal of Biopharmaceutical Statistics 16: 657-677.
- 15. Wakana A, Yoshimura I & Hamada C. (2007). A method for dose selection in phase II trial. Biometrics 26: 498-511.
- 16. Klingenberg B. (2009). Proof of concept and dose estimation by binary responses. Statistics in Medicine 28: 274-292.
- 17. Benda A. (2010). The impact of dropouts on the analysis of dose-finding. Statistics in Medicine 29: 1096-1106.
- 18. Wouter W. (2012). Statistical analysis of longitudinal data for dose finding. M.Sc. thesis, University of Gent.
- 19. Tao A, Lin Y, Pinheiro J & Shih WS. (2015). Joint modeling of efficacy and safety in phase II studies. International Journal of Statistics and Probability 4: 33-45.
- 20. Dette H, Titoff S, Volgushev S & Bretz F. (2015). Model identification for dose response detection. Biometrics. DOI: 10.1111/biom.12357.
- 21. Baayan C, Hougaard P & Pipper B. (2015). Testing effect of a drug using nested models for the dose-response. Biometrics 71: 417-427.
- 22. Gutjahr J & Bornkamp B. (2015). Likelihood ratio tests for a dose-response effect using multiple nonlinear models. Technical Report, Cornell University Library. Available at: http://arxiv.org/abs/1510.06253.
- 23. Miller F. (2010). Adaptive dose-finding: Proof of concept with type error control. Biometrical Journal 52: 577-589.
- 24. Tanaka Y. (2011). An adaptive two-stage dose-response design method for establishing proof of concept in drug development. PhD thesis, University of Pittsburgh.
- 25. Franchetti Y, Anderson S & Sampson A. (2013). An adaptive two-stage dose-response design method for establishing proof-of-concept. Journal of Biopharmaceutical Statistics 23: 1124-1154.
- 26. Dragalin V, Bornkamp B, Bretz F, Miller F, Padmanban SK, Patel N, Pereovskaya I, Pinheiro J & Smith JR. (2010). A simulation study to compare new adaptive dose-ranging designs. Statistics in Biopharmaceutical Research 2: 487-512.
- 27. Bornkamp B, Bretz F, Dette H & Pinheiro J. (2011). Response-adaptive dose-finding under model uncertainty. Annals of Applied

