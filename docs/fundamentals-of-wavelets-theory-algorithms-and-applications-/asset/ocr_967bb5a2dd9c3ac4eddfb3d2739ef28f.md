good example. To avoid aliasing, this chirp signal must be sampled at least twice of its highest frequency. For a chirp signal with wide bandwidth, this Nyquist rate may be too high for the low frequency portion of the chirp. Consequently, there is a lot of redundant information to be carried around if one uses a fixed rate for the entire chirp. There is the area of multirate signal processing which deals with signal representation using more than one sampling rate. The mechanisms for changing the sample rate are decimation and interpolation. We discuss their basic characteristics in the time and spectral domains here.

# 7.1.1 Decimation

An M-point decimation retains only every Mth sample of a given signal. In the time-domain, an M-point decimation of an input sequence {x(n)} is given by

```
(7.1) y(n) = x(nM), for n \in \mathbb{Z}.
```

Figure 7.1 depicts the system diagram of an M-point decimator. The output of the decimator may be written in terms of a product of x(n) and a sequence of unit impulses separated by M samples \sum_{k \in \mathbb{Z}} \delta(n - kM) . Let

```
(7.2) u(n) = \sum_{k \in \mathbb{Z}} x(n) \delta(n - kM), \text{for } k \in \mathbb{Z}
```

# FIGURE 7.1: An M-point decimator.