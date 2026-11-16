
- 8.7.1 Expected Value of Perfect Information ...... 249
- 8.7.2 Expected Value of Imperfect Information ...... 252
- 8.8 Discussion and Further Reading ...... 253
- 8.8.1 Academics ...... 254
- 8.8.2 Business and Finance ...... 254
- 8.8.3 Capital Equipment ...... 254
- 8.8.4 Computer Games ...... 254
- 8.8.5 Computer Vision ...... 254
- 8.8.6 Computer Software ...... 255
- 8.8.7 Medicine ...... 255
- 8.8.8 Natural Language Processing ...... 256
- 8.8.9 Planning ...... 256
- 8.8.10 Psychology ...... 256
- 8.8.11 Reliability Analysis ...... 256
- 8.8.12 Scheduling ...... 256
- 8.8.13 Speech Recognition ...... 256
- 8.8.14 Vehicle Control and Malfunction Diagnosis ...... 257

## III Emergent Intelligence ...... 265

## 9 Evolutionary Computation ...... 267

- 9.1 Genetics Review ...... 268
- 9.2 Genetic Algorithms ...... 270
- 9.2.1 Algorithm ...... 271
- 9.2.2 Illustrative Example ...... 271
- 9.2.3 Traveling Salesperson Problem ...... 274
- 9.3 Genetic Programming ...... 284
- 9.3.1 Illustrative Example ...... 285
- 9.3.2 Artificial Ant ...... 288
- 9.3.3 Application to Financial Trading ...... 291
- 9.4 Discussion and Further Reading ...... 294

## 10 Swarm Intelligence ...... 297

- 10.1 Ant System ...... 298
- 10.1.1 Real Ant Colonies ...... 298
- 10.1.2 Artificial Ants for Solving the TSP ...... 298
- 10.2 Flocks ...... 302
- 10.3 Discussion and Further Reading ...... 306

## IV Learning ...... 309

## 11 Learning Deterministic Models ...... 311

- 11.1 Supervised Learning ...... 312
- 11.2 Regression ...... 312
- 11.2.1 Simple Linear Regression ...... 312
- 11.2.2 Multiple Linear Regression ...... 315
- 11.2.3 Overfitting and Cross Validation ...... 317
- 11.3 Learning a Decision Tree ...... 319
- 11.3.1 Information Theory ...... 321
- 11.3.2 Information Gain and the ID3 Algorithm ...... 323
- 11.3.3 Overfitting ...... 326

## 12 Learning Probabilistic Model Parameters ...... 331

- 12.1 Learning a Single Parameter ...... 332
- 12.1.1 Binomial Random Variables ...... 332
- 12.1.2 Multinomial Random Variables ...... 335
- 12.2 Learning Parameters in a Bayesian Network ...... 336
- 12.2.1 Procedure for Learning Parameters ...... 337
- 12.2.2 Equivalent Sample Size ...... 339
- 12.3 Learning Parameters with Missing Data★ ...... 341

## 13 Learning Probabilistic Model Structure ...... 351

- 13.1 Structure Learning Problem ...... 352
- 13.2 Score-Based Structure Learning ...... 353
- 13.2.1 Bayesian Score ...... 353
- 13.2.2 BIC Score ...... 360
- 13.2.3 Consistent Scoring Criteria ...... 362
- 13.2.4 How Many DAGs Must We Score? ...... 362
- 13.2.5 Using the Learned Network to Do Inference ...... 363
- 13.2.6 Learning Structure with Missing Data★ ...... 364
- 13.2.7 Approximate Structure Learning ...... 373
- 13.2.8 Model Averaging ...... 377
- 13.2.9 Approximate Model Averaging★ ...... 380
- 13.3 Constraint-Based Structure Learning ...... 383
- 13.3.1 Learning a DAG Faithful to P ...... 383
- 13.3.2 Learning a DAG in which P Is Embedded Faithfully ...... 389
- 13.4 Application: MENTOR ...... 390
- 13.4.1 Developing the Network ...... 390
- 13.4.2 Validating MENTOR ...... 394
- 13.5 Software Packages for Learning ...... 394
- 13.6 Causal Learning ...... 394
- 13.6.1 Causal Faithfulness Assumption ...... 395
- 13.6.2 Causal Embedded Faithfulness Assumption ...... 397
- 13.6.3 Application: College Student Retention Rate ...... 401
- 13.7 Class Probability Trees ...... 404
- 13.7.1 Theory of Class Probability Trees ...... 405
- 13.7.2 Application to Targeted Advertising ...... 407
- 13.8 Discussion and Further Reading ...... 410
- 13.8.1 Biology ...... 410
- 13.8.2 Business and Finance ...... 411
- 13.8.3 Causal Learning ...... 411
- 13.8.4 Data Mining ...... 411
- 13.8.5 Medicine ...... 411
- 13.8.6 Weather Forecasting ...... 412

## 14 More Learning ...... 417

- 14.1 Unsupervised Learning ...... 417
- 14.1.1 Clustering ...... 418
- 14.1.2 Automated Discovery ...... 419
- 14.2 Reinforcement Learning ...... 420
- 14.2.1 Multi-Armed Bandit Algorithms ...... 420
- 14.2.2 Dynamic Networks* ...... 423
- 14.3 Discussion and Further Reading ...... 436

## V Language Understanding ...... 439

## 15 Natural Language Understanding ...... 441

- 15.1 Parsing ...... 442
- 15.1.1 Recursive Parser ...... 445
- 15.1.2 Ambiguity ...... 447
- 15.1.3 Dynamic Programming Parser ...... 449
- 15.1.4 Probabilistic Parser ...... 454
- 15.1.5 Obtaining Probabilities for a PCFG ...... 456
- 15.1.6 Lexicalized PCFG ...... 456
- 15.2 Semantic Interpretation ...... 458
- 15.3 Concept/Knowledge Interpretation ...... 460
- 15.4 Information Extraction ...... 461
- 15.4.1 Applications of Information Extraction ...... 462
- 15.4.2 Architecture for an Information Extraction System ...... 463
- 15.5 Discussion and Further Reading ...... 464

## Bibliography ...... 467

## Index ...... 493

## Chapter 1

## Introduction to Artificial Intelligence

![](img/67fa924962ee21b3590be9f3b10d9fe7_14_0.png)

In 1990, I (Richard Neapolitan) was relatively new to the field of **Artificial Intelligence** (**AI**). At the *6th Conference on Uncertainty in Artificial Intelligence*, which was held at MIT, I met Eugene Charniak, who at the time was a well-known researcher in AI. During a conversation while strolling along the campus, I said, “I heard that the Japanese are applying fuzzy logic to AI.” Gene responded “I don’t believe the Japanese have been any more successful at AI than us.” This comment substantiated that which I had already begun to realize, namely that AI seemed to be a dismal failure.

Dr. Charniak’s comment was correct in 1990 and it is still correct today. If we consider AI to be the development of an artificial entity such as the Termi-
