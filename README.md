# Insurance Data Analytics (Power BI)

## Introduction
This Power BI project analyzes an insurance portfolio by combining **policy-level** information with **claim-related** outcomes to provide clear, interactive insights. The goal is to transform raw data into a reporting layer that supports:

- **Business monitoring** (e.g., premium volume, coverage exposure, claim status distribution)
- **Analytical insights** (e.g., claim patterns across policy types, age groups, and customer segments)

As a first step, the dataset was prepared by importing the source CSV into **Microsoft SQL Server**, creating a structured and reusable table that Power BI can reliably consume for modeling, DAX measures, and dashboard development.

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
