# Retail_Data_Analysis
For the purposes of this project, you have been tasked with computing various Key Performance Indicators (KPIs) for an e-commerce company, RetailCorp Inc. You have been provided real-time sales data of the company across the globe. The data contains information related to the invoices of orders placed by customers all around the world. You will get to know the details of the data in the next segment.

 

At the industry level, an end-to-end data pipeline is built for this purpose. Tools such as HDFS(Hadoop Distributed File System) are used to store the data that is processed by the real-time processing framework and then shown on a dashboard with tools such as Tableau and PowerBI. The image given below is an example of such a complete data pipeline.

<img width="400" height="234" alt="{A5F49EFC-46B5-44C4-99EE-14884E4EE8C9}" src="https://github.com/user-attachments/assets/f21b3c06-0a7b-401a-b891-cfa07043d88e" />

For our project, we will be focusing on the ‘Order Intelligence’ part of this data pipeline. The image given below shows the architecture of the data pipeline that we will follow in this project.

<img width="400" height="282" alt="{C164C998-8066-4517-8D3E-A1B7D61469C5}" src="https://github.com/user-attachments/assets/0d76dc34-52a3-40ef-ae95-e0f8527b0c2d" />


Broadly, you will perform the following tasks in this project:

Reading the sales data from the Kafka server

Preprocessing the data to calculate additional derived columns such as total_cost etc

Calculating the time-based KPIs and time and country-based KPIs

Storing the KPIs (both time-based and time- and country-based) for a 10-minute interval into separate JSON files for further analysis

The data is based on an Online Retail Data Set in the UCI Machine Learning Repository. Each order’s invoice has been represented in a JSON format. The sample data looks like this.

 

{
  "items": [
    {
      "SKU": "21485",
      "title": "RETROSPOT HEART HOT WATER BOTTLE",
      "unit_price": 4.95,
      "quantity": 6
    },
    {
      "SKU": "23499",
      "title": "SET 12 VINTAGE DOILY CHALK",
      "unit_price": 0.42,
"quantity": 2
}
],
  "type": "ORDER"
  "country": "United Kingdom",
  "invoice_no": 154132541653705,
  "timestamp": "2020-09-18 10:55:23",
}
 

 


As you can see, the data contains the following information:

Invoice number: Identifier of the invoice

Country: Country where the order is placed

Timestamp: Time at which the order is placed

Type: Whether this is a new order or a return order

SKU (Stock Keeping Unit): Identifier of the product being ordered

Title: Name of the product is ordered

Unit price: Price of a single unit of the product

Quantity: Quantity of the product being ordered

You will be using these columns to derive some additional columns as well, which will help you in calculating the KPIs. You will learn more about this in the next segment.

The KPIs that you will be calculated are as follows:

 


Total volume of sales:

By calculating this, you can see where and when demand is higher and try to understand the reason. It helps in creating projections for the future. The total volume of sales is the sum of the transaction value of all orders in the given time window. The total transaction value of a specific order will be calculated as follows:

<img width="216" height="61" alt="{9AD06064-2375-4A9E-9BDC-227F989253B9}" src="https://github.com/user-attachments/assets/2cf712b5-e190-4c0f-b00d-6991b638e95b" />

 

The total volume of sales in a time interval can be calculated as the summation of the transaction values of all the orders in that time interval. Also, the sales data stream contains a few returns. In the case of returns, the transaction amount needs to be subtracted. So, the equation for the total volume of sales, in this case, will be calculated as follows:
<img width="339" height="47" alt="{8CAF6B2D-A8C8-432F-BAB1-439923F7EC27}" src="https://github.com/user-attachments/assets/1060410a-423a-4146-8e1e-879199f194d9" />


OPM (orders per minute):

Orders per minute (OPM) is another important metric for e-commerce companies. It is a direct indicator of the success of the company. As the name suggests, it is the total number of orders received in a minute.



Rate of return: 

No business likes to see a customer returning their items. Returns are costly because they need to be processed again and have adverse effects on revenue. The rate of return indicates customer satisfaction for the company. The more satisfied the customer is, the lower the rate of return will be. The rate of return is calculated against the total number of invoices using the following equation:

<img width="164" height="58" alt="{6329B3AF-9E66-413F-B322-DE86E922B7AD}" src="https://github.com/user-attachments/assets/4f561145-0ec4-435f-8606-f6a9a6c48a8f" />

 

Average transaction size:

The average transaction size helps in measuring the amount of money spent on average for each transaction. Evaluating this KPI over a year is a good indicator of when the customers are more likely to spend money, which enables the company to adapt their advertising accordingly. This can be calculated using the following equation:

<img width="165" height="54" alt="{741E58F7-395F-4509-8413-7F69EEE84AA4}" src="https://github.com/user-attachments/assets/225f4a10-0548-483a-98f5-065e31e97086" />

 

You will be calculating the four KPIs mentioned above for all the orders. You will also be calculating the first three KPIs on a per-country basis.

Note that in some cases, the total sales volume can be negative if the return cost is more than that of new orders in that window.

In the next segment, you will look at the solution approach as well as the tasks that you will be performing in this project.
