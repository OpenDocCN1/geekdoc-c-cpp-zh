
[37] J. Nocedal and S. J. Wright *Numerical optimization*, Springer, 1999.

[38] H. Risken, *The Fokker-Planck equation, methods of solution and applications*, Second Edition, Springer-Verlag, 1989.

[39] H. Szu and R. Hartley, Fast simulated annealing, *Phys. Lett. A*, 122(3-4), 157-162. 1987,

[40] Pavlyukevich, Ilya, Simulated annealing for Le'vy-driven jump-diffusions, *Stochastic Process. Appl.* 118 (2008), no. 6, 1071-1105.

[41] A. Torn, Global Optimization as a Combination of Global and Local Search, *Ph.D. Thesis, Abo Akademi University, HHAAA 13*, 1974.

[42] A. Torn and A. Zilinskas, *Global optimization*, Springer Verlag, Berlin, 1989.

[43] D. Wales and J. Doye, Global optimization by basin-hopping and the lowest energy structures of Lennard-Jones clusters containing up to 110 atoms, *J. Phys. Chem. A*, 101, 1997, pp. 5111-5116.

[44] R. L. Yang, Convergence of the simulated annealing algorithm for continuous global optimization, *J. Optim. Theory Appl.*, 104(3), 691-716, 2000.

[45] K. Yiu, Y. Liu and K. Teo, A Hybrid Descent Method for Global Optimization, *J. of Global Optimization*, 28, 2004, pp. 229-238.

[46] J. Zhang, Derivative-free hybrid methods in global optimization and their applications to data mining, protein folding, unfolding, misfolding, *Ph.D Thesis, University of Ballarat, Australia*, 2004.

## HOW WE FOUND THE MISSING MEMRISTOR*

The memristor—the functional equivalent of a synapse—could revolutionize circuit design By R. Stanley Williams

IT'S TIME TO STOP SHRINKING. Moore's Law, the semiconductor industry's obsession with the shrinking of transistors and their commensurate steady doubling on a chip about every two years, has been the source of a 50-year technical and economic revolution. Whether this scaling paradigm lasts for five more years or 15, it will eventually come to an end. The emphasis in electronics design will have to shift to devices that are not just increasingly infinitesimal but increasingly capable.

Earlier this year, I and my colleagues at Hewlett-Packard Labs, in Palo Alto, Calif., surprised the electronics community with a fascinating candidate for such a device: the memristor. It had been theorized nearly 40 years ago, but because no one had managed to build one, it had long since become an esoteric curiosity. That all changed on 1 May, when my group published the details of the memristor in Nature.

Combined with transistors in a hybrid chip, memristors could radically improve the performance of digital circuits without shrinking transistors. Using transistors more efficiently could in turn give us another decade, at least, of Moore's Law performance improvement, without requiring the costly and increasingly difficult doublings of transistor density on chips. In the end, memristors might even become the cornerstone of new analog circuits that compute using an architecture much like that of the brain.

For nearly 150 years, the known fundamental passive circuit elements were limited to the capacitor (discovered in 1745), the resistor (1827), and the inductor (1831). Then, in a brilliant but underappreciated 1971 paper, Leon Chua, a professor of electrical engineering at the University of California, Berkeley, predicted the existence of a fourth fundamental device, which he called a memristor. He proved that memristor behavior could not be duplicated by any circuit built using only the other three elements, which is why the memristor is truly fundamental.

Memristor is a contraction of "memory resistor," because that is exactly its function: to remember its history. A memristor is a two-terminal device whose resistance depends on the magnitude and polarity of the voltage applied to it and the length of time that voltage has been applied. When you turn off the voltage, the memristor remembers its most recent resistance until the next time you turn it on, whether that happens a day later or a year later.

Think of a resistor as a pipe through which water flows. The water is electric charge. The resistor's obstruction of the flow of charge is comparable to the diameter of the pipe: the narrower the pipe, the greater the resistance. For the history of circuit design, resistors have had a fixed pipe diameter. But a memristor is a pipe that changes diameter with the amount and direction of water that flows through it. If water flows through this
pipe in one direction, it expands (becoming less resistive). But send the water in the opposite direction and the pipe shrinks (becoming more resistive). Further, the memristor remembers its diameter when water last went through. Turn off the flow and the diameter of the pipe “freezes” until the water is turned back on.

### THINKING MACHINE
This artist's conception of a memristor shows a stack of multiple crossbar arrays, the fundamental structure of R. Stanley Williams's device. Because memristors behave functionally like synapses, replacing a few transistors in a circuit with memristors could lead to analog circuits that can think like a human brain. IMAGE BRYAN CHRISTIE DESIGN

![](img/039e7d3c23390584a66737067db8b75b_496_0.png)

PICTURING MEMRISTANCE: HP Labs senior fellow R. Stanley Williams [left] and research physicist Duncan Stewart [right] explain the fourth fundamental circuit element. Williams worked with nearly 100 scientists and engineers to find the memristor. PHOTO: PAUL SAKUMA/AP PHOTO.

That freezing property suits memristors brilliantly for computer memory. The ability to indefinitely store resistance values means that a memristor can be used as a nonvolatile memory. That might not sound like very much, but go ahead and pop the battery out of your laptop, right now—no saving, no quitting, nothing. You’d lose your work, of course. But if your laptop were built using a memory based on memristors, when you popped the battery back in, your screen would return to life with everything exactly as you left it: no lengthy reboot, no half-dozen auto-recovered files.

But the memristor’s potential goes far beyond instant-on computers to embrace one of the grandest technology challenges: mimicking the functions of a brain. Within a decade, memristors could let us emulate, instead of merely simulate, networks
of neurons and synapses. Many research groups have been working toward a brain in silicon: IBM’s Blue Brain project, Howard Hughes Medical Institute’s Janelia Farm, and Harvard’s Center for Brain Science are just three. However, even a mouse brain simulation in real time involves solving an astronomical number of coupled partial differential equations. A digital computer capable of coping with this staggering workload would need to be the size of a small city, and powering it would require several dedicated nuclear power plants.

Memristors can be made extremely small, and they function like synapses. Using them, we will be able to build analog electronic circuits that could fit in a shoebox and function according to the same physical principles as a brain.

A hybrid circuit—containing many connected memristors and transistors—could help us research actual brain function and disorders. Such a circuit might even lead to machines that can recognize patterns the way humans can, in those critical ways computers can’t—for example, picking a particular face out of a crowd even if it has changed significantly since our last memory of it.

THE STORY OF THE MEMRISTOR is truly one for the history books. When Leon Chua, now an IEEE Fellow, wrote his seminal paper predicting the memristor, he was a newly minted and rapidly rising professor at UC Berkeley. Chua had been fighting for years against what he considered the arbitrary restriction of electronic circuit theory to linear systems. He was convinced that nonlinear electronics had much more potential than the linear circuits that dominate electronics technology to this day.

Chua discovered a missing link in the pairwise mathematical equations that relate the four circuit quantities—charge, current, voltage, and magnetic flux—to one another. These can be related in six ways. Two are connected through the basic physical laws of electricity and magnetism, and three are related by the known circuit elements: resistors connect voltage and current, inductors connect flux and current, and capacitors connect voltage and charge. But one equation is missing from this group: the relationship between charge moving through a circuit and the magnetic flux surrounded by that circuit—or more subtly, a mathematical doppelgänger
