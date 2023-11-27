# Excel Exploratory Analysis and Data Cleaning

My first objective was to understand the data more by studying how the sheets are setup, what each sheet contains, how columns and rows relate to each other, what is this data telling us, etc.

There are two worksheets contained in this dataset. The first sheet "sales_figures" contains 14 columns. The names of each column and their datatype are as follows:
- MonthYear - Text
- Time Index - General
- Country - General
- StoreID - General
- City - General
- Dept_ID - General
- Dept. Name - General
- HoursOwn - General
- HoursLease - General
- Sales units - General
- Turnover - General
- Customer - General
- Area (m2) - General
- Opening hours - General

The second sheet opening_schemes contains 28 columns. The names of each column and it's dat type are as follows:
- id - General
- Store name - General
- Region - General
- Scheme - General
- Month-by-month:
  -  10.2016 through 09.2017 - All 12 are General
- Cumulated:
  -  10.2016 through 09.2017 - All 12 are General
 
---

Now I want to start to clean up the columns and eliminate any duplicates or irrelevant cells, rows, and/or columns.

In the opening_schemes sheet, I need to correct the Store_name column by removing the id on the left side of the column since id already has its own column.

<img width="281" alt="opening_schemes - Store_name with ID" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/007a8239-4754-4fda-b9ec-68577c36b87c">

I used the `=RIGHT(B7, LEN(B7) - 6)` function to pull only the store name and remove the id # from the column into a new column titled "Store Name (new)".

<img width="381" alt="opening_schemes - Store Name (new)" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/8b04eabf-aa82-4f08-a468-e6b7d5277dec">

---

In the sales_figures sheet, we have data from October 2016 - June 2017.

In this sheet, looking at the columns data types, the HoursOwn column is set up as General instead of Number and has 3 decimal places.

<img width="377" alt="sales_figures HoursOwn General" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/51b08da4-c5a0-4ac0-ada1-6d5f675fd4a2">

I changed the entire column to number and it automatically moves the decimal to 2 decimal places.

Columns HoursLease, Sales units, Turnover, and Area(m2) all have the datatype General, as well. I converted them all to Numeric datatype and eliminated the decimal for all except the HoursLease and Area column.

---

The Customer column doesn't have any information so it has been removed.

<img width="407" alt="sales_figures - Customer blank column" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/fcd052b8-b1ec-42d9-9a18-15fb0bdb112d">

---

I noticed when filtering each column that the Month.Year column has “- - - -” in it. They don’t contain any other information in any other column except the 4 dashes. I also noticed that they are separated by a pretty large number, between 700 and 900 cells. I filled in the background of all 8 of these cells red and found out that they separate each of the months represented in this sheet. They are simply placement dividers for each month of data.

<img width="510" alt="sales_figures - Month Year dashes" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/4b077f77-5f97-4cd3-a4bc-a161afff8bce">

To help me recognize them in the sheet, I filled them in red to make them pop out.

---

For June 2017, the Area column has #NV for all of its rows.

<img width="1083" alt="sales_figures - 06 2017 #NV values" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/3ec8d620-61d8-4e32-b173-04638a1f6151">

Since there is no data for that column for that month, I deleted all rows for 06.2017. We are now only working with data from October 2016 - May 2017.

---

The HoursOwn column has 2 “?”s in it. This is likely a data entry error since there is information for all the other cells that looks relevant.

<img width="1083" alt="sales_figures - Hours Own  ? s" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/7978a41f-4fd1-485e-b150-2e3ebca4bac0">

I filled in the cell color green to help identify and investigate these in their respective cell ranges to make a decision on what to do with these 2 cells.

I calculated the mean for Hours Own, department 2 with the formula `=AVERAGEIF(F:F, "2",H:H)` and resulted in 2471.62.
For department 6, I used the formula `=AVERAGEIF(F:F, "6",H:H)` and resulted in 10217.17.

I believe this is the best way to correct data for these cells. Since they were likely entered incorrectly manually, we now have a close number that represents the mean for these 2 departments to give us an approximate correction.

---

Next, I want to make the datatypes match the data I'm working with instead of most being General. I made the following changes so that when I upload this into a data visualization tool later, the datatypes won't be an issue to work around in the viz tool. I also renamed the columns so that they have more consistent format

sales_figures column changes:
- Month.Year - Text
- Time Index - Number
- Country - Text
- Store ID - Number
- City - Text
- Dept. ID - Number
- Dept. Name - Text
- Hours Own - Number, changed from 3 decimal places to 2
- Hours Lease - Number, added 2 decimal places
- Sales Units - Number
- Turnover - Number
- Area (m2) - Number, kept 2 decimal places
- Opening Hours - Text

opening_schemes column changes:
- Store ID - Number
- Store Name - Text
- Region - Text
- Scheme - Text
- Month-by-month:
  -  10.2016 through 09.2017 - All Number
- Cumulated:
  -  10.2016 through 09.2017 - All Number

---

In the opening_schemes sheet, I deleted the columns for 6/2017 - 9/2017 since we don’t have that data for the sales_figures sheet anymore. We are only working with data from Oct. 2016 - May 2017.

---

I added a Cumulated Hours column to the sales_figures sheet by using VLOOKUP with the following formula:
`=VLOOKUP($E4,opening_schemes!$C$7:$V$56, 20, FALSE)`

This pulls the exact match for Cumulated hours worked from the opening_schemes sheet over to the sales_figure sheet that matches City name in column E.

I replicated this for all cells in the new Cumulated Hours column by simply double clicking the fill handle in the bottom right corner.

---

I created a new column Total Department Hours Ratio where I used the formula

=H3/J3

To get the ratio of how many hours each department worked compared to the amount of hours each store was open.

I then created Conditional Formatting for the Total Department Hours Ratio to make it easier to see how each department fared compared to the hours the store was open. If the ratio was less than 1.0 it is yellow, between 1 and 10 is green, and greater than 10 is blue.

This helps us judge departments in each store based on the hours they worked.

---

I created 2 pivot tables to better view the sales portion of this data.
The first displayed City name in rows, Month.Year in columns, and sum of sales as the values.

<img width="781" alt="Pivot Table - Sum of Sales Units by Store #" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/6101c8f3-bcfc-4c70-ada1-cdb2d6362847">

The 2nd pivot table displayed sales by department over all months.

<img width="788" alt="Pivot Table - Sum of Sales Units by Dept" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/d136dc1a-a3c5-463c-97c5-688af9d4c9b5">

This revealed some interesting data that was much harder to find without this pivot table. A few departments look a little suspicious and require more analysis.

Admin, all, Checkout, Customer Services, other, and others need to be researched more to determine if they should stay in the dataset, be altered, or be removed.

---

Admin didn’t have any meaningful sales data. Sales were either 0 or very low, so it was removed.

Other has some varying figures in Hours Own, Cumulated Hours, Sales Units, etc. but the Total Department Hours Ratio is all the same with 0.02.

<img width="818" alt="sales_figures - other filter" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/13017621-be8e-43fd-b252-89a0cd93fd93">

This seems like an error and since there is already a Non Food department, this department doesn’t seem necessary or relevant.

I also filtered the Customer Services and others departments and both have no significant Sales Units and have been deleted.

The Checkout and the all columns seem to have all the data from everything sold in each store. This can skew the data since we are analyzing each department instead of the whole store, so both have been removed from the dataset.

---

Now I have many blank rows from each department that has been deleted and need to clean this up throughout the whole sheet.

<img width="1143" alt="sales_figures - blanks from deleting departments" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/92adfd06-4ca6-46d9-b6a3-27db1dd554b6">

I had to delete the pivot tables for this next step. Then I selected the cells that I’ve been working on instead of all the cells > clicked on Find & Select > Go To Special > Blanks > OK. This selected all blank cells/rows which I then deleted.

I then recreated the pivot tables.

---

The final sheets look like this:

sales_figures
<img width="1437" alt="sales_figures - final" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/37b0319a-91fb-4441-840b-e366cfe22bf4">

opening_schemes
<img width="1432" alt="opening_schemes - final" src="https://github.com/PaxtonTaylor/Sales-and-Workload-In-Retail-Industry-using-Excel-and-Tableau/assets/147224800/d4f46906-5606-476b-a1d6-2a35f9316dec">

That is all for the data cleaning and analysis in Excel.

Next I will create a visualization for this using Tableau Public.
