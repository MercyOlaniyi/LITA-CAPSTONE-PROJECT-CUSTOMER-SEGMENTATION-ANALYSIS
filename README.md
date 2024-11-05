# LITA-CAPSTONE-PROJECT-Customer Subscription Analysis

### Project Overview

This repository contains the code and data for analyzing customer subscription data for a fictional subscription service. The goal is to understand customer behavior, track subscription types, and identify trends in cancellations and renewals.

### Dataset Description

The dataset consists of information such as CustomerID, CustomerName, Region, SubscriptionType, SubscriptionStart, SubscriptionEnd, Canceled, Revenue

#### Data Source
This is a public dataset that was freely provided by the facilitator.

#### Data Fields

The customer_data excel file contains the following columns:

- CustomerID: Unique identifier for each customer

- CustomerName: Name of the customer

- Region: Region of the customer

- SubscriptionType: Type of subscription (Basic, Standard, Premium)

- SubscriptionStart: Start date of the subscription

- SubscriptionEnd: End date of the subscription

- Canceled: Whether the subscription was canceled (TRUE/FALSE)

- Revenue: Revenue generated from the subscription

#### Time Period
The dataset spans from 2022-2024

### Exploratory Data Analysis 

The following insights will be drawn from the dataset

- Key customer segments
  
- Subscription cancellations

- subscription trends.

### Data Preprocessing

Data loading and inspection: To have a general overview of the data

**Data Cleaning Process**

During the initial data inspection, several duplicate rows were identified, which could potentially skew the analysis results. To address this:

**1. Identification of Duplicates:**
   
**- Method:** Conditional formatting in Excel was used to highlight duplicate rows, enabling quick identification of repeated data entries.
  
**2. Removal of Duplicates:**
   
**- Tool:** Excel’s "Remove Duplicates" function was applied to eliminate all duplicate entries from the dataset.
  
**- Fields Considered:** Duplicate checks were conducted across key fields (e.g., customer ID, subscription type, and date fields) to ensure unique records without unintended loss of data.
  
After this cleaning step, the dataset was verified to ensure accuracy and consistency before proceeding with further analysis.

#### Analytical Tools Employed

- Microsoft Excel was used in analysis and summarization of the dataset

- SQL was used to query the data for further insights

- PowerBI was used to visualize the insight drawn from the dataset.

### Analysis Breakdown

#### 1a. Using Excel, Use pivot tables to summarize

**i. Average subscription duration**

![Calculating Average Sub Duration](https://github.com/user-attachments/assets/916bb719-3db5-41ed-b75e-c77c11358f29)

**ii. The most popular subscription types**

![Most Popular Sub Type](https://github.com/user-attachments/assets/40a5c539-2906-4773-ba22-aa019b74f123)

**iii. Revenue Generated by Region**

![Revenue by Region](https://github.com/user-attachments/assets/a7386080-0dce-4b0b-9b09-f0c326422ba0)

**iv. Revenue by Subscription Type**

![Revenue by Subscription type](https://github.com/user-attachments/assets/9e62c673-29f5-48f9-8559-c3b407603beb)

**v. Subscription Trend**

![Subscription Trend](https://github.com/user-attachments/assets/1c4b88e8-8610-4bfa-b4d0-a5b4f0b0b049)

**vi. Top 5 Subscribers**

![Top 5 Subscribers](https://github.com/user-attachments/assets/5f07f2a6-4f31-4094-b0bf-5908354a3816)

#### 1b. Write queries to extract key insights

**i. Total number of customers from each region**

```
SELECT region, COUNT(CustomerID) AS Total_Customers
FROM Customer_data
GROUP BY region
ORDER BY region;
```

![Total Sales by Customers SQL](https://github.com/user-attachments/assets/513a00e1-40cb-4e1a-86ce-3f1ee9693004)

**ii. Most popular subscription type by the number of customers.**

```
SELECT TOP 1 SubscriptionType, COUNT(CustomerID) AS Total_Customers
FROM Customer_data
GROUP BY SubscriptionType
ORDER BY Total_Customers DESC;
```

![Most Popular Sub by Customers](https://github.com/user-attachments/assets/0ce5ad0c-1b47-4bf4-96e0-b2fb483681e4)

**iii. Customers who canceled their subscription within 6 months;** None. All subscription were for 12 months or higher

```
SELECT CustomerID, SubscriptionType, Region, 
       DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) AS Subscription_Duration
FROM Customer_data
WHERE DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) <= 6
  AND Canceled = 'TRUE';
```

![Customers who canceled in 6 Months](https://github.com/user-attachments/assets/1b680a83-a73e-4e00-a76b-27e36a9590c7)

**iv. The average subscription duration for all customers.**

```
SELECT AVG(DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd)) AS Average_Subscription_Duration
FROM Customer_data;
```

![Average Sub Duration](https://github.com/user-attachments/assets/f6ec92ea-ada5-4171-b231-2a79dec36d8a)

**v. Customers with subscriptions longer than 12 months.**

```
SELECT CustomerID, SubscriptionType, Region, 
       DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) AS Subscription_duration
FROM Customer_data
WHERE DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) > 12;
```

![Sub Longer than 12 months](https://github.com/user-attachments/assets/e9708b85-8be3-4466-ae0d-96ea0ad0e5b5)

**vi. Total revenue by subscription type.**

```
SELECT SubscriptionType, SUM(Revenue) AS Total_Revenue
FROM Customer_data
GROUP BY SubscriptionType;
```

![Total Revue by Sub Type](https://github.com/user-attachments/assets/ba8f896a-cfe6-4a02-a2a3-982a0b51c909)


**vii.  The top 3 regions by subscription cancellations.**

```
SELECT TOP 3 region, COUNT(CustomerID) AS Total_Cancellations
FROM Customer_data
WHERE Canceled = 'TRUE'
GROUP BY Region
ORDER BY Total_Cancellations DESC;
```

![Total Cancellation by Region](https://github.com/user-attachments/assets/ccf6378b-b8a0-4822-b2bd-9ca9bbe25587)

**viii. The total number of active and canceled subscriptions. **

```
SELECT Canceled, COUNT(CustomerID) AS Total_Subscriptions
FROM Customer_data
GROUP BY Canceled;
```

![Number of canceled and Active users](https://github.com/user-attachments/assets/60ed4316-f3c1-4442-9baa-64b87b6650d3)


### 3. Dashboard Overview 

