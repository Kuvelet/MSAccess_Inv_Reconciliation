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

- **MS Access**: For data transformation and analysis.

### Data Context & Preparation

In the context of SAGE data, the most critical columns for efficient inventory and financial management are Item ID, Quantity on Purchase Orders, Quantity on Sales Orders, and Quantity On Hand. The Item ID serves as a unique identifier for each product, ensuring accurate tracking and differentiation across inventory and financial systems. The Quantity on Purchase Orders column reflects the number of units that have been ordered from suppliers but have not yet been received, providing crucial insight into incoming stock levels and aiding in supply chain planning. The Quantity on Sales Orders captures the quantity of products committed to customer orders but not yet fulfilled, offering visibility into outgoing inventory demands. This is essential for aligning production and procurement with sales requirements. Lastly, the Quantity On Hand indicates the current stock available in the warehouse, serving as a key metric for evaluating whether inventory levels are sufficient to meet ongoing sales commitments and operational needs. Monitoring these three quantities ensures accurate forecasting, reduces the risk of stock shortages or overstocking, and supports timely procurement and order fulfillment. Integrating this data into the MS Access system enhances real-time visibility, enabling the operations team to make informed decisions and maintain optimal inventory levels.

WMS data is sourced directly from the physical inventory system, providing real-time insights into stock levels within the warehouse. Ideally, when generating a pivot table from WMS data, the figures—especially regarding available stock—should perfectly align with the inventory records in SAGE. However, discrepancies between the two systems often occur due to various operational factors. These can include timing differences in data updates, human errors in data entry, false scanning during stock movements, or stock adjustments that are not promptly recorded. False scanning, such as scanning the wrong product barcode or incorrect quantities, can significantly contribute to data mismatches. Additionally, accounting-related issues like delayed purchase order receipts or misallocated sales orders can further widen these discrepancies. Such variances necessitate regular reconciliation processes to identify and resolve inconsistencies. By consolidating data from both systems within the MS Access database, discrepancies can be detected early, investigated, and corrected, ensuring greater accuracy in inventory reporting and more reliable decision-making for procurement, sales, and operations teams.



