# Russian-Energy-Dependence-and-European-Voting-Patterns
Panel regression analysis examining whether dependence on Russian natural gas influences electoral support for pro-Russia and Euroskeptic parties across Europe, using WITS trade data and country election results.

### Project Background 
I wish to study Russian energy dependence and voting patterns in Europe for my final project. Today, Russia plays a substantial role in shaping global energy markets and frequently dominates news headlines regarding natural gas exports and geopolitical actions. As one of the major suppliers of natural gas, Russia is in a unique position to leverage its energy resources as a tool of influence, especially in Europe. I will seek to answer the following questions: does dependence on Russian natural gas influence electoral support for pro-Russia or Euroskeptic political parties in Europe, and does it shape voter sentiment or behavior toward Russia through votes for parties opposing Ukraine aid or EU integration? To explore this empirically, I will assemble a dataset of electoral results from publicly available aggregated datasets and individual country election reporting offices and Russian natural gas imports by country over time from the World Bank data platform World Integrated Trade Solution (WITS). I will then build a model using panel regressions and country and time fixed effects. 


### Data Sources and Background

**Gaseous and Liquid Natural Gas** 
*https://wits.worldbank.org/trade/comtrade/en/country/ALL/year/2024/tradeflow/Imports/partner/RUS/product/271111*
*https://wits.worldbank.org/trade/comtrade/en/country/ALL/year/2024/tradeflow/Imports/partner/RUS/product/271121*

The World Bank's World Integrated Trade Solution (WITS) reports imports of both liquid and gas form natural gas from 1992 to 2024 for a variety of countries and sources. WITS is a free platform that draws its data from the UN's Comtrade platform. As a result, sharing the raw data is not allowed but including brief summary tables and visualizations for a project is allowed. 

Because country natural gas usage can vary depending on population and size, I create two variables, "ngg_ratio" for gas form and "lng_ratio" for liquid form. They are calculated by taking the ratio of natural gas imported from Russia over the amount of natural gas imported from all countries for each country, year, and form.

**CHES**  
*https://www.chesdata.eu/ches-europe*

The Chapel Hill Expert Survey collects data on ideological and political positioning of parties and relationships between parties and international entities across the world. I use CHES data to create two variables: "euroskep" and "envs"

I created "euroskep" to represent the overall voteshare for euroskeptic parties for each country. The variable is calculated using the CHES “EU_POSITION” variable. “EU POSITION” ranges from 1 to 7 representing the following:
	1 = Strongly opposed
	2 = Opposed
	3 = Somewhat opposed
	4 = Neutral
	5 = Somewhat in favor
	6 = In favor
	7 = Strongly in favor. 
Countries with a score of 3 or less were coded as euroskeptic and given a binary value, 1 for true, and 0 for false. The final euroskep variable is calculated by finding the total vote share attributed to parties flagged as euroskeptic for each country and year combination. Values can range from 0 to 1.

I created "env" to represent a party's priority of enviornmental sustainability versus economic growth. The "ENVIONMENT" variable in the CHES data trend file ranges from 0, where a party "strongly supports environmental protection even at the cost of economic growth" to 10 where a party "strongly supports economic growth even at the cost of environmental protection". Parties with a 4 or lower “ENVIRONMENT” score are coded as 1 meaning they support the environment over the economy and all other values are coded as 0 since they are either neutral or value the opposite. The final “env” variable is created by aggregating the total voteshare of parties who support the environment over economic growth. Values can range from 0 to 1.

**Eurostat**  
*https://ec.europa.eu/eurostat/databrowser/view/nrg_ind_id/default/table?lang=en*

Eurostat provides data on energy import dependency by country and year. Data is in percent form which represents the total share of energy needs met by foreign imports calculated by the following equation: Energy dependence = (imports – exports) / gross available energy. Negative scores represent countries that are net exporters and a score of over 100% means energy has been stored. Energy is counted as domestic if it is produced in the same country even if input materials are imported from other countries. 

**Our World In Data**  
*https://ourworldindata.org/grapher/gdp-per-capita-worldbank*

Data on GDP per capita is sourced from Our World in Data and it is calculated by taking the GDP and dividing by population. They have aggregated values from the World Bank's World Development Indicators using international purchasing power parity reported in constant 2021 USD prices to adjust for inflation. Observations are widely available for every country and year.

**European Commission** 
*https://economy-finance.ec.europa.eu/euro/eu-countries-and-euro_en* 

Data on when each country joined and left the EU as well as when they adopted the Euro (if applicable).

**Dummy Variables**

Georgia (post2008)
“post2008” is a dummy variable that indicates if the year is after the August 2008 Russian invasion of Georgia. Years before and including 2008 are “0” and years after 2008 are ”1”. 

European Debt Crisis (post2013)
"eu_debt" is a dummy variable that indicates years 2010-2013 to account for the debt crisis.

Crimea (post2014)
“post2014” is a dummy variable that indicates if the year is after the March 2014 Russian annexation of Crimea. Years before and including 2014 are “0” and years after 2014 are ”1”. 

Ukraine (post2022)
“post2022” is a dummy variable that indicates if the year is after the February 2022 Russian invasion of Ukraine. Years before and including 2022 are “0” and years after 2022 are ”1”. 

USSR Alignment (postcomm)
“postcomm” is a dummy variable that indicates if a country was aligned with the Soviet Union following World War II. Countries that were included in the USSR or were Soviet satellite states are coded with “1”. All other countries are coded with “0”.


