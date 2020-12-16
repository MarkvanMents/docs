# Uniqueness Constraint Migration

You can resolve this issue simply, by moving unique validation rules of these attributes to the generalization entity where the attribute it defined.

![](attachments/datastorage/unique-validation-rule-resolved.png)

## 3 Unique Associations

A comparable situation occurs for associations. Consider the following example:

![](attachments/datastorage/one-to-many-assoc.PNG)

Initially, the domain model contains a one-to-many association between **Address** and **Person**. This means that a Person can have multiple addresses. After some time, the data structure is changed, because logic has been added to the app that only allows one Address per Person. Proper data modeling prescribes changing the association into a one-to-one association. New data will reflect the updated association properly.

![](attachments/datastorage/one-to-one-assoc.PNG)

Existing association data in the database must also adhere to the updated one-to-one association. This is checked at deployment. If a person has multiple addresses, the model will not deploy, and an error will be given in Studio Pro or in the logs of deployment in the (Mendix) cloud:

![](attachments/datastorage/startup-error-assoc.png)

We enforce this new stricter association on existing data in order to avoid easily overlooked mistakes that result in returning only a single address per person (where in fact they still have multiple addresses in the database). The Mendix Platform consistently returned the same address each run, but other addresses would be dormant entries in the database.

## 4 Help with Migration

To help with migrating your old data, Mendix has developed a migration toolkit. For details on this, please contact [Mendix Support](http://support.mendix.com).
