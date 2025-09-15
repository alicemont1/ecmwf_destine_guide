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


# Digital Twins (DTE)
 ECMWF currently produces two high priority digital twins, the Climate-Dt and the Extremes DT.


## Climate Digital Twin

The climate digital twin is implemented in a partnership, lead by CSC (IT-Center for Finaland) along with 12 other partners (which inlcude Met Services, supercomputing centers, research institutions). This DT produces climate projection data on multi-decadal timescales and under different climate scenarios.

Three different global climate models are being used to run the simulations. They include:
* ICON
* IFS-NEMO
* IFS-FESOM


Temporal resolution
* Hourly for atmospheric fields
* Daily means for ocean fields

Spatial resolution:



# Digital Twin Engine (DTE)

{expand:title=class}
  d1
  {expand:title=model}
    ICON
    {expand:title=resolution}
      high
      {expand:title=Final JSON}
        {code:json}
        {
          "class": "d1",
          "model": "ICON",
          "resolution": "high"
        }
        {code}
      {expand}
    {expand}
  {expand}
{expand}
