# Deloitte Case Study

### Dashboard Link : 

## Problem Statement

This dashboard helps  as a collective term to refer to a broad range of economic services provided
by the ﬁnance industry, which encompasses a broad range of organizations that
manage money, including credit unions, banks, credit card companies, insurance
companies, consumer ﬁnance companies, stock brokerages, investment funds A
banking domain is comprised of all the components needed to run a ﬁnancial service
end-to-end. It covers the transaction and distribution process; the ways in which
customers interact with the system, products, and services the organization oﬀers; and
the technology involved.



### Steps followed 
First, for all three files—CPI, exchange rate, and merchandise exports—any missing values should be filled using backfill and forward fill methods. This is because these variables, namely CPI, exchange rate, and merchandise exports, often exhibit a growing trend or remain stable over time. Therefore, the most suitable approach to impute missing values is to use the nearest available value.

    After in Power BI

- Step 1 : Load data into Power BI Desktop, all dataset is  csv file.
- Step 2 : Transform all data table unpivot other(other than period column) in transform option and name new column country
- Step 3 : Than name period column in annual data of all file
- Step 4 : Split period column in monthly data of all file year and month wise name respectively
- Step 5 : Merage all data annually and monthly wise
        
Snap of new annual data ,
![annuAL](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/ae83814b-5427-4ada-bbfe-336a49ef7410)

Snap of new monthly data,
![Monthly](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/2c5f7e1a-b32b-4ff4-9bb9-b9e3ccbd9054)

- Step 6 : After applying Dax querry to get annualy and monthly growth rate of country according to Cpi,Exchange rate and Export Merchandise
  
Following DAX expression was written for the annualy growth of cpi
Percentage Growth of CPI = 
VAR PreviousYearCPI = CALCULATE(MAX('Merge all file annual'[CPI_value]), 
                    FILTER('Merge all file annual', 
                           'Merge all file annual'[Country] = EARLIER('Merge all file annual'[Country]) && 
                           'Merge all file annual'[Year] = EARLIER('Merge all file annual'[Year]) - 1))
RETURN
IF(ISBLANK(PreviousYearCPI), BLANK(), ('Merge all file annual'[CPI_value] - PreviousYearCPI) / PreviousYearCPI * 100)

Exchange rate and Export Merchandise DAX expression also same apart from column name 

-snap after apply DAX expression

![Screenshot 2024-04-22 201224](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/1aa6e29f-42dd-4032-bdf2-ae4e71107782)

Following DAX expression was written for the monthly  growth of cpi
CPI_Growth(%) = 
VAR CurrentCPI = [Cpi_value]  // Replace 'YourCPIColumnName' with the actual name of your CPI column
VAR PreviousCPI = 
CALCULATE(
    MAX([Cpi_value]), 
    FILTER(
        ALL('Merge all file monthly'), 
        'Merge all file monthly'[Country] = EARLIER('Merge all file monthly'[Country]) &&
        'Merge all file monthly'[Month] = EARLIER('Merge all file monthly'[Month]) - 1 &&
        'Merge all file monthly'[Year] = EARLIER('Merge all file monthly'[Year])
    )
)
RETURN
IF(
    ISBLANK(PreviousCPI) || PreviousCPI = 0, 
    BLANK(),
    ((CurrentCPI - PreviousCPI) / PreviousCPI) * 100
)


Exchange rate and Export Merchandise DAX expression also same apart from column name 
-snap after apply DAX expression

![Screenshot 2024-04-22 201504](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/b3b41e34-7d4b-495c-84d2-151a1c85a08d)


- Step 7 : After that card are used for show growth percentage accordingly to monthly and annualy of cpi,Exchange rate and Export Merchandise of
  of different country
- Step 8 : Slicer used Yearly and Country in Annualy page
- Step 9 : Slicer used Yearly ,Country and Monthly in Monthly page
- Step 10 : Use Line Chart to study how one variable impact other variable E.g How export merchandise impact the exchange rate
- Step 11 : Use map to view location of country
  
# Snapshot of Dashboard (Power BI Service)
    Snap of dashboard of annualy
![page1](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/43c22c72-ea2b-4d7c-9945-31388030a084)

  Snap of dashboard of monthly



 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://user-images.githubusercontent.com/102996550/174074051-4f08287a-0568-4fdf-8ac9-6762e0d8fa94.jpg)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings

    a) Baggage Handling - 3.63/5
    b) Check-in Service - 3.31/5
    c) Cleanliness - 3.29/5
    d) Ease of online booking - 2.88/5
    e) Food & Drink - 3.21/5
    f) In-flight Entertainment - 3.36/5
    g) In-flight service - 3.64/5
    h) In-flight Wifi service - 2.81/5
    i) Leg room service - 3.37/5
    j) On-board service - 3.38/5
    k) Online boarding - 3.33/5
    l) Seat comfort - 3.44/5
    m) Departure & arrival convenience - 3.22/5
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Delay 
  
      a) Average delay in arrival(minutes) - 15.09
      b) Average delay in departure(minutes) - 14.71
Average delay will change if different visual filters will be applied.

 ### [4] Some other insights
 
 ### Class
 
 1.1) 47.87 % customers travelled by Business class.
 
 1.2) 44.89 % customers travelled by Economy class.
 
 1.3) 7.25 % customers travelled by Economy plus class.
 
         thus, maximum customers travelled by Business class.
 
 ### Age Group
 
 2.1)  21.69 % customers belong to '0-25' age group.
 
 2.2)  52.44 % customers belong to '25-50' age group.
 
 2.3)  25.57 % customers belong to '50-75' age group.
 
 2.4)  0.31 % customers belong to '75-100' age group.
 
         thus, maximum customers belong to '25-50' age group.
         
### Customer Type

3.1) 18.31 % customers have customer type 'First time'.

3.2) 81.69 % customers have customer type 'returning'.
       
       thus, more customers have customer type 'returning'.

### Type of travel

4.1) 69.06 % customers have travel type 'Business'.

4.2) 30.94 % customers have travel type 'Personal'.

        thus, more customers have travel type 'Business'.
