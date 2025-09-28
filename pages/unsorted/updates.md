
Past 9 months:

Climate-DT
Improving workflows on EuroHPC
Added IFS-FESOM projections
Extended extreme events storylines (replay recent extreme events)

Explaining more storyline simulations ex play a storm that happened in 2024 with conditions of 1950 (see how much precipitation would get with less warm world, etc)

Quality control -> trust and addded value


Operationalization of climate dt
d - suite: continuously evolve models
e - suite: trialing suite for new mode version and evaluate quality
o - suite: operational production which is frozen, traceble, reproduceable

we started a new set of complete runs 1990-2040
o-suite at 5km res (following highresmip protocol)

Extremes-DT
evaluation of added value

ecmwf ecpds 45gib/day -> eurohpc -> 1PiB/day (multio) -> hpc FDB 250tb/day -> databridge fdb -> polytope at data bridge 10GiB/day/user-> users
new pilot services


uncertaintity quantification
AI earth system model (complementing what we do alerady for AIFS atmospheric component)
expanding towrds an earth system ai model with destine




Global Extremes DT

Added Value:
Comparison Extremes vs ECMWF Operational forecast (9km)
* Improvement in the representation of tropical cyclones and medicanes
* Increase intensity of orographic precipitation (steper slopes of the orography)
* More penetration of wind gust over land
* Improvement of 2m temperature prediction 



Works on the physics of the IFS model:
Points of improvement:
Improving the representation of deep convection (ongoing)
Increasing resolution of orography (copernicus GLO-30 DEM)
Integration of prognosic Turbulent kinectic energy (TKE) scheme in IFS
Producing 4.4km ensemble (10 members) simulations to address uncertainty

Integration of 2 Impact sector models
* CAMA Flood to model river discharge
* Flexible prognostic aerosol scheme


2 Use cases
* Flood Prediction (deltares)
  * Km scale data improves river flow modelling
  * Anciliary data (high res bathymetry for coastal flooding) as important but missing
  *  uncertainty quantification important but we did not provide
* Air quality (Forschungszentrum Julich)
  * light precipitation bias had impact on results


Regional, On Demand DT
* connect earth system models to impact sector models within same workflow
* Workflow running Piloting on Atos HPC (trigger is end of ecmwf ensemble ) -> creates configs -> Weateher twin runs coupled to global dt -> then impact models -> post processing -> will arrive at data bridge in the future.
* Testing still on the EuroHPC
* Trigerring on only metereological parameters (big part of work) -> expanding to impact sector based triggering
* In development (pre operation stage) -> Uncertainty estimation (post-processing, ensembles, ai based methodologies)

Impact sector models
* floods (already included)
* air quality
* frost
* storm surge
* wildfire
* thermal comfort
* renewable energy
mainly piloting and developing on past cases
piloting also no present cases -> providing info for met services
2025 -> 200 runs in real time test mode -> 


DE 373 Contract - 
Develop Quality Control Framework for Extremes DT and Climate DT
Univeristy of Utrecht lead with partnerns
Concept for framework (no code)
Recomendations:
1) Build on Copernicus Climate Change Serice (C3S)'s Evaluation and Quality Control Framework and adapt to DestinE
2) Include an assessment of user interaction of DTs and user requirements process



FUTURE
Climate-DT
Expand 5km SSP3-7 scenarion data from 1990-2050 (currently 2020-2039)
Continuous updates of storyline simulations
Adding additional parameters
Co design on different impact sectors (updated and more direct responses to users who are involved in this pliot services and research)
ML demonstrators results from mid/26


Extremes DT
Continuous updates of modeling components
Enhancing coupling between global and on demand extremes dt
Continue evaluating user scenarios and added value/quality with National meteorological and hydrological services (NMHS)

Phase 3
Simulation Extremes in a Warming Climate

Phase 2
Digital Twin Engine
Improve Interoperabily and use
    - Stac Catalogue
    - Dashboard information on climate dt data production monitoring and verification
    - improve documentation and support


AI supported forecast in a box
climate and weather chatbot
New ML demonstrators (water resilience, agriculture, fusion of climate projections)
