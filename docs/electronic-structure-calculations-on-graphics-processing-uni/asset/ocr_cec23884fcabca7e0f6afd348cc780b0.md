# 14

# Perturbative Coupled-Cluster Methods on Graphics Processing Units: Single- and Multi-Reference Formulations

Wenjing Ma¹, Kiran Bhaskaran-Nair², Oreste Villa³, Edoardo Aprà², Antonino Tumeo⁴, Sriram Krishnamoorthy⁴ and Karol Kowalski²

¹Institute of Software, Chinese Academy of Sciences, Beijing, China ²William R. Wiley Environmental Molecular Sciences Laboratory, Battelle, Pacific Northwest National Laboratory, Richland, WA, USA ³Nvidia, Santa Clara, CA, USA ⁴Computational Sciences and Mathematics Division, Pacific Northwest National Laboratory, Richland, WA, USA

In this chapter, we discuss the implementation of perturbative coupled-cluster methods on graphics processing units and their implementation within the NWChem quantum chemistry software package. Both single and multi-reference formulations are discussed with the background theory provided for both. This is followed by an overview of the NWChem software architecture and how coupled-cluster methods are handled on GPUs within the global arrays framework that the NWChem software uses. We talk about specific optimizations used to improve performance of the GPU implementation as well as the specifics of the hybrid CPU–GPU (central processing unit–graphics processing unit approach that we employ. Finally, we show performance for CCSD(T) and MRCCSD(T) on GPU cluster and HPC hardware.