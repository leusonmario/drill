---
title: "Using Apache Drill with Tableau 9 Server"
parent: "ODBC/JDBC Interfaces"
---

This document describes how to connect Tableau 9 Server to Apache Drill and explore multiple data formats instantly on Hadoop, as well as share all the Tableau visualizations in a collaborative environment. Use the combined power of these tools to get direct access to semi-structured data, without having to rely on IT teams for schema creation and data manipulation. 

To use Apache Drill with Tableau 9 Server, complete the following steps: 

1.	Install the Drill ODBC driver from MapR on the Tableau Server system and configure ODBC data sources.

----------

### Step 1: Install and Configure the MapR Drill ODBC Driver 

Drill uses standard ODBC connectivity to provide easy data-exploration capabilities on complex, schema-less data sets. For the best experience use the latest release of Apache Drill. For Tableau 9.0 Server, Drill Version 0.9 or higher is recommended.

Complete the following steps to install and configure the driver:

1. Download the 64-bit MapR Drill ODBC Driver for Windows from the following location:<br> [http://package.mapr.com/tools/MapR-ODBC/MapR_Drill/](http://package.mapr.com/tools/MapR-ODBC/MapR_Drill/)     
**Note:** Tableau 9.0 Server works with the 64-bit ODBC driver.
2. Complete steps 2-8 under on the following page to install the driver:<br> 
[http://drill.apache.org/docs/step-1-install-the-mapr-drill-odbc-driver-on-windows/](http://drill.apache.org/docs/step-1-install-the-mapr-drill-odbc-driver-on-windows/)
3. Complete the steps on the following page to configure the driver:<br>
[http://drill.apache.org/docs/step-2-configure-odbc-connections-to-drill-data-sources/](http://drill.apache.org/docs/step-2-configure-odbc-connections-to-drill-data-sources/)
4. If Drill authentication is enabled, select **Basic Authentication** as the authentication type. Enter a valid user and password. ![drill query flow]({{ site.baseurl }}/docs/img/tableau-odbc-setup.png)

Note: If you select **ZooKeeper Quorum** as the ODBC connection type, the client system must be able to resolve the hostnames of the ZooKeeper nodes. The simplest way is to add the hostnames and IP addresses for the ZooKeeper nodes to the `%WINDIR%\system32\drivers\etc\hosts` file. ![drill query flow]({{ site.baseurl }}/docs/img/tableau-odbc-setup-2.png)

----------

### Step 2: Install the Tableau Data-connection Customization (TDC) File

The MapR Drill ODBC Driver includes a file named `MapRDrillODBC.TDC`. The TDC file includes customizations that improve ODBC configuration and performance when using Tableau.

For Tableau Server, you need to manually copy this file to the Server Datasources folder:


For more information about Tableau TDC configuration, see [Customizing and Tuning ODBC Connections](http://kb.tableau.com/articles/knowledgebase/customizing-odbc-connections)

----------


### Step 3: Publish Tableau Visualizations and Data Sources

For collaboration purposes, you can now use Tableau Desktop to publish data sources and visualizations on Tableau Server.

####Publishing Visualizations

To publish a visualization from Tableau Desktop to Tableau Server:

5. Sign into Tableau Server using the server hostname or IP address, username, and password. ![drill query flow]({{ site.baseurl }}/docs/img/tableau-server-signin2.png)

6. You can now publish a workbook to Tableau Server. Select **Server > Publish Workbook**. ![drill query flow]({{ site.baseurl }}/docs/img/tableau-server-publish1.png)

7. Select the project from the drop-down list. Enter a name for the visualization to be published and provide a description and tags as needed. Assign permissions and views to be shared. Then click **Authentication**. ![drill query flow]({{ site.baseurl }}/docs/img/tableau-server-publish2.png)

8. In the Authentication window, select **Embedded Password**, then click **OK**. Then click **Publish** in the Publish Workbook window to publish the visualization to Tableau Server. ![drill query flow]({{ site.baseurl }}/docs/img/tableau-server-authentication.png)

####Publishing Data Sources

If all you want to do is publish data sources to Tableau Server, follow these steps:










----------

In this quick tutorial, you saw how you can configure Tableau Server 9.0 to work with Tableau Desktop and Apache Drill. 
