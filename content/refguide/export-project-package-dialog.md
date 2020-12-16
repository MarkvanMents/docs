# Export Project Package

## 1 Introduction
You can export a project package (*.mpk*) from Mendix Studio Pro for backup purposes or to share it with other Mendix developers. This is useful if you want to give someone the entire app, or if you need to provide a test app when submitting a ticket.

Project packages can be imported again into a new app using the [Import Project Package](import-project-package-dialog).

To export the package, open the **File** menu > **Export Project Package** and select the relevant options in the **Export Project Package** dialog box:

![Export Project Package Dialog Window](attachments/file-menu/export-project-package.png)

 For more information on what options you can select, see the sections below. 

## 2 Destination

You can specify the folder to export the package to. The default location is a folder named *packages* inside the project directory.

## 3 Export Data

Mendix project packages can be exported to a Mendix package file (*.mpk*).  You can choose to export the built-in deployment database and uploaded files as well, or export with no data. You can choose one of the following options:

* **No data** – the package will be exported without data.

* **Existing snapshot** – this option will include the existing database snapshot in the export project package
  
	{% hint style="info" %}This option is only available when a snapshot is already created. Snapshots can be created via **Version Control** > **Add Snapshot of Data**.
	{% endhint %}
  
* **New snapshot from current database** – will create a new snapshot from the database and include it in the export

	{{% alert type="info" %}}This option is available after you run the app locally at least once, because a local database will be created when running the app for the first time.
	{% endhint %}

## 4 Read More

* [Import Project Package](import-project-package-dialog)
* [Version Control Menu](version-control-menu)