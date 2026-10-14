```
45          attrib_dict["throw"] = attrib_dict.get("str")
            * 2    #meters
46          attrib_dict["load"] = (attrib_dict.get("str")
47                + attrib_dict.get("build")) * 2   #
                    kilograms
48
49          return attrib_dict
50
51          ##Get build value from attribute dictionary to
              calculate hp
52          attrs = makeAttrib()
53          build = attrs.get("build")
54
55          def makeHP(build):
56              #——Make dictionary of hit points
57              hp_dict = {}
58
59              #——Get hit points
60              hp_dict["head"] = hitPoints(build, 1)
61              hp_dict["torso"] = hitPoints(build, 2)
62              hp_dict["larm"] = hitPoints(build)
63              hp_dict["larm"] = hitPoints(build)
64              hp_dict["rleg"] = hitPoints(build)
65              hp_dict["lleg"] = hitPoints(build)
66
67              return hp_dict
68
69          def test():
70              """Show test values."""
71
72              attrs = makeAttrib()
73              build = attrs.get("build")
74              hp = makeHP(build)
75              print attrs
76              print hp
77
78          if __name__ == "__main__":
79              test()
```