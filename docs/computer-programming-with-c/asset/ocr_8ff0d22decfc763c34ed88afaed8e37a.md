By step as the loop proceeds its execution. For each value of \(k\) from 1 to \(x\), we perform addition of \(k^2\) with the sum of previous squares as shown. Note that as with previous examples when \(k=1\), there is no previous value of sum hence the initial value of sum (say variable \(s\)) is set to zero and each time variable \(s\) is updated so that it represents the latest computed sum so far as shown in Figure 5.13.

![](bbox=[0.147, 0.221, 0.853, 0.748])

**Figure 5.13:** Evaluation of the series \(1^2+2^2+3^2+4^2+\cdots+x^2\) using for loop

Also note the presence of if else that formats the output to print a message "1*1+2*2+3*3+...+x*x" where a symbol + is to be printed for all the numbers except the last number and symbol = is required to be printed after the last number. As the loop runs from \(k=1\) to \(x\), in the last iteration of loop \(k\) will be same as \(x\) where we can print the symbol =