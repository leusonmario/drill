---
title: "Drill in 10 Minutes"
parent: "Tutorials"
description: Get started with Drill in 10 minutes or less.
---
## Objective

Use Apache Drill to query sample data in 10 minutes. For simplicity, you
run Drill in _embedded_ mode rather than _distributed_ mode to try out Drill
without having to perform any setup tasks.

## Installation Overview

You can install Drill to run in embedded mode on a machine running Linux, Mac OS X, or Windows. For information about installing Drill to run in distributed mode, see [Installing Drill in Distributed Mode]({{ site.baseurl }}/docs/installing-drill-in-distributed-mode).

This installation procedure includes how to download the Apache Drill archive file and extract the contents to a directory on your machine. The Apache Drill archive contains sample JSON and Parquet files that you can query immediately.

After installing Drill, you start the Drill shell. The Drill shell is a pure-Java console-based utility for connecting to relational databases and executing SQL commands. Drill follows the SQL:2011 standard with [extensions]({{site.baseurl}}/docs/sql-extensions/) for nested data formats and other capabilities.

## Embedded Mode Installation Prerequisites

You need to meet the following prerequisites to run Drill:

* Linux, Mac OS X, and Windows: [Oracle Java SE Development (JDK) Kit 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) installation  
* Windows only:  
  * A JAVA_HOME environment variable set up that points to the JDK installation  
  * A PATH environment variable that includes a pointer to the bin directory of the JDK installation 
  * A third-party utility for unzipping a .tar.gz file 
  
### Java Installation Prerequisite Check

Run the following command in a terminal (Linux and Mac OS X) or Command Prompt (Windows) to verify that Java 7 is the version in effect:

`java -version`

The output looks something like this:

    java version "1.7.0_79"
    Java(TM) SE Runtime Environment (build 1.7.0_7965-b15)
    Java HotSpot(TM) 64-Bit Server VM (build 24.79-b02, mixed mode)

## Install Drill on Linux or Mac OS X

Complete the following steps to install Drill:  

1. In a terminal window, change to the directory where you want to install Drill.

2. To download the latest version of Apache Drill, download Drill from the [Drill web site](http://getdrill.org/drill/download/apache-drill-1.1.0.tar.gz) or run one of the following commands, depending on which you have installed on your system:

   * `wget http://getdrill.org/drill/download/apache-drill-1.1.0.tar.gz`  
   *  `curl -o apache-drill-1.1.0.tar.gz http://getdrill.org/drill/download/apache-drill-1.1.0.tar.gz`  

3. Copy the downloaded file to the directory where you want to install Drill. 

4. Extract the contents of the Drill .tar.gz file. Use sudo if necessary:  

    `tar -xvzf <.tar.gz file name>`  

The extraction process creates an installation directory containing the Drill software.

At this point, you can start Drill.

## Start Drill on Linux and Mac OS X
Start Drill in embedded mode using the `drill-embedded` command:

1. Navigate to the Drill installation directory. For example:  

    `cd apache-drill-<version>`  

2. Issue the following command to launch Drill in embedded mode:

    `bin/drill-embedded`  

   The message of the day followed by the [`0: jdbc:drill:zk=local>`  prompt]({{site.baseurl}}/docs/starting-drill-on-linux-and-mac-os-x/#about-the-drill-prompt) appears.  

   At this point, you can [submit queries]({{site.baseurl}}/docs/drill-in-10-minutes/#query-sample-data) to Drill.

### Install Drill on Windows

You can install Drill on Windows 7 or 8. First, set the JAVA_HOME environment variable, and then install Drill. Complete the following steps to install Drill:

1. Click the following link to download the latest version of Apache Drill:  [http://getdrill.org/drill/download/apache-drill-1.1.0.tar.gz](http://getdrill.org/drill/download/apache-drill-1.1.0.tar.gz)  
2. Move the `apache-drill-<version>.tar.gz` file to a directory where you want to install Drill.  
3. Unzip the `TAR.GZ` file using a third-party tool. If the tool you use does not unzip the TAR file as well as the `TAR.GZ` file, unzip the `apache-drill-<version>.tar` to extract the Drill software. The extraction process creates the installation directory named apache-drill-<version> containing the Drill software. 

At this point, you can start Drill.  

## Start Drill on Windows
Start Drill by running the sqlline.bat file and typing a connection string, as shown in the following procedure. The `zk=local` in the connection string means the local node is the ZooKeeper node:

Start the Drill shell using the **sqlline command**. Complete the following steps to launch the Drill shell:

1. Open Command Prompt.  
2. Open the apache-drill-<version> folder. 
3. Go to the bin directory. For example:  
   ``cd bin``
4. Type the following command on the command line:
   ``sqlline.bat -u "jdbc:drill:zk=local"``
   ![drill install dir]({{ site.baseurl }}/docs/img/sqlline1.png)

The `zk=local` means the local node is the ZooKeeper node. At this point, you can [run queries]({{ site.baseurl }}/docs/drill-in-10-minutes/#query-sample-data).

## Stopping Drill

Issue the following command when you want to exit the Drill shell:

`!quit`

## Query Sample Data

At the root of the Drill installation, a `sample-data` directory includes JSON and
Parquet files that you can query. The default `dfs` storage plugin configuration represents the local file system on your machine when you install
Drill in embedded mode. For more information about storage plugin
configuration, refer to [Storage Plugin Registration]({{ site.baseurl }}/docs/connect-a-data-source-introduction).

Use SQL to query the sample `JSON` and `Parquet` files in the `sample-data` directory on your local file system.

### Querying a JSON File

A sample JSON file, [`employee.json`]({{site.baseurl}}/docs/querying-json-files/), contains fictitious employee data. To view the data in the `employee.json` file, submit the following SQL query
to Drill, using the [cp (classpath) storage plugin]({{site.baseurl}}/docs/storage-plugin-registration/) configuration to point to the file.
    
``0: jdbc:drill:zk=local> SELECT * FROM cp.`employee.json` LIMIT 3;``

The query output is:

    +--------------+------------------+-------------+------------+--------------+---------------------+-----------+----------------+-------------+------------------------+----------+----------------+------------------+-----------------+---------+--------------------+
    | employee_id  |    full_name     | first_name  | last_name  | position_id  |   position_title    | store_id  | department_id  | birth_date  |       hire_date        |  salary  | supervisor_id  | education_level  | marital_status  | gender  |  management_role   |
    +--------------+------------------+-------------+------------+--------------+---------------------+-----------+----------------+-------------+------------------------+----------+----------------+------------------+-----------------+---------+--------------------+
    | 1            | Sheri Nowmer     | Sheri       | Nowmer     | 1            | President           | 0         | 1              | 1961-08-26  | 1994-12-01 00:00:00.0  | 80000.0  | 0              | Graduate Degree  | S               | F       | Senior Management  |
    | 2            | Derrick Whelply  | Derrick     | Whelply    | 2            | VP Country Manager  | 0         | 1              | 1915-07-03  | 1994-12-01 00:00:00.0  | 40000.0  | 1              | Graduate Degree  | M               | M       | Senior Management  |
    | 4            | Michael Spence   | Michael     | Spence     | 2            | VP Country Manager  | 0         | 1              | 1969-06-20  | 1998-01-01 00:00:00.0  | 40000.0  | 1              | Graduate Degree  | S               | M       | Senior Management  |
    +--------------+------------------+-------------+------------+--------------+---------------------+-----------+----------------+-------------+------------------------+----------+----------------+------------------+-----------------+---------+--------------------+
    3 rows selected (0.827 seconds)

### Querying a Parquet File

Query the `region.parquet` and `nation.parquet` files in the `sample-data`
directory on your local file system.

#### Region File

If you followed the Apache Drill in 10 Minutes instructions to install Drill
in embedded mode, the path to the parquet file varies between operating
systems.

To view the data in the `region.parquet` file, use the actual path to your Drill installation to construct this query:

``SELECT * FROM dfs.`<path-to-installation>/apache-drill-<version>/sample-data/region.parquet`;``

The query returns the following results:

    +--------------+--------------+-----------------------+
    | R_REGIONKEY  |    R_NAME    |       R_COMMENT       |
    +--------------+--------------+-----------------------+
    | 0            | AFRICA       | lar deposits. blithe  |
    | 1            | AMERICA      | hs use ironic, even   |
    | 2            | ASIA         | ges. thinly even pin  |
    | 3            | EUROPE       | ly final courts cajo  |
    | 4            | MIDDLE EAST  | uickly special accou  |
    +--------------+--------------+-----------------------+
    5 rows selected (0.409 seconds)

#### Nation File

The path to the parquet file varies between operating
systems. Use the actual path to your Drill installation to construct this query:

``SELECT * FROM dfs.`<path-to-installation>/apache-drill-<version>/sample-data/nation.parquet`;``

The query returns the following results:

    SELECT * FROM dfs.`Users/drilluser/apache-drill-1.1.0/sample-data/nation.parquet`;
    +--------------+-----------------+--------------+-----------------------+
    | N_NATIONKEY  |     N_NAME      | N_REGIONKEY  |       N_COMMENT       |
    +--------------+-----------------+--------------+-----------------------+
    | 0            | ALGERIA         | 0            |  haggle. carefully f  |
    | 1            | ARGENTINA       | 1            | al foxes promise sly  |
    | 2            | BRAZIL          | 1            | y alongside of the p  |
    | 3            | CANADA          | 1            | eas hang ironic, sil  |
    | 4            | EGYPT           | 4            | y above the carefull  |
    | 5            | ETHIOPIA        | 0            | ven packages wake qu  |
    | 6            | FRANCE          | 3            | refully final reques  |
    | 7            | GERMANY         | 3            | l platelets. regular  |
    | 8            | INDIA           | 2            | ss excuses cajole sl  |
    | 9            | INDONESIA       | 2            |  slyly express asymp  |
    | 10           | IRAN            | 4            | efully alongside of   |
    | 11           | IRAQ            | 4            | nic deposits boost a  |
    | 12           | JAPAN           | 2            | ously. final, expres  |
    | 13           | JORDAN          | 4            | ic deposits are blit  |
    | 14           | KENYA           | 0            |  pending excuses hag  |
    | 15           | MOROCCO         | 0            | rns. blithely bold c  |
    | 16           | MOZAMBIQUE      | 0            | s. ironic, unusual a  |
    | 17           | PERU            | 1            | platelets. blithely   |
    | 18           | CHINA           | 2            | c dependencies. furi  |
    | 19           | ROMANIA         | 3            | ular asymptotes are   |
    | 20           | SAUDI ARABIA    | 4            | ts. silent requests   |
    | 21           | VIETNAM         | 2            | hely enticingly expr  |
    | 22           | RUSSIA          | 3            |  requests against th  |
    | 23           | UNITED KINGDOM  | 3            | eans boost carefully  |
    | 24           | UNITED STATES   | 1            | y final packages. sl  |
    +--------------+-----------------+--------------+-----------------------+
    25 rows selected (0.101 seconds)

## Summary

Apache Drill supports nested data, schema-less execution, and decentralized metadata. At this point, you know how to create a simple query on a JSON or Parquet file.

## Next Steps

Now that you have an idea about what Drill can do, you might want to:

  * [Install Drill on a cluster.]({{ site.baseurl }}/docs/installing-drill-on-the-cluster)
  * [Configure storage plugins to connect Drill to your data sources]({{ site.baseurl }}/docs/connect-a-data-source-introduction).
  * Query [Hive]({{ site.baseurl }}/docs/querying-hive) and [HBase]({{ site.baseurl }}/docs/hbase-storage-plugin) data.
  * [Query Complex Data]({{ site.baseurl }}/docs/querying-complex-data)
  * [Query Plain Text Files]({{ site.baseurl }}/docs/querying-plain-text-files)

## More Information

For more information about Apache Drill, explore the [Apache Drill web site](http://drill.apache.org).