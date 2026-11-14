```
#define sizeX 350
define sizeY 350

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

# FIG. 7.12

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
22.         full loop unlookPerfected = false; // at this point the strategy decides about
23.         }
24.       } else {
25.         // calling aspect to determine the cost when fully unroll the loop
26.         call CostfullyUnrollAll(currentLoop);
27.         if((cost > threshold) {
28.           call InsertPragma(currentLoop, "pragma HLS UNROLL");
29.         }
30.       }
31.       call child: getChildLoop(currentLoop);
32.       currentLoop = child.$loop;
33.     } while(currentLoop != undefined);
34. end
```

# FIG. 7.13

A LARA example to select a loop and to apply loop flattening and full loop unrolling.