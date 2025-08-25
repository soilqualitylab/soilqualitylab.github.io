### **40. HydrophobicityMapper**
This model predicts the development and persistence of soil water repellency, forecasting impacts on infiltration and preferential flow. It learns relationships between organic matter chemistry, moisture history, and hydrophobicity.

Training needs water drop penetration time tests, contact angle measurements, and organic matter characterization using pyrolysis-GC/MS. Fire-affected soil studies have some data but background hydrophobicity is poorly documented. Future efforts should employ sessile drop goniometry with chemical imaging to link hydrophobicity to specific compounds.

### **41. SaltAccumulation**
This model forecasts salt accumulation patterns and salinization risk under irrigation and natural conditions. It learns salt movement through profiles and critical thresholds for plant stress and structural degradation.

Building this requires electromagnetic induction surveys, soil solution sampling, and detailed salt chemistry including sodium adsorption ratios. The Global Soil Salinity Database has extent data but lacks process measurements. New strategies should use time-domain reflectometry arrays for continuous salinity monitoring with periodic pore water extraction.

### **42. BioturbationModel**
This model simulates soil mixing by earthworms, arthropods, and other fauna, predicting impacts on structure, organic matter distribution, and nutrient cycling. It learns species-specific bioturbation rates and preferences for different soil conditions.

Training data needs earthworm abundance surveys, casting production measurements, and tracer experiments using rare earth elements or microspheres. Some ecological studies exist but quantitative bioturbation rates are scarce. Future collection should use CT scanning of soil columns with introduced fauna to track mixing in 3D over time.

### **43. CrackNetwork**
This model predicts crack initiation, propagation, and healing in shrink-swell soils, forecasting preferential flow paths and gas exchange. It learns crack geometry relationships with moisture, clay content, and stress history.

The model requires time-lapse imaging of surface cracks, dye infiltration to map crack depth, and mechanical property measurements. Limited systematic data links crack patterns to soil properties. New methods should combine drone imaging for surface patterns with ground-penetrating radar for subsurface crack detection.

### **44. ParticlePacking**
This model predicts optimal particle size distributions for achieving desired structural properties like maximum density or high permeability. It learns packing arrangements from CT data and predicts resulting physical properties.

Building this requires systematic mixing experiments with different particle combinations, CT scanning of resulting structures, and hydraulic/mechanical testing. Geotechnical engineering has theoretical models but lacks soil-specific validation. Future work should use discrete element modeling validated against physical experiments.

### **45. WindErosion-AI**
This model forecasts wind erosion risk and dust generation, predicting threshold wind speeds and transport rates. It learns effects of surface crusts, vegetation, and soil moisture on erosion resistance.

Training needs wind tunnel experiments, field monitoring with sediment samplers, and surface characterization including aggregate size and crusting. The Wind Erosion Research Unit has data but coverage of diverse soil types is limited. New collection should deploy networks of dust monitors with meteorological stations across erosion-prone regions.

## **Soil Chemistry & Mineralogy (46-65)**

### **46. CationBalance**
This model predicts base saturation, cation exchange dynamics, and nutrient availability from soil mineralogy and organic matter. It learns ion selectivity coefficients and competition effects under varying ionic strength and pH.

Training this model requires complete exchangeable cation measurements, cation exchange capacity by multiple methods, and detailed clay mineralogy from XRD. The National Cooperative Soil Survey has extensive data but methods vary between laboratories. Future collection should standardize on silver-thiourea extraction with ICP-MS analysis and include mineralogical characterization.

### **47. pHBuffer-AI**
This model forecasts soil pH buffering capacity and lime requirements for pH adjustment, learning from mineralogy, organic matter, and exchangeable aluminum. It predicts pH changes from amendments and natural processes like nitrification.

Building this requires titration curves, lime incubation studies, and monitoring of pH changes under field conditions. Soil testing laboratories have pH data but buffering capacity is rarely measured comprehensively. New protocols should use automated titrators with continuous pH monitoring during base additions, coupled with aluminum speciation measurements.

### **48. OrganoMineral**
This model predicts the formation and stability of organo-mineral associations that protect carbon for decades to millennia. It learns binding mechanisms from molecular structure, mineral surface properties, and environmental conditions.

Training data needs sequential density fractionation, specific surface area measurements, and spectroscopic characterization of organic-mineral interfaces using techniques like STXM-NEXAFS. Limited molecular-level data exists on binding mechanisms. Future efforts should employ nano-SIMS to map organic matter on mineral surfaces with compound-specific isotope labeling.

### **49. WeatheringRates**
This model predicts primary mineral dissolution kinetics under field conditions, forecasting nutrient release and secondary mineral formation. It learns to scale from laboratory rates to field conditions accounting for biological enhancement.

The model requires mineral dissolution experiments, soil solution chemistry monitoring, and mineralogical changes over time. The Critical Zone Observatory network has some weathering data but long-term studies are rare. New strategies should use mineral bags buried in soil with periodic retrieval for surface analysis and solution sampling.

