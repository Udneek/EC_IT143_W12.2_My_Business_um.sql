# EC_IT143_W12.2_My_Business_um.sql

/*****************************************************************************************************************
NAME:    My Script Name
PURPOSE: My script purpose... Answer dataset questions .... kalimati_tarkari_dataset.csv 

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/23/2023   Uduak Mbaba       1. Built this script for EC IT440


RUNTIME: 
Xm Xs

NOTES: 
This script is created to answer questions I created for my datasets; kalimati_tarkari_dataset.csv.
 
******************************************************************************************************************/

-- Q1: What is the percentage change in the average price of fruits and vegetables in Nepal from 2019 to 2020? 
---   How does this compare to the percentage change in previous years?
-- A1: Create a sql script to query the dataset.

SELECT ((AVG(price) FILTER (WHERE year = 2020) - AVG(price) FILTER (WHERE year = 2019)) / AVG(price) FILTER (WHERE year = 2019)) * 100 AS percent_change_2019_2020,
       ((AVG(price) FILTER (WHERE year = 2019) - AVG(price) FILTER (WHERE year = 2018)) / AVG(price) FILTER (WHERE year = 2018)) * 100 AS percent_change_2018_2019
FROM kalimati_tarkari_dataset
WHERE year IN (2018, 2019, 2020);




/*****************************************************************************************************************
NAME:    My Script Name
PURPOSE: My script purpose... Answer dataset questions .... kalimati_tarkari_dataset.csv 

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/23/2023   Uduak Mbaba       1. Built this script for EC IT440


RUNTIME: 
Xm Xs

NOTES: 
This script is created to answer questions I created for my datasets; kalimati_tarkari_dataset.csv.
 
******************************************************************************************************************/

-- Q2: Which fruits and vegetables have seen the greatest percentage increase in prices between pre-COVID-19 (2019) 
---    and post-COVID-19 (2020-2021) in Nepal?
-- A1: Create a sql script to query the dataset.

    SELECT 
          Commodity,
            100 * (AVG(CASE WHEN YEAR(date) = 2020 OR YEAR(date) = 2021 
            THEN average_price ELSE NULL END) - AVG(CASE WHEN YEAR(date) = 2019 THEN average_price ELSE NULL END)) / 
            AVG(CASE WHEN YEAR(date) = 2019 THEN average_price ELSE NULL END) AS percentage_increase
    FROM kalimati_tarkari_dataset
    GROUP BY Commodity
    ORDER BY percentage_increase DESC;
    
    
    
    
    /*****************************************************************************************************************
NAME:    My Script Name
PURPOSE: My script purpose... Answer dataset questions .... kalimati_tarkari_dataset.csv 

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/23/2023   Uduak Mbaba       1. Built this script for EC IT440


RUNTIME: 
Xm Xs

NOTES: 
This script is created to answer questions I created for my datasets; kalimati_tarkari_dataset.csv.
 
******************************************************************************************************************/

-- Q3: Which commodities have experienced the largest price increases and which have experienced the largest price decreases?
-- A1: Create a sql script to query the dataset.

    SELECT Commodity, 
          (MAX(average_price) - MIN(average_price)) / MIN(average_price) * 100 AS percentage_change,
          MAX(average_price) AS max_price,
          MIN(average_price) AS min_price
    FROM kalimati_tarkari_dataset
    WHERE date >= '2013-01-01' AND date <= '2021-12-31'
    GROUP BY Commodity
    ORDER BY percentage_change DESC;
    
    
    
    
        /*****************************************************************************************************************
NAME:    My Script Name
PURPOSE: My script purpose... Answer dataset questions .... kalimati_tarkari_dataset.csv 

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/23/2023   Uduak Mbaba       1. Built this script for EC IT440


RUNTIME: 
Xm Xs

NOTES: 
This script is created to answer questions I created for my datasets; kalimati_tarkari_dataset.csv.
 
******************************************************************************************************************/

-- Q4: What is the overall percentage change in the average price of each commodity from 2013 to 2021?
-- A1: Create a sql script to query the dataset.

      SELECT Commodity, 
            (MAX(average_price) - MIN(average_price)) / MIN(average_price) * 100 AS percentage_change
      FROM kalimati_tarkari_dataset
      WHERE date >= '2013-01-01' AND date <= '2021-12-31'
      GROUP BY Commodity
      ORDER BY percentage_change DESC;
      
      
      
      
/*****************************************************************************************************************
NAME:    My Script Name
PURPOSE: My script purpose... Answer dataset questions .... interest_rate.csv

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/23/2023   google       1. Built this script for EC IT440


RUNTIME: 
Xm Xs

NOTES: 
This script is created to answer questions I created for my datasets; interest_rate.csv
 
******************************************************************************************************************/

-- Q5: How has the interest rate changed for each country since the start of the dataset?
-- A1: Create a sql script to query the dataset.

      SELECT 
          date, 
          federal_reserve, 
          europen_bank, 
          england_bank, 
          brazil_bank, 
          swiss_bank, 
          japan_bank 
      FROM 
          interest_rate;
          
          
          
          

/*****************************************************************************************************************
NAME:    My Script Name
PURPOSE: My script purpose... Answer dataset questions .... cardata.csv

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/23/2023   google       1. Built this script for EC IT440


RUNTIME: 
Xm Xs

NOTES: 
This script is created to answer questions I created for my datasets; cardata.csv
 
******************************************************************************************************************/

-- Q6: What is the total number of cars sold for each car model by fuel type, seller type, and transmission?
-- A1: Create a sql script to query the dataset.

      SELECT car_name, fuel_type, seller_type, transmission, COUNT(*) AS total_cars_sold
      FROM ardata
      GROUP BY car_name, fuel_type, seller_type, transmission
      ORDER BY total_cars_sold DESC;




