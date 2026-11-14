+   • G(n) = gain value for current sample
+   • d₀ = threshold in dB
+   • ρ = ratio

The CEnvelopeDetector object you used in the last chapter has a log output mode so we can combine the detector and log conversion blocks together, as shown in the dotted box in Figure 13.4. These feed the gain calculation block, which uses the threshold (in dB) and the ratio to set the gain for a given detector output. Orfanidis (1996), Zölzer (2011), and Reiss (2011) have given equations that describe the gain reduction calculation. The Zölzer equations (Equations 13.1 and 13.2) seem to be the most concise. These equations require additional slope variables (CS and ES) that are calculated from the ratio. In the compressor, CS varies between 0 and 1 as the ratio r varies from 1 to ∞. In the downward expander, ES varies between 0 and −∞ as the ratio r varies from ∞ to 1.

![](bbox=[0.15, 0.28, 0.85, 0.41])

Figure 13.3: The feed-forward and feedback topologies for a dynamics processor. A detector calculates the peak or RMS value of the signal to create a control signal. The DCA attenuates the input signal according to its control value.

![](bbox=[0.15, 0.52, 0.85, 0.65])

Figure 13.4: A generalized feed-forward topology for the compressor/downward expander families.

Compressor gain (dB):

```
G(n) = f(d(n))
```

where

```
CS = { 1 - (1/ρ)   for compression
       1.0         for limiting
     }
f = { CS · (d₀ - d(n))   if d(n) ≥ d₀
      0.0                if d(n) < d₀
    }
(13.1)
```

Downward expander gain (dB):