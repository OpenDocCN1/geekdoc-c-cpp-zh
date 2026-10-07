# 530 Performance, Reliability, and Availability of Computational Systems

SN 29500 was conceived and has been supported and updated by Siemens company. This standard is adopted by Siemens and its associates as the source for reliability of electronic and electromechanical components. It gives component failure rates expressed in FIT$^2$ for a list of device classes having a reference state.

The process for estimating the failure rate (FIT units) of a device involves looking up the device's failure rate (in FIT) at reference state ($rs$) by a table. The SN 29500 standard also provides a method for estimating the failure rate at operating state ($\lambda_{os}$ - in FIT) from at reference state ($\lambda_{rs}$ - in FIT).

```
$\lambda_{os} = \lambda_{rs} \times f_{temp} \times f_v \times f_c \times f_{stress},$ (25.1.3)
```

where $f_{temp}$ is the temperature factor, $f_v$ is the velocity factor, $f_c$ is the current factor, and $f_{stress}$ is the stress factor [348].

The British Handbook of Reliability Data for Electronic Components in Telecommunication Systems (HRD-5) provides definitions, failure rates and outlines a methodology for assessing system (sub-systems, circuit) reliability from electronic and electromechanical component failure information. This handbook has strive in the light of components' field data gathered by British Telecom, France Telecom, and laboratory-derived data. The reliability estimation has been adopted to (1) afford a FIT rate unity expressed as the number of failures in one billion hours (2) identify critical reliability components, and (3) to provide means of assessing the reliability impact on system design and analyzing alternative options [402].

The Automotive Electronics Council (AEC) was initially established by Chrysler, Ford, and GM to establish common part-qualification and quality-system standards. The AEC Technical Committee is responsible for establishing standards for pursuing highly reliable systems. The reliability data produced are primarily concerned with electronic parts employed in military, transport, manufacturing, integrated circuits, discrete semiconductors, passive electronic components, telecommunication, and information systems. The documents produced by AEC are available on the website [5, 10].

Xilinx publishes reports to reliability product manufacturing. Xilinx executes reliability programs in internal requirements for supporting reliability qualities of new devices or adjusting manufacturing processes to sustain quality standards. The manufacturing process is supervised by a reliability monitor that considers the maturity of the manufacturing process, the number of device hours, and the failure in time rate. The reliability tests are periodically conducted, but the number of tests can be reduced or eliminated based on the maturity of the process [473].

> $2$Failure in Time (FIT) is of failure rate expressed as the number observed failure in a period of one billion hours [348]. Hence, 1 FIT represents one observed failure in