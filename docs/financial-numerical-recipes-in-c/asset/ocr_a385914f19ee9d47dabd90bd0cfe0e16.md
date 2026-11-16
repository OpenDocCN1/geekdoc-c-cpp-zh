# 16.4 Monte Carlo Pricing of options whose payoff depend on the whole price path

Monte Carlo simulation can be used to price a lot of different options. The limitation is that the options should be European. American options can not be priced by simulation methods. There is (at least) two reasons for this. First, the optimal exercise policy would have to be known. But if the exercise policy was known there would be an analytical solution. Second, approximations using Monte Carlo relies on a law of large numbers. But if some of the sample paths were removed, the LLN would be invalidated.

In chapter 14 we looked at a general simulation case where we wrote a generic routine which we passed a payoff function to, and the payoff function was all that was necessary to define an option value. The payoff function in that case was a function of the terminal price of the underlying security. The only difference to the previous case is that we now have to generate a price sequence and write the terminal payoff of the derivative in terms of that, instead of just generating the terminal value of the underlying security from the lognormal assumption.

# 16.4.1 Generating a series of lognormally distributed variables

Recall that one will generate lognormally distributed variables as

$$S_T = S_t e^{(r - \frac{1}{2}\sigma^2)(T-t) + \sigma \sqrt{T-t} \varepsilon}$$

where the current time is $t$ and terminal date is $T$. To simulate a price sequence one splits this period into say $N$ periods, each of length

$$\Delta t = \frac{T - t}{N}$$

![](bbox=[0.15, 0.51, 0.85, 0.58])

Each step in the simulated price sequence is

$S_{t+\Delta t} = S_t e^{(r - \frac{1}{2}\sigma^2)\Delta t + \sigma \sqrt{\Delta t} \varepsilon}$$

C++ Code 16.4 shows how one would simulate a sequence of lognormally distributed variables. This code is then used in the generic routine to do calculations, as shown in C++ Code 16.5.

To price an option we are then only in need of a definition of a payoff function. We consider a couple of examples. One is the case of an Asian option, shown in C++ Code 16.6.2

Another is the payoff for a lookback, shown in C++ Code 16.7.3.