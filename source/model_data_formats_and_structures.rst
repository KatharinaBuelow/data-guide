
=====================================
**Model data formats and structures**
=====================================

What kind of data do models generally produce?
----------------------------------------------

Regional climate model simulations produce 3-dimensional fields of
climate variables like temperature, humidity, wind velocity etc. and in
addition 2-dimensional fields of surface precipitation, radiation, etc.
ESD, on the other hand, may produce time series for a point (1D), a
group of points (2D) or derived quantities such as storm tracks, and
follow the format of the observations. ESD can also be gridded like
observations to provide 2D data objects. In several portals EURO-CORDEX
data are used to explore climate model data and to calculate climate
impact indicators. Below some links to websites of interest are listed:

-  is-enes project: exploring climate model
   data:\ ` <https://climate4impact.eu/impactportal/general/index.jsp>`__\ `*https://climate4impact.eu/impactportal/general/index.jsp* <https://climate4impact.eu/impactportal/general/index.jsp>`__
-  CLIPC – Climate Information Platform for
   Copernicus:\ ` <http://www.clipc.eu/>`__\ `*http://www.clipc.eu/* <http://www.clipc.eu/>`__
-  IMPACT2C - Quantifying projected impacts under 2°C warming:
   `*https://www.atlas.impact2c.eu/en/* <https://www.atlas.impact2c.eu/en/>`__\ 

How to download EURO-CORDEX projections?
----------------------------------------

EURO-CORDEX simulations for Europe have been performed for two different
horizontal resolutions:

-  0.44 degree (EUR-44, ~50 km)
-  0.11 degree (EUR-11, ~12.5km)

The EURO-CORDEX simulations (EUR-44 and EUR-11) are openly available
through the Earth System Grid Federation (ESGF) under the CORDEX
project.

**Steps towards the data download:**

-  **Accessing and registering at the ESGF Portal**:

   -  Access the Earth System Grid Federation (ESGF) Search Portal via
          one of the available data nodes (Select nodes from:
          `*http://www.data.euro-cordex.net* <http://www.data.euro-cordex.net>`__)

   -  Look for the hyperlink “Create Account” to be granted an ESGF
          OpenID and corresponding password. This account is needed to
          be able to download data.

-  **Searching for data**:

   -  After registration, go back to the Search Portal and look for the
          hyperlink allowing to access the CORDEX Data Search (this may
          differ depending on the portal you chose)

   -  You may specify the data you are looking for by ticking the
          respective selection options on the left (e.g. Project:
          “Cordex”, Domain: “EUR-11”, Variable Long Name: “Air
          Temperature”, etc.)

   -  Clicking on “Search” generates a list with all available data that
          match your specifications.

   -  Clicking on the interrogation mark next to the “Search” button
          provides you with additional search information

-  **Choosing the desired data:**

   -  If you are unsure which item from the list you are looking for,
          press “show metadata” below each result of the data search to
          check for additional information or refine your search
          criteria.

-  **Downloading a certain set of data:**

   -  By opening “Show Files”, you may access a list of files that
          contains the requested data. Depending on the temporal
          resolution of the data, this can be several data files.

   -  You may either download each of these files individually, by
          clicking on “HTTPServer OPENDAP” located right of the file…

   -  ...or you download a shell script by clicking on “WGET Script”,
          which manually downloads all data files if run.

   -  The download of multiple files could be easier via 'datacart'
          option. You can create a wget-script over all selected files
          to download them at once.

-  **Data Access Login:**

   -  Enter your ESGF OpenID and corresponding password to download the
          data

More details on how to access CORDEX data are provided in Data Access
section on the CORDEX website
(`*http://www.cordex.org/index.php?option=com\_content&view=article&id=228&Itemid=537* <http://www.cordex.org/index.php?option=com_content&view=article&id=228&Itemid=537>`__).

A subset of the Euro-CORDEX simulations (both EUR-11 and EUR-44),
bias-adjusted by a few different methods, are also openly available on
ESGF under the CORDEX-Adjust project
(`*http://www.cordex.org/index.php?option=com\_content&view=article&id=275&Itemid=785* <http://www.cordex.org/index.php?option=com_content&view=article&id=275&Itemid=785>`__).
Currently the bias-adjusted daily data for mean/max/min temperature and
precipitation is available. This subset of bias-adjusted Euro-CORDEX
simulations is a first step. At moment not all Euro-CORDEX simulations
are bias-adjusted but work on expanding and filling the bias-adjusted
Euro-CORDEX matrix is ongoing.

How to change netcdf into other formats?
----------------------------------------

The conversion of NetCDF-data into other formats can be carried out with
the Climate Data Operator (CDO), which is available at
`*https://code.zmaw.de/projects/cdo* <https://code.zmaw.de/projects/cdo>`__.
The CDO is a collection of command line operators to manipulate and
analyse climate and numerical weather prediction model Data. Supported
data formats are GRIB, NetCDF, SERVICE, EXTRA and IEG. There are more
than 600 operators available

With this tool, data can be converted into the following data formats:
grb, grb2, nc2, nc4, nc4c, srv, ext, ieg.

To convert a NetCDF-file into a GRIB-file:

cdo -f grb copy input\_file.nc output\_file.grb

Furthermore, there is also an option to write NetCDF-data as a
customised table into an ASCII-file. However, a NetCDF-file containing
two or three dimensional data may not appropriate to write into an
ASCII-file without modifications since the data will be written line by
line according grid-cells and timesteps orders. Therefore, it can be
helpful to calculate a fieldmean of the data or extract one grid-cell
before writing into the ASCII-file first:

To calculate a fieldmean:

cdo fldmean input\_file.nc output\_file.nc

To extract a longitude/latitude point using the *nearest-neighbour
mapping*:

cdo remapnn,lon=XX/lat=yy input\_file.nc output\_file.nc

Notice: When you are using single grid-cells from climate model data, it
may appropriate to calculate the weighted average of each grid point
plus the 8 surrounding points to avoid strange values:

cdo smooth9 input\_file.nc output\_file.nc

To write data as a customised table into an ASCII-file:

cdo outputtab,name,year,month,day,lon,lat,value input\_file.nc
>output\_file.txt

How to read EURO-CORDEX data into analysis tools?
-------------------------------------------------

The free data analysis tool R
(`*http://cran.r-project.org* <http://cran.r-project.org>`__) can read
netCDF files (CF conventions) and allows a large universe of statistical
analysis, tests, and visualisation (e.g. regression and extreme value
analysis). There is a wide range of R-packages which can be installed on
top of R that have been designed for specific uses and purposes. One
such package has been especially designed for general climate data
analysis and ESD, and is freely available from a GitHub repository
(`*http://github.com/metno/esd* <http://github.com/metno/esd>`__). It
has also been written to process RCM results.

How to extract a specific region?
---------------------------------

There are two proven methods how you can select a region: the software
‘Climate Data Operators’ (CDO) for your downloaded files on your
computer or a web-based method
(`*https://climate4impact.eu* <https://climate4impact.eu/>`__) in order
to download data that contain only the region of interest.

Once you have downloaded the EURO-CORDEX simulation (see `*How to
download EURO-CORDEX projections?* <#_2yutaiw>`__), you can select a
region by using the command ‘cdo sellonlatbox’ by giving the longitude
and latitude coordinates of the edges of the region of interest. For
further information or if you have not installed the software CDO,
please follow the introductions of this
website:\ ` <https://code.zmaw.de/projects/cdo>`__\ `*https://code.zmaw.de/projects/cdo* <https://code.zmaw.de/projects/cdo>`__.

When you prefer to download data only for a specific region, use this
web-based method. Login
at\ ` <https://climate4impact.eu/>`__\ `*https://climate4impact.eu* <https://climate4impact.eu/>`__
with your ESGF account, go to Account -> Processing, select ‘convert and
subset.’ Under ‘select a file’, a window opens where you can access via
the ‘search function’ the ESGF data. After choosing your file of
interest, select your file for processing by clicking on the
‘basket’-icon. Back in the main window, you can either select a region
by specifying the longitude and latitude coordinates of the edges of the
region. Or you can select the region with your mouse by changing the
size of the box which is presented on the map on the right.

After choosing a file name at the bottom of the page, you can press the
‘Start processing’ button and a file in netcdf format with your selected
region will be automatically produced and ready for download.

Examples of EURO-CORDEX data use
--------------------------------

In the following, some examples of practical use cases of the
EURO-CORDEX data are listed, e.g., national diagnostics on climate
change. The list is nonexhaustive and growing with time.

-  EURO-CORDEX climate change simulations have already been used in the
   frame of national climate services such as in France through the
   DRIAS web portal
   (`*www.drias-climat.fr* <http://www.drias-climat.fr/>`__\ ).
-  Climate change scenarios retrieved from EURO-CORDEX have provided the
   basis to assess impacts on solar photovoltaic (Jerez et al., 2015)
   and wind power (Tobin et al., 2016) production across Europe along
   the 21st century.
-  EURO-CORDEX simulations will be used in preparing the Climate Change
   Adaptation Strategy for Republic of Croatia (2016-2017;
   `*http://prilagodba-klimi.hr* <http://prilagodba-klimi.hr>`__)
-  EURO-CORDEX simulations form the basis for the Norwegian Climate
   Service Center’s climate projections visualization web service:
   `*https://klimaservicesenter.no/faces/desktop/scenarios.xhtml?org.apache.catalina.filters.CSRF\_NONCE=D73DBECDCC6FA4A727931C4A6E2A8BE6* <https://klimaservicesenter.no/faces/desktop/scenarios.xhtml?org.apache.catalina.filters.CSRF_NONCE=D73DBECDCC6FA4A727931C4A6E2A8BE6>`__

**Further Reading**

-  Jerez, S.; Tobin, I.; Vautard, R.; Montavez, J. P.; Lopez-Romero, J.
   M.; Thais, F.; Bartok, B.; Christensen, O. B.; Colette, A.; Deque,
   M.; Nikulin, G.; Kotlarski, S.; van Meijgaard, E.; Teichmann, C. &
   Wild, M., 2015: The impact of climate change on photovoltaic power
   generation in Europe, Nature Communications, 6,
   `*https://doi.org/doi:10.1038/ncomms10014* <https://doi.org/doi:10.1038/ncomms10014>`__
-  Tobin, I.; Jerez, S.; Vautard, R.; Thais, F.; van Meijgaard, E.;
   Prein, A.; Déqué, M.; Kotlarski, S.; Maule, C. F.; Nikulin, G.; Noël,
   T. & Teichmann, C., 2016: Climate change impacts on the power
   generation potential of a European mid-century wind farms scenario,
   Environmental Research Letters, 11, 034013,
   `*https://dx.doi.org/10.1088/1748-9326/11/3/034013* <https://dx.doi.org/10.1088/1748-9326/11/3/034013>`__

How to cite the EURO-CORDEX ensemble in publications?
-----------------------------------------------------

ToDo

Existing Guidelines

-  Mearns, L. O., F. Giorgi, P. Whetton, D. Pabon, M. Hulme, M. Lal,
   2003: Guidelines for Use of Climate Scenarios Developed from Regional
   Climate Model Experiments, Final Version - 10/30/03, DDC of IPCC
   TGCIA,
   `*www.ipcc-data.org/guidelines/dgm\_no1\_v1\_10-2003.pdf* <http://www.ipcc-data.org/guidelines/dgm_no1_v1_10-2003.pdf>`__\ 
-  Wilby, R.L., Charles, S.P., Zorita, E., Timbal, B., Whetton, P.,
   Mearns, L.O., 2004: Guidelines for Use of Climate Scenarios Developed
   from Statistical Downscaling Methods,
   `*www.ipcc-data.org/guidelines/dgm\_no2\_v1\_09\_2004.pdf* <http://www.ipcc-data.org/guidelines/dgm_no2_v1_09_2004.pdf>`__\ 
-  World Meteorological Organization, 2011: Guide to Climatological
   Practices, WMO-No. 100, World Meteorological Organization, Geneva,
   ISBN 978-92-63-10100-6
-  Bund- Länder- Fachgespräch "Interpretation regionaler
   Klimamodelldaten", 2014: Leitlinien zur Interpretation regionaler
   Klimamodelldaten,
   `*http://klimawandel.hlug.de/?id=448* <http://klimawandel.hlug.de/?id=448>`__\ 
-  Kreienkamp, F., H. Huebener, C. Linke and A. Spekat (2012): Good
   practice for the usage of climate model simulation results - a
   discussion paper. Environmental Systems Research 2012, 1:9,
   `*https://doi.org/10.1186/2193-2697-1-9* <https://doi.org/10.1186/2193-2697-1-9>`__

