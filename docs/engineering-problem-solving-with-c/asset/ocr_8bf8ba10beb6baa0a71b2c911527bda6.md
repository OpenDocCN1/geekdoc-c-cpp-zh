30. Write a program that simulates the design shown in Figure 6.19, using a component reliability of 0.95 for all components. Print the estimate of the reliability using 5000 simulations. (The analytical reliability of this system is 0.99976.)

![](bbox=[0.226, 0.163, 0.781, 0.396])

**Flight Simulator Wind Speed.** This set of problems relates to a computer simulation of wind speed for a flight simulator. Assume that the wind speed for a particular region can be modeled by using an average value and a range of gust values that is added to the average. For example, the wind speed might be 10 miles an hour, with added noise (which represents gusts) that ranges from 22 miles per hour to 2 miles per hour, as shown in Figure 6.20. Use the function `randfloat` developed in this chapter.

31. Write a program to generate a data file named wind.dat that contains 1 hour of simulated wind speeds. Each line of the data file should contain the time in seconds and the corresponding wind speed. The time should start with 0 seconds. The increment in time should be 10 seconds and the final line of the data file should correspond to 3,600 seconds. The user should be prompted to enter the average wind speed and the range of values of the gusts.

![](bbox=[0.226, 0.703, 0.881, 0.936])