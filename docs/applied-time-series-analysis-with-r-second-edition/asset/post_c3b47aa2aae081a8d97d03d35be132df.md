
### EXAMPLE 13.14: SAMPLING SCHEME FOR AN SLC PROCESS

Let $X(t)=\cos(2\pi t^2+\psi)$ where $\psi\sim\mathrm{Uniform}[0,2\pi]$, and let $t\in[-2,2]$ with $\Delta_t=0.05$. Then, as defined earlier, $t_{(0)}=-2$, $t_{(1)}=2$, $a=1$, and $b=0$, and consequently $-b/(2a)=0$. Taking $u=g(t)=t^2$, then from Equation 13.26, if $t_k\in[t_{(0)},-b/(2a)]=[-2,0]$ then $u\in[0,4]$. For this example we let $t_k=-\sqrt{u_k}$ where $u_k=|k|\Delta_u$, $k=-40,-39,\ldots,-2,-1,0$, and $\Delta_u=0.1$. Also, if $t_k\in(-b/(2a),t_{(1)}]=(0,2]$, then $u\in(0,4]$ and $t_k=\sqrt{u_k}$, where $u_k=|k|\Delta_u$, $k=1,2,\ldots,39,40$, and $\Delta_u=0.1$. We note that $\Delta_u=0.1$ was selected to ensure that the number of data values in the dual realization is the same as the number of data values in the original realization.

Figure 13.16 is similar to Figure 13.1 for the case of a linear chirp. A realization of $X(t)$, where $\psi=0$, is shown in Figure 13.16a which shows the plot of 81 equally spaced sampling points $t$ between $-2$ and $2$. Examining the plot shows that the sampling rate per cycle is lower in the regions of the data where the frequency is high. Conversely, the sampling rate per cycle is higher where the frequency is low, which is clearly undesirable. Figure 13.16b displays the same realization seen in Figure 13.16a sampled at time points $t_k$, where $t_k=\pm\sqrt{|k|\,\Delta_u}$. As evidenced by the tick marks in Figure 13.16b, this sampling strategy strategically defines $t_k$ so that there are the same number of observations per cycle, and proceeds across the reflection point without interruption. Finally, Figure 13.16c shows a plot of the data in Figure 13.16b indexed on $k$. This is the dual process, and it can be seen that the frequencies are fixed.

The analysis steps for analyzing the GLC(p) processes are very similar to those for the G(p; λ) processes, the only difference being the specific time transformation. As in the G(p; λ) case, the $t_k$'s are not equally spaced and are obtained by interpolation. Wang et al. (2009) give a Kalman filtering-based approach to avoid the need for interpolation. However, as stated previously, in most cases, we find the linear interpolation to be satisfactory. See also Haney (2011) and Bao (2014) for a discussion of the use of a Fourier-based interpolation. We will use simple linear interpolation in the examples through this book.

![](img/a0e0259119deb8c7b41dfd4f664e541d_702_0.png)
![](img/a0e0259119deb8c7b41dfd4f664e541d_702_1.png)
![](img/a0e0259119deb8c7b41dfd4f664e541d_702_2.png)

**FIGURE 13.16**  
(a) Linear chirp signal showing equally spaced time points, (b) same realization as in (a) showing the $t_k$ time points given in Equation 13.26, and (c) realization in (b) indexed on $k$.

### EXAMPLE 13.15: GLC(p) ANALYSIS OF SIMULATED CHIRP DATA

In this example, we consider the GLC(2) process associated with the discrete AR(2) dual process $(1-1.927B+0.99B^2)Y_k=a_k$. A realization of 400 evenly spaced time points from this GLC(2) process is plotted in Figure 13.17a, in which it is clear that the frequency content is time varying, and in particular is non-monotonic in nature. The Wigner–Ville plot is shown in Figure 13.17d, where the linearity of the frequency change on each side of the reflection point can be seen. As in other cases, in order to analyze such a time-varying data set, we must find a stationary dual based on a transformation of the time index. The Wigner–Ville plot is used for estimating $a$ and $b$ in

![](img/a0e0259119deb8c7b41dfd4f664e541d_705_0.png)
![](img/a0e0259119deb8c7b41dfd4f664e541d_705_1.png)
![](img/a0e0259119deb8c7b41dfd4f664e541d_705_2.png)
![](img/a0e0259119deb8c7b41dfd4f664e541d_705_3.png)
![](img/a0e0259119deb8c7b41dfd4f664e541d_705_4.png)

**FIGURE 13.18**  
(a) Realization from model in Equation 13.27, (b) low-frequency TVF signal in (a), (c) high-frequency TVF signal in (a), (d) and (e) results of low-pass fourth order Butterworth filter applied to (a) with cutoff frequencies 0.05 and 0.12, respectively.

Xu et al. (2012) proposed a method for filtering TVF data by using the following strategy:

- 1. Transform the time axis to obtain a stationary dual realization.
- 2. Filter the dual process using standard, for example, Butterworth, techniques.
- 3. Transform back to the original timescale.

In Figure 13.19a we show the data in Figure 13.18a while in Figure 13.19b we show the dual process obtained using λ = 0 and offset = 175. Figure 13.19c shows the Parzen spectral estimate of the original data displaying the typical spread spectrum for TVF data. Figure 13.19d shows the Parzen spectral density estimate for the dual data where two peaks are visible, and it appears that the dual data are composed of two frequency components, one at about f = 0.05 and another at about f = 0.15. In Figure 13.19e we show the results of applying a fourth order Butterworth filter with cutoff point at f = 0.1. There it can be seen that the lower frequency component is obtained. Figure 13.19f shows the data in Figure 13.19e transformed back to the original timescale. Comparing Figure 13.19e with the actual low-frequency component in Figure 13.18b shows that the procedure did a good job of retrieving the low-frequency TVF component, $c_1$, and in particular note the dramatic improvement over the low-pass filter results shown in Figure 13.18d and e in which the TVF data were filtered directly. For more details about this procedure see Xu et al. (2012). See also Xu et al. (2012, 2013, 2014).

**Using R:** The steps using tswge functions to obtain the low-pass filtered data in Figure 13.19 are given in Appendix 13B.

![](img/a0e0259119deb8c7b41dfd4f664e541d_707_0.png)

**FIGURE 13.19**  
(a) Realization from model in Equation 13.27, (b) dual data, (c) periodogram for data in (a), (d) periodogram for data in (b), (e) low-pass filtered dual data using cutoff f = 0.075, and (f) low-pass filtered data after transforming back to original time.

## 13.6 Concluding Remarks

TVF analysis such as that described above has also been applied to TVF data with long-memory dual models. See Bao (2014). Additionally, Chen (2014) has developed techniques for obtaining the time-transformation function using nonparametric methods as an alternative to the G(λ) and linear chirp models which use specific functional forms for the time-transformation function. See Chen (2014).

In this chapter, we have introduced important and relatively new methods for analyzing nonstationary time series with TVF behavior. The general approach is to transform the time axis to a dual space in order to obtain a stationary dual realization that can then be analyzed using standard techniques based on stationarity. A surprisingly large number of applications (chirp signals, Doppler signals, bat echolocation signals, seismic data, etc.) can be advantageously analyzed using these techniques. For more details concerning analysis and theoretical details, see the references listed throughout this chapter.

## Appendix 13A: G-Stationary Basics

### 13A.1 Generalized Instantaneous Period and IF of a G-Stationary Process

For nonstationary signals, whose spectral content varies with time, the frequency at a particular time is described by the concept of IF. We consider first a simple sinusoidal signal of the form

$X(t)=A\cos(\phi(t)),$ (13A.1)

where $A$ is constant and $\phi$ is called the cumulative phase of the signal.

A common definition (Boashash, 1992a,b) of the IF of $X(t)$ in Equation 13A.1 is

$\mathrm{IF}=\phi'(t)/2\pi.$

Note that this definition shows the rate of change of $\phi(t)$ per $2\pi$ units. However, for some processes, this definition may not have a physical interpretation. Therefore, in Definition 13A.2 we will give a new definition of IF for G-stationary processes. First, in Definition 13A.1 we define the concepts of the G-period and generalized instantaneous period (GIP) of a G-periodic function. These definitions were first given by Jiang et al. (2006). Consider the function $H(t)$ and let $u=g(t)$, so $t=g^{-1}(u)$ and $H(t)=H(g^{-1}(u))=h(u)$. Now suppose $h(u+\delta)=h(u)$ for all $u$ and that $\delta$ is the smallest such value for which this relationship occurs. Therefore $h(u)$ is a periodic function of $u$ with
