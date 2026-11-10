
series are sampled at the rate of 10 Hertz. The length of the time series for each day is 864,000. The data was analyzed separately for each month. The frequency data are preprocessed using the *k*-Medians approach with *k* set to 5.

The allowance value (*k*) for the CUSUM algorithm is set to 1, the minimum shift (μ) to be detected is set to 0.05, and the in-control distribution mean (μ₀) is 0. An anomalous event is defined as a subsequence of a month-long time series in which the CUSUM statistic is greater than zero. Based on an understanding of the domain, an anomalous event is considered *significant* if it lasts for at least 2 seconds (20 observations).

### 9.5.2.2 *Raw Results*

Table 9.1 summarizes the number of significant anomalous events identified for each of the sensors for May 2008 and June 2008. The results show that for all the FDRs, the fraction of time in which the system is in an anomalous state is a small fraction of the total time, but that fraction itself can be a large number. For example, FDR 11 in Grand Rapids, MI, was in an anomalous state, 0.0082 fraction of the total time, approximately 200,000 observations. However, the number of significant anomalous events for each sensor for a month is not more than 119.

TABLE 9.1 Summary Statistics for CUSUM-Based Anomaly Detection Output for Different FDRs

| FDR # | Location | State | May 2008 Fraction Alarms | May 2008 No. Anomalous Events | June 2008 Fraction Alarms | June 2008 No. Anomalous Events |
|---:|---|:---:|---:|---:|---:|---:|
| 11 | Grand Rapids | MI | 0.0082 | 117 | 0.0094 | 115 |
| 13 | Carmel | IN | 0.0081 | 115 | 0.0095 | 113 |
| 38 | Holyoke | MA | 0.007 | 97 | 0.0093 | 106 |
| 40 | St Paul | MN | 0.008 | 116 | 0.0092 | 111 |
| 42 | Tallahassee | FL | 0.0081 | 116 | 0.0095 | 116 |
| 510 | Blacksburg | VA | 0.0038 | 64 | 0.0046 | 85 |
| 513 | State College | PA | 0.0082 | 119 | 0.0095 | 113 |
| 514 | Simpsonville | SC | 0.0009 | 16 | 0.0005 | 13 |
| 516 | Rochester | NY | 0.0056 | 88 | 0.009 | 108 |
| 519 | Newport News | VA | 0.0034 | 53 | 0.0034 | 37 |
| 521 | Chillicothe | OH | 0.0076 | 117 | 0.0058 | 71 |
| 523 | Oak Ridge | TN | 0.0033 | 43 | 0.0019 | 19 |
| 526 | Birmingham | AL | 0.0082 | 118 | 0.0095 | 113 |
| 560 | Duluth | MN | 0.0068 | 92 | 0.0079 | 90 |
| 561 | Madison | WI | 0.0081 | 119 | 0.0095 | 115 |
| 566 | Gulfport | MS | 0.0081 | 116 | 0.0095 | 113 |
| 568 | Montgomery | AL | 0.0082 | 117 | 0.0095 | 113 |
| 570 | Atlanta | GA | 0.0082 | 118 | 0.004 | 54 |
| 571 | Pensacola | FL | 0.0082 | 118 | 0.0095 | 111 |
| 596 | Cookeville | TN | 0.0067 | 93 | 0.0062 | 69 |
| 597 | Cookeville | TN | 0.0067 | 92 | 0.0056 | 66 |

Evaluation of the output of the anomaly detector is a challenge, given the lack of ground truth data about the grid-related events for that time period. A possibility is to examine the local news sources for the specific days of the events, although that process can be expensive, as well as not guaranteed to cover every grid event. To further consolidate the output, a *spatial co-location constraint* can be applied, as discussed below.

### 9.5.2.3 *Incorporating Spatial Information*

Electric grid events (such as outages, trips) typically have a cascading effect. Hence, a grid event must manifest itself in data collected at spatially co-located sensors. Table 9.2 shows the number of significant events identified by the CUSUM-based anomaly detection system for each sensor, while taking the spatial information into consideration. Thus, an alarm raised at a sensor is considered “true” if it was also raised by the neighboring sensors (eight for this study). The number of significant events is reduced by incorporating the spatial information. While one cannot infer that the events that are thus ignored are not useful, this approach does allow a reduced set for further analysis.

The data have already been centered using the *k*-Medians approach by using the medians as centers to shift the subset of data.

As shown in Table 9.2, the number of significant events is sharply reduced to 143 by taking the spatial context into account. While the real benefit of this approach can be validated only by confirming that the detected events are indeed beneficial in terms of identifying the actual events, the lack of availability of reliable ground truth regarding grid events makes the validation challenging. At the time of writing this chapter, the detected events were being validated through a manual process, the results of which will be documented in future publications.

TABLE 9.2 Number of Significant Events for Spatially Aware CUSUM-Based Anomaly Detection Output for Different FDRs

| FDR # | Location | State | May 2008 | June 2008 |
|---|---|---|---|---|
| 11 | Grand Rapids | MI | 8 | 8 |
| 13 | Carmel | IN | 5 | 6 |
| 38 | Holyoke | MA | 0 | 0 |
| 40 | St Paul | MN | 8 | 8 |
| 42 | Tallahassee | FL | 0 | 0 |
| 510 | Blacksburg | VA | 0 | 0 |
| 513 | State College | PA | 0 | 0 |
| 514 | Simpsonville | SC | 0 | 0 |
| 516 | Rochester | NY | 0 | 0 |
| 519 | Newport News | VA | 0 | 0 |
| 521 | Chillicothe | OH | 0 | 0 |
| 523 | Oak Ridge | TN | 0 | 0 |
| 526 | Birmingham | AL | 9 | 8 |
| 560 | Duluth | MN | 8 | 8 |
| 561 | Madison | WI | 8 | 8 |
| 566 | Gulfport | MS | 9 | 8 |
| 568 | Montgomery | AL | 9 | 8 |
| 570 | Atlanta | GA | 0 | 0 |
| 571 | Pensacola | FL | 9 | 8 |
| 596 | Cookeville | TN | 0 | 0 |
| 597 | Cookeville | TN | 0 | 0 |

## 9.6 CONCLUSIONS

Data mining has immense significance in terms of addressing several key power grid problems, specifically in the arena of rapid event detection, as discussed in this chapter, which have the potential of going a long way in terms of realizing the promised benefits of the smart grid. The key challenges associated with this domain, in terms of data analysis, are the massive nature of the data and the short reaction time allowed (on the order of a few seconds) for allowing adequate response. The analytic solutions proposed in this chapter focus primarily on simple analyses that can be scaled to the data sizes and the high sampling rate of the incoming power signal. In the future, as the synchrophasors become more and more advanced (both in terms of sampling rate as well as the number of deployed sensors across the country), more research will be required to make the data analysis solutions scalable.

## REFERENCES

- 1. J.N. Bank, O.A. Omitaomu, S.J. Fernandez, and Y. Liu, Visualization and classification of power system frequency data streams, *Proceedings of the IEEE International Conference on Data Mining Workshops*, pp. 650–655, 2009.
- 2. P. Domingos and G. Hulten, Mining high-speed data streams, *Proceedings of the Sixth ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, pp. 71–80, 2000.
- 3. G. Hulten, L. Spencer, and P. Domingos, Mining time-changing data streams, *Proceedings of KDD 2001*, pp. 97–106, 2001.
- 4. D. Kifer, S. Ben-David, and J. Gehrke, Detecting change in data streams, *Proceedings of the 30th VLDB Conference*, pp. 180–191, 2004.
- 5. L. O'Callaghan, N. Mishra, A. Meyerson, S. Guha, and R. Motwani, Streaming data algorithms for high-quality clustering, *Proceedings of the 18th International Conference on Data Engineering*, 2002.
- 6. B. Qiu, L. Chen et al. Internet-based frequency monitoring network (FNET), *IEEE Power Engineering Society, Winter Meeting*, 2001. Vol. 3, 28 Jan.–1 Feb. 2001, pp. 1166–1171.
- 7. J.K. Wang, R.M. Gardner, and Y. Liu, Analysis of system oscillations using wide-area measurements, *IEEE Power Engineering Society, General Meeting*, 2007, 25 June–28 June 2007.
- 8. J.N. Bank, O.A. Omitaomu, S.J. Fernandez, and Y. Liu, Extraction and visualization of power system inter-area oscillatory modes, *Proceedings of the IEEE Power & Energy Society Annual Meeting*, Minneapolis, MN, July 25–29, 2010.
- 9. N.E. Huang, Z. Shen, S.R. Long, M.C. Wu, S.H. Shih, Q. Zheng, C.C. Tung, and H.H. Liu, The empirical mode decomposition method and the Hilbert spectrum for non-stationary time series analysis, *Proceedings of the Royal Society of London*, A454: 903–995, 1998.
- 10. H. Liang, Z. Lin, and R.W. McCallum. Artifact reduction in electrogastrogram based on the empirical mode decomposition method, *Medical & Biological Engineering & Computing*, 38: 35–41, 2000.
- 11. A.K. Jain and R.C. Dubes, *Algorithms for Clustering Data*. Prentice-Hall, Englewood Cliffs, NJ, 1981.
- 12. N.E. Huang, M.-L. Wu, W. Qu, S.R. Long, and S.P. Shen. Applications of Hilbert–Huang transform to non-stationary financial time series analysis, *Applied Stochastic Models in Business and Industry*, 19: 245–268, 2003.
- 13. S.T. Quek, P.S. Tua, and Q. Wang. Detecting anomalies in beams and plate based on the Hilbert–Huang transform of real data, *Smart Materials and Structures*, 12: 447–460, 2003.
- 14. Z. Zhong, C. Xu, et al. Power system Frequency Monitoring Network (FNET) implementation, *IEEE Trans. on Power Systems*, 20(4): 1914–1921, 2005.
- 15. T.K. Sarkar and O. Pereira. Using the matrix pencil method to estimate the parameters of a sum of complex exponentials, *IEEE Antennas and Propagation Magazine*, 37(1): 48–55, 1995.
