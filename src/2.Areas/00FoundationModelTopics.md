# **Curated Portfolio of 100 Soil Quality Foundation Model Concepts**

## **Soil Microbiome & Molecular Dynamics (1-25)**

### **1. SoilMetaGen**
This model predicts complete functional potential of soil microbial communities from partial metagenomic sequencing data combined with environmental parameters, enabling cost-effective assessment of soil biological capacity. It learns to infer the presence of uncaptured genes and pathways based on ecological co-occurrence patterns and environmental constraints.

Building SoilMetaGen requires extensive paired datasets of deep metagenomic sequencing and shallow shotgun sequencing from the same soils across diverse ecosystems and management conditions. The Joint Genome Institute and Earth Microbiome Project already maintain large metagenomic databases, though most lack the paired deep/shallow sequencing needed for training. New data collection should focus on creating standardized protocols for gradient sequencing depths across major soil types and land uses.

### **2. RhizosphereNet**
This model captures the dynamic interplay between plant roots, soil microbes, and soil organic matter in the rhizosphere, predicting how different plant-microbe combinations affect carbon stabilization and nutrient cycling. It integrates root exudate chemistry, microbial community composition, and soil physical properties to forecast rhizosphere processes.

Training data must include time-resolved sampling of rhizosphere soil with paired measurements of root exudates (collected via root washing or microdialysis), microbial community profiling, and enzyme activities. The Noble Foundation and several USDA Agricultural Research Service locations have rhizosphere sampling programs, though most lack comprehensive exudate characterization. Future collection efforts should employ stable isotope labeling to track carbon flow from roots through microbial communities into soil organic matter pools.

### **3. MycorrhizalMapper**
This model predicts the establishment, extent, and functional capacity of mycorrhizal fungal networks based on plant community composition, soil properties, and management history. It forecasts nutrient transfer rates between plants and identifies conditions that promote extensive hyphal networks for soil aggregation.

The model requires datasets combining molecular identification of mycorrhizal fungi (via ITS sequencing), hyphal length measurements, and nutrient transfer rates measured using isotope tracers. The International Collection of Arbuscular Mycorrhizal Fungi and various forest ecology networks have taxonomic data, but few studies measure functional attributes like nutrient transfer. New data collection should use quantum dot labeling and microfluidic soil chips to observe hyphal networks and nutrient flows in real-time.

### **4. EnzymeKinetics-Soil**
This model predicts extracellular enzyme production and activity rates under varying temperature, moisture, pH, and substrate availability, enabling forecast of decomposition rates and nutrient mineralization. It learns the complex regulatory networks controlling enzyme expression and the effects of environmental factors on enzyme stability and kinetics.

Training requires high-frequency measurements of multiple enzyme activities paired with detailed environmental monitoring and substrate availability assessments. The Enzymes in the Environment Research Coordination Network has compiled enzyme activity data from hundreds of studies, though standardization remains challenging. Future data collection should employ continuous fluorometric monitoring in field conditions using embedded microsensors to capture temporal dynamics.

### **5. NitrogenCycler**
This model provides complete prediction of nitrogen transformations including mineralization, nitrification, denitrification, and N₂O emissions based on soil properties, microbial communities, and environmental conditions. It integrates gene abundance data (amoA, nirK, nosZ) with process rate measurements to predict nitrogen fate.

Building this model requires datasets combining gross nitrogen transformation rates (measured via ¹⁵N pool dilution), N₂O flux measurements, and quantitative PCR of nitrogen cycling genes. The Global N₂O Database and various LTER sites have extensive process measurements, though few include comprehensive molecular data. New collection strategies should employ automated chamber systems with isotope analyzers to capture high-resolution N₂O dynamics alongside microbial sampling.

### **6. PhosphoCycle-AI**
This model predicts phosphorus availability and mobilization through both geochemical and biological pathways, forecasting plant-available P from total P pools. It integrates mineral dissolution kinetics, organic P mineralization, and microbial P solubilization mechanisms.

Training data must include sequential P extraction data, phosphatase enzyme activities, P-solubilizing microorganism abundance, and plant P uptake measurements. The International Phosphorus Institute maintains some datasets, but comprehensive biological-chemical integration is rare. Future collection should use ³¹P NMR spectroscopy to characterize organic P forms alongside metagenomic sequencing for P-cycling genes.

### **7. QuorumSense-Soil**
This model predicts bacterial communication networks and resulting community behaviors like biofilm formation, antibiotic production, and coordinated enzyme secretion. It learns to identify quorum sensing signals from metabolomic data and predict community-level responses.

The model requires paired metagenomics, metatranscriptomics, and metabolomics data with specific focus on acyl-homoserine lactones and other signaling molecules. Few existing datasets comprehensively measure signaling molecules in soil; most research focuses on pure cultures. New data collection should employ solid-phase microextraction coupled with mass spectrometry to detect signaling molecules in soil microsites.

### **8. ViralShunt**
This model predicts viral abundance, host range, and impacts on microbial turnover and nutrient cycling in soil, quantifying the "viral shunt" that redirects carbon and nutrients. It learns virus-host relationships from metagenomic data and predicts lysis rates under different conditions.

Training requires virome sequencing paired with bacterial/archaeal community profiling and measurements of cell lysis rates. The IMG/VR database contains soil viral sequences but lacks corresponding host and process data. Future collection should use fluorescent staining and flow cytometry to quantify viral production rates alongside sequencing efforts.

### **9. ProtistPredictor**
This model forecasts soil protist community composition and their impacts on bacterial populations through predation, affecting nutrient mineralization and carbon cycling. It predicts selective grazing patterns and resulting changes in bacterial community function.

Building this requires 18S rRNA sequencing for protists paired with bacterial community analysis and grazing rate measurements using fluorescently labeled bacteria. The Protist Diversity Database has taxonomic information but lacks functional data. New protocols should employ single-cell sequencing to identify protist gut contents and quantify grazing preferences.

### **10. ExopolymerMatrix**
This model predicts microbial production of extracellular polymeric substances (EPS) that bind soil particles into aggregates, forecasting aggregate stability from microbial community data. It learns relationships between environmental stress, community composition, and EPS production.

Training data needs measurements of EPS composition (polysaccharides, proteins, DNA), aggregate stability tests, and microbial community profiling. Limited datasets exist linking EPS chemistry to aggregate formation. Future collection should use lectin-binding assays and confocal microscopy to map EPS distribution in aggregates.

### **11. MetabolicFlux-Soil**
This model reconstructs complete metabolic networks in soil communities, predicting carbon and nutrient flow through microbial food webs. It integrates genome-scale metabolic models of individual organisms into community-level flux predictions.

The model requires metagenome-assembled genomes, metatranscriptomic data, and metabolite measurements under different conditions. The KBase platform provides tools for metabolic modeling but lacks soil-specific training data. New efforts should employ ¹³C-labeled substrates with metabolomics to trace carbon flow through specific pathways.

### **12. CarbonUseEfficiency**
This model predicts microbial carbon use efficiency (CUE) - the fraction of consumed carbon converted to biomass versus respired as CO₂ - under varying environmental conditions and substrate qualities. It learns how temperature, moisture, and nutrient availability affect the balance between growth and maintenance metabolism.

Training requires simultaneous measurements of microbial growth (via ¹⁸O-water labeling), respiration, and environmental conditions across gradients. The Microbial Carbon Use Efficiency Database has some data but coverage is limited. Future collection should employ continuous respiration monitoring with periodic biomass sampling using chloroform fumigation or substrate-independent methods.

### **13. DormancyDynamics**
This model predicts transitions between active and dormant states in soil microbial communities, forecasting the responsive fraction under changing conditions. It learns triggers for dormancy induction and resuscitation from environmental time series.

Building this requires RNA/DNA ratios to assess activity, BONCAT labeling to identify active cells, and high-frequency environmental monitoring. Few studies track dormancy dynamics over time; most are snapshots. New approaches should combine flow cytometry with viability staining and metatranscriptomics during wetting-drying cycles.

### **14. HorizontalGeneFlow**
This model predicts rates and patterns of horizontal gene transfer in soil communities, forecasting the spread of functional traits like antibiotic resistance or degradation capabilities. It identifies transfer hotspots and environmental conditions promoting gene exchange.

Training data needs metagenomic assemblies to identify mobile genetic elements, conjugation gene expression data, and experimental transfer rates. The Mobile Genetic Elements Database catalogs sequences but lacks environmental context. Future work should use fluorescent reporter systems to track real-time transfer events in soil microcosms.

### **15. ChemotaxisNavigator**
This model predicts bacterial movement toward nutrient sources and root exudates in soil pore networks, affecting colonization patterns and biogeochemical hotspots. It integrates chemotactic gene expression with pore-scale physics.

The model requires microfluidic device experiments tracking bacterial movement, chemoreceptor gene expression data, and chemical gradient measurements. Limited data exists on chemotaxis in realistic soil structures. New experiments should use transparent soil analogs with fluorescent bacteria to observe movement in response to introduced gradients.

### **16. BiocideResistance**
This model forecasts the evolution and spread of pesticide resistance in soil microbiomes, predicting community resilience to chemical stressors. It learns resistance mechanisms from genomic data and predicts cross-resistance patterns.

Training needs before/after pesticide application sampling, resistance gene quantification, and pesticide degradation rate measurements. The Pesticide Properties Database has chemical information but lacks microbiome responses. Future collection should track community changes over multiple pesticide applications with functional metagenomics.

### **17. SyntrophicNetworks**
This model predicts the establishment and stability of syntrophic relationships where multiple organisms cooperate to degrade complex compounds. It identifies potential partners and predicts degradation rates for recalcitrant substrates.

Building this requires co-culture experiments, metabolic modeling, and in situ visualization of spatial associations. The Syntrophy Database has some characterized partnerships but soil-specific data is scarce. New methods should use NanoSIMS to track metabolite exchange between adjacent cells in soil aggregates.

### **18. RedoxGradient-AI**
This model predicts oxygen distribution and alternative electron acceptor availability in soil aggregates and profiles, forecasting anaerobic microsites and their biogeochemical impacts. It integrates diffusion physics with microbial consumption rates.

Training data needs microelectrode measurements of O₂, microsensor data for other electron acceptors, and corresponding microbial community analysis. Some data exists from wetland studies but upland soil coverage is poor. Future efforts should employ planar optodes for 2D oxygen imaging with parallel sequencing of adjacent samples.

### **19. MineralMicrobe**
This model predicts microbe-mineral interactions affecting weathering rates, nutrient release, and organic matter stabilization. It learns mineral preferences of different organisms and resulting transformation rates.

The model requires paired mineralogical analysis (XRD, SEM), microbial community profiling on mineral surfaces, and weathering rate measurements. The Deep Carbon Observatory has some deep subsurface data but soil-specific datasets are limited. New collection should use mineral-amended microcosms with time-series sampling and synchrotron-based mineral characterization.

### **20. PrimeDecomposer**
This model predicts priming effects where fresh organic inputs accelerate or retard decomposition of existing soil organic matter. It learns to identify conditions and inputs that trigger positive or negative priming.

Training needs ¹³C-labeled substrate additions with partitioned respiration measurements, enzyme activities, and microbial community shifts. Various isotope studies exist but lack standardization. Future experiments should use position-specific labeling to track metabolic pathways and continuous CO₂ isotope monitoring.

### **21. BiocharColonizer**
This model predicts microbial colonization patterns and community assembly on biochar particles, forecasting functional changes over time. It learns surface property preferences and succession dynamics.

Building this requires time-series sampling of biochar-amended soils, SEM imaging of colonization, and pore-scale community analysis. The International Biochar Initiative has amendment studies but detailed colonization data is rare. New methods should use FISH-SIMS to identify specific colonizers and their metabolic activity on biochar surfaces.

### **22. AntibioticResistome**
This model tracks antibiotic resistance gene abundance and diversity in agricultural soils, predicting risks of resistance transfer to pathogens. It learns associations between management practices and resistance gene proliferation.

Training data needs comprehensive resistance gene screening, mobile element identification, and antibiotic residue measurements. The CARD database catalogs resistance genes but soil-specific prevalence data is fragmented. Future collection should employ long-read sequencing to link resistance genes with mobile elements and host organisms.

### **23. FungalHighway**
This model predicts bacterial dispersal along fungal hyphae networks, forecasting enhanced degradation of spatially separated pollutants. It learns which bacterial-fungal pairs form effective partnerships for contaminant degradation.

The model requires microscopic tracking of bacterial movement on hyphae, co-inoculation degradation experiments, and network topology analysis. Few studies quantify dispersal rates; most are qualitative observations. New approaches should use microfluidic devices with hyphal networks and fluorescent bacteria to quantify transport rates.

### **24. MethaneCycle-Soil**
This model predicts methane production and consumption in upland and wetland soils, forecasting net CH₄ fluxes under changing conditions. It integrates methanogen and methanotroph abundance with environmental controls.

Training needs CH₄ flux measurements, pmoA/mcrA gene quantification, and porewater chemistry profiles. The Global Methane Budget project compiles flux data but lacks corresponding microbial information. Future collection should use automated chambers with laser spectroscopy and parallel DNA/RNA sampling.

### **25. CrypticCarbon**
This model predicts the accessibility and vulnerability of physically protected organic matter to decomposition under changing conditions. It learns relationships between aggregate structure, organic matter chemistry, and decomposition rates.

Building this requires aggregate fractionation with compound-specific isotope analysis, enzyme accessibility assays, and micro-CT imaging. Limited data links physical protection to chemical composition. New methods should use sequential density fractionation with NMR characterization and controlled aggregate disruption experiments.

## **Soil Physics & Structure (26-45)**

### **26. AggregateArchitect**
This model predicts the hierarchical formation of soil aggregates from primary particles to large macroaggregates, forecasting aggregate size distributions and stability under different management. It learns the roles of organic binding agents, clay mineralogy, and wetting-drying cycles in aggregate formation.

Training this model requires extensive aggregate fractionation data using methods like wet sieving and slaking tests, paired with organic matter characterization and clay mineral identification. The National Soil Survey Center has aggregate stability data for US soils, though most lacks detailed binding agent analysis. Future data collection should employ X-ray micro-CT scanning before and after aggregate stability tests to track structural changes, combined with FTIR imaging to map organic binding agents.

### **27. PoreSpace3D**
This model generates realistic three-dimensional pore networks from basic soil properties, predicting pore size distributions, connectivity, and tortuosity. It learns relationships between particle arrangements and resulting pore geometries that control fluid flow and gas diffusion.

Building PoreSpace3D requires extensive X-ray CT scanning of undisturbed soil cores at multiple resolutions, paired with measured hydraulic properties and particle size distributions. Several soil physics laboratories have CT facilities, including UC Davis and Rothamsted Research, though scanning remains expensive and time-consuming. New data strategies should focus on developing rapid CT protocols and automated image analysis pipelines to process thousands of samples across soil types and management systems.

### **28. WaterRetention-AI**
This model predicts soil water characteristic curves - the relationship between water content and matric potential - from easily measured properties like texture and organic matter. It learns how aggregate structure and pore geometry affect water retention across the full moisture range.

Training data needs high-resolution water retention curves measured using pressure plates, dewpoint potentiometers, and centrifuge methods, linked to comprehensive soil characterization. The UNSODA database contains retention curves but many lack complete property data. Future collection should use automated systems like HYPROP to generate continuous retention curves while simultaneously measuring hydraulic conductivity.

### **29. InfiltrationPredictor**
This model forecasts water infiltration rates and patterns under varying initial conditions, rainfall intensities, and surface configurations. It learns to predict preferential flow initiation and the transition from matrix to macropore flow.

The model requires infiltration measurements using tension infiltrometers, rainfall simulators, and dye tracing experiments paired with detailed surface and profile characterization. USDA-NRCS has infiltration data from soil surveys but lacks process detail. New protocols should combine time-lapse electrical resistivity tomography with infiltration tests to track three-dimensional flow patterns.

### **30. CompactionRisk**
This model predicts soil susceptibility to compaction from machinery and livestock traffic, forecasting changes in bulk density and pore structure. It learns critical moisture contents for compaction and recovery potential through freeze-thaw and shrink-swell cycles.

Building this requires Proctor compaction tests, precompression stress measurements, and field traffic experiments with penetrometer mapping. Agricultural engineering departments have machinery impact data but often lack soil recovery monitoring. Future studies should use embedded sensors to track bulk density changes over multiple seasons following compaction events.

### **31. CrustFormation**
This model predicts surface seal and crust development from raindrop impact and slaking, forecasting reduced infiltration and increased erosion risk. It learns relationships between aggregate stability, rainfall energy, and crust characteristics.

Training needs rainfall simulation experiments with crust strength measurements, microscopic imaging of crust structure, and infiltration monitoring. Limited systematic data exists linking crust properties to formation conditions. New collection should use high-speed photography to capture aggregate breakdown dynamics during rainfall with subsequent micro-CT of crust architecture.

### **32. MacroporeFlow**
This model predicts preferential flow through macropores from root channels, earthworm burrows, and cracks, critical for contaminant transport. It learns to identify conditions triggering bypass flow and resulting chemical breakthrough patterns.

The model requires dye tracing experiments, tension infiltration at multiple pressures, and breakthrough curve measurements for conservative tracers. Some lysimeter facilities have detailed datasets but field-scale data is sparse. Future efforts should employ fiber-optic distributed temperature sensing to detect preferential flow in real-time during infiltration events.

### **33. ThermalRegime**
This model predicts soil temperature profiles and heat flux under varying atmospheric conditions and vegetation cover. It learns thermal property changes with moisture and the effects of management on soil temperature dynamics.

Training data needs continuous multi-depth temperature monitoring, thermal property measurements, and surface energy balance data. The Soil Climate Analysis Network provides temperature data but thermal properties are rarely measured. New instrumentation should integrate heat pulse sensors for in situ thermal property determination with standard temperature monitoring.

### **34. FreezeThawCycles**
This model forecasts the impacts of freezing and thawing on soil structure, predicting changes in aggregate stability, hydraulic properties, and carbon mineralization. It learns critical conditions for ice lens formation and structural reformation.

Building this requires controlled freeze-thaw experiments with monitoring of unfrozen water content, aggregate size distributions, and CO₂ flux. Permafrost research networks have some data but temperate soil coverage is limited. Future collection should use impedance spectroscopy to track ice formation with parallel structural and biological measurements.

### **35. ShrinkSwellDynamics**
This model predicts volume changes in clay-rich soils during wetting-drying cycles, forecasting crack network development and self-mulching behavior. It learns relationships between clay mineralogy, exchangeable cations, and shrink-swell potential.

Training needs continuous monitoring of soil volume changes using displacement transducers, crack network imaging, and corresponding moisture measurements. The Vertisol research community has scattered datasets but lacks standardization. New methods should employ photogrammetry for 3D surface tracking combined with subsurface moisture sensing.

### **36. ErosionVulnerability**
This model predicts soil loss potential from water and wind erosion at multiple scales, from splash detachment to gully formation. It learns critical thresholds for erosion initiation and sediment transport capacity.

The model requires rainfall simulation data, wind tunnel experiments, and field erosion monitoring using pins, laser scanning, and sediment collection. The National Soil Erosion Research Laboratory has extensive plot data but landscape-scale measurements are limited. Future strategies should deploy UAV-based photogrammetry for high-resolution erosion monitoring across watersheds.

### **37. TillageImpact**
This model forecasts long-term effects of different tillage systems on soil structure, predicting changes in pore networks, aggregate stability, and stratification. It learns recovery trajectories following tillage and optimal timing for operations.

Building this requires long-term tillage experiments with annual structural assessments, penetration resistance mapping, and pore characterization. Various agricultural research stations maintain tillage trials but detailed structural monitoring is rare. New protocols should use in-field CT scanning to track structural evolution without disturbing experiments.

### **38. RootPenetration**
This model predicts root ability to penetrate compacted layers, forecasting rooting depth and architecture under mechanical constraints. It learns critical penetration resistance thresholds for different species and the role of biopores.

Training data needs controlled rhizotron experiments with penetration resistance mapping, root force measurements, and 3D root architecture analysis. Limited data exists linking mechanical properties to root growth. Future collection should use transparent soil with embedded pressure sensors to observe root-soil mechanical interactions.

### **39. GasFlux-Soil**
This model predicts CO₂, N₂O, and CH₄ emissions from soil profiles, integrating production, consumption, and transport processes. It learns how soil structure controls gas diffusion and the formation of anaerobic microsites.

The model requires continuous multi-gas flux measurements using automated chambers, soil gas profile sampling, and corresponding environmental data. FLUXNET sites have CO₂ data but trace gas coverage is limited. New deployments should use quantum cascade laser spectroscopy for simultaneous multi-gas monitoring with depth-resolved sampling.

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

### **50. ClayGenesis**
This model forecasts secondary clay mineral formation pathways and rates, predicting the evolution of cation exchange capacity and water retention. It learns transformation sequences from primary minerals to different clay types.

Building this needs detailed clay mineralogy using XRD with oriented samples, TEM imaging, and solution chemistry of weathering environments. Soil genesis studies provide snapshots but transformation rates are poorly constrained. Future collection should use synthesis experiments under controlled conditions with isotopic tracers to track Si and Al incorporation.

### **51. IronRedox**
This model predicts iron oxidation-reduction dynamics and impacts on phosphorus availability, aggregate stability, and carbon protection. It learns Fe phase transformations under fluctuating redox conditions.

Training requires Fe extraction by multiple methods, Mössbauer spectroscopy for Fe phases, and monitoring of Fe²⁺/Fe³⁺ during redox cycles. Wetland studies have redox data but upland soil dynamics are understudied. New methods should use microelectrodes for real-time redox monitoring with X-ray absorption spectroscopy for Fe speciation.

### **52. AluminumToxicity**
This model forecasts aluminum speciation and plant toxicity risk in acid soils, predicting Al³⁺ activity from pH, organic matter, and base saturation. It learns critical thresholds for different plant species and amelioration strategies.

The model needs Al fractionation data, solution Al³⁺ measurements, and plant response trials at different Al levels. Acid soil research has scattered data but lacks integration. Future efforts should use ion-selective electrodes for Al³⁺ with rhizotron studies of root response to Al gradients.

### **53. HeavyMetalSpeciation**
This model predicts trace element partitioning between solution, exchangeable, and bound phases, forecasting bioavailability and mobility. It learns how pH, organic matter, and competing ions affect metal speciation.

Building this requires sequential extraction procedures, diffusive gradients in thin films (DGT) measurements, and plant uptake studies. Contaminated site assessments have data but background soil coverage is poor. New protocols should combine DGT with micro-XRF mapping to link speciation to spatial distribution.

### **54. SulfurTransformations**
This model forecasts sulfur cycling including mineralization, oxidation, and reduction, predicting sulfate availability and acid generation potential. It learns S transformation rates from microbial communities and environmental conditions.

Training data needs total S, sulfate, and organic S measurements, sulfur isotope analysis, and monitoring during wetting-drying cycles. Limited integrated S cycling data exists for non-wetland soils. Future collection should use S isotopes to trace transformations with parallel sequencing of S-cycling genes.

### **55. CarbonateEquilibrium**
This model predicts carbonate dissolution-precipitation dynamics, CO₂ fluxes, and pH buffering in calcareous soils. It learns kinetic constraints on equilibrium under field conditions.

The model requires carbonate content, CO₂ partial pressure measurements, and solution chemistry including alkalinity. Arid land studies have some data but reaction kinetics are poorly constrained. New methods should use in situ pH and CO₂ microsensors with isotopic tracing of carbonate dissolution.

### **56. SilicaCycling**
This model forecasts silicon availability and phytolith formation, important for plant health and long-term carbon sequestration. It learns Si dissolution from minerals and precipitation in plant tissues.

Building this needs Si extraction procedures, phytolith analysis, and plant Si content measurements. Limited data exists on Si cycling in agricultural soils. Future efforts should track Si isotopes from minerals through plants with electron microscopy of phytolith formation.

### **57. HumicEvolution**
This model predicts the formation and transformation of humic substances, learning molecular structures that confer recalcitrance. It forecasts changes in humic composition under different management.

Training requires advanced characterization using techniques like FT-ICR-MS, NMR spectroscopy, and size exclusion chromatography. The International Humic Substances Society has standard materials but field sample data is limited. New strategies should use ultrahigh resolution mass spectrometry with ¹³C labeling to track humic formation pathways.

### **58. CharDecomposition**
This model predicts biochar aging, functionalization, and integration into soil organic matter over decades. It learns surface chemistry changes and interactions with minerals and microbes.

The model needs aged biochar samples from long-term field trials, surface characterization using XPS and FTIR, and incubation studies. The International Biochar Initiative has some aged samples but systematic studies are rare. Future collection should establish chronosequences with periodic sampling for comprehensive characterization.

### **59. NutrientSorption**
This model forecasts competitive sorption of nutrients and contaminants on soil surfaces, predicting availability and leaching risk. It learns multi-component isotherms and kinetics from batch and column experiments.

Building this requires extensive isotherm data for multiple elements, surface complexation modeling parameters, and spectroscopic verification of binding mechanisms. Scattered data exists but multi-component systems are understudied. New experiments should use flow-through reactors with real-time monitoring and surface spectroscopy.

### **60. ColloidMobility**
This model predicts the generation, stability, and transport of soil colloids that carry nutrients and contaminants. It learns effects of solution chemistry and flow rates on colloid mobilization.

Training data needs particle size analysis of soil solutions, zeta potential measurements, and column transport experiments. Limited field-scale colloid transport data exists. Future efforts should use single particle ICP-MS to track colloid composition during transport experiments.

### **61. RedoxPoising**
This model forecasts redox buffering capacity and the sequence of electron acceptor utilization during reduction. It learns redox ladder progression from mineralogy and organic matter quality.

The model requires redox potential monitoring, electron accepting capacity measurements, and identification of redox-active phases. Wetland studies have extensive data but upland soil redox dynamics are poorly characterized. New methods should use mediated electrochemistry to quantify electron accepting/donating capacity.

### **62. MicronutrientCycling**
This model predicts trace element (Zn, Cu, Mn, B, Mo) availability from total contents, accounting for pH, organic matter, and competitive interactions. It learns plant-available pools from different extraction methods.

Building this needs multi-element extractions, plant tissue analysis, and pot trials with micronutrient additions. Soil testing services have data but extraction methods vary widely. Future collection should standardize on DGT measurements with validation against plant uptake.

### **63. AllelopathyPredictor**
This model forecasts the production, accumulation, and degradation of plant-produced toxins that inhibit other plants. It learns persistence of different allelochemicals and their effects on seed germination and growth.

Training requires identification of allelochemicals using LC-MS, soil bioassays, and field observations of plant interactions. Limited systematic data exists on allelochemical fate in soil. New studies should track specific compounds using isotope labeling with parallel bioassays.

### **64. PesticideFate**
This model predicts pesticide degradation pathways, half-lives, and metabolite formation under varying conditions. It learns effects of soil properties and microbial communities on persistence.

The model needs pesticide dissipation studies, metabolite identification, and measurements of bound residues. The Pesticide Properties Database has laboratory data but field validation is limited. Future efforts should use ¹⁴C-labeled pesticides with position-specific labeling to track complete fate.

### **65. RadiocarbonAge**
This model forecasts carbon turnover times in different soil pools using radiocarbon signatures. It learns to partition bulk soil carbon into pools with distinct residence times.

Building this requires radiocarbon dating of bulk soil and fractions, combined with modeling of bomb-carbon incorporation. Limited facilities can measure radiocarbon and costs are high. New strategies should focus on compound-specific radiocarbon analysis to resolve individual molecule ages.

## **Ecosystem & Landscape Processes (66-85)**

### **66. CarbonSequestrator**
This model optimizes management strategies for maximum soil carbon storage, predicting sequestration potential under different practices. It learns interactions between inputs, decomposition, and stabilization mechanisms across soil types and climates.

Training this model requires long-term carbon stock measurements under diverse management, isotopic partitioning of new versus old carbon, and deep soil sampling to 1+ meter. The Soil Health Institute and various LTER sites have management trials but deep carbon data is often missing. Future collection should establish paired chronosequences with eddy covariance towers for continuous CO₂ monitoring and periodic deep coring.

### **67. NutrientBudget-Regional**
This model predicts watershed-scale nutrient balances, tracking inputs, transformations, and exports through landscapes. It learns how topography, land use, and hydrology control nutrient redistribution from hillslopes to streams.

Building this requires stream water quality monitoring, spatially distributed soil sampling, and atmospheric deposition measurements across watersheds. The National Water Quality Monitoring Council has stream data but linkage to soil processes is weak. New strategies should deploy sensor networks for continuous nutrient monitoring with periodic synoptic sampling campaigns during storm events.

### **68. DesertGreenShield**
This model forecasts biological soil crust development in arid lands, predicting succession from cyanobacteria to mosses and impacts on erosion resistance. It learns environmental triggers for crust establishment and recovery after disturbance.

Training data needs crust composition surveys, chlorophyll measurements, surface stability tests, and monitoring of recovery trajectories. The USGS Canyonlands Research Station has extensive crust data but coverage of global drylands is limited. Future efforts should use hyperspectral imaging to map crust types with field validation and controlled disturbance experiments.

### **69. WetlandSoilGen**
This model predicts hydric soil development and biogeochemical cycling in wetlands, forecasting methane emissions and carbon burial rates. It learns relationships between hydroperiod, plant communities, and soil formation.

The model requires water table monitoring, redox measurements, greenhouse gas fluxes, and soil carbon accumulation rates. The National Wetlands Research Center has some data but process measurements are fragmented. New protocols should install automated chambers with multi-gas analysis and continuous redox/pH monitoring.

### **70. ForestFloorProcessor**
This model forecasts litter decomposition and humus formation in forest soils, predicting nutrient release and organic horizon development. It learns species-specific decomposition rates and interactions with soil fauna.

Building this needs litterfall measurements, decomposition bag studies, and chemical analysis of litter and humus layers. The LIDET network has decomposition data but lacks detailed chemistry. Future collection should use FTIR and NMR to track chemical changes during decomposition with DNA-based identification of decomposer communities.

### **71. GrasslandBuilder**
This model predicts soil carbon accumulation and nutrient cycling under different grassland types and management. It learns how root architecture, fire, and grazing affect soil properties.

Training requires root biomass measurements to depth, soil carbon fractionation, and monitoring under different grazing intensities. The Konza Prairie LTER has extensive data but global grassland coverage is poor. New efforts should use minirhizotrons for continuous root monitoring with isotopic labeling to track root carbon inputs.

### **72. PeatAccumulation**
This model forecasts peat formation rates and carbon storage in wetlands, predicting responses to drainage and climate change. It learns controls on decomposition versus accumulation under waterlogged conditions.

The model needs peat core dating, bulk density profiles, and carbon accumulation rates from different wetland types. The International Peat Society has some data but tropical peatlands are understudied. Future strategies should use ground-penetrating radar for peat depth mapping with multi-proxy analysis of cores.

### **73. MangroveCarbon**
This model predicts blue carbon dynamics in coastal wetlands, forecasting carbon burial and methane emissions from mangrove soils. It learns effects of salinity, tides, and sediment inputs on carbon cycling.

Building this requires sediment accretion measurements, carbon burial rates using ²¹⁰Pb dating, and greenhouse gas monitoring. The Blue Carbon Initiative has mapped extent but process data is limited. New methods should deploy sensor networks for continuous salinity/redox monitoring with sediment traps.

### **74. PermafrostThaw**
This model forecasts active layer dynamics and carbon release from thawing permafrost, predicting tipping points for rapid degradation. It learns thermal-hydrological-biogeochemical feedbacks.

Training data needs borehole temperature monitoring, active layer measurements, and carbon flux monitoring in permafrost regions. The Global Terrestrial Network for Permafrost has temperature data but carbon dynamics are poorly constrained. Future efforts should use electrical resistivity tomography for thaw detection with automated CO₂/CH₄ monitoring.

### **75. FireImpact-Soil**
This model predicts wildfire effects on soil properties including organic matter loss, water repellency, and nutrient availability. It learns recovery trajectories and management effects on resilience.

The model requires burn severity mapping, post-fire soil sampling, and monitoring of vegetation recovery. The Burned Area Emergency Response program has some data but long-term recovery is rarely tracked. New protocols should establish permanent plots with pre-fire baseline data and annual post-fire monitoring.

### **76. LandslideRisk**
This model forecasts slope stability based on soil properties, predicting failure risk under different rainfall scenarios. It learns critical combinations of soil depth, moisture, and slope angle for instability.

Building this needs shear strength measurements, soil depth mapping, and monitoring of slope movement. Geotechnical studies exist but integration with soil properties is limited. Future collection should use InSAR for slope movement detection with in situ monitoring of pore pressure.

### **77. RiparianBuffer**
This model predicts nutrient retention efficiency of riparian buffers, optimizing vegetation and width for water quality protection. It learns subsurface flow paths and biogeochemical hotspots.

Training requires nutrient flux measurements across buffers, water table monitoring, and denitrification rate measurements. The Riparian Ecosystem Management Model has some data but field validation is limited. New strategies should use conservative tracers with high-frequency nutrient monitoring.

### **78. UrbanSoilEvolution**
This model forecasts soil development in urban environments, predicting effects of compaction, contamination, and novel parent materials. It learns trajectories of human-altered soil formation.

The model needs urban soil surveys, contamination assessments, and temporal sampling of greenspaces. NYC Urban Soils Institute has mapped some cities but coverage is limited. Future efforts should establish urban soil observatories with regular monitoring and historical reconstruction.

### **79. MineralWeathering-Landscape**
This model predicts landscape-scale patterns of mineral depletion and soil development from bedrock. It learns how climate, topography, and time control weathering fronts.

Building this requires geochemical mass balance studies, cosmogenic isotope dating, and mineralogical gradients with depth. Critical Zone Observatories have detailed data but are limited to few sites. New methods should use portable XRF for rapid field mapping with targeted sampling for detailed analysis.

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

### **90. RespirometryPredictor**
This model forecasts long-term carbon mineralization from short-term respiration measurements, learning decay kinetics of different carbon pools. It predicts cumulative CO₂ evolution and identifies labile versus recalcitrant fractions.

Building this needs extended incubation studies (months to years) with high-frequency CO₂ monitoring and periodic sampling for property changes. Standard soil tests use short incubations but long-term data for validation is rare. Future protocols should use automated multiplexed systems for parallel long-term incubations under controlled conditions.

### **91. PLFAInterpreter**
This model predicts complete microbial community structure from phospholipid fatty acid profiles, learning associations between biomarkers and taxonomic groups. It estimates biomass, diversity, and functional groups from PLFA patterns.

Training requires paired PLFA analysis and DNA sequencing from the same samples across diverse soils. Commercial laboratories offer PLFA but interpretation varies between providers. New efforts should calibrate PLFA against quantitative PCR and metagenomics, focusing on improving biomarker specificity.

### **92. DNAQuality-Soil**
This model predicts DNA extraction efficiency and sequencing success from soil metadata, learning effects of clay, humic substances, and contaminants. It recommends optimal extraction protocols for challenging samples.

The model needs extraction yield data, DNA quality metrics (260/280, 260/230 ratios), and sequencing success rates linked to soil properties. Microbiome studies encounter extraction problems but systematic documentation is poor. Future collection should benchmark multiple extraction kits across soil types with standardized quality metrics.

### **93. ProximaSensor**
This model integrates data from multiple proximal sensors (EC, pH, temperature, moisture) to create high-resolution soil property maps. It learns spatial correlation structures and uncertainty propagation.

Building this requires co-located sensor measurements with laboratory validation across fields and seasons. Precision agriculture generates sensor data but calibration is site-specific. New strategies should develop universal calibration sets using diverse soils with transfer learning approaches.

### **94. LabToField**
This model scales laboratory measurements to field conditions, learning how sample preparation and storage affect results. It predicts field-relevant values from standard laboratory protocols.

Training data needs paired laboratory and in-field measurements accounting for moisture, temperature, and structure differences. Discrepancies between lab and field results are widely recognized but poorly quantified. Future efforts should use intact soil sensors to benchmark laboratory methods against field conditions.

### **95. SampleOptimizer**
This model predicts optimal sampling strategies for characterizing soil variability, learning efficient designs for different objectives and budgets. It recommends sampling density, depth, and timing for maximum information gain.

The model requires high-density sampling campaigns with geostatistical analysis and cost-benefit evaluation. Limited studies compare sampling strategies systematically. New research should use exhaustive sampling in representative fields to evaluate subsampling strategies.

### **96. ContaminantScreen**
This model rapidly predicts multiple pollutants from a single analytical measurement like XRF or spectroscopy. It learns spectral signatures of heavy metals, pesticides, and organic contaminants.

Building this needs comprehensive contaminant analysis paired with rapid screening methods across contamination gradients. Environmental consulting firms have data but it's proprietary. Future collection should focus on creating public databases of contaminated soil spectra with certified reference materials.

### **97. TextureRapid**
This model predicts complete particle size distributions from simplified measurements like settling time or laser diffraction. It learns to correct for organic matter and dispersion effects.

Training requires parallel analysis by pipette, hydrometer, and laser methods with pretreatment variations. Texture analysis is routine but method comparison is limited. New protocols should systematically compare methods across soil types with standardized pretreatments.

### **98. BioassayPredictor**
This model forecasts plant growth response from soil chemical data without growing plants, learning nutrient interactions and toxicity thresholds. It predicts crop-specific responses from general soil tests.

The model needs greenhouse bioassays paired with comprehensive soil analysis across fertility gradients. Agricultural research has yield data but controlled bioassays are less common. Future efforts should use standardized test plants with multi-element manipulation experiments.

### **99. QualityIndexer**
This model integrates multiple biological, chemical, and physical indicators into unified soil health scores. It learns indicator weights and interactions for different objectives like productivity or carbon storage.

Building this requires datasets with complete soil health measurements and outcome variables like yield or ecosystem services. The Soil Health Institute is developing frameworks but validation datasets are limited. New strategies should link indicator measurements to specific outcomes across management systems.

### **100. CalibrationTransfer**
This model adapts analytical calibrations between different instruments, laboratories, and methods, enabling data integration. It learns systematic biases and develops transfer functions for harmonization.

Training needs ring tests with identical samples analyzed by multiple laboratories using different instruments. Proficiency testing exists but focuses on accuracy not transfer. Future efforts should distribute reference samples globally with centralized database development for model training.

