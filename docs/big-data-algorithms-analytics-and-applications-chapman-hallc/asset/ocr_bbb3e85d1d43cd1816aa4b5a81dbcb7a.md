# GEMS: Graph Database Engine for Multithreaded Systems

Alessandro Morari, Vito Giovanni Castellana, Oreste Villa, Jesse Weaver, Greg Williams, David Haglin, Antonino Tumeo, and John Feo

# CONTENTS

+   8.1 Introduction 140
+   8.2 Related Infrastructures 141
+   8.3 GEMS Overview 142
+   8.4 GMT Architecture 146
+   8.4.1 GMT: Aggregation 148
+   8.4.2 GMT: Fine-Grained Multithreading 149
+   8.5 Experimental Results 150
+   8.5.1 Synthetic Benchmarks 151
+   8.5.2 BSBM 152
+   8.5.3 RDESC 153
+   8.6 Conclusions 155
+   References 155

# ABSTRACT

Many fields require organizing, managing, and analyzing massive amounts of data. Among them, we can find social network analysis, financial risk management, threat detection in complex network systems, and medical and biomedical databases. For these areas, there is a problem not only in terms of size but also in terms of performance, because the processing should happen sufficiently fast to be useful. Graph databases appear to be a good candidate to manage these data: They provide an