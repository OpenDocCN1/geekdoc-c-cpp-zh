
```c
#define sizeX 350
#define sizeY 350

void smooth(short IN[sizeX][sizeY], short OUT[sizeX][sizeY]) {
    short K[3][3] = { {1, 2, 1}, {2, 4, 2}, {1, 2, 1}};
    L1: for (int i = 1; i < sizeX-2; i++) {
    L2:     for (int j = 1; j < sizeY-2; j++) {
#pragma HLS PIPELINE II=1
        int sum = 0;
        L3:     for (int r=0; r < 3; r++) {
        L4:         for (int c = 0; c < 3; c++) {
            sum += IN[i+r-1][j+c-1]*K[r][c];
        }
    }
    sum = sum / 16;
    OUT[i-1][j-1] = (short) sum;
    }
}
```

### FIG. 7.12

Smooth image operator example after applying the strategy to select the loop for the pipeline directive.

```
1. aspect_def strategy2_v4/avivadoHLS
2.
3. input
4.   functName = "smooth",
5.   threshold = 100 // threshold to decide about fully unrolling
6. end
7.
8. /* Select each loop nest starting at the loop nest root */
9. select function(functName=loop[isoutermost=true]) end
10. apply
11.   var lookPerfected = true;
12.   var unroll = false;
13.   var currentLoop = $loop;
14.   do {
15.     if(lookPerfected) {
16.       seqLoops.push(currentLoop);
17.       call B: PerfectedNestedLoops(seqLoops) {
18.         if(isPerfect && (seqLoops.length > 2)) {
19.           call InsertPragma(currentLoop, "loop_flatten");
20.           "pragma HLS LOOP_FLATTEN");
21.         }
22.         lookPerfected = false; // at this point the strategy decides about
23.         }
24.       } else {
25.         // calling aspect to determine the cost when fully unroll the loop
26.         call CostfullyUnrollAll(currentLoop);
27.         if(cost > threshold) {
28.           call InsertPragma(currentLoop, "pragma HLS UNROLL");
29.         }
30.       }
31.       call child: getChildLoop(currentLoop);
32.       currentLoop = child.$loop;
33.     } while(currentLoop != undefined);
34. end
```

### FIG. 7.13

A LARA example to select a loop and to apply loop flattening and full loop unrolling.

```c
#define sizeX 350
#define sizeY 350

void smooth(short IN[sizeX][sizeY], short OUT[sizeX][sizeY]) {
    short KC[3][3] = {{1, 2, 1}, {2, 4, 2}, {1, 2, 1}};
    int sum;
    L1: for (int i = 0; i < sizeY; i++) {
        L2: for (int r = 1; r < sizeX-1; r++) {
#pragma HLS LOOP_FLATTEN
        int sum = 0;
        L3: for (int r = 0; r < 3; r++) {
#pragma HLS UNROLL
        L4: for (int c = 0; c < 3; c++) {
#pragma HLS UNROLL
        }
        sum += IN[i+r][c]*KC[r][c];
        }
        sum = sum / 16;
        OUT[r+1][i+1] = (short) sum;
        }
    }
}
```

### FIG. 7.14

Smooth image operator example after applying the strategy to select the loop for the loop flattening directive and to consider loop unrolling for the other loops.

When this second strategy is applied to the smooth image operator example we obtain the code in Fig. 7.14, which includes the LOOP_FLATTEN and the UNROLL directives specified using C pragmas.

One of the key aspects of using LARA is that strategies can be extended or combined, thus increasing their transformational power and scope of applicability. This is clearly illustrated in the LARA strategy described earlier, which can be easily extended to consider loop pipelining in addition to the loop unrolling transformation.

## 7.7 SUMMARY

This chapter expanded the topics on code retargeting for heterogeneous computing platforms, mainly leveraging the use of hardware accelerators such as GPUs and FPGAs. Special attention has been given to OpenCL and high-level synthesis (HLS) which translates C descriptions to hardware designs. The chapter revisited the roofline model and other performance models that aim at helping programmers with issues such as workload distribution and offloading computation to accelerators.

## 7.8 FURTHER READING

An excellent overview about reconfigurable computing is the book of Hauck and DeHon [5]. With respect to compilation to reconfigurable fabrics (such as FPGAs) the surveys presented in Refs. [6,7] provide a good starting point. A summary of the main high-level synthesis stages is presented in Ref. [8] but for a more in-depth description we suggest the book by Gajski et al. [13]. Readers interested in specific HLS tools can start by learning about LegUp [14], an available academic tool [9]. A recent survey comparing available HLS tools targeting FPGAs can be found in Ref. [26]. The impact of compiler optimizations on the generation of FPGA-based hardware is described in Ref. [27]. Details of the use of the Xilinx Vivado HLS tool are presented in Ref. [12] and the tutorials provided by Xilinx are important material source for beginner users of Vivado HLS.

For an introduction to the OpenCL programming model and its computing platform we suggest the material in Refs. [3,4]. Recent industrial development efforts on using OpenCL as the input programming model and underlying computing platform for FPGAs can be found in Refs. [19,20].

## REFERENCES

- [1] Williams S, Waterman A, Patterson D. Roofline: an insightful visual performance model for multicore architectures. Commun ACM 2009;52(4):65–76.
- [2] Hawes S. The roofline model. In: Bailey DH, Lyons RF, Williams S, editors. Performance tuning of scientific applications. Chapman & Hall/CRC Computational Science. Boca Raton, FL, USA: CRC Press; 2010. p. 195–215.
- [3] Howes L, editor. The OpenCL specification. Version: 2.1. document revision: 23. Khronos OpenCL Working Group. Last revision date: November 11, 2015. https://www.khronos.org/registry/cl/specs/opencl-2.1.pdf.
- [4] Kaeli DR, Mistry P, Schaa D, Ping Zhang D. Heterogeneous computing with OpenCL 2.0. 1st ed. San Francisco, CA: Morgan Kaufmann Publishers Inc.; 2015.
- [5] Hauck S, DeHon A. Reconfigurable computing: the theory and practice of FPGA-based computation. 1st ed. San Francisco, CA: Morgan Kaufmann Publishers Inc.; 2007.
- [6] Compton JMP, Pedro C. D. Coarse-grained reconfigurable architectures. New York, NY, USA: Springer; Oct. 2008.
- [7] Cardoso JMP, Diniz P. Weinhardt M. Compiling for reconfigurable computing: a survey. ACM Comput Surv 2010;42(4):1–65. Article 13.
- [8] Cardoso JMP, Weinhardt M. High-level synthesis. In: Koch D, Hannig F, Ziener D, editors. FPGAs for software engineers. New York, NY, USA: Springer; 2016. p. 23–48 (Chapter 2).
- [9] Guo Z, Najjar W, Buyukturun B. Efficient hardware code generation for FPGAs. ACM Trans Archit Code Optim 2008;5(1). Article 6, 26 pages.
- [10] Cong J, Liu B, Neuendorffer S, Noguera J, Vissers K, Zhang Z. High-level synthesis for FPGAs: from prototyping to deployment. IEEE Trans CAD Integr Circuits Syst 2011;30(4):473–91.
- [11] De Micheli G. Synthesis and optimization of digital circuits. 1st ed. New York, NY, USA: McGraw-Hill Higher Education; 1994.
- [12] Xilinx Inc. Vivado design suite user guide. High-level synthesis. UG902 (v2016.3) October 5, 2016.
- [13] Gajski D, Dutt N, Wu A, Lin S. High-level synthesis: introduction to chip and system design. Norwell, MA: Kluwer Academic Publishers; 1992.
- [14] Canis A, Choi J, Aldham M, Zhang V, Kammoona A, Czajkowski T, et al. LegUp: an open-source high-level synthesis tool for FPGA-based processor/accelerator systems. ACM Trans Embed Comput Syst 2013;13(2): Article 24, 27 pages.
- [15] Xilinx Inc. http://www.xilinx.com [Accessed October 2016],
- [16] Fingerhoff M. High-level synthesis blue book. Bloomington, IN, USA: Xlibris Corporation; 2010,
- [17] Impulse Accelerated Technologies, Inc. http://www.impulseaccelerated.com/ [Accessed in November 2016],
- [18] Pellerin D, Thibault S. Practical FPGA programming in C. 1st ed. Upper Saddle River, NJ: Prentice Hall Press; 2005,
- [19] Xilinx Inc. SDAccel environment user guide. UG1023 (v2016.3). November 30 2016,
- [20] Intel Inc. SDAccel FPGA SDK for OpenCL getting started guide. UG-OCL-001, 2016.10.31. Last updated for Quartus Prime Design Suite: 16.1,
- [21] Intel Corp. FPGA devices. http://www.intel.com/content/www/us/en/fpga/devices.html,
- [22] Pell O, Mencer O. Surviving the end of frequency scaling with reconfigurable dataflow computing. SIGARCH Comput Archit News 2011;39(4):60–5,
- [23] Pell O, Averbuch V. Maximum performance computing with dataflow engines. Comput Sci Eng 2012;14(4):98–103,
- [24] Mei B, Vernalde S, Verkest D, Lauwereins R. Design methodology for a tightly coupled VLIW/reconfigurable matrix architecture: a case study. In: Proceedings of the conference on design, automation and test in Europe (DATE’04), vol. 2. Washington, DC: IEEE Computer Society; 2004. p. 1224–9,
- [25] Hartenstein R. Coarse grain reconfigurable architecture (embedded tutorial). In: Proc. of the 2001 Asia and South Pacific design automation conf. (ASP-DAC’01). New York, NY: ACM; 2001. p. 564–70,
- [26] Nane R, Mihai Sima V, Pilato C, Choi J, Fort B, Canis A, et al. A survey and evaluation of FPGA high-level synthesis tools. IEEE Trans CAD Integr Circuits Syst 2016;35(10):1591–604,
- [27] Huang Q, Lian R, Canis A, Choi J, Xi R, Calagar N, et al. The effect of compiler optimizations on high-level synthesis-generated hardware. ACM Trans Reconfig Technol Syst 2015;8(3). Article 14, 26 pages.
