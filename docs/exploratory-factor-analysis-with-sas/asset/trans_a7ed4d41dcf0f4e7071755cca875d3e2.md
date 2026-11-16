
to use; percent, the percentile to use in determining whether the eigenvalues are significantly above the mean; kind, the type of parallel analysis (1=PCA and 2=factor analysis); randtype, the type of random data to be used (1=from normally distributed random data and 2=random permutations of the raw data); and seed, the seed value to use in computations. You can then run the parallel macro from % parallel ( datafile,ndatasets,percent,kind,randtype,seed ). The syntax to do this for the engineering data is presented below.

```
*Include MAP and PARALLEL ANALYSIS macro syntax for use below;
filename parallel 'C:\Location of File\parallel_macro.sas';
filename map 'C:\Location of File\map_macro.sas';
*include map;
*Run MAP and Parallel Analysis;
%map(engdata);
%parallel(engdata,100,95,2,2,99);
```

The results produced by the O'Connor (2000) MAP analysis are presented in Figure 3.4 on page 42 below. The results show the eigenvalues extracted from the data, the average squared partial correlations, and the average partial correlations to the fourth power. Recall that, using MAP analysis, we want to choose a number of factors where the average partial correlations hits a minimum (the squared partial correlation based on the 1976 criteria and the average partial correlation to the fourth power based on the revised criteria). According to the results, two factors should be retained.

### 图 3.4 MAP 分析结果

### Velicer 最小平均偏相关 (MAP) 检验：

| 特征值 |
| :--- |
| 7.6534 |
| 3.5048 |
| 0.4568 |
| 0.3597 |
| 0.3149 |
| 0.2760 |
| 0.2736 |
| 0.2147 |
| 0.2124 |
| 0.1750 |
| 0.1615 |
| 0.1373 |
| 0.1326 |
| 0.1273 |

### 平均偏相关

| | 平方 | 四次方 |
| :--- | :--- | :--- |
| 0.0000 | 0.3167 | 0.1645 |
| 1.0000 | 0.2458 | 0.0743 |
| 2.0000 | 0.0236 | 0.0018 |
| 3.0000 | 0.0295 | 0.0034 |
| 4.0000 | 0.0436 | 0.0088 |
| 5.0000 | 0.0580 | 0.0119 |
| 6.0000 | 0.0724 | 0.0229 |
| 7.0000 | 0.0926 | 0.0436 |
| 8.0000 | 0.1213 | 0.0511 |
| 9.0000 | 0.1719 | 0.0711 |
| 10.0000 | 0.2175 | 0.1042 |
| 11.0000 | 0.3221 | 0.1816 |
| 12.0000 | 0.4853 | 0.3613 |
| 13.0000 | 1.0000 | 1.0000 |

The smallest average squared partial correlation is

0.0236

The smallest average 4th power partial correlation is

0.0018

The Number of Components According to the Original (1976) MAP Test is

2.0000

The Number of Components According to the Revised (2000) MAP Test is

2.0000

Another way to visualize these results is to plot them. Figure 3.5 on page 43 presents a plot of the average squared partial correlations. As you can see, the inflection point (minimum) on the plot is at 2.

### 图 3.5 工程数据 MAP 检验的平均偏相关图

![](img/29951003f0d11c9d825feb73bff9c8e6_55_0.png)

The results for the parallel analysis are presented in Figure 3.6 on page 44 below. The parallel analysis computed the eigenvalues from the data and then generated a series of comparable sets of random data. The mean eigenvalues across the sets of random data were computed along with the 95th percentile of those values. These values are presented on the right of the figure, in the columns labeled Raw Data, Means, and Prcntyle. Remember, the goal is to select the number of factors whose observed eigenvalues exceed those produced from random data. The current results would recommend two factors be extracted since the raw data eigenvalue goes below the generated mean eigenvalue and 95th percentile eigenvalue among the random data sets at factor 3. Again, we can visualize these results by plotting the mean eigenvalues of the random data against the eigenvalues in the raw data. (See Figure 3.7 on page 44.)

### 图 3.6 并行分析结果

Parallel Analysis:
PAF/Common Factor Analysis & Raw Data Permutation
Specifications for this Run.

| 规范 | 值 |
|---|---|
| Ncases | 372 |
| Nvars | 14 |
| Ndatasets | 100 |
| Percent | 95 |

| 根 | 原始数据 | 均值 | 百分位数 |
|---|---|---|---|
| 1.000000 | 7.411470 | 0.383973 | 0.463048 |
| 2.000000 | 3.271016 | 0.299095 | 0.355149 |
| 3.000000 | 0.197160 | 0.237595 | 0.284848 |
| 4.000000 | 0.069918 | 0.179115 | 0.219735 |
| 5.000000 | 0.048940 | 0.129584 | 0.173288 |
| 6.000000 | 0.039340 | 0.081095 | 0.116472 |
| 7.000000 | 0.021963 | 0.041350 | 0.075104 |
| 8.000000 | -0.013937 | -0.000732 | 0.033558 |
| 9.000000 | -0.032820 | -0.043398 | -0.016535 |
| 10.000000 | -0.046677 | -0.080289 | -0.053319 |
| 11.000000 | -0.071557 | -0.120243 | -0.088454 |
| 12.000000 | -0.082612 | -0.159143 | -0.129139 |
| 13.000000 | -0.097253 | -0.202976 | -0.171653 |
| 14.000000 | -0.108182 | -0.253813 | -0.222440 |

### 图 3.7 工程数据并行分析图

![](img/29951003f0d11c9d825feb73bff9c8e6_56_0.png)

## 标准如何比较？

Now that we are familiar with the different extraction criteria and the SAS syntax and output for each criterion, let's examine the potential differences between the criteria. We will review these criteria in each of our three data sets and see how the criteria agree or disagree.

**工程数据。** 我们在上一节中检查了该数据的每个标准。理论、Kaiser 准则、最小特征值和方差贡献率都推荐两因子解；碎石图推荐两因子解，但也识别出可能的三因子解；MAP 和并行分析都推荐两因子解。一般来说，当我们使用通常具有强两因子结构的量表时，这些方法倾向于得出结论：提取两个因子是最佳数量。鑒于结果在理论模型的背景下是合理的，我们可能会提取两个因子进行旋转和解释。

Before we examine these criteria in the next set of data, let us briefly review how a two-factor extraction of this data affects the subsequent factor loadings. We will examine the unrotated factor loading since we have not yet discussed rotation. The loadings are plotted in Figure 3.8 on page 46 (we requested this plot by adding the INITLOADINGS plot to the PLOTS option, `plots = (initloadings scree)`). As you can see from the factor loading plot, the data is clustered into two clear and distinct factors. In our opinion, this is about as good as it gets in exploratory factor analysis at this stage of the analysis.

### 图 3.8 因子载荷图，迭代 PAF 提取

![](img/29951003f0d11c9d825feb73bff9c8e6_58_0.png)

Self-description questionnaire data. Because the data from the SDQ seemed to be relatively well-behaved across the initial extraction comparisons, we will use ML extraction and explore whether our expected three-factor solution is tenable. Syntax to produce all of results to examine the extraction criteria for this data set is presented below.

```
ods graphics on;
proc factor data = sdgdata method = ML plots = SCREE;
   var Eng: Math: Par:;
run;
ods graphics off;

*Assuming the include statement has already read in the MACROS;
tmap(sdqdata);
*parallel(sdqdata,100,95,2,99);
```

The initial eigenvalues are presented in Figure 3.9 on page 47, and the scree plot is presented in Figure 3.10 on page 48. Theory, the Kaiser Criterion, the minimum eigenvalue, and the proportion of variance suggest the data has a three-factor solution. The scree plot, however, is a little less clear. Scree plots do not always have one clear elbow. In this case, it is possible to argue that any one of several points is the true “elbow” — including 2, 3, 4, or 5. In this example, the scree plot is not terribly informative.

The parallel analysis results are presented in Figure 3.11 on page 48 and Figure 3.12 on page 49 and the MAP analysis results are presented in Figure 3.13 on page 50 and Figure 3.14 on page 51. Because the sample size was so large, parallel analysis might not be as useful. The largest randomly generated eigenvalue (95th percentile) was 0.057. Using the criteria for parallel analysis, one would recommend examining either three or four factors (depending on how “significantly” different the raw data eigenvalue should be). The data from the MAP analysis seems to further reinforce theory and other criteria, indicating that three factors is the right number to extract. As you can see in Figure 3.14 on page 51, the minimum inflection point is at 3.

In summary, theory and the Kaiser Criterion recommend three factors, the scree plot recommends between two and five factors, parallel analysis recommends four, and MAP recommends three factors. As Velicer and others have argued, the MAP appears to be, at least in this case, more congruent with theory and eigenvalues. That is reassuring. The three-factor model seems to be the best recommendation as it makes for a strong, interpretable model.

### 图 3.9 SDQ 数据的特征值

| | 特征值 | 差异 | 比例 | 累积 |
|---|---|---|---|---|
| 1 | 9.07976678 | 3.65235893 | 0.5411 | 0.5411 |
| 2 | 5.42743785 | 1.77049075 | 0.3234 | 0.8645 |
| 3 | 3.65694710 | 2.99021550 | 0.2179 | 1.0825 |
| 4 | 0.66673160 | 0.71076308 | 0.0397 | 1.1222 |
| 5 | -0.4403148 | 0.07803164 | -0.0026 | 1.1196 |
| 6 | -1.2206312 | 0.01122060 | -0.0073 | 1.1123 |
| 7 | -1.3328372 | 0.03628945 | -0.0079 | 1.1044 |
| 8 | -1.6957317 | 0.05296247 | -0.0101 | 1.0942 |
| 9 | -2.2253564 | 0.06266504 | -0.0133 | 1.0810 |
| 10 | -2.8519068 | 0.03336312 | -0.0170 | 1.0640 |
| 11 | -3.1855380 | 0.0849750 | -0.0190 | 1.0450 |
| 12 | -3.2705130 | 0.10111286 | -0.0195 | 1.0255 |
| 13 | -4.2816416 | | -0.0255 | 1.0000 |

3 factors will be retained by the PROPORTION criterion.
