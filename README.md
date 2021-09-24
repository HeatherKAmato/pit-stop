# pit-stop
This READme file was generated on 2021-09-24 by Heather Amato.
Description: Data and files for an interrupted time series analysis of reports of exposed feces before and after San Francisco Pit Stop restroom interventions.


GENERAL INFORMATION

1. Title: Data from: Somewhere to go: Assessing the impact of public restroom interventions on reports of open defecation in San Francisco, California from 2014 to 2020
2. Author Information:
	A. Corresponding author contact info
		Name: Heather K. Amato
		Institution: Environmental Health Sciences, 
		Email: heather_amato@berkeley.edu
		
3. Research Domains: environmental health, WASH

4. Keywords: open defecation, environmental contamination, sanitation, San Francisco, public toilets, homelessness

5. Date of data collection (single date, range, approximate date): January 2014 - January 2020 

6. Geographic location of data collection: 10 neighborhoods of San Francisco, California

7. Funding sources: N/A


SHARING/ACCESS INFORMATION

1. Licenses/restrictions placed on the data: N/A

2. Links to publications that cite or use the data: N/A

3. Recommended citation for this dataset: 
Heather K. Amato, Douglas Martin, Christopher M. Hoover, Jay P. Graham (2021). 
Data from: Somewhere to go: Assessing the impact of public restroom interventions on reports of open defecation in San Francisco, California from 2014 to 2020.
<insert Dryad doi link here>


DATA & FILE OVERVIEW

1. Data: Data on Pit Stop restrooms were obtained from the SF Department of Public Works. Data on 311 calls (i.e. feces reports) are publicly available here: https://datasf.org/opendata/
	
	A. weekly_calls.csv - this is a processed dataset ready for analysis, including the number of 311 calls (i.e. feces reports) within a 500 meter walking distance of each 
  	Pit Stop intervention in each week during a six month pre-intervention period and a six month post-intervention period. This dataset was produced in the RMD file
  	'SF_PitStop_PrepData.Rmd', and is used to conduct the final analysis in 'SF_PitStop_ITSAnalysis.Rmd'.
	
	B. all311calls_filtered.csv - this is a processed dataset containing all 311 calls containing reports of exposed feces. This dataset is necessary for prepping the 
	weekly_calls.csv dataset using code in 'SF_PitStop_PrepData.Rmd'.

	C. buffer_0_1km.shp, buffer_0_322km.shp, & buffer_0_5km.shp - these are shapefiles from walking distance buffer polygons around each Pit Stop intervention location. 
	These files are necessary for creating the weekly_calls.csv in 'SF_PitStop_PrepData.Rmd'.

	D. Pit_Stops_Dates.csv - raw data file with information on Pit Stop restroom interventions.

2. Code:
	A. SF_PitStop_PrepData.Rmd - R code used to process data and conduct spatial/temporal join of Pit Stop interventions and 311 calls. This code uses datasets in B, C, 
	and D listed above, and produces dataset A.

	B. SF_PitStop_ITSAnalysis.Rmd - R code used to conduct interrupted time series analysis and permutation tests using the weekly_calls.csv dataset.


METHODOLOGICAL INFORMATION

1. Description of methods used for collection/generation of data: 
	Data on Pit Stop locations and intervention start dates were provided by the San Francisco Department of Public Works (DPW) upon request. 
	We downloaded San Francisco 311 reports from a public website: https://datasf.org/opendata/. 

2. The following methods were used for processing the raw/collected data used for this submitted dataset: 
	A. Only included Pit Stop interventions implemented between Jan. 1 2014 and Jan. 1 2020.
	B. Only included 311 reports of type 'Human/Animal Waste', excluded reports with “dup” or “transfer” in the status notes, and only included reports from agencies 
  that respond to feces reports.
	C. In ArcGIS Online, we created 500-meter walking distance buffers (polygon derived from all 500m routes following pedestrian paths and roads) around each Pit Stop 
  location to capture the number of 311 feces reports within the surrounding area of each intervention. Feces reports were then spatially and temporally matched to 
  each Pit Stop intervention in RStudio.

3. Software-specific information needed to interpret the data: All analyses were conducted using R Studio version 1.3 using the following packages: 
   sf, lubridate, data.table, ggspatial, mapview, ggpubr, ggplot2, Rmisc, perm, MASS, sandwich, lmtest, car, and tidyverse


DATA-SPECIFIC INFORMATION FOR: weekly_calls.csv

1. Number of variables: 16

2. Number of cases/rows: 4836

3. Variable List: 
id - intervention id (31 unique numeric ids)
site.id - intervention location id (27 unique numeric site ids)
neighborhood - San Francisco DPH Analysis Neighborhoods based on location of Pit Stop intervention
pitstop.type - type of Pit Stop restrooms (Portable, JC Decaux, or Rec + Park)
intervention.type - type of Pit Stop intervention (New Restroom Installed, Existing Restroom, Unstaffed -> Staffed, or Existing Staffed Restroom, Daytime Only -> 24/7)
start.date - start date of Pit Stop intervention
week.start - first day of each week including six months before start.date and six months after start.date
week.end - last day of each week based on start.date
distance.km - walking buffer distance in km (0.1, 0.322, or 0.5)
count - number of 311 calls (i.e. feces reports) within the buffer distance (distance.km) that occurred between the week.start and week.end dates
site - address of Pit Stop restroom
pre.start - first date of six-month pre-intervention period
post.start - first date of post-intervention period
intervention - whether or not the intervention had been implemented during a given week based on week.start (0=pre-intervention, 1=post-intervention)
time - observed week number (1-53) (note: not calendar week number)
month - calendar month number based on week.start (1-12)

4. Missing data codes: N/A
