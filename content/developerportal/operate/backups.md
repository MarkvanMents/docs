# Backups
**Origin of Environment** | v3 | From which environment this backup was made
**Status** | v3 & v4 | The status of the backup. Backups can have the status of **Queued**, **Running**, **Failed**, and **Completed**
**Created by**/ <br /> **Type** | v3 <br /> v4 | The name of the person who created the backup. Automated system backups are named **Nightly**
**ID**/ <br /> **Snapshot id** | v3 <br /> v4 | Unique identifier for the backup *snapshot*
**Date**/ <br /> **Created on** | v3 <br /> v4 | The creation date of the backup
**Expires on** | v3 & v4 | The date on which the backup will be removed from the system
**Mendix version** | v3 & v4 | The version of the deployment package used during backup creation
**Comment** | v3 & v4 | A specific comment added to the backup

At the bottom of the screen, you can click **Delete** to delete this particular backup.

## 4 Known issues

**Mendix Cloud v4** backups that contain a very large number of files (that is, greater than about 50,000) will experience slow performance for _all_ backup operations (create, download, restore, and upload). This is because of the inherent overhead associated with each file; as the number of files increases, this overhead becomes quite significant, and can be in the order of hours.

## 5 Read More

* [How to Create a Backup](create-backup)
* [How to Download a Backup](download-backup)
* [How to Restore a Backup](restore-backup)
* [How to Restore a Backup Locally](database-size-reduction)
* [Database Size Reduction](database-size-reduction)
