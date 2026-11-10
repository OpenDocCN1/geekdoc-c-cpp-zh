![](bbox=[0.1571, 0.1125, 0.8571, 0.2679])

**Figure 17.7**
Simple grid (left), and the same grid with pincushion (center) and barrel (right) distortions

Most headsets utilize high field-of-view lenses that suffer from pincushion distortion. For example, consider the popular stereoscopic headset, the Google Cardboard® [GC20], in which the user places a cell phone inside of a cardboard frame that incorporates a pair of lenses. If the cell phone displays a side-by-side stereoscopic image, it can be viewed in 3D through the Google Cardboard. Figure 17.8 shows a Google Cardboard headset, along with the leftmost grid from Figure 17.7, but actually photographed through one of the Google Cardboard lenses. A pincushion distortion can clearly be observed.

![](bbox=[0.2214, 0.5348, 0.7829, 0.7342])

**Figure 17.8**
Google Cardboard® headset (left) and a simple grid viewed through one of its lenses (right), exhibiting pincushion distortion

Because headsets tend to use lenses that produce pincushion distortion, applications that target virtual reality headsets usually try to anticipate the pincushion distortion and correct for it by applying a reverse distortion, specifically barrel distortion. Since different headset lenses can have different properties, this *distortion correction* would ideally be tunable for different headsets.