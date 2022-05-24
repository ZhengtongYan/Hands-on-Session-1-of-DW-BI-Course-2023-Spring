# **Hands-on Session 1: DW&BI Project With PostgreSQL and Pentaho**
**This repository contains the instructions of the first hands-on session in our DW&BI course.**

## **Recorded Video Links**
- [Software Installation Guide for Hands-on Session 1 of DW&BI Course](https://www.youtube.com/watch?v=--afzrAZjyc)


## **Learning Objectives**
Gain hands-on experience in building a DW&BI project using PostgreSQL and Pentaho.
- Learn how to create star schema with fact tables and dimension tables using Pentaho Date Integration (PDI);
- Learn how to create OLAP cube using Pentaho Schema Workbench (PSW);
- Learn how to conduct OLAP analysis using Saiku Analytics tool in Pentaho Server.


## **Software Requirements**
**1. Install PostgreSQL database**

* Install PostgreSQL on Windows: 
https://www.postgresqltutorial.com/install-postgresql/
* Install PostgreSQL on Linux: 
https://www.postgresqltutorial.com/install-postgresql-linux/
* Install PostgreSQL on MacOS: 
https://www.postgresqltutorial.com/install-postgresql-macos/

**2. Install the community edition of Pentaho**
- 2.1 Pentaho Server
- 2.2 Pentaho Data Integration (PDI)
- 2.3 Pentaho Schema Workbench (PSW)

Please refer to the two pdf documents about downloading and installing Pentaho software in the Installation Guide folder:
- [Pentaho Installation Guide.pdf](https://github.com/ZhengtongYan/Hands-on-Session-1-of-DW-BI-Course/blob/main/Installation%20Guide/Pentaho%20Installation%20Guide.pdf)
- [Pentaho Installation Problems.pdf](https://github.com/ZhengtongYan/Hands-on-Session-1-of-DW-BI-Course/blob/main/Installation%20Guide/Pentaho%20Installation%20Problems.pdf)

**Many students said that they have problems with installing and running the PDI software in macOS. You can refer to the following articles if you use macOS:**
- [How I setup my Pentaho Data Integration (PDI) and solving the problem on running it on Mac OSX Catalina 10.15.4](https://medium.com/@gembit.soultan/how-i-setup-my-pentaho-data-integration-pdi-and-solving-the-problem-on-running-it-on-mac-osx-6f0cc7f3b97c)
- [ETL Tool: Install pentaho 9.0 on mac (2020)](https://gingkolane.medium.com/install-pentaho8-3-on-mac-on-2-1-2020-69ca6e7b24c5)
- [Pentaho Data Integration not starting on new Mac M1](https://stackoverflow.com/questions/67972804/pentaho-data-integration-not-starting-on-new-mac-m1)



## **Exercises (20 points)**

Download the following data files from the [Data_Sources](https://github.com/ZhengtongYan/Hands-on-Session-1-of-DW-BI-Course/tree/main/Data_Sources) folder and use them to complete the exercises.

- **customers.csv** - Customers information 
- **products.csv** - Products information
- **promotions.csv** - Promotions information
- **salesrep.csv** -  Employees (sales representatives) information
- **orders.csv**	 - Order items information


**1.ETL processing**

Use PDI to create a star schema and store the tables (fact and dimension tables) in PostgreSQL

(1) Create a star schema and then output these tables in PostgreSQL. **(4 points)**

The star schema includes:
 - a fact table (*sales_fact*) 
 - five dimension tables (*customer_dim, date_dim, product_dim, salesrep_dim, promotion_dim*)
 - two measures (*dollars_sold, amount_sold*)

Requirments in the date_dim table:
Please embellish the Date Dimension with the following date attributes:
-  *sales_year*: Year of date 
- *sales_quarter*: Quarter of date
- *sales_month*: Month of date
- *sales_day_of_year*: Day of year of date 
- *sales_day_of_month*: Day of month of date 
- *sales_day_of_week*: Day of week of date 
- *sales_week_of_year*: Week of year of date 


**Tip 1:** Create individual transformation for each table, and create a job to execute all the transformations with condition checks and validations (e.g., check whether the file exists)

**Tip 2:** For the creation of *sales_week_of _quarter* dimension, one possible way is to add a "Formula" step (in the "Scripting" folder) after the "Calculate Additional Fields" step. You can use the "sales_week_of_year" field to calculate the new "sales_week_of_quarter" field.

(2) Discover different slowly changing dimension (SCD) types. **(2 points)**

In the "dimension lookup/update" step, you can set different SCD types to handle the future changes with different ways in the dimension tables. The default type of dimension update is "Insert", i.e., SCD type 2.  
- Step 1: Open the customers_export.csv file;
- Step 2: Find customer 146 Elia Fawcett and change her address from "8989 N Port Washington Rd" to "8990 S Port Washington Rd";
- Step 3: Re-run the transformation, see what happens in the dimension table;
- Step 4: Clear the customer_dim table, and restore the changes in the customers_export.csv file;
- Step 5: Change the type of dimension update from "Insert" to "Punch through' (i.e., SCD type 1);
- Step 6: Repeat step 1 to step 3.
  
Compare the different results of customer_dim table when using SCD type 1 and SCD type 2, and explain the use cases of those two types. 


**Tips**: You may refer to the following wikipedia page about SCD types:
https://en.wikipedia.org/wiki/Slowly_changing_dimension



**2.OLAP Cube Generation**

Use Pentaho Schema Workbench to generate an OLAP cube based on the star schema created in the previous step. This cube should be created on two measures in the five dimension tables. You should create some hierarchies (e.g., year-month-day) on the dimensions. Finally, publish the cube into Pentaho server for further analysis. **(2 points)**


**3. OLAP Analysis and Results Reporting**

(1) Use the Saiku Analytics tool to create an analysis report using the OLAP cube created in the previous step. **(2 points)**

(2) Then, create a report to visualize the analysis results with charts (e.g., line chart, pie chart, and bar chart). **(2 points)**





## **Submission Requirements**: 
- Please upload all the files of ETL processing, OLAP cube generation, etc.
- Please show the star schema figure and give 10 rows of each table. 
- Post the queries and demonstrate the results.
- Please upload all the results in a single PDF file and then compress all the files into a zip file.
- Please submit to Moodle page and the deadline is **April 14th, 2022**.


## **Some Useful Links**
[**1. Pentaho documentation**](https://help.hitachivantara.com/Documentation/Pentaho/9.2)

[**2. Multidimensional Data Modeling in Pentaho**](https://help.hitachivantara.com/Documentation/Pentaho/9.2/Work_with_data/Multidimensional_Data_Modeling_in_Pentaho )

[**3. How to Design a Mondrian Schema**](http://www-master.ufr-info-p6.jussieu.fr/2009/Ext/naacke/mondrian/doc/schema.html#Star_schemas)

[**4. Understanding Pentaho Data Integration(PDI)**](https://www.youtube.com/watch?v=J8NbYQaQiPo&t=4660s)

[**5. Using Pentaho Schema Workbench**](https://www.youtube.com/watch?v=Tqw3oOk5jsM&list=PLIS-R80eiu1snl5wW893-BLiE0yDVhQAe)


