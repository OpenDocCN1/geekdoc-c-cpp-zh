

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

### 图 7.12

应用流水线指令循环选择策略后的平滑图像算子示例。

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

### 图 7.13

选择循环并应用循环展平和完全循环展开的 LARA 示例。

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

### 图 7.14

应用循环展平指令循环选择策略并考虑对其他循环进行循环展开后的平滑图像算子示例。

将此第二策略应用于平滑图像算子示例时，我们得到图 7.14 中的代码，该代码包括使用 C pragma 指定的 LOOP_FLATTEN 和 UNROLL 指令。

使用 LARA 的一个关键方面是策略可以扩展或组合，从而增加其变换能力和适用范围。这在前面描述的 LARA 策略中得到了清楚的说明，该策略可以轻松扩展以在循环展开变换之外考虑循环流水线。

## 7.7 总结

本章扩展了关于异构计算平台代码重定向的主题，主要利用 GPU 和 FPGA 等硬件加速器。特别关注了 OpenCL 和高级综合（HLS），后者将 C 描述转换为硬件设计。本章重新探讨了屋顶线模型和其他性能模型，这些模型旨在帮助程序员解决工作负载分布和将计算卸载到加速器等问题。

## 7.8 进一步阅读

关于可重构计算的出色概述见 Hauck 和 DeHon 的书 [5]。关于编译到可重构结构（如 FPGA），Refs. [6,7] 中的综述提供了良好的起点。Ref. [8] 提供了高级综合主要阶段的摘要，但如需更深入的描述，我们建议阅读 Gajski 等人的书 [13]。对特定 HLS 工具感兴趣的读者可以先了解 LegUp [14]，这是一个可用的学术工具 [9]。一篇比较可用于 FPGA 的 HLS 工具的最新综述可见 Ref. [26]。编译器优化对基于 FPGA 硬件生成的影响在 Ref. [27] 中有描述。Xilinx Vivado HLS 工具的使用细节在 Ref. [12] 中介绍，Xilinx 提供的教程是 Vivado HLS 初学者的重要材料来源。

如需了解 OpenCL 编程模型及其计算平台的介绍，我们建议参考 Refs. [3,4] 中的材料。关于将 OpenCL 用作 FPGA 输入编程模型和底层计算平台的最近工业开发工作可见 Refs. [19,20]。

## 参考文献

- [1] Williams S, Waterman A, Patterson D. 屋顶线：多核架构的深入可视性能模型。Commun ACM 2009;52(4):65–76.
- [2] Hawes S. 屋顶线模型。In: Bailey DH, Lyons RF, Williams S, 编. 科学应用性能调优。Chapman & Hall/CRC 计算科学。Boca Raton, FL, USA: CRC Press; 2010. p. 195–215.
- [3] Howes L, 编. OpenCL 规范。版本：2.1。文档修订版：23。Khronos OpenCL 工作组。最后修订日期：2015年11月11日。https://www.khronos.org/registry/cl/specs/opencl-2.1.pdf.
- [4] Kaeli DR, Mistry P, Schaa D, Ping Zhang D. 使用 OpenCL 2.0 进行异构计算。第1版。San Francisco, CA: Morgan Kaufmann Publishers Inc.; 2015.
- [5] Hauck S, DeHon A. 可重构计算：基于 FPGA 计算的理论与实践。第1版。San Francisco, CA: Morgan Kaufmann Publishers Inc.; 2007.
- [6] Compton JMP, Pedro C. D. 粗粒度可重构架构。New York, NY, USA: Springer; 2008年10月.
- [7] Cardoso JMP, Diniz P. Weinhardt M. 面向可重构计算的编译：一项综述。ACM Comput Surv 2010;42(4):1–65. 文章 13.
- [8] Cardoso JMP, Weinhardt M. 高级综合。In: Koch D, Hannig F, Ziener D, 编. 面向软件工程师的 FPGA。New York, NY, USA: Springer; 2016. p. 23–48 (第2章).
- [9] Guo Z, Najjar W, Buyukturun B. FPGA 的高效硬件代码生成。ACM Trans Archit Code Optim 2008;5(1). 文章 6，26页.
- [10] Cong J, Liu B, Neuendorffer S, Noguera J, Vissers K, Zhang Z. FPGA 的高级综合：从原型到部署。IEEE Trans CAD Integr Circuits Syst 2011;30(4):473–91.
- [11] De Micheli G. 数字电路的综合与优化。第1版。New York, NY, USA: McGraw-Hill Higher Education; 1994.
- [12] Xilinx Inc. Vivado 设计套件用户指南。高级综合。UG902 (v2016.3) 2016年10月5日.
- [13] Gajski D, Dutt N, Wu A, Lin S. 高级综合：芯片和系统设计导论。Norwell, MA: Kluwer Academic Publishers; 1992.
- [14] Canis A, Choi J, Aldham M, Zhang V, Kammoona A, Czajkowski T, 等. LegUp：面向基于 FPGA 的处理器/加速器系统的开源高级综合工具。ACM Trans Embed Comput Syst 2013;13(2): 文章 24，27页.
- [15] Xilinx Inc. http://www.xilinx.com [2016年10月访问],
- [16] Fingerhoff M. 高级综合蓝皮书。Bloomington, IN, USA: Xlibris Corporation; 2010,
- [17] Impulse Accelerated Technologies, Inc. http://www.impulseaccelerated.com/ [2016年11月访问],
- [18] Pellerin D, Thibault S. C 语言 FPGA 实用编程。第1版。Upper Saddle River, NJ: Prentice Hall Press; 2005,
- [19] Xilinx Inc. SDAccel 环境用户指南。UG1023 (v2016.3). 2016年11月30日,
- [20] Intel Inc. SDAccel FPGA SDK for OpenCL 入门指南。UG-OCL-001, 2016.10.31. 最后更新用于 Quartus Prime Design Suite: 16.1,
- [21] Intel Corp. FPGA 器件。http://www.intel.com/content/www/us/en/fpga/devices.html,
- [22] Pell O, Mencer O. 使用可重构数据流计算应对频率缩放的终结。SIGARCH Comput Archit News 2011;39(4):60–5,
- [23] Pell O, Averbuch V. 使用数据流引擎的最大性能计算。Comput Sci Eng 2012;14(4):98–103,
- [24] Mei B, Vernalde S, Verkest D, Lauwereins R. 紧耦合 VLIW/可重构矩阵架构的设计方法：一项案例研究。In: 设计、自动化和欧洲测试会议 (DATE’04) 论文集，卷 2。Washington, DC: IEEE Computer Society; 2004. p. 1224–9,
- [25] Hartenstein R. 粗粒度可重构架构（嵌入式教程）。In: 2001年亚洲和南太平洋设计自动化会议 (ASP-DAC’01) 论文集。New York, NY: ACM; 2001. p. 564–70,
- [26] Nane R, Mihai Sima V, Pilato C, Choi J, Fort B, Canis A, 等. FPGA 高级综合工具的调查与评估。IEEE Trans CAD Integr Circuits Syst 2016;35(10):1591–604,
- [27] Huang Q, Lian R, Canis A, Choi J, Xi R, Calagar N, 等. 编译器优化对高级综合生成硬件的影响。ACM Trans Reconfig Technol Syst 2015;8(3). 文章 14，26页.

