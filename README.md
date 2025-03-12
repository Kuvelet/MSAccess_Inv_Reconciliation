# MS Access Approach to Stock Management

### Table of Contents

-[Project Overview](#project-overview)

-[Data Sources](#data-sources)

-[Tools](#tools)

-[Data Cleaning & Preparation](#data-cleaning--preparation)

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


