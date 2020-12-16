# Trends in Mendix Cloud v4
**read** | Read ops on the disk holding the database. 
**write** | Write ops on the disk holding the database.

### 5.11 Database IOPS Burst Balance {#Trends-dbmxdatabaseburstbalance}

The **Database IOPS burst balance** graph shows the number of IOPS credits accrued to support burstable performance. The metric is expressed as percentage; 100% means that the volume has accumulated the maximum number of credits.

![](attachments/trends-v4/db-burst-balance.png)

Apps running on Mendix Cloud V4 use AWS databases to store their data. These databases are **burstable**, which means that it has a specified performance baseline. See the AWS document [Overview of Monitoring Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MonitoringOverview.html) for more information.

Burstable performance means that if you use fewer IOPS than is required for baseline performance (such as when it is idle), the unspent IOPS credits are accrued until they reach a maximum. If a burstable performance instance needs to burst above the baseline performance level, it spends the accrued credits. The more credits that a burstable performance instance has accrued, the more time it can burst beyond its baseline when more performance is needed.

You can find more details about the credit system in the official AWS documentation: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MonitoringOverview.html.

If your database uses a high level of IOPS over a sustained period, this may impact your app's performance. If your database burst balance reduces consistently, you will need to ensure that there are periods when there is less activity so that the database burst balance can be restored.

For more information, see the *AWS Database blog* [Understanding Burst vs. Baseline Performance with Amazon RDS and GP2](https://aws.amazon.com/blogs/database/understanding-burst-vs-baseline-performance-with-amazon-rds-and-gp2/).

## 6 Read More

* [Alerts](monitoring-application-health)
* [Maintenance Windows: Configuration](/developerportal/deploy/maintenance-windows)
* [Migrate to Mendix Cloud v4](/developerportal/deploy/migrating-to-v4)
* [How to Receive Environment Status Alerts](receive-alerts)
* [Cloud Version and Region in the Mendix Cloud](/developerportal/deploy/cloud-version-region)
* [Mendix Cloud v4 - FAQ](/developerportal/deploy/mxcloudv4)
