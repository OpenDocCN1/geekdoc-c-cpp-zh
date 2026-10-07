# Document Clustering: The Next Frontier

![](bbox=[0.131, 0.07, 0.868, 0.25])

**FIGURE 13.7:** Plate notation for the $\alpha$-DLDA (a) and $\gamma$-DLDA (b) generative models.

simultaneous training of two LDA models, the **target** model on the short texts and the **auxiliary** model on the long ones.

Depending on how the models are related to each other, Jin et al. [55] propose two sets of topics for auxiliary and target data and asymmetric Dirichlet priors to control the relative importance of when generating a document. $\alpha'$ is given higher values for entries associated with auxiliary topics. $\gamma$-DLDA introduces a document-binary switch that constraints each document to be generated from either the target model or from the auxiliary. In addition to the multinomial distributions over topics, each document is also associated with a multinomial distribution over target or auxiliary topics with a Beta prior $\gamma$. Similar to a parameter in $\alpha$-DLDA, $\gamma$ is given higher values for entries associated with target topics. Figure 13.7 (b) depicts the plate notation for the $\gamma$-DLDA model, whose generation for each document is detailed below.

+   1. For each target topic, generate a multinomial distribution over terms, $\beta'_k \sim Dir_M(\\eta')$, $k \in \{1, \dots, K^*\}$
2. For each auxiliary topic, generate a multinomial distribution over terms, $\beta''_k \sim Dir_M(\\eta'')$, $k \in \{1, \dots, K^*\}$
3. For each corpus (auxiliary and target data), $c \in \{a, t\}$
   a. For each corpus document $d_i$, $i \in \{1, \dots, N^c\}$
      i. Generate a multinomial distribution over target topics, $\theta'_i \sim Dir_K(\\alpha')$
      ii. Generate a multinomial distribution over auxiliary topics, $\theta''_i \sim Dir_K(\\alpha'')$
      iii. Generate a multinomial distribution over target, auxiliary topics, $\pi_i \sim Beta(\\gamma)$
      iv. For each word $w_{ij}$ in document $d_i$:n         1. Choose a value for $x_{ij} \sim Binomial(\\pi_i)$
         2. If $x_{ij}=t$, choose a target topic $z_{ij} \sim Multi(\	heta'_i)$
         3. If $x_{ij}=a$, choose an auxiliary topic $z_{ij} \sim Multi(\	heta''_i)$
         4. Choose word $w_{ij}$ from topic $z_{ij}$, i.e., $w_{ij} \sim Multi(\eta_{z_{ij}})$

Jin et al. [55] compare their DL algorithms against direct clustering with CLUTO, topic model-based clustering on the individual collections and against several algorithms that transfer knowledge from the long texts when clustering the short. While $\alpha$-DLDA and $\gamma$-DLDA outperformed the competition, the authors also note that methods utilizing long texts performed significantly better than the others, demonstrating the value of external information when noisy short documents.