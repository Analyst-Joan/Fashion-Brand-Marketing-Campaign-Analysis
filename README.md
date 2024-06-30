# Marketing Campaign Analysis  - UK Fashion Brand

![Store Image]( Fable_and_thread.jpeg)

[Photo Credit](https://create.microsoft.com/en-us/features/ai-image-generator)

## Background
A UK-based clothing store launched a series of targeted marketing campaigns for the **Spring, Fall, and summer** seasons. Each campaign included **two distinct advertisements** on **Facebook, Pinterest, and Instagram**: one highlighting _discount_ and the other showcasing the _latest clothing collections_. The campaigns specifically targeted three major cities: London, Birmingham, and Manchester. Daily performance metrics were meticulously captured across various dimensions, including cities, channels, devices, and individual ads. These metrics encompassed `Impressions`, `Click-Through Rate (CTR)`, `Clicks`, `Daily Average Cost-Per-Click (CPC)`, `Spend`, `Conversions`, `Total Conversion Value`, `Likes`, `Shares`, and `Comments` 

![](Maketing_campaign_Image.jpeg)

[Photo Credit](https://create.microsoft.com/en-us/features/ai-image-generator)

## About the Data
The dataset is a Microsoft Excel file that contains one table, consisting of **9,900 rows and 18 columns**, of the Daily performance metrics, of a Marketing Campaign data for a **UK Fashion brand**, carried out during 3 seasons in 2023 - Spring (March to May), Summer (June to August), and Fall (October to November). The dataset was gotten from [Onyx Data](https://onyxdata.ck.page/datadna-jun-2024).  

## Client’s Need 
A comprehensive Power BI report that:
-	Analyzes the Marketing Campaign performance metrics
-	Provides insights into the effectiveness of each campaign, and 
-	Identifies opportunities for optimization.
## Target Audience
-	Technical and Non-technical Business Users
## Skills/Concepts applied
-	Defining & Computing KPIs
-	Cleaning/Validation in Power Query
-	Power BI DAX Concepts: Calculated Measures
-	Data Visualization in Power BI
-	[Zoomcharts Drill-Down Visuals](https://zoomcharts.com/en/)  
-	Power BI Dashboard building
-	Filters and Slicers
- Bookmarks and Tooltips 
-	Microsoft PowerPoint (to enhance UI design & commentary)
## Defining Key Performance Indicators (KPIs)
The following metrics were identified as essential Key Performance Indicators (KPIs) to provide the business user with insights into the effectiveness of each campaign, and  Identify opportunities for optimization:

**Provided KPIs (Within the dataset)**
- _Impressions_ – Daily impressions (times ad was shown to a viewer) for each ad
- _CTR (%)_ - Daily average click-through rate for each ad
- _Clicks_ - Daily clicks for each ad
- _Daily Average CPC_ - Daily average cost-per-click for each ad
- _Spend, GBP_ - Total daily amount of advertising spending for each ad, in Great Britain Pounds(GBP)
- _Conversions_ - Total daily purchases attributed to a specific ad
- _Total Conversion Value, GBP_ - Total amount received from purchases attributed to a specific ad (Revenue)
- _Likes_ - Total daily likes (or other reactions) per ad
- _Shares_ - Total daily shares per ad (For the simplicities sake, each Pin on Pinterest was counted as a share)
- _Comments_  - Total daily comments per ad


**Additional(computed) KPIs.**
- Total Engagement - _What is the overall level of user interaction or engagement with our Ads across different metrics (likes, shares, and comments)?_
- Conversion rate (%) - _What percentage of ad viewers are converting into Paying customers?_
- Cost per Acquisition - _How much does it cost to acquire a single customer?_
- Return on Ad-spend (ROAS) - _How much revenue is generated for every dollar spent on advertising?_
- Return on Investment (ROI) (%) - _How much profit or loss is generated from our investment relative to its cost?_
- Monetary ROI (£) - _What is the net financial return (in monetary terms) on our investment after accounting for all costs and revenues?_

## Data Transformation/Preprocessing
The dataset was imported into Power BI’s Power Query for data validation and cleaning.  The column profiling was changed from ‘based on Top 1000 rows’ to ‘based on entire dataset’. ‘Column quality’ and ‘Column distribution’ checkboxes were selected to get a summary information about each column for effective cleaning/Preprocessing. The data table was fairly clean and required minimal transformation, which was carried out as follows:
- Column datatypes were validated appropriately - the data types of Impressions, Clicks and comments columns were changed from decimal to whole number. The data type of Click-through rate (CTR) column was changed from decimal to percentage.
- Columns that contain financial data such as the daily “Average CPC (cost-per-click) & Spend (GBP) Columns were rounded off to 2 decimal places, for consistency.
- There were no missing values, empty cells or duplicates
To enable flexibility of time-based analysis, a **Calendar Table** was then created in power query using the [M Query language](https://devinknightsql.com/2015/06/16/creating-a-date-dimension-with-power-query/) shown below: 
```
//Create Date Dimension
(StartDate as date, EndDate as date)=>
let
    //Capture the date range from the parameters
    StartDate = #date(Date.Year(StartDate), Date.Month(StartDate), Date.Day(StartDate)),
    EndDate = #date(Date.Year(EndDate), Date.Month(EndDate), Date.Day(EndDate)),
    //Get the number of dates that will be required for the table
    GetDateCount = Duration.Days(EndDate - StartDate) + 1,
    //Take the count of dates and turn it into a list of dates
    GetDateList = List.Dates(StartDate, GetDateCount, #duration(1,0,0,0)),
    //Convert the list into a table
    DateListToTable = Table.FromList(GetDateList, Splitter.SplitByNothing(), {"Date"}, null, ExtraValues.Error),
    //Add Year Column
    YearNumber = Table.AddColumn(DateListToTable, "Year", each Date.Year([Date])),
    //Add Quarter Column
         QuarterNumber = Table.AddColumn(YearNumber , "Quarter", each "Q" & 	Number.ToText(Date.QuarterOfYear([Date]))),
     //Add Week Number Column
    WeekNumber= Table.AddColumn(QuarterNumber , "Week Number", each Date.WeekOfYear([Date])),
    //Add Month Number Column
    MonthNumber = Table.AddColumn(WeekNumber, "Month Number", each Date.Month([Date])),
    //Add Month Name Column
    MonthName = Table.AddColumn(MonthNumber , "Month", each Date.ToText([Date],"MMMM")),
    //Add Day Column
    DayNumber = Table.AddColumn(MonthName , "Day", each Date.Day([Date])),
    //Add Day of Week Column
    DayOfWeek = Table.AddColumn(DayNumber , "Day of Week", each Date.ToText([Date],"dddd"))
in
   DayOfWeek
```
An additional table was created to house the social media Channels’ image URL to enhance the visual appeal of the final dashboard.
## Data Modelling
The Model from the cleaned data is a **basic Star Schema** comprising of:
one fact table (the data table) and two, dimension tables (Calendar & Image). The `date` column from the Marketing data table was connected to the `date` column in the calendar table, via a Many-to-one relationship while the `channel` column from the Marketing data table was connected to the `Channel` column in the image table, via a Many-to-one relationship. This is shown in the image below:
![]( marketing_data_Model.JPG)

## Data Exploration (EDA) / KPI Visualization (WIP)

## Key Insights (WIP)

## Recommendations (WIP)

## Dashboard (WIP)
