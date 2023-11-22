# Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau

## Introduction

I wanted to practice more advanced Excel functions and get more familiar with Tableau Public while working with a new dataset.

### Context

Raw data of real analytical use cases in a number of industries and companies is frequently provided in an Excel-based form. Here, an Excel spreadsheet will be presented which in this form is closely oriented to a real case, but contains only simulated figures for reasons of data and business results protection. The form and structure of the file correspond to a real case and could be encountered by a data scientist in a company in this way. Such a file can be the result of a download from a financial controlling system, e.g. SAP.

## Data

The data used for this project is available via Kaggle as [Sales and Workload in Retail Industry](https://www.kaggle.com/datasets/dgluesen/sales-and-workload-data-from-retail-industry) by Dennis Gluesenkamp. This workbook contains 2 sheets - sales_figures and opening_schemes.

The data includes information about sold goods resp. product units, the associated turnover and hours worked. This information is grouped by month, store and department of the retailer. Moreover, information about the sales area in a specific department as well as about the opening hours of the store is provided.

This dataset uses a free, copyleft license for software and other kinds of work under [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html).

## Data Exploration, Cleaning, and Analysis

I used Excel to clean raw data from a dataset with 2 different sheets and analyzed that data with using more intermediate and advanced Excel functions and practices.

I performed the following data cleansing and analysis in Excel:
- Removed text from a column using =RIGHT function.
- Reformatted the data type of certain columns.
- Used filters to simplify data.
- Deleted columns that were empty or irrelevant.
- Found missing data using =AVERAGEIF function.
- Renamed column headers for continuity.
- Added columns with data from one table to another using VLOOKUP.
- Created a ratio calculation by dividing one column results from another column.
- Used conditional formatting to highlight certain cells that were below, between, and above a determined mark.
- Created 2 pivot tables to display certain data points much easier.


You can download and view the raw, uncleaned data [here](https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/files/13433883/salesworkload_raw.xlsx).


You can download and view my cleaned data with [here](https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/files/13433863/salesworkload_cleaned.xlsx).
