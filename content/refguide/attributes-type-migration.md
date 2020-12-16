# Attribute Type Migration
**&#x2713;** | Conversion always possible.
**\*<sup><small>note</small></sup>** | Conversion is not always possible, or data will be changed during conversion. See related note for more information. If conversion is not possible, the behavior is the same as for "**X**", below.
**X** | Conversion not possible. The original column will be removed and a new column will be created with default values for the existing rows.

![Table of conversions - click to enlarge](attachments/attributes-type-migration/conversion-table.png)
(*Click the image to enlarge*)

### 2.3 Manual Conversion

Even if Mendix cannot convert the values of a specific column to another type, you can still manage that manually. Change the name of the attribute, for example append the text 'Deleted' to its name. Create a new attribute with the same name and the new data type. Look up each occurrence of the old (renamed) attribute in the whole model and change this to the new attribute. Be sure that there is no microflow or page anymore which refers to the old attribute.

Create a microflow in which you retrieve all instances of the entity, loop through the instances and for each instance, read the value of the old attribute, convert the value, store it in the new attribute and commit the instance. Place a button on an administrator page which calls this microflow.

When you deploy, you have to run this microflow one time, after which you can remove both the microflow and the button pointing to it, and then you can also remove the old attribute.

## 3 Association Type Changes on Existing Associations

When you have a one-to-many association and change it into a one-to-one association, be aware that duplicate associations are not cleaned up in the database. For example, a one-to-many association from entity A to entity B allows multiple references: a1 to b1, a1 to b2, etc. One-to-one associations only allow a single reference per object: a1 to b1. Duplicate association entries like a1 to b2 are not cleaned up when you redeploy your app.
