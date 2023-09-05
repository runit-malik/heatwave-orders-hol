# Build a real-time dashboard in Oracle Analytics Cloud with MySQL HeatWave

![mysql heatwave](./images/mysql-heatwave-logo.jpeg " mysql heatwave")

## Introduction

MySQL HeatWave can easily be used for development tasks with existing Oracle services, such as Oracle Cloud Analytics. -> Oracle Analytics Cloud (OAC) provides the industry’s most comprehensive cloud analytics in a single unified platform, including self-service visualization and inline data preparation to enterprise reporting, advanced analytics, and self-learning analytics that deliver proactive insights.

Use MySQL HeatWave with OAC to explore and perform collaborative analytics with your MySQL data.

_Estimated Time:_ 20 minutes


### Objectives

In this lab, you will be guided through the following tasks:

- Create Oracle Analytics Cloud and connect to MySQL HeatWave
- Create a dashboard on OAC for the delivery-orders

### Prerequisites

- An Oracle Trial or Paid Cloud Account
- Some Experience with MySQL Shell
- Completed Lab ______

## Task 1: Create an Oracle Analytics Cloud Instance

1. From the OCI Console, nagivate to Analytics & AI > Analytics Cloud
    ![analytics menu](./images/analytics-menu.png " analytics menu")

2. Select the **lakehouse** Compartment and Click the **Create Instance** button
    ![create analytics instance](./images/create-instance-oac.png " create analytics instance")
    
3. On the Create Analytics Instance enter the required information as shown below

    Name:
     ```bash
    <copy>hwoac</copy>
     ```

    Description:
    ```bash
    <copy>Oracle Analytics Cloud HeatWave Test</copy>
     ```

    Capacity: Select **OCPU** and select **1**

    License and Edition:
        - Select **License Included**
        - Select **Enterprise Edition**

4. Click the **Create** button
    ![oac config](./images/config-oac.png " oac config")

5. It takes about 12-15 minutes for the OAC instance creation to complete
    ![created oac](./images/created-oac.png " created oac")

## Task 2: Configure Private Access Channel

1. Go down to the “Private Access Channel” resources page and click on the **Configure Private Access Channel** button.

2. Click the **Create Private Access Channel** button

3. On the create Private Access Channel page enter the following:

    Name:
    ```bash
    <copy>hwoacpac</copy>
     ```

     DNS Zones: **Check Virtual Cloud Network's domain name as DNS zone (hwvcn.oraclevcn.com)**

    Description:
    ```bash
    <copy>Testing</copy>
     ```

     **Remove second DNS Zone entry**
    ![config pac oac](./images/config-pac-oac.png " config pac oac")

4. Click the **Configure** button

5. Wait 15 minutes for the configuration process to complete before proceeding to Task 3.
    ![created pac oac](./images/created-pac-oac.png " created pac oac")

## Task 3: Get HeatWave DB Hostname

1. Before we start, go to Menu > Databases > DB Systems

2. Select HeatWave database: **heatwave-db**

3. Click on the "Connections" tab on the Endpoints > Internal FQDN > Click on the Copy link.
    ![hw db endpoint](./images/hw-db-endpoint.png " hw db endpoint")

4. Save the Hostname in your notepad for use with OAC
    Example: **hwdb.sub09012...hwvcn.oraclevcn.com**

## Task 4: Create Connection from HeatWave DB to OAC

1. Navigate to Menu > Analytics > Analytics Clouds

2. Select the OAC instance you provisioned to access the OAC console by clicking on Analytics Home Page. Click on the "Analytics Home Page" button.
    ![analytics go home page](./images/analytics-go-home-page.png " analytics go home page")

3. Create a Connection to HeatWave to build a dashboard
    ![analytics home page](./images/analytics-home-page.png " analytics home page")

4. Click the "Create Connection" button
    ![analytics dataset connections](./images/analytics-dataset-connections.png " analytics dataset connections")

5. Search for HeatWave and select HeatWave as the database.
    ![add connection mysql](./images/add-connection-mysql.png " add connection mysql")

6. Specify the connections details
    - Specify the hostname of heatwave-db
    - Use the FQDN information you save in Step 3
    - Port: 3306
    - Database Name: mysql_customer_orders
    - Be sure to use the Heatwave DB username and password

    Hit the "Save" button to fisnish creating the connection.
    ![config add connection mysql](./images/config-add-connection-mysql.png " config add connection mysql")

7. The completed connection will display a "New Dataset" page. Click on the "Schemas" link and select the "mysql_customer_orders" schema
    ![open schema](./images/open-schema.png " open schema")

## Task 5: Use OAC to Analyze the store_orders table data

1. Drag and drop the store_orders table from the sidebar into the **New Dataset** page.
    ![drag drop store orders](./images/drag-drop-store-orders.png " drag drop store orders")

2. Save the dataset and specify name.
    ![save dataset](./images/save-dataset.png " save dataset")

3. In the top right corner, click the **Create Workbook** button.
    ![create workbook](./images/create-workbook.png " create workbook")

4. Drag and drop **store_name** and **total_sales** into the visualization area. We are only interested in these values as we will be creating a heatmap to visualize total sales by store location. 
    ![drag drop store name total sales](./images/drag-drop-store-name-total-sales.png " drag drop store name total sales")

5. Click on the **Pick Visualization** button and select the **Map** visualization.
    ![pick visualization](./images/pick-visualization.png " pick visualization")

6. Ensure that **store_name** is under the **Category (Location)** header and **total_sales** is under **Color**.
    ![map visualization](./images/map-visualization.png " map visualization")

7. We want to exclude Online orders from the heatmap of store orders. In the map visualization, right click on the **Online** bubble and select **Remove Selected**.
    ![click online bubble](./images/click-online-bubble.png " click online bubble")

Your final visualization should look like this: 
    ![final map](./images/final-map.png " final map")

8. Save the workbook as "store_total_sales".

9. Let's review our map and determine how it can be used to aggregate total sales by country or by region. 


**Congratulations! You have successfully finished the Lab. Please proceed to the next lab.**


## Acknowledgements

- **Author** - Runit Malik, MySQL Cloud Solution Engineer
- **Contributors** - Perside Foster, MySQL Principal Solution Engineer
- **Last Updated By/Date** - Runit Malik, MySQL Cloud Solution Engineer, September 2023