# Customer Insights and Sales Performance Dashboard

## Project Overview

This project, titled **Customer Insights and Sales Performance Dashboard**, focuses on analyzing retail transactional data to uncover insights into customer behavior, segmentation, and sales patterns. The project was undertaken to develop a comprehensive understanding of customer dynamics, particularly focusing on retention rates, repeat customer behavior, and sales performance across various segments.

### Dashboard Preview
![Dashboard](https://github.com/user-attachments/assets/97a22545-f06f-4337-8746-8c44d75f745f)
[View the full interactive dashboard here](https://www.novypro.com/profile_projects/jagger-01?Popup=memberProject&Data=1723587669154x508693181431507700)

## Problem Statement

Retail businesses thrive on understanding their customers and optimizing sales strategies based on data-driven insights. However, raw data is often messy and requires significant cleaning and processing before it can be used for meaningful analysis. In this project, I started with a retail transactional dataset that contained several inconsistencies and missing values. The challenge was to clean this data, derive meaningful insights, and present them in a user-friendly dashboard.

## Dataset

The dataset used in this project was sourced from [Kaggle](https://www.kaggle.com/datasets/bhavikjikadara/retail-transactional-dataset/data) (Retail Transactional Dataset). The dataset contains detailed information on customer transactions, including:

- **Customer Information:** Customer ID, Name, Email, Phone, Address, City, State, Zipcode, Country, Age, Gender, Income, Customer Segment.
- **Transaction Details:** Last Purchase Date, Total Purchases, Amount Spent.
- **Product Information:** Product Category, Product Brand, Product Type.
- **Feedback:** Customer feedback or rating related to the product or service received.
- **Transaction Logistics:** Shipping Method, Payment Method, Order Status.

## Project Workflow

### 1. Data Cleaning

The first step involved cleaning the raw dataset to remove inconsistencies, handle missing values, and prepare the data for analysis. This was achieved through a series of steps, which are documented in the Jupyter notebook **Clean_The_Data.ipynb**. Key steps include:

- **Dropping rows with missing critical information:** Rows with missing values in key columns like `Transaction_ID`, `Customer_ID`, `Email`, `Phone`, etc., were removed to ensure data integrity.
- **Handling duplicates:** Duplicates were identified based on `Transaction_ID` and `Customer_ID`, and only the first occurrence was retained.
- **Filling missing values:** Missing values in columns such as `Amount`, `Total_Purchases`, and `Total_Amount` were calculated and filled based on existing data.
- **Parsing dates:** Dates were parsed and converted into a consistent format. Additional columns for `Year`, `Month`, and `Day_of_Week` were created to facilitate time-based analysis.
- **Dropping rows with missing `Zipcode` or `Address`:** Rows missing both `Zipcode` and `Address` were removed, and further missing values in `City`, `State`, or `Country` were filled where possible.

The cleaned dataset was saved as both a CSV and an Excel file to ensure compatibility with various tools.

#### **Data Cleaning Process**
![Cleaning Preview](https://github.com/user-attachments/assets/95f38fdf-7cb9-4649-ac3c-d35b65f4d799)

### 2. Data Conversion for Power BI

To make the cleaned data compatible with Power BI, it was saved as an Excel file using the notebook **csv to xlsx.ipynb**. This step ensured no loss of data and allowed seamless integration into Power BI for visualization.

#### **Data Conversion**
![Data Conversion Preview](https://github.com/user-attachments/assets/9c5c2aad-ca51-44db-99a2-b6ac817080f1)

### 3. Dashboard Creation in Power BI

The cleaned data was imported into Power BI to create a dynamic and interactive dashboard. The dashboard, titled **Customer Insights and Sales Performance Dashboard**, includes the following components:

- **Main Left Column - Customer Overview:**
  - **Retention Rate:** Displayed as both a text percentage and a doughnut chart.
  - **3-Panel Card:** Shows the number of customers, average order value, and repeat customer rate.
  ![Main Left Column](https://github.com/user-attachments/assets/a6e0c56c-367b-4c90-b073-e8f552982d70)

- **Top Row:**
  - **3-Panel Card:** Displays total sales, units sold, and average rating.
  - **Year Filter:** Allows filtering by year (2023 - 2024).
  ![Top Row](https://github.com/user-attachments/assets/70202837-b645-416f-82df-ec42edfe7c46)

- **Middle Row:**
  - **Ribbon Chart:** Visualizes customer segmentation over time by month.
  - **Column Graph:** Shows sales by customer segment.
  ![Middle Row](https://github.com/user-attachments/assets/934f4fd8-65e1-44ae-88a6-f648f7de4cb0)

- **Bottom Row:**
  - **Small Doughnut Chart:** Displays sales by category.
  - **Large Matrix:** Shows sales per category by month.
  ![Bottom Row](https://github.com/user-attachments/assets/957a5ad6-be11-4d50-a279-b03308366d0b)

### 4. DAX Calculations

To further enhance the dashboard, DAX (Data Analysis Expressions) was used to create custom columns and measures:

- **Combined Customer Segment Column:**
  ```DAX
  CombinedCustomerSegment = 
  SWITCH(
      TRUE(),
      'Retail-Sales-Analysis'[Customer_Segment] = "Premium", "Returning Customer",
      'Retail-Sales-Analysis'[Customer_Segment] = "Regular", "Returning Customer",
      'Retail-Sales-Analysis'[Customer_Segment] = "New", "New",
      BLANK()  // Handle any unexpected values
  )
  ```

- **Repeat Customer Rate Measure:**
  ```DAX
  RepeatCustomerRate = DIVIDE(
      CALCULATE(DISTINCTCOUNT('Retail-Sales-Analysis'[Customer_ID]), 'Retail-Sales-Analysis'[Customer_Segment] = "Regular"),
      DISTINCTCOUNT('Retail-Sales-Analysis'[Customer_ID])
  )
  ```

- **Retention Rate Measure:**
  ```DAX
  RetentionRate = 
  DIVIDE(
      CALCULATE(
          COUNTROWS('Retail-Sales-Analysis'), 
          'Retail-Sales-Analysis'[CombinedCustomerSegment] = "Returning Customer"
      ),
      COUNTROWS('Retail-Sales-Analysis'),
      0  // Optional: Default value to return if the denominator is 0
  )
  ```

#### **DAX Calculations**
![DAX Calculation](https://github.com/user-attachments/assets/ab1e0093-ee62-4283-9dfc-db414274f17a)

### 5. Final Output and Visualization

The final output is a Power BI dashboard that provides comprehensive insights into customer behavior, segmentation, and sales performance. The dashboard is visually appealing and user-friendly, allowing stakeholders to make informed decisions based on data.

### **Link to Dashboard**
[View the full dashboard here](https://www.novypro.com/profile_projects/jagger-01?Popup=memberProject&Data=1723587669154x508693181431507700)

## Tools Used

- **Python (Pandas, NumPy):** For data cleaning, manipulation, and processing.
- **Jupyter Notebook:** For documenting and running the data cleaning process.
- **Power BI:** For data visualization and creating the interactive dashboard.
- **DAX (Data Analysis Expressions):** For creating custom columns and measures in Power BI.
- **Icons8:** For sourcing icons used in the dashboard.

## Conclusion

This project demonstrates the entire workflow from raw data to actionable insights, showcasing my ability to clean, process, and analyze large datasets using Python and Power BI. The final dashboard provides valuable insights into customer behavior and sales performance, enabling data-driven decision-making. 

For further details, you can explore the provided notebooks and the Power BI dashboard.

### **License**
This project is licensed under the MIT License.