analysis section includes high-pass and low-pass filters that are complementary to each other so that information in the input signal is processed by either one of the two filters. The block diagram for a two-channel PR filter bank is shown in Figure 7.19.

# FIGURE 7.19: Two-channel perfect reconstruction filter bank.

![](bbox=[0.14, 0.3, 0.82, 0.45])

The perfect reconstruction condition is an important condition in filter bank theory. It establishes the unique relationship between the low-pass and high-pass filters of the analysis section. Removal of the aliasing caused by decimation defines the relations between the analysis and synthesis filters. We will elaborate these conditions in much greater detail below.

The filters in a two-channel PR filter bank is specially designed so that the component signals may be reconstructed perfectly with no loss of information. The output of the filter bank is simply a delayed version of the input signal. For a two-channel filter bank, the filtering operation is exactly the same as the wavelet algorithm. Because of the PR condition and the need to remove the aliasing components in the output, one needs to design only one of the four filters. For further details on filter