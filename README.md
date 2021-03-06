# Extracting Building Values by Zip Code

---

Created by Amit Marwaha, Colton Dowling, and Meggan Lanpher

---

## Problem Statement

During a disaster, it is important to model and estimate the potential or forecasted effect of the event, including the projected/forecasted damage.

Existing indicators of forecasted damage include number of structures within the affected area, number of people in the area, number of households, demographics of the impacted population, etc. This project will add an additional indicator: the value of the properties in the affected area.

## Building a Simple API

### Data Collection

Data Sources:

- [ATTOM Property Data API](https://www.attomdata.com) &rarr; API key needed
- [Zillow](https://www.zillow.com) == [Quandl](https://www.quandl.com) &rarr; API key needed
- [Realtor.com](https://www.realtor.com)
- [Zipcodes](https://pypi.org/project/zipcodes/)

Data Dictionary:

| Feature                   | ATTOM Field Name | Description                                                                 |
| ------------------------- | ---------------- | --------------------------------------------------------------------------- |
| Zip Code                  | postal1          | For the U.S. this is the 5-digit ZIP Code                                   |
| Property type - indicator | proptype         | A specific property classification such as "Detached Single Family"         |
| Calculated Improved Value | calcimprvalue    | Derived Assessed Value of the improvement(s) used to calculate property tax |
| Calculated Land Value     | calclandvalue    | Derived Assessed Value of the land used to calculate property tax           |
| Calculated Total Value    | calcttlvalue     | Derived Total Value used to calculate property tax                          |

### API Deliverable

We created a Simple API that can be utilized in a Python IDE.

First, the user will input the desired zip code and date of which they are interested in seeing property value data. The Simple API will return the Mean, Median, Minimum, Maximum, and Total Values of the Land, Improved, and Calculated Total Property Values.

&rarr; _"There are 9264 properties found in the 78758 zipcode for the year preceding 2/21/2020."_

Then, the user may opt to receive this information broken down by property type.

![Bar Graph of Property Values](images/stacked_property_val_chart_78758_2020_2_21.png)

Lastly, the user may opt to see the historical sales trends of the given zip code.

![ATTOM Sales Trends Data](images/sales_trends_graph_78758_2020_2_21.png)

&rarr; _"This dataset includes 50 months of Zillow sales data."_

![Zillow Sales Trends Data](images/zillow_trends_graph_78758_All_Homes_Median_Price.png)

## Conclusions

Our simple API may be utilized by a government agency, such as FEMA, to determine the range of property values within a given zip code and therefore how much aid may be required to repair damages to properties in the area. This property value data may be combined with many other factors in order to build a prediction model for the direct damages of a natural disaster in a given area. Other factors include but are not limited to the type and severity of the storm, types of industries in the area, and dynamics of the population demographics. Calculating the economic impact of a disaster would include many indirect costs, such as wage loss and decreased market supply. So the total economic loss may not be directly determined, but there is some macroeconomic research that can help explain further damage costs.

### Overview of Interface

The index.html file contains a frame work for a form that submits to a flask app,
as well as embedded Tableau tables. This stage of EDA informed our perspective on
damages caused by a storm. We noted that it was possible for a storm to hit an
unpopulated zip code, or a less insured zip code, or a zip code that costs more to
fix: variation in property market value, material costs, insured for the type
of storm, etc. From this understanding we moved to create a ratio of past payouts
per affected zip codes. This was done with FEMA data, as other data tended to be
propriety from a paid source. You can visually see this relationship in the embedded
tables.

The form then sends the zip code, and time_code information to a function that
returns a series of data frames.

### Challenges:

- API documentation was deprecated or turned into a premium (paid) service
- Zillow aggregate data was no longer available
- Using DASH inside of a Flask app is nuanced
- The format of Plot.ly inside of DASH required manipulating the returned DataFrames

### Resources

- ["How a Disaster’s Economic Impacts Are Calculated"](https://www.theatlantic.com/business/archive/2017/08/harvey-economic-impacts/538353/)
- ["A Multiregional Impact Assessment Model for disaster analysis"](https://www.tandfonline.com/doi/full/10.1080/09535314.2016.1232701)
- ["Predicting Postdisaster Residential Housing Reconstruction Based on Market Resources"](https://ascelibrary.org/doi/pdf/10.1061/%28ASCE%29NH.1527-6996.0000339)
- ["The Economic Impacts of Natural Disasters: A Review of Models and Empirical Studies"](https://academic.oup.com/reep/article/13/2/167/5522921#139660432)
- [(ATTOM API Docs)](https://api.developer.attomdata.com/docs)
