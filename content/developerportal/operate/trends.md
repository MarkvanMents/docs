# Trends in Mendix Cloud v3
active | a microflow or client xpath request is using the database right now
idle in transaction | the connection is in use by a microflow, but it is currently executing a microflow activity that is not using the database 
idle | the connection is open and available to quickly allocate to a microflow or xpath request that needs it

### 5.5 Database Node Operating System Memory{#Trends-dbmemory}

The **Database node operating system memory** graph shows the distribution of operating system memory that is available for this server.

![](attachments/trends/db-os-memory.png)

The most important values on this graph are **cache** and **apps**.

The **cache** values show the memory used to hold parts of the database that have been read from disk earlier. It is crucial to the performance of an application that parts of the database data and indexes that are referenced a lot are always available in the working memory of the server, in the cache. A lack of disk cache on a busy application will result in continuous re-reads of data from disk, which takes several orders of magnitude more time, slowing down the entire application. This may indicate that you have a large number of concurrent database connections from your app and that the environment is not large enough to support these.

The **apps** values show the amount of memory allocated to the database server (postgresql) to perform database queries.

### 5.6 Database Node CPU Usage{#Trends-dbcpu}

The **Database node CPU usage** graph shows the amount of CPU usage in percentage, broken down into different types of CPU usage. Each CPU is counted as 100%, so in a multi-CPU system, the scale will be several hundred percent.

![](attachments/trends/db-cpu-usage.png)

The most important values in here are: **user**, which shows the CPU time used for running database queries, and **iowait**, showing the length of time a CPU core is idle and waiting for disk operations to finish (for example, waiting for information that has to be read from disk, or waiting for a synchronous write operation to finish).

Clearly visible amounts of **iowait**, in combination with a high number of disk read operations, and having all free system memory filled as disk cache ([Database Node Operating System Memory](#Trends-dbmemory)), are a sign of a lack of available server memory for use as disk cache. This situation will slow down database operations tremendously, because getting data from disk over and over again takes considerably longer than having it present in memory.

### 5.7 Database Node Disk Usage (in Bytes){#Trends-dbappdbnodedfabs}

The **Database node disk usage (in bytes)** graph displays the absolute amount of data that is stored on disk.

![](attachments/trends/db-disk-usage-bytes.png)

### 5.8 Database Node Disk Usage in Percentage (%){#Trends-dbappdbnodedfpercent}

The **Database node disk usage (percentage)** graph shows the displays the relative amounts of data that are stored on disk.

![](attachments/trends/db-disk-usage-pct.png)

This graph should be interpreted in combination with other graphs. See [Combining Information](#combine-info), above.

### 5.9 Database Node Load{#Trends-dbload}

This value is commonly used as a general indication for overall server load that can be monitored and alerted upon.

![](attachments/trends/db-load.png)

The **Database node load** value is a composite value, calculated from a range of other measurements, as shown in the other graphs on this page. When actually investigating high server load, this graph alone is not sufficient.

## 6 Read More

* [Alerts](monitoring-application-health)
* [Database Size Reduction](database-size-reduction)
* [How to Calculate the Total Amount of Diskspace of a Cloud App Environment](calculate-diskspace-of-a-cloud-app-environment)
* [Maintenance Windows: Configuration](/developerportal/deploy/maintenance-windows)
* [Migrate to Mendix Cloud v4](/developerportal/deploy/migrating-to-v4)
* [How to Receive Environment Status Alerts](receive-alerts)
* [Cloud Version and Region in the Mendix Cloud](/developerportal/deploy/cloud-version-region)
* [Mendix Cloud v4](/developerportal/deploy/mxcloudv4)
