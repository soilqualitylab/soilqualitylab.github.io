# **2. RhizosphereNet**
This model captures the dynamic interplay between plant roots, soil microbes, and soil organic matter in the rhizosphere, predicting how different plant-microbe combinations affect carbon stabilization and nutrient cycling. It integrates root exudate chemistry, microbial community composition, and soil physical properties to forecast rhizosphere processes.

Training data must include time-resolved sampling of rhizosphere soil with paired measurements of root exudates (collected via root washing or microdialysis), microbial community profiling, and enzyme activities. The Noble Foundation and several USDA Agricultural Research Service locations have rhizosphere sampling programs, though most lack comprehensive exudate characterization. Future collection efforts should employ stable isotope labeling to track carbon flow from roots through microbial communities into soil organic matter pools.

[Rhizosphere models](https://link.springer.com/article/10.1007/s11104-021-05201-7), integrate root exudate chemistry, microbial community composition, and soil physical properties to predict carbon stabilization and nutrient cycling, aligns with advanced rhizosphere models like CORPSE and REWT. These models combine multiple ecological and physical factors to simulate complex, real-world rhizosphere interactions. 

#### Integration of core components
* [Root Exudate Chemistry](https://www.sciencedirect.com/science/article/pii/S266732582200070X): The model accounts for how the chemical composition of substances released by roots, such as sugars and amino acids, influences microbial behavior. Different exudate compounds can attract or repel specific microbes, shaping the local community.
* Microbial Community Composition: By incorporating microbial community data, the model can simulate how different microbial populations (bacteria, fungi, etc.) respond to root exudates and environmental stress. This affects the decomposition of organic matter and nutrient release.
* Soil Physical Properties: The model includes factors like soil water content, porosity, and aggregate stability. These physical properties are critical for determining the transport of exudates, water, and nutrients, as well as providing microhabitats for microbes. 

#### Predicted outcomes
Carbon Stabilization: The model predicts how the interplay between roots and microbes affects the fate of plant-derived carbon. This includes forecasting:
The Priming Effect: Where fresh root exudates stimulate microbes to break down older, more stable soil organic matter, releasing carbon dioxide into the atmosphere.
Carbon Sequestration: How root exudates and microbial activity can also promote the formation of stable soil aggregates, locking carbon away in the soil for longer periods.
Nutrient Cycling: The model forecasts how nutrient availability changes in the rhizosphere.
Nitrogen Cycling: Predictions include how root exudates and microbial activity influence processes like nitrogen mineralization, where microbes convert organic nitrogen into a plant-available form, and the "nitrogen mining" effect.
Phosphorus Solubilization: The model can show how organic acids in root exudates alter pH levels to release phosphates from mineral particles, making them available for plant uptake. 

#### Related models and research

* [CORPSE (Carbon, Organisms, Rhizosphere and Protection in the Soil Environment)](https://besjournals.onlinelibrary.wiley.com/doi/full/10.1111/1365-2435.13510): This is a process-based model designed to simulate the decomposition of soil organic matter. It assumes that microbial decomposition is a function of microbial biomass rather than just the amount of available substrate. This makes it suitable for modeling the effects of complex rhizosphere inputs.

* [REWT (Root Exudation and Water Transport)](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2019wr026606): This is a hydrobiogeochemical transport model that simulates the movement of root exudates, water, and nutrients through the soil. It incorporates the link between root exudates, microbial biomass dynamics, and soil organic carbon turnover, often implemented to analyze critical zone processes.

* [For-PRAN (Forest Plantation Rhizosphere Available Nitrogen)](https://bg.copernicus.org/articles/15/4943/2018/): Created for Eucalyptus plantations, this model links fine root growth and rhizodeposition with carbon and nitrogen cycling. It explicitly incorporates microbial and faunal dynamics to predict rhizosphere priming effects on C and N. 

#### The challenge of rhizosphere modeling

The model described is a significant step towards a more holistic understanding of the rhizosphere. However, accurately modeling such a complex system remains a challenge due to factors such as: 

* Variable Exudate Chemistry: The composition of root exudates varies dynamically with plant species, growth stage, and environmental conditions.
* Spatial Heterogeneity: The rhizosphere is not uniform. Root exudates, microbe populations, and soil properties all change drastically over very small distances.
* Bridging Scales: Researchers must bridge the gap between microscopic pore-scale interactions and macroscopic ecosystem-level effects to create accurate and predictive models. 

