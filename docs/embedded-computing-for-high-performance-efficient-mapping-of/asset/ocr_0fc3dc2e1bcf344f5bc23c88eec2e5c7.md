```
1. import xilinx;
2. expectsdofs
3.
4.     aspectdef All("^filter_subband", "vhdl");
5.     call b:simul("^filter_subband");
6.     println("RESULT:");
7.     print("Execution Time: *"+lat);
8.     var lat = @design.filter_subband_kernel.latency;
9.     println("####### Number of clock cycles: *"+lat);
10.    call C:xilinx("^filter_subband");
11.    print("Execution Time: *"+lat|C:MaxFreq|*" us");
12. end
```

FIG. 3.42
An example using the LARA run action to invoke different tools and reporting the results considering performance.

```
1. import xilinx;
2. expectsdof olUnrollKInnerloops1 modular
3.
4.     var confs = {}; var best_lat = Number.MAX_VALUE;
5.     var best_conf; var exploreParam = ["*", "*", "*", "*", "*"];
6.     for(var i=0; i<exploreParam[0].length; i++){
7.         call A:compile("^filter_subband", "vhdl", "UnrollKInnerloops1_inner",
8.             call b:simul("^filter_subband", "-arg=" + exploreParam[i] + ")"););
9.         call b:simul("^filter_subband");
10.        println("RESULT:");
11.        printObject(@design);
12.        print("Execution Time: *"+lat);
13.        var lat = @design.filter_subband_kernel.latency;
14.        confs.push({lat:lat, conf:exploreParam[i]});
15.        if(lat < best_lat){
16.            best_lat = lat;
17.            best_conf=exploreParam[i];
18.        }
19.    }
20.    println("####### Number of clock cycles: *"+lat);
21.    println("best lat: *"+ best_lat + " * best conf: " + best_conf );
22.    println("Design points and correspondent no. of clock cycles:");
23.    printObject(confs);
24. end
```

FIG. 3.43
An example using the LARA run action iteratively.

# 3.5.6 COMPILATION AND SYNTHESIS STRATEGIES IN LARA

The compilation and synthesis strategies in LARA include code transformations, exploration of parameters, and specification of complementary program knowledge that can be conveyed to other compilation tools in producing better quality code. As mentioned in Chapter 1, the use of LARA in this book intends to fulfill two goals: (1) to provide a specification of code transformations and optimization strategies and (2) as a DSL to be used in experiments regarding learning activities. Goal (2) has focused on using specific tools with LARA support, namely, the following tools: