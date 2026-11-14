![](bbox=[0.15, 0.01, 0.85, 0.17])

Figure 8.10: The frequency response for the resonant LPF test filter.

![](bbox=[0.16, 0.23, 0.85, 0.4])

Figure 8.11: The ringing IR of the resonant LPF.

# 8.2.3 The IR File Format

The IR file actually contains C++ code and you can quickly understand how it works by using the clipboard functions. In the analyzer window that you still have pulled up, click on the button h(n) → Clipboard and after the success message, open a text editor or a C++ compiler. Then, use the operating system (OS) paste function to paste the clipboard data into your editor. You will see something like this at the top:

```
// h(n) Impulse Response
// Length= 1024
m_nIRLength= 1024;
m_h_Left[0] = 0.00000000;
m_h_Left[1] = 0.00503618;
m_h_Left[2] = 0.01998402;
m_h_Left[3] = 0.03938961;
m_h_Left[4] = 0.05777339;
m_h_Left[5] = 0.07477701;
m_h_Left[6] = 0.09007415;
m_h_Left[7] = 0.10337673;
etc...
```

This is the IR data starting with the length (1024) and then the left and right channels respectively. If you scroll to the bottom, you will see the last few samples of the IR: