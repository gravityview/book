# Setting up Edit Entry

**Since Version 1.5**

In previous versions of GravityView, all form fields were shown when editing a View. In Version 1.5, you can choose which fields are editable in the Edit Entry screen.

## If you want the user who created the entry to be able to edit the entry, check the "Allow User Edit" checkbox

If the box is not checked, only Administrators and users who have access to editing Gravity Forms entries in the WordPress Dashboard will be able to see the Edit Entry links and edit the entry.

![][1]

[1]: https://gravityview.co/wp-content/uploads/2018/01/if-you-want-the-user-who-created-the-entry-to-be-able-to-edit-the-entry-check-the--allow-user-edit-.png?1468538262

## 1. Go to All Views

![][2]

[2]: https://gravityview.co/wp-content/uploads/2018/01/go-to-all-views.png?1468538263

## 2. Click on the View you would like to Edit

![][3]

[3]: https://gravityview.co/wp-content/uploads/2018/01/click-on-the-view-you-would-like-to-edit.png?1468538263

## 3. If your View doesn't already have an Edit Entry field, add one

For Edit Entry to be possible on a View, there needs to be an Edit Entry field. This will add a link to edit the entry to your layout.

### 3.1 Click the Single Entry tab

You can also have Edit Entry fields on the Multiple Entries view.

![][4]

[4]: https://gravityview.co/wp-content/uploads/2018/01/click-the-single-entry-tab.png?1468538264

### 3.2 Click Add Field in the zone where you want the Edit Entry link to appear

![][5]

[5]: https://gravityview.co/wp-content/uploads/2018/01/click-add-field-in-the-zone-where-you-want-the-edit-entry-link-to-appear.png?1468538265

### 3.3 Scroll down to "Edit Entry" and click on it

![][6]

[6]: https://gravityview.co/wp-content/uploads/2018/01/scroll-down-to-edit-entry--and-click-on-it.png?1468538265

### You can configure link text and other settings by clicking on the gear icon

Okay, now we've added an Edit Entry field. Let's configure the Edit Entry View layout.

![][7]

[7]: https://gravityview.co/wp-content/uploads/2018/01/you-can-configure-link-text-and-other-settings-by-clicking-on-the-gear-icon.png?1468538266

## 4. Click on the Edit Entry tab available in the View Configuration box

This step and the steps below only apply to GravityView 1.5 or higher.

![][8]

[8]: https://gravityview.co/wp-content/uploads/2018/01/click-on-the-edit-entry-tab-available-in-the-view-configuration-box.png?1468538267

## You will see an empty configuration

When the Edit Entry configuration is empty, all form fields will be displayed as editable. When not configured, GravityView hides fields with ["Admin Only" visibility](https://www.gravityhelp.com/gravity-forms-feature-highlight-admin-only-visibility/) from being edited by non-administrators. If the Edit Entry tab is configured, then GravityView will use the field settings in the configuration, overriding Gravity Forms settings. 

*Developers: to override this functionality, return false on the **gravityview/edit_entry/use_gf_admin_only_setting** filter.*

![][9]

[9]: https://gravityview.co/wp-content/uploads/2018/01/you-will-see-an-empty-configuration.png?1468538268

## 5. Click the "+ Add Field" button to add a field to be edited.

![][10]

[10]: https://gravityview.co/wp-content/uploads/2018/01/click-the-add-field--button-to-add-a-field-to-be-edited.png?1468538268

## 6. Click fields to add them to the configuration

![][11]

[11]: https://gravityview.co/wp-content/uploads/2018/01/click-fields-to-add-them-to-the-configuration.png?1468538269

## In this example, we have added four fields

![][12]

[12]: https://gravityview.co/wp-content/uploads/2018/01/in-this-example-we-have-added-four-fields.png?1468538269

## You can drag and drop the fields in the order you desire

![][13]

[13]: https://gravityview.co/wp-content/uploads/2018/01/you-can-drag-and-drop-the-fields-in-the-order-you-desire.png?1468538270

## 7. To limit field editing capabilities, click the gear icon

![][14]

[14]: https://gravityview.co/wp-content/uploads/2018/01/to-limit-field-editing-capabilities-click-the-gear-icon.png?1468538272

## You can make fields editable by only Administrators

This is helpful if you have "Allow User Edit" enabled, but you don't want to allow editing of a field by the user who created the entry. In this example, Administrators will still be able to edit the field in the Edit Entry screen.

![][15]

[15]: https://gravityview.co/wp-content/uploads/2018/01/you-can-make-fields-editable-by-only-administrators.png?1468538272

## 8. Update the View

Everything is now configured! 

![][16]

[16]: https://gravityview.co/wp-content/uploads/2018/01/update-the-view.png?1468538273

## Visit the View and edit an entry to see the Edit Entry configuration

Let's take a look at the Edit Entry functionality.

![][17]

[17]: https://gravityview.co/wp-content/uploads/2018/01/visit-the-view-and-edit-an-entry-to-see-the-edit-entry-configuration.png?1468538273

## What administrators see

All the fields are visible in this screenshot because we're logged in as administrators.

![][18]

[18]: https://gravityview.co/wp-content/uploads/2018/01/what-administrators-see.png?1468538274

## What the Entry Creator sees

The Entry Creator won't see any of the fields that are limited by role in Step 7. In this example, the Company Name is not visible.

![][19]

[19]: https://gravityview.co/wp-content/uploads/2018/01/what-the-entry-creator-sees.png?1468538275