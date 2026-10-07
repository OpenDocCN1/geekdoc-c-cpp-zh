# PERFORMING A LOGISTIC ANALYSIS USING PROC LOGISTIC 363

TABLE 16.1 Common Options for PROC LOGISTIC
| Option | Explanation |
| | | |
| DATA = dataname DESCENDING | Specifies which data set to use reverses the sorting order for the levels of the response variable. By default, the procedure will predict the outcome corresponding to the lower value of the dichotomous-variable. So, if the dependent variable takes the values 0 and 1, then by default SAS predicts the probability that the dependent variable is 0 unless you use the DESCENDING option. (See information about the EVENT= option below.) |
| EVENT='option' | Specifies which value of a binary response variable is treated as the one modeled. For example, the left of the equal in a MODEL statement DEATH='Event'1'. | |
| ALPHA= value NOPRINT | Specifies significance level confidence limits suppresses output | |
| SIMPLE PLOTS= option | Displays descriptive statistics In current views of SAS, the Odds Ratio is displayed by default. Use PLOTS=NONE to suppress this plot. PLOTS=ALL produces a number of plots including receiver-operating characteristic (ROC) and influencing diagnostics |

# Common statements for PROC LOGISTIC

| MODEL devar=indvar(s); | Specifies the dependent and independent variables for the analysis. More specifically, it takes the form MODEL dependentvariable=independentvariable(s); More explanation follows |
| CLASS variable list; | Specifies classification (either categorical character or discrete numeric) variables for the analysis. They can be numeric or including the option REF='value'. You can specify a reference value for a class variable by character. For example, CLASS RACE (REF='HISPANIC') URBAN; Specifies HISPANIC as the reference value to RACE. For URBAN the reference value will be the last ordered (alphabetic or numeric) value |
| ODDSRATIO 'label' var; | Creates a table with odds ratio estimates and Wald confidence intervals. For example, ODDSRATIO='Injury' ISS; ODDSRATIO='Age' AGE; |
| OUTPUT out=NAME; | Creates an output data with all predictors and response probabilities. For example, OUTPUT=MYFILE P=PRED; where MYFILE is the name of the resulting data and the predictions are named PRED |

BY, FORMAT, LABEL, WHERE These statements are common to most procedures and may be used here