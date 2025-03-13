# MS Access Approach to Stock Management

### Table of Contents

-[Project Overview](#project-overview)

-[Data Sources](#data-sources)

-[Tools](#tools)

-[Data Context & Preparation](#data-context--preparation)

-[Analysis](#analysis)

-[Results & Findings](#results--findings)

-[Next Steps](#next-steps)

### Project Overview
---

As a Data Analyst in the automotive sector, ensuring seamless inventory management is crucial for maintaining efficient operations. To support the operations department in their day-to-day activities, I have designed and implemented a comprehensive Microsoft Access database system. This system is tailored to provide real-time access to inventory data, enabling both technical and non-technical staff to interact with live data in an intuitive and user-friendly manner.

Our company utilizes two primary systems for tracking inventory: the Warehouse Management System (WMS) and SAGE, which manages accounting and financial data. While WMS is responsible for monitoring the physical stock levels within the warehouse, SAGE provides insights into the financial records related to inventory, including purchase orders, cost tracking, and accounting reconciliations.

The system implemented provides actionable insights that assist in optimizing inventory control processes, reducing operational inefficiencies, and supporting strategic decision-making. It empowers the operations team to maintain optimal stock levels, mitigate risks associated with stock shortages or overstocking, and improve overall supply chain transparency.

One of the key functionalities of the implemented MS Access system is to consolidate data from both WMS and SAGE, offering a unified view of inventory levels. Additionally, the system is designed to detect and analyze discrepancies between the two data sources. This involves conducting detailed investigations into stock differences to identify potential causes, whether due to logistical issues, data entry errors, or accounting variances. By pinpointing these discrepancies, the system supports proactive problem-solving and enhances the accuracy of inventory records.

Overall, the implementation of this database system not only streamlines inventory management but also fosters better cross-departmental collaboration. It ensures that all stakeholders have timely access to accurate inventory data, thereby contributing to the operational resilience and financial integrity of the organization.

### Data Sources
---

Both SAGE and WMS data are updated daily through scheduled imports to the company file servers. This process ensures that the most current and accurate information is consistently available across systems, supporting efficient operations and informed decision-making.

**1.** WMS Data refers to information that monitors and tracks the physical stock levels within the warehouse, ensuring accurate inventory control. It consists of `Part Number`, `Barcode`, `Location`, `Quantity Available`, `Quantity Reserved For Picking`, `Total Quantity`, `Deleted Quantity`, `ID` columns in it.

**2.** The SAGE data described here refers to financial and accounting information related to inventory, including sales orders, purchase orders, and qouantity on hand. It consists of `Item ID`, `Item Description`, `Description for Sales`, `Description for Purchases`, `Sales Price 1`, `Case Qty`, `Quantity on Sales Orders`, `Quantity on Purchase Orders`, `Quantity On Hand`, `Vendor ID` columns in it.

### Tools
---

- **MS Access**: For data transformation and analysis.

### Data Context & Preparation
---

In the context of SAGE data, the most critical columns for efficient inventory and financial management are Item ID, Quantity on Purchase Orders, Quantity on Sales Orders, and Quantity On Hand. The Item ID serves as a **unique identifier** for each product, ensuring accurate tracking and differentiation across inventory and financial systems. The Quantity on Purchase Orders column reflects the number of units that have been ordered from suppliers but have not yet been received, providing crucial insight into incoming stock levels and aiding in supply chain planning. The Quantity on Sales Orders captures the quantity of products committed to customer orders but not yet fulfilled, offering visibility into outgoing inventory demands. This is essential for aligning production and procurement with sales requirements. Lastly, the Quantity On Hand indicates the current stock available in the warehouse, serving as a key metric for evaluating whether inventory levels are sufficient to meet ongoing sales commitments and operational needs. Monitoring these three quantities ensures accurate forecasting, reduces the risk of stock shortages or overstocking, and supports timely procurement and order fulfillment. Integrating this data into the MS Access system enhances real-time visibility, enabling the operations team to make informed decisions and maintain optimal inventory levels.

On the other hand, WMS data is structured distinctly from SAGE, requiring careful alignment for accurate analysis. The key columns in WMS for this purpose are `Part Number` (equivalent to the `Item ID` in the SAGE table), `Location`, `Quantity Available`, and `Quantity Reserved`. Each `Location` code corresponds to one of the company’s four warehouses: **Galant**, **KTL**, **TRH**, and **Main**.

- **Galant** warehouse locations are identified by codes starting with **"GAL"**.  
- **KTL** warehouse locations begin with **"KTL"**.  
- **TRH** warehouse locations are marked by codes starting with **"TRH"**.  
- **Main** warehouse locations, however, do not follow a specific prefix pattern and are represented by the remaining location codes.

**Each location can store multiple part numbers, and a single part number may be distributed across multiple locations within the same or different warehouses.** This structure requires meticulous analysis to ensure that quantities are accurately tracked across the entire inventory system. By understanding these location code distinctions, the MS Access database can effectively map and consolidate data, facilitating accurate inventory reporting and supporting strategic decision-making.

WMS data is sourced directly from the physical inventory system, providing real-time insights into stock levels within the warehouse. Ideally, when generating a pivot table from WMS data, the figures—especially regarding available stock—should perfectly align with the inventory records in SAGE. However, discrepancies between the two systems often occur due to various operational factors. These can include timing differences in data updates, human errors in data entry, false scanning during stock movements, or stock adjustments that are not promptly recorded. False scanning, such as scanning the wrong product barcode or incorrect quantities, can significantly contribute to data mismatches. Additionally, accounting-related issues like delayed purchase order receipts or misallocated sales orders can further widen these discrepancies. Such variances necessitate regular reconciliation processes to identify and resolve inconsistencies. By consolidating data from both systems within the MS Access database, discrepancies can be detected early, investigated, and corrected, ensuring greater accuracy in inventory reporting and more reliable decision-making for procurement, sales, and operations teams.

Below are two sample datasets that illustrate the data structure. While each dataset contains additional columns, only the ones relevant to our analysis are included here.

<table>
  <tr>
    <td>

#### **SAGE Table (Financial Inventory Data)**

| **Item ID** | **Qty on<br>Purchase Orders** | **Qty on<br>Sales Orders** | **Qty<br>On Hand** |
|-------------|------------------------------|----------------------------|---------------------|
| ITEM001     | 100                          | 50                         | 200                 |
| ITEM002     | 250                          | 150                        | 300                 |
| ITEM003     | 0                            | 20                         | 80                  |
| ITEM004     | 50                           | 70                         | 100                 |
| ITEM005     | 150                          | 100                        | 400                 |

</td>
    <td>

#### **WMS Table (Warehouse Management Data)**

| **Part<br>Number** | **Location** | **Qty<br>Available** | **Qty<br>Reserved** |
|--------------------|-------------|----------------------|----------------------|
| ITEM001            | GAL011      | 120                  | 30                   |
| ITEM001            | 854A02      | 80                   | 20                   |
| ITEM002            | KTL055      | 200                  | 50                   |
| ITEM003            | TRH034      | 60                   | 15                   |
| ITEM005            | 845B04      | 400                  | 80                   |

</td>
  </tr>
</table>

> **Note:** These tables are representative samples and does not include all records from the actual dataset. Part numbers and pricing information have been modified for confidentiality.

**1.** I want to establish a live link between the data and MS Access to eliminate the need for re-importing whenever analysis is required.

To link a CSV file in MS Access, go to the External Data tab, select Text File, browse to your CSV, and choose "Link to the data source by creating a linked table". Follow the Link Text Wizard to specify delimiters, field names, and primary keys, then finish to create the linked table.

Link both WMS and Sage Data using the same method.

### Analysis

**1.** To begin with, it is essential to transform the **WMS** table into a more structured format that can provide meaningful insights for analysis. Given that each location can store multiple part numbers, and a single part number may be distributed across multiple locations within the same or different warehouses, it is important to consolidate this data effectively. 

In our specific case, while the detailed location codes are not particularly relevant, understanding which part number is stored in which warehouse is crucial for accurate inventory tracking and decision-making. The primary objective is to identify and distinguish part numbers based on their corresponding warehouses, ensuring that each part number is uniquely represented in the final dataset.

To achieve this, the WMS data needs to be pivoted in a way that automatically recognizes the warehouse associated with each part number by identifying warehouse locations based on their prefixes—Galant locations start with "GAL", KTL with "KTL", TRH with "TRH", while Main warehouse locations do not follow a specific prefix pattern and are represented by the remaining location codes. The transformation should result in generating new columns for each warehouse, where the available and reserved quantities are appropriately categorized. This approach will ensure that each part number appears as a unique entry in the dataset, with corresponding values reflecting its distribution across the different warehouses (e.g., **Galant**, **KTL**, **TRH**, and **Main**).

The pivoted structure will enhance analytical efficiency by facilitating the swift identification of which warehouses stock specific part numbers, enabling the aggregation of quantities across warehouses for a comprehensive inventory overview.

By automating this pivot process, the transformed dataset will provide a clearer and more efficient view of inventory distribution. This structure not only enhances data clarity but also supports more informed operational and strategic decisions regarding inventory management, stock allocation, and order fulfillment.

See the SQL query below for the transformation explained above, written specifically for MS Access.

```sql
-- Pivoting the data to categorize quantities by warehouse location
TRANSFORM 
    -- Summing the total quantity for each pivoted column, replacing zero with Null for clarity
    IIf(
        Sum([TUF_Stock_WMS_w_Loc].[Total Quantity]) = 0, 
        Null, 
        Sum([TUF_Stock_WMS_w_Loc].[Total Quantity])
    ) AS [SumOfTotal Quantity]

-- Main SELECT clause for aggregating and calculating relevant inventory metrics
SELECT 
    -- The unique identifier for each product, ensuring accurate grouping and reporting
    TUF_Stock_WMS_w_Loc.[Suspensia Number],

    -- Summing the quantity available across all locations for each part number.
    -- Replaces zero with Null to distinguish between actual zero values and absence of data.
    IIf(
        Sum([TUF_Stock_WMS_w_Loc].[Quantity Available]) = 0, 
        Null, 
        Sum([TUF_Stock_WMS_w_Loc].[Quantity Available])
    ) AS Quantity_Available,

    -- Summing the quantity reserved for picking, helping to identify the committed stock.
    -- Zero is replaced with Null to highlight only meaningful reserved stock quantities.
    IIf(
        Sum([TUF_Stock_WMS_w_Loc].[Quantity Reserved For Picking]) = 0, 
        Null, 
        Sum([TUF_Stock_WMS_w_Loc].[Quantity Reserved For Picking])
    ) AS Quantity_Reserved,

    -- Aggregating the total quantity available across all warehouse locations for each part.
    -- Zero values are replaced with Null to avoid cluttering reports with insignificant data.
    IIf(
        Sum([TUF_Stock_WMS_w_Loc].[Total Quantity]) = 0, 
        Null, 
        Sum([TUF_Stock_WMS_w_Loc].[Total Quantity])
    ) AS Total_Quantity,

    -- Summing the deleted quantity, representing stock that is no longer available or has been written off.
    -- Zero is replaced with Null to focus on meaningful data in the final output.
    IIf(
        Sum([TUF_Stock_WMS_w_Loc].[Deleted Quantity]) = 0, 
        Null, 
        Sum([TUF_Stock_WMS_w_Loc].[Deleted Quantity])
    ) AS Deleted_Quantity,

    -- Calculating the Immediately Available ISC stock, excluding quantities from key warehouses (GAL, TRH, KTL).
    -- This helps identify the stock specifically available for ISC fulfillment.
    -- The `Nz` function ensures that Null values are treated as zero to avoid calculation errors.
    IIf(
        Sum([TUF_Stock_WMS_w_Loc].[Quantity Available]) 
        - Nz(Sum(IIf(Left([Location], 3) = "GAL", [Total Quantity], 0)), 0)
        - Nz(Sum(IIf(Left([Location], 3) = "TRH", [Total Quantity], 0)), 0)
        - Nz(Sum(IIf(Left([Location], 3) = "KTL", [Total Quantity], 0)), 0) = 0,
        Null,
        Sum([TUF_Stock_WMS_w_Loc].[Quantity Available]) 
        - Nz(Sum(IIf(Left([Location], 3) = "GAL", [Total Quantity], 0)), 0)
        - Nz(Sum(IIf(Left([Location], 3) = "TRH", [Total Quantity], 0)), 0)
        - Nz(Sum(IIf(Left([Location], 3) = "KTL", [Total Quantity], 0)), 0)
    ) AS [Immediately Available ISC]

-- Specifying the table from which data is being pulled
FROM 
    TUF_Stock_WMS_w_Loc

-- Grouping the results by Suspensia Number to ensure aggregated data is calculated for each unique product.
GROUP BY 
    TUF_Stock_WMS_w_Loc.[Suspensia Number]

-- Pivoting the data based on the warehouse location.
-- The SWITCH function categorizes warehouse locations based on their code prefix.
PIVOT 
    Switch(
        -- If location starts with 'GAL', categorize it as 'Galaxy Total Quantity'
        Left([Location], 3) = "GAL", "Galaxy Total Quantity",

        -- If location starts with 'TRH', categorize it as 'TRH Total Quantity'
        Left([Location], 3) = "TRH", "TRH Total Quantity",

        -- If location starts with 'KTL', categorize it as 'KTL Total Quantity'
        Left([Location], 3) = "KTL", "KTL Total Quantity",

        -- Any other location is categorized as 'ISC Total Quantity' (catch-all condition)
        True, "ISC Total Quantity"
    );
```

The table below showcases a refined sample output derived from the above query, illustrating how the transformed data will be structured within MS Access. This output provides a clear and concise overview of inventory distribution across warehouses, offering valuable insights for strategic decision-making.

| **Part Number** | **Quantity Available** | **Quantity Reserved** | **Total Quantity** | **Deleted Quantity** | **Immediately Available MAIN** | **Galant Total Quantity** | **TRH Total Quantity** | **KTL Total Quantity** | **MAIN Total Quantity** |
|-----------------|-----------------------|-----------------------|--------------------|----------------------|--------------------------------|---------------------------|------------------------|------------------------|--------------------------|
| ITEM001         | 500                   | 200                   | 700                | 10                   | 300                            | 200                       | 150                    | 100                    | 250                      |
| ITEM002         | 300                   | 100                   | 400                | 5                    | 200                            | 100                       | 50                     | 50                     | 200                      |
| ITEM003         | 150                   | 80                    | 230                | 0                    | 80                             | 70                        | 30                     | 50                     | 80                       |
| ITEM004         | 600                   | 250                   | 850                | 20                   | 400                            | 100                       | 150                    | 150                    | 450                      |
| ITEM005         | 400                   | 180                   | 580                | 15                   | 250                            | 90                        | 60                     | 100                    | 330                      |




**1.** In some cases, there are unique part numbers that are recorded in only one table. For example, certain part numbers may exist exclusively in the WMS table due to recent stock arrivals that haven't yet been updated in the SAGE system. Conversely, some part numbers might appear only in the SAGE table if they are discontinued or no longer stocked but still have outstanding purchase or sales orders. These discrepancies highlight the importance of aligning data between systems for accurate inventory analysis.


