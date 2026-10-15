+   32. Iterator over one dart per each i-cell incident to a j-cell for *n*-maps ........................................ 165
+   33. Iterator over one dart per each i-cell adjacent to an i-cell for *n*-maps ........................................ 166
+   34. `isFreeNMap(cm,d,i)`: test if a dart is i-free for *n*-maps ........ 166
+   35. `createDartNMap(cm)`: create a new isolated dart in an *n*-map ........ 167
+   36. `removeIsolatedDartNMap(cm,d)`: remove an isolated dart in an *n*-map ........ 167
+   37. `copyNMap(cm,cm′)`: copy an *n*-map into a second *n′*-map ........ 168
+   38. `increaseDimNMap(cm)`: increase the dimension of an *n*-map ........ 168
+   39. `decreaseDimNMap(cm)`: decrease the dimension of an *n*-map ........ 168
+   40. `mergeNMaps(cm,cm′)`: merge two given *n*-maps ........ 169
+   41. `restrictNMap(cm,D′)`: restrict an *n*-map to a subset of darts ........ 170
+   42. `sewableNMap(cm,d,d′,i)`: test if two darts are i-sewable for *n*-maps ........ 171
+   43. `sewNMap(cm,d,d′,i)`: i-sew two darts for *n*-maps ........ 172
+   44. `1sewNMap(cm,d,d′)`: 1-sew two darts for *n*-maps ........ 173
+   45. `unsewNMap(cm,d,i)`: i-unsew two darts for *n*-maps ........ 174
+   46. `1unsewNMap(cm,d)`: 1-unsew two darts for *n*-maps ........ 174
+   47. `closeNGMap(gm,i)`: i-close an *n*-Gmap ........ 190
+   48. `closeNMap(cm,i)`: i-close an *n*-map ........ 196
+   49. `1closeNMap(cm)`: 1-close an *n*-map ........ 198
+   50. `isRemovableNGMap(gm,d,i)`: test if an i-cell is removable for *n*-Gmaps ........ 204
+   51. `removeNGMap(gm,d,i)`: remove a given i-cell for *n*-Gmaps ........ 205
+   52. `isRemovableNMap(cm,d,i)`: test if an i-cell is removable for *n*-maps ........ 211
+   53. `removeNMap(cm,d,i)`: remove an i-cell for *n*-maps ........ 212
+   54. `0removeNMap(cm,d)`: remove a 0-cell for *n*-maps ........ 213
+   55. `isContractibleNGMap(gm,d,i)`: test if an i-cell is contractible for *n*-Gmaps ........ 218
+   56. `contractNGMap(gm,d,i)`: contract an i-cell for *n*-Gmaps ........ 218
+   57. `isContractibleNMap(cm,d,i)`: test if an i-cell is contractible for *n*-maps ........ 222
+   58. `contractNMap(cm,d,i)`: contract an i-cell for *n*-maps ........ 222
+   59. `1contractNMap(cm,d)`: contract a 1-cell for *n*-maps ........ 223
+   60. `isInsertableNGMap(gm,c,i,assoc)`: test if an i-cell is insertable for *n*-Gmaps ........ 228
+   61. `insertNGMap(gm,c,i,assoc)`: insert an i-cell in an *n*-Gmap ........ 229
+   62. `isExpansibleNGMap(gm,c,i,assoc)`: test if an i-cell is expansible for *n*-Gmaps ........ 232
+   63. `expandNGMap(gm,c,i,assoc)`: expand an i-cell in an *n*-Gmap ........ 233
+   64. `chamferingNGMap(gm,d,i)`: chamfer an i-cell for *n*-Gmaps ........ 239
+   65. `extrudeNGMap(gm,gm′)`: extrude an *n*-Gmap along a path ........ 244