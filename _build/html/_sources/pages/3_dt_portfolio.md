---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
(ch3)=

# ECMWF's Destination Earth Data Porfolio

This section covers Digital Twin Data — datasets produced or curated by ECMWF. Currently, ECMWF operates two high-priority digital twins: the Climate Adaptation Digital Twin (Climate-DT) and the Extremes Digital Twin (Extremes-DT).

An overview of the data produced is available on the [Climate Twin](https://destine.ecmwf.int/climate-change-adaptation-digital-twin-climate-dt/) and on the [Extremes Digital twin](https://destine.ecmwf.int/weather-induced-extremes-digital-twin/) pages of ECMWF's official Destination Earth website.

For detailed information on parameters, temporal resolution, and known issues (errata), refer to ECMWF’s [data catalogue](https://confluence.ecmwf.int/display/DDCZ/DGOV+DestinE+Collaboration+Zone+Home) which serves as the primary reference for both Climate-DT and Extremes-DT data.

Additionally, a STAC (SpatioTemporal Asset Catalog) catalogue is in development, though it is not yet available. (A STAC catalogue is a standardized framework for organizing and discovering geospatial data).



## Climate Digital Twin

The Climate Digital twin models produce climate projections over multi-decadal time periods at 5-10km resolution.

These models are being developed through a collaboration led by Finland’s IT Center for Science (CSC), involving climate institutions, supercomputing centers, national meteorological services, academia, and industrial partners.

The objectives of the Climate DT are:
* operationalize climate projections on a regular basis (yearly)
* Provide on-demand simulations to explore “what if” scenarios
* Establish an operational framework encompassing monitoring, evaluation, quality assurance, and uncertainty quantification

Three different global climate models are being used to run the simulations. They include:
* ICON: The ICOsahedral Non-hydrostatic model, developed by DWD, MPI-M, DKRZ, KIT, and C2SM
* IFS-NEMO: ECMWF’s IFS coupled with the NEMO ocean model, implemented by BSC with ECMWF
* IFS-FESOM: ECMWF’s IFS coupled with the Alfred Wegener Institute’s Finite-VolumE Sea ice–Ocean Model (FESOM)


### Historical Simulations

DestinE’s historical runs follow the **Coupled Model Intercomparison Project Phase 6 (CMIP6)**, a global initiative to coordinate and compare climate models. CMIP6 provides simulations of past, present, and future conditions and underpins the **IPCC assessment reports**.

### Control Experiments

Baseline simulations use the **High Resolution Model Intercomparison Project (HighResMIP)**, part of CMIP6. HighResMIP focuses on higher-resolution models to better capture regional climate patterns and extremes, supporting adaptation planning, risk management, and improved projections.

### Future Projections

Future scenarios are based on the **Scenario Model Intercomparison Project (ScenarioMIP)**. DestinE currently uses **SSP3-7.0**, a high-emissions pathway marked by limited international cooperation and weak climate policy. Simulations start in 2020 from reanalysis data, include a five-year ocean spin-up, and extend forward under SSP3-7.0. Later phases will add more scenarios.


### Storyline Simulations (Story-Nudging)
Storyline simulations provide a *what-if* framework to explore how recent weather events might look under different climate conditions—such as a warmer world or pre-industrial times.

To keep these simulations close to reality, a **nudging approach** aligns the large-scale circulation with the **ERA5 reanalysis** for 2017–2023. Meanwhile, small-scale dynamics and thermodynamic processes are free to evolve. This setup allows scientists to ask, for example: *How would an observed extreme precipitation event change in a warmer climate?*  

Initial conditions are drawn from:  
- ocean-only spin-up simulations for **1950** and **2017**, and  
- the **IFS–FESOM projection for a +2 °C world (tplus2.0)**. 



## Extremes Digital Twin
Provides information on extreme events on a timescale of a few days ahead, at very high spatial resolution 

> ⚠️ * Forecasts can only be retrieved for start dates 15 days behind the current date.


### Global Component (continuous)
Developed by ECMWF, produces global simulations at 4.4 km atmosphere and 25 km ocean resolution for up to 4 days ahead.
Initialized daily from the 00UTC ECMWF operational analysis (IFS)

The global models used are IFS-NEMO


### Regional Component (on-demand)
> ⚠️ * In Development, not available yet

Procured by ECMWF and developed in partnership led by Meteo France and several european institutions such as national meteorological services (NMS).
Produces regional simulations over Europe at 500-700 meter resolution up to 2 days ahead.
Based on high-resolution models developed within the ACCORD consortium. Impact-sector models for floods, air quality and renewable energy will be integrated in its workflow.



## Model Versions and Documentation

* Nemo: v4.0.7 (https://zenodo.org/records/3878122/files/NEMO_book.pdf?download=1)
* SI3: [NEMO_SI3_book.pdf](https://zenodo.org/doi/10.5281/zenodo.7534899)
* IFS cycle CY48r3.0 <!--TODO check if this is only valid for extremes dt! -->
* <!--TODO ICON/FESOM model versions??? -->
  

We currently do not have DOIs for the specific DT datasets and these should be cited by referring to the https://platform.destine.eu/destine-data-portfolio/ and the specific descriptions at:

https://destine.ecmwf.int/climate-change-adaptation-digital-twin-climate-dt/ (climate DT)
https://destine.ecmwf.int/weather-induced-extremes-digital-twin/ (extremes DT)
in addition, with respect to scientific literature we suggest the following 2 articles

Wedi et al,
Implementing Digital Twin technology of the Earth System in Destination Earth,
Journal of the European Meteorological Society, 2025, in review.
Doblas-Reyes et al,
The Destination Earth digital twin for climate change adaptation,
Geoscientific Model Development (GMD), 2025, in review.

## Data policy

https://platform.destine.eu/wp-content/uploads/2024/11/Terms-and-Conditions-for-DestinE-Users-Granted-Upgraded-Access.pdf



## Monitoring and Evaluation Framework: Aqua
