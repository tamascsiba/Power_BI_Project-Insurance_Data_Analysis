# Insurance Data Analytics (Power BI)

## Introduction
This Power BI project analyzes an insurance portfolio by combining **policy-level** information with **claim-related** outcomes to provide clear, interactive insights. The goal is to transform raw data into a reporting layer that supports:

- **Business monitoring** (e.g., premium volume, coverage exposure, claim status distribution)
- **Analytical insights** (e.g., claim patterns across policy types, age groups, and customer segments)

As a first step, the dataset was prepared by importing the source CSV into **Microsoft SQL Server**, creating a structured and reusable table that Power BI can reliably consume for modeling, DAX measures, and dashboard development.

## Documentation
A complete, detailed project documentation is available in: `Insurance_Data_Analysis_Documentation.pdf`.

---

## Data Source & SQL Server Import (CSV → dbo.InsuranceData)

### Data source
The project is based on a CSV file named **`InsuranceData`**, which contains records related to insurance policies and claims.

### Import into SQL Server
The CSV file was imported into **Microsoft SQL Server**, and the data was loaded into:

- **Database:** `Insurancedb`  
- **Schema/Table:** `dbo.InsuranceData`  
- **Row count:** **10,004 rows** (confirmed after import)

Validation query used after loading:

```sql
SELECT *
FROM [dbo].[InsuranceData];
```

![SQL Server - InsuranceData table imported](pics/sql_server.png)

### Main columns (high level)
The `dbo.InsuranceData` table contains the key attributes needed for insurance reporting and claim analysis, including:

- **PolicyNumber** – unique policy identifier  
- **CustomerID** – customer identifier  
- **Gender**, **Age** – customer demographics  
- **PolicyType** – insurance product category (e.g., Auto, Travel, Health, Home, Life)  
- **PolicyStartDate**, **PolicyEndDate** – policy active period  
- **PremiumAmount** – premium value associated with the policy  
- **CoverageAmount** – coverage/insured amount (exposure)  
- **ClaimNumber** – claim identifier (when applicable)  
- **ClaimDate** – date of the claim event (when applicable)  
- **ClaimAmount** – monetary value of the claim (when applicable)  
- **ClaimStatus** – claim processing status (e.g., Pending / Settled / Rejected)

---

## Power BI - SQL Server Connection
The dataset was imported into Power BI directly from Microsoft SQL Server using the native **SQL Server database** connector.  
The connection was configured in **Import** mode to enable fast in-memory analytics, DAX calculations, and interactive visuals.

**Connection details (high level):**
- **Server:** TOMA-YOGA
- **Connectivity mode:** Import
- **Source table:** Insurancedb.dbo.InsuranceData

![Power BI SQL Server connector settings](pics/import_from_sql_server.png)

---

## Data Preparation (Power Query)
To support segmentation and clearer reporting, two additional derived columns were created in Power Query using **Conditional Column** rules. These columns are used for filtering, grouping, and high-level analysis in the report.

### Age Group (Conditional Column)
A new `Age Group` column was derived from `Age` to enable demographic segmentation in visuals and slicers:

- **Young Adults:** Age <= 24  
- **Adult:** Age <= 60  
- **Elder:** Age > 60  

![Power Query - Age Group conditional column](pics/new_column.png)

### Active vs Inactive Policy (Conditional Column)
A new `Active/Inactive` status column was derived from `PolicyEndDate` to differentiate active policies from expired ones (using a cut-off date):

- **Inactive:** PolicyEndDate <= 2024-12-10  
- **Active:** otherwise  

![Power Query - Active/Inactive conditional column](pics/active_inactive.png)



