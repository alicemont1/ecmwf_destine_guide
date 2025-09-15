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
(ch4)=
# Retrieving Data with Polytope

Polytope is an open-source feature‑extraction service developed by ECMWF. It allows users to request n‑dimensional data subsets—called polytopes—from enormous, structured weather data “datacubes” without having to download entire data fields.

Instead of inefficient bounding-box extraction (which reads full fields and post‑processes them), Polytope extracts only the precise data requested—e.g. a flight path, a time series, or a geographic region—reducing I/O significantly.

Polytope follows a client–server architecture, where a Polytope client allows users to define and submit data extraction requests, while the Polytope server, which has access to the FDB, processes those requests. The server handles the computational geometry, identifies the relevant data, and retrieves only the required subsets from the Field Database (FDB). Communication between client and server happens via a REST API, enabling scalable and efficient access to high-resolution datasets.


In the context of the Destination Earth project, a Polytope server is deployed on the Data Bridge, within the Data Lake, with direct access to the Data Lake’s FDB. Unlike services such as the Harmonized Data Access (HDA), Polytope is limited to extracting Digital Twin data only. While Digital Twin data is also available through the HDA, that service does not support feature-based extraction—making Polytope the recommended tool for retrieving DT data. Please note that HDA is developed and maintained by EUMETSAT, and ECMWF does not provide support for it.


You can find more detailed information on the polytope service in our [polytope documentation](https://polytope.readthedocs.io/en/latest/)


## Polytope Client

The recommended client for Polytope feature extraction is the earthkit-data Python library, which is also developed and maintained by ECMWF. Alternatively, the polytope-client Python package is available as a lower-level interface.

For more information on using polytope with earthkit data please refer to the earthkit data [polytope documentation section](https://earthkit-data.readthedocs.io/en/latest/guide/sources.html#polytope)


### Authentication

To use Polytope with Digital Twin data, you must first request **upgraded access** through the Destination Earth Platform. Instructions for this can be found in [Requesting Access to Destination Earth Data](ch2).

Once access is granted, you need to authenticate using the [`desp-authentication.py`](https://github.com/destination-earth-digital-twins/polytope-examples/blob/main/desp-authentication.py) script, available in the Polytope examples repository. When you run the script, it will prompt you for your Destination Earth username and password (the same credentials you used to register on the platform).

After successful authentication, the script retrieves a long-living access token from the Destination Earth Service Platform (DESP) and stores it in a file named `.polytopeapirc` in your home directory. As long as this file exists, re-authentication is not necessary.

> **Note:** These credentials provide access **only to Digital Twin data on the Destine Data Lake**.  
> While Polytope can also be used to access ECMWF data (not covered here), that requires connecting to a different server.  
> Polytope uses the same `.polytopeapirc` file for all services, so if you switch between servers, be sure to update the credentials.  
> If you're only working with Destine data, you can ignore this.


### Examples

A comprehensive collection of Polytope examples is available in the [polytope-examples](https://github.com/destination-earth-digital-twins/polytope-examples) repository. 

This section provides a brief overview of how to make a request:

#### Using Earthkit Data:

```python
import earthkit.data

request = {
    'activity': 'ScenarioMIP',
    'class': 'd1',
    'dataset': 'climate-dt',
    'date': '20200102',
    'experiment': 'SSP3-7.0',
    'expver': '0001',
    'generation': '1',
    'levtype': 'sfc',
    'model': 'IFS-NEMO',
    'param': '134/165/166',
    'realization': '1',
    'resolution': 'standard',
    'stream': 'clte',
    'time': '0100', # '0100/0200/0300/0400/0500/0600'
    'type': 'fc'
}

# The polytope source accesses the Polytope web services, using the polytope-client package.
data = earthkit.data.from_source("polytope", "destination-earth", request, address="polytope.lumi.apps.dte.destination-earth.eu", stream=False)
```

#### Using Python Polytope Client:

```python
from polytope.api import Client

client = Client(
    address="polytope.lumi.apps.dte.destination-earth.eu")

file = client.retrieve("destination-earth", request, "output_file.grib")
```


## Request Language Syntax

When writing a request for Digital Twin (DT) data, you’ll need to use a syntax that is based on **ECMWF’s Mars language**, extended with a few additional keywords specific to Destin and some modified keywords. 

If you’re just starting out, two key references will save you time:
- 📖 The [DestinE data catalogue](https://confluence.ecmwf.int/display/DDCZ/DestinE+Parameter+Portfolios) — a complete list of available datasets and parameters.  
- 📖 The [Mars keywords reference](https://confluence.ecmwf.int/display/UDOC/Keywords+in+MARS+and+Dissemination+requests) — useful when building queries for date ranges, time steps, or forecast intervals.

Together, these resources will help you craft valid Polytope requests.

⚠️ Important: The mars "resol" keyword does not work on DestinE data, and instead the key "resolution" should be used to specify dataset resolution.


---

### Common Keywords

Here’s a quick guide to the most important keywords you’ll use when constructing DT requests.

### Common Keywords

Here’s a tabular overview of the most relevant keywords for DestinE requests:

| **Keyword**   | **Applies To**           | **Values                                                                | **Notes** |
|---------------|--------------------------|----------------------------------------------------------------------------------------|-----------|
| `class`       | climate-dt, extremes-dt  | `d1` , `ng`                                                                            | Main category of data (d1 for destine data, ng for nextgems) |
| `dataset`     | climate-dt, extremes-dt  | `climate-dt`, `extremes-dt`                                                            | Which dataset to query |
| `expver`      | climate-dt, extremes-dt  | `001`                                                                                  | Experiment version (distinguishes model/data runs) |
| `stream`      | climate-dt               | `clte`                                                                                 | Climate stream |
|               | extremes-dt              | `wave`, `oper`                                                                         | Wave or atmospheric model stream |
| `activity`    | climate-dt only          | `story-nudging`, `scenariomip`, `highresmip`, `cmip6`, `baseline`                      | Scientific project or activity |
| `type`        | climate-dt, extremes-dt  | `fc`                                                                                   | Forecast data |
| `resolution`  | climate-dt, extremes-dt  | `standard`, `high`                                                                     | Spatial resolution |
| `experiment`  | climate-dt only          | `tplus2.0k`, `ssp3-7.0`, `hist`, `cont`                                                | Model scenario or setup |
| `generation`  | climate-dt only          | `1`                                                                                    | Data/model generation |
| `model`       | climate-dt only          | `ifs-nemo`, `ifs-fesom`, `icon`                                                        | Model type |
| `realization` | climate-dt only          | `1`                                                                                    | members of an ensemble of simulations that differ only in their initial conditions. [More info](https://wcrp-cmip.github.io/WGCM_Infrastructure_Panel/Papers/CMIP6_global_attributes_filenames_CVs_v6.2.7.pdf) |
| `feature`     | optional                 | JSON object                                                                            | Used for Polytope feature extraction requests |



### Feature Extraction

Polytope can enhance standard requests with **feature extraction**, allowing you to specify a `feature` keyword that contains a JSON dictionary describing the shape or path of interest. The service then extracts only the points that fall within that feature.

For details on constructing a feature request, see the [official guide](https://polytope.readthedocs.io/en/latest/Service/Features/feature/).

Supported feature types include (availability may vary by dataset):
- Time series  
- Flight paths  
- Geographic polygons  
- Point extractions  

⚠️ Note: Feature extraction requests return **CoverageJSON**, not the GRIB format used in standard requests.

---

### Regriding

DT data archive model grid is typically in Healpix or Reduced Gausian Grid (reduced_gg). <!-- TODO: Verify -->


#### Server Side Regriding

Polytope as software supports interpolation of archived grid to user defined grid with keywords: "grid". The interpolation is perfomed then on the server side (not using resources from your local machine).

Currently, only Octahedral (O), Full (regular) Gaussian grid (F), healpix (H), original ECMWF reduced Gausian grid (N), and lat/lon grids are supported.
You can read more about our grids [here](https://confluence.ecmwf.int/pages/viewpage.action?pageId=123799065)


If the letter denoting the type of Gaussian grid is omitted, e.g. grid=320, a full (or regular) Gaussian grid with 320 grid lines is returned.

A lat/lon grid can be requested with:
grid = 0.1/0.2 where the first number is the longitude and the second the latitude

grid=av ("archived value") or ommited grid keyword, will retrieve data on the model grid.


#### Client Side Regriddng
Sometimes, Polytope resources might not be sufficient for performing regridding.  <!-- TODO: Check limits -->

Client side regridding is possible using the earthkit regrid library. Earthkit regrid supports the following [grid types](https://earthkit-regrid.readthedocs.io/en/latest/inventory/index.html#matrix-inventory)



### Polytope Quota Limits for DestinE

To keep the system stable and fair for all users, the following limits are applied:

- **API Rate Limit:** up to 50 requests per second (may be adjusted depending on usage).  
- **Concurrent Operations Limit:** no more than 5 active download requests at the same time.  <!-- REVIEW LIMITS -->





