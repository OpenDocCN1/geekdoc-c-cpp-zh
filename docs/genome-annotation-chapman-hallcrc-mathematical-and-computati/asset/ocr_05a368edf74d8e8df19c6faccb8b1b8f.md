# Visualization Techniques and Tools for Genomic Data

![](bbox=[0.137, 0.093, 0.863, 0.419])

FIGURE 6.7 MeV display of nine expression profile plots, showing the result of clustering genes based on expression values over four different tissues. In each profile, the darkest grey line (excluding the midline) represents the mean profile of genes in the cluster.

variation in the first three components. Scatter plots are good for obtaining a first insight into the general characteristics of the data, by the chief drawback is that the plotted data points cannot be mapped back to the observed data (e.g., to extract corresponding experimental conditions), as they have already gone through an irreversible dimensionality reduction procedure.

# 6.5.2 Visualization for Biological Interpretation

The visualization techniques described so far focus on gene expression data only, without showing any information on the biological meaning that the expression profiles might imply. A new direction in gene analysis is to link gene expression profiles to the functional annotation of genes. To achieve this, in essence expression profiles are mapped to functional profiles, such that gene functions are upregulated or downregulated can be shown, in addition to, or instead of simple gene names. Most visualization tools are capable of doing this mapping use the Gene Ontology (GO) to allow the classification of gene function, which offers standardized terminology for gene function annotation.