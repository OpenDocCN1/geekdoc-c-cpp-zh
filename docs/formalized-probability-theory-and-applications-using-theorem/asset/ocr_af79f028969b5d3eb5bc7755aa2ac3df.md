# 13.3 FORMAL ANALYSIS OF WSN FOR FOREST FIRE DETECTION

Wireless sensor networks have been extensively explored for forest fire detection (Liu, Wu, Xiao, & Sun, 2011). Indeed, forest fires are considered to be one of the worst natural disasters throughout the world. They threaten forests, animals, and people, and cause a lot of environmental degradations. Indeed, more than 100,000 wild fires occur annually. For example, in Tunisia, 103 fires destroyed 287 hectares of forests just between May 1, 2012 and July 25, 2012. In such context, the main job of the sensors is to sense and communicate temperature, humidity and barometric pressure values to a base station. Moreover, the harsh nature of the field of interest makes a random deployment by air-dropping sensors much easier. In this section, we are interested in formally analyzing the coverage performances of a wireless sensor network deployed for a forest fire application. Due to the safety-critical feature of the target application, the deployed WSN has to remain alive as long as possible while ensuring an efficient coverage of any fire breakthrough. Nevertheless, most of the existing WSNs for forest fire detection suffer from lifetime limitations. In order to extend the whole network lifetime, the k-set randomized scheduling algorithm has been proposed for a given forest fire detection application using wireless sensor networks. In the specified application, the nodes have a sensing area r = 30, and are deployed into a forest region of size a = 100m x 100m, whereas the success probability q of a sensor covering a point, is q = r / a = 0.003.

Based on our theoretical development done in the previous section, we now conduct a formal asymptotic analysis of the probabilistic coverage based on the parameters n and k (Elleuch, Hasan, Tahar & Abid, 2012). For that, we are going to tackle the generic case and then instantiate it for the given forest fire application. Hence, we simply denote (cvrge_intsty_network p X k s C n q) by (Cn_wsn p X k s C n q). In the context of our application, we can formally specify the given forest fire detection application by specializing Definition 13.11 since it describes the generic coverage intensity of a WSN using a k-set randomized scheduling algorithm.

# Definition 13.12

```
⊢ ∀ p X k s C n.
cn_wsn_frst p X k s C n = cvrge_intsty_network p X k s C n
(0.003).
```

Then, we easily check in HOL that (cn_wsn_frst p X k s C n) equals

Normal (1 - (1 - (0.003/k)^n)) (13.6)