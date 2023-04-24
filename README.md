# Analysis of "Gentrification" data set — 2000 to 2017 


## Data

The spreadsheets with our data come from the following sources:

- Name of source:
  - 'new york city, new york_data.csv': Raw measurements on demographic changes in NYC, including changes in census tracts according to race, median home value or income
  - 'file_201_data_sm_tract.csv': Filtered Tax Commision Income and Expense data from the Department of Taxation. 

Each of the spreadsheets contain, among others, the following columns relevant to the analysis:

- 'new york city, new york_data.csv
    - `GEOID` — Census Tract ID
    - `gentrified` — Identifies whether or not a particular tract has been gentrified between 2000 and 2017
    
- 'file_201_data_sm_tract.csv'
    - `Unregulated` – number of unregulated units in xyz 
    - 'Regulated' – number of regulated units in xyz
    - `TOTAL INCOME FROM REAL ESTATE'
    
## Methodology

The notebook [`Merged Data - Gentrification`] performs the following analyses:


##### Part 1: Filter Tracts
- Removed (Blank) items from the “tract_10” column in order to better identify census tracts and BBL numbers of select buildings/rental properties.
- Hid columns including: 
    -FROM_LOT
    -TO_LOT
    -FILING YEAR

##### Part 2: Use '=SPLIT' function 
- Added a new column to the Demographic Data sheet named “Boro”
-Identified which borough each building belonged to by splitting text in the original “name” column, which labels the name of each census tract. This was done to later easily sort and filter demographic and TCIE data according to borough population. 

##### Part 3:  '=Vlookup' series to merge data 
- =vlookup(boro)
Used tract_10 and GEOID data to merge data from “Boro” column with TCIE data

- =vlookup(population)
Transferred total population data from Demographic Data to TCIE data sheet 

- =vlookup(gentrified)
Added “Gentrified?” data to TCIE data sheet from Demographic Data sheet

- =vlookup(pct_white_alone_chg)
Added column to TCIE data sheet listing percentage-point change for population that was white alone in order to analyze if an increase or decrease of white tenants in an area correlates with gentrification in an area.

- =vlookup(pct_Black_alone_chg)
Added column to TCIE data sheet listing percentage-point change for population that was Black alone in order to analyze if an increase or decrease of white tenants in an area correlates with gentrification in an area.

- =vlookup(various populations)
Transferred 2019 demographic info of tenants of all races to TCIE data sheet to further analyze how and if the racial/ethnic make-up of a community reflects gentrification

##### Part 4: Analysis of Unregulated Units
- Sorted items by tract_10 and deleted rows that had blank values, so we’ll only look at rows that have both TCIE data and demographic data.
- Filter the “Unregulated” row to hide blank entries from view — now we’ll only look at rows that describe buildings with unregulated units.
- Use =COUNT function to count the number of rows (buildings) with unregulated units.
- Use =COUNTIF function to count how many unregulated unit buildings are in each borough. (Ex. =COUNTIF(C2:C135, “New York County”) for Manhattan)
- Use =AVERAGE and =MEDIAN to find averages of income for unregulated units.
- Use =AVERAGE to find average change in population for white residents and for Black residents.
- Take sums of total population, total white population, total Black population, etc. Then divide the sum of each racial group by the total population to find the percent of population. (Ex. (sum of Asian population for all unregulated rows) divided by (sum of total population for all unregulated rows) equals average Asian population for all.

##### Part 5: Analysis of Regulated Units
- Filtered items by “Regulated” only, leaving blanks outside. 
- Copied all the items and pasted it without values in another sheet.
- Did a pivot table. In values I put the “census code”. Just with that, I had the number of regulated buildings. In columns, I used the “BORO” column, which gave me the number of regulated units each borough had.
- To calculate the average, formatted the “Regulated” columns to numbers and used the formula “AVERAGE”.
- To calculate the median, I duplicated the “Regulated column” and used the “MEDIAN” formula. 
- Take sums of total population, total white population, total Black population, etc. Then divide the sum of each racial group by the total population to find the percent of population. (Ex. (sum of Asian population for all unregulated rows) divided by (sum of total population for all unregulated rows) equals average Asian population for all.

##### Part 6: Identify Gentrified Units
- Filter sheet "Gentrified, True"
- Use COUNT function in column "C" to measure number of gentrified units in each borough
    -e.g. =COUNTIF(C2:C244, "New York County")

##### Part 7: Remove "(blank)" cells
- filter out “blank” from the REGULATED column. Count the number of remaining rows. Repeat in UNREGULATED column.

##### Part 8: Calculate demographic info
- Use SUM function to determine population for each racial group 
    (white, Black, Native American, Asian, Native Hawaiian Pacific Islander (NHPI), Hispanic). 
- Divide sum of each racial group by total population to find %s.

##### Part 9: Calculate BORO info 
- Sort BORO NAME column by A-Z
- filter for "Kings County"
- Use SUM function to determine population for Kings County
- Divide sum by total population to find %s.
- Repeat for "New York County"

##### Part 10: Calculate percent change 
-  Use =AVERAGE function To find average % changes of white and Black populations
- Filter column BORO NAME to find % change in Brooklyn (Kings County) and Manhattan(New York County)

##### Part 11: Calculate average and mediam total income from real estate
- Use =AVERAGE and =MEDIAN functions for all values in TOTAL INCOME FROM REAL ESTATE column to find average and median total income from real estate

##### Part 12: Identify units that are not gentrified
- In a new sheet, filter data "Gentrified, False only"
- Repeat Parts 6 - 11

## Outputs

The notebooks output this spreadsheet which contains TKTK: [`output/tktktk.csv`](output/tktktk.csv).

## Running the analysis yourself

You can run the analysis yourself. To do so, you'll need the following installed on your computer:

- Python 3
- The Python libraries specified in [`requirements.txt`](requirements.txt)

## Licensing

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.

## Feedback / Questions?

Contact Amaya McDonald at amaya.mcdonald90@journalism.cuny.edu
