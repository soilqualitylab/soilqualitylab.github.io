### **80. TerraceStability**
This model forecasts stability of agricultural terraces, predicting failure risk and maintenance requirements. It learns effects of rainfall, vegetation, and construction methods on longevity.

Training data needs terrace surveys, stability monitoring, and documentation of failures. Mediterranean regions have ancient terraces but systematic monitoring is rare. Future collection should use UAV photogrammetry for change detection with geotechnical assessment of terrace walls.

### **81. KarstDevelopment**
This model predicts soil formation over limestone, forecasting sinkhole risk and carbon dynamics in karst landscapes. It learns dissolution rates and soil accumulation patterns.

The model requires CO₂ monitoring in soil and caves, water chemistry of karst springs, and soil depth mapping. Karst research focuses on hydrology but soil processes are understudied. New efforts should instrument caves below soil profiles to link surface processes to subsurface dissolution.

### **82. DuneStabilization**
This model forecasts sand dune soil development and vegetation establishment for stabilization. It learns succession sequences and management interventions that accelerate stabilization.

Building this needs vegetation surveys on dunes of different ages, soil development indicators, and sand movement monitoring. Coastal management agencies have some data but soil formation is rarely quantified. Future strategies should establish chronosequences with OSL dating and comprehensive soil characterization.

### **83. RockWeathering**
This model predicts initial soil formation from bare rock, forecasting rates of physical and chemical weathering. It learns how pioneer organisms accelerate weathering and organic matter accumulation.

Training requires weathering rinds analysis, lichen/moss effects on weathering, and dating of exposed surfaces. Limited quantitative data exists on early pedogenesis. New methods should use micro-watersheds on rock outcrops to quantify weathering fluxes.

### **84. GlacialTillEvolution**
This model forecasts soil development on glacial deposits, predicting property changes over millennia. It learns weathering sequences and carbon accumulation patterns in post-glacial landscapes.

The model needs chronosequences on dated moraines, mineralogical evolution, and carbon stock development. Glacier forefields provide sequences but are limited to specific regions. Future collection should expand to continental glacial deposits with comprehensive dating.

### **85. VolcanicAshWeathering**
This model predicts Andisol formation from volcanic ash, forecasting unique properties like high water retention and phosphorus fixation. It learns ash weathering rates and allophane formation conditions.

Building this requires ash deposition dating, mineralogical transformation monitoring, and Andisol property development. Volcanic observatories have eruption records but pedogenic data is scattered. New efforts should establish monitoring networks on recent ash deposits with regular sampling.

## **Laboratory & Sensing Integration (86-100)**

### **86. SpectraInterpreter-Soil**
This model interprets visible, near-infrared, and mid-infrared spectra to simultaneously predict multiple soil properties from a single spectral measurement. It learns spectral signatures of minerals, organic matter, and water that encode information about soil composition and quality.

Training this model requires extensive spectral libraries paired with comprehensive wet chemistry analysis including carbon, nitrogen, texture, CEC, and nutrients. The World Agroforestry Centre and USDA-NRCS have built spectral libraries covering thousands of samples, though standardization across instruments remains challenging. Future data collection should focus on developing transfer functions between laboratory and portable spectrometers, with particular emphasis on challenging properties like biological activity and aggregate stability.

### **87. XRayDiffraction-AI**
This model identifies and quantifies clay minerals and other crystalline phases from X-ray diffraction patterns, handling peak overlaps and disorder. It learns to deconvolute complex patterns and estimate properties like layer charge and stacking disorder.

Building this requires XRD patterns from oriented and random powder mounts, paired with independent verification using techniques like TEM and chemical analysis. The Clay Minerals Society provides reference patterns but soil-specific databases are limited. New collection should focus on creating synthetic mixtures with known compositions for validation and using Rietveld refinement for quantitative analysis.

### **88. MicroscopyAnalyzer**
This model quantifies soil structure, porosity, and particle arrangements from electron microscopy and micro-CT images. It learns to segment images, identify features, and predict physical properties from microstructure.

Training data needs paired imaging at multiple scales with measured physical properties like permeability and aggregate stability. Several soil physics groups have image datasets but lack standardized analysis protocols. Future efforts should develop automated scanning protocols with machine-readable metadata and ground-truth measurements.

### **89. IsotopeTracer**
This model predicts carbon and nitrogen flow through soil pools from isotope labeling experiments, learning turnover times and transfer coefficients. It deconvolutes isotope signals to track specific pathways and transformations.

The model requires time series isotope data (¹³C, ¹⁵N, ¹⁸O) from labeled substrate additions with compound-specific measurements. Isotope facilities generate data but experiments are expensive and limited in scope. New strategies should use cavity ring-down spectroscopy for continuous isotope monitoring of CO₂ with parallel position-specific labeling.
