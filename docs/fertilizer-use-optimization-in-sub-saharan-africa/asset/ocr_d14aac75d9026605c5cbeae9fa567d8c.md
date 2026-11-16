![](bbox=[0.253, 0.102, 0.746, 0.386])

Figure 2.2. Nigerian climate zones.

# 2.3 Spatial data

Several agriculturally relevant SSA spatial data are available. Though the resolution is coarse, the data describes regional trends that influence potential crop production (Van Wart et al., 2013) and guide local crop suitability decisions. The Africa Soil Information Service (AfSIS) modelled soil properties at six soil depths. Several climate indices have been published (WorldClim, CGIAR CSI). The 2000 Shuttle Radar Topography Mission's elevation data are available worldwide for locations between 60°N and 56°S latitudes. Elevation derivatives are also available (HydroSHEDS) and the MAPSPAM project provides crop production estimates.

Spatial raster, vector and object data are processed with Geographic Information System (GIS) software programs. GIS packages often include complex spatial analysis and modelling tools in addition to basic mapping and data processing functionality. Several free (DIVA-GIS, GeoDa, GRASS, gvSIG Desktop and Mobile, SAGA, SPRING, QGIS, Whitebox Geospatial Analysis Toolbox) and proprietary (TerSet formerly IDRISI), ArcGIS, ERDAS IMAGINE) programs are available.

The Optimising Fertilizer Recommendations in Africa (OFRA) project strives to improve greatly the profitability of fertilizer use, especially for financially constrained fertilizer use as is the

case for most smallholder farmers (Chapter 1). The OFRA approach uses results of past and recent research to determine crop nutrient response functions relevant for each site's agro-ecological zone (or inference area) so that economic analysis can be applied. Use of spatial data is important to finding and compiling information from research conducted under crop growing conditions similar to the conditions of the targeted recommendation domain.

# 2.4 OFRA Inference Tool

The OFRA Inference Tool (Wortmann and Milner 2015) is an ArcGIS 10.3 ArcPy script tool that identifies SSA research results and crop production estimates associated with growing conditions similar to those found at a user-defined point of interest (http://agronomy.unl.edu/OFRA).

The tool queries seven raster layers selected for agronomic importance. The amount of annual rainfall relative to potential evapotranspiration relates to water availability for crop production and is captured in CGIAR CSI's 30-arc second Global Aridity Index (Zomer et al., 2007, 2008). The manner in which temperature varies throughout a year impacts crop selection and is represented by WorldClim's 30-arc second Temperature Seasonality (bio4) layer (Hijmans et al., 2005). Mean temperature and