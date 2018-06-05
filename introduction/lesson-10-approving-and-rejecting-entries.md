# Lesson 10: Approving and Rejecting Entries

In this lesson, we'll talk about one of the most-frequently-used features of GravityView - **Entry Approval and Rejection.**

Entry Approval is particularly useful for submission-style websites. **If you want to let users submit data** _**but**_ **don't want it to automatically be added to the View, Entry Approval is for you.** In other words, you want to moderate submissions before displaying them in the View. As this is the most common use-case for this feature, we'll focus on it in this lesson.

### 1. Make sure _Show only approved entries_ is enabled for your View.

Before you do anything else, make sure that you've enabled "Show only approved entries" for your View. This option is under the _View Settings &gt; View Settings_ tab on the View Configuration page.

![show-only-approved-entries](../.gitbook/assets/show-only-approved-entries.png)

### 2. Enable _Show all entries to administrators._

After you enable the Show all entries option, a new option will appear below. When this is enabled, administrators will be able to see _all_ Entries, not only the approved ones. This is particularly useful if you're using the Front End to approve and reject Entries.

![show-all-entries](../.gitbook/assets/show-all-entries.png)

### 3. Go to the Gravity Forms page for your desired Form.

Then, go to the _Gravity Forms &gt; Entries_ page for the form attached to your Entries. Click the _Entries_ tab.

![entries](../.gitbook/assets/entries.png)

On the left-hand side, you'll see a column with a spaceman at the top. This is the _Approve/Reject_ column.

![approve-reject](../.gitbook/assets/approve-reject.png)

**An Entry can have three possible statuses:**

* **Not Yet Reviewed,** which is represented by an orange circle
* **Rejected,** which is represented by a red X
* **Approved**, which is represented by a green checkmark

![not-yet-rated](../.gitbook/assets/status.png)

To change the status of an Entry, simply click on it. Once approved or rejected, an Entry cannot return to the "Not Yet Reviewed" status.

As we mentioned above, if you have enabled the "Show only approved entries" option, Entries will not be displayed in a View until they are manually given the _Approved_ status by an administrator. That is to say - Entries with the _Not Yet Reviewed_ or _Rejected_ status will not be displayed.

## Front End Entry Approval

Approving and Rejecting Entries in the back end WordPress dashboard is useful, no doubt. But what if you have a _ton_ of Entries? Or what if you want [to give non-administrator users the ability to approve or reject Entries?](https://docs.gravityview.co/article/311-gravityview-capabilities)

In that case, you'll want to set up Entry Approval/Rejection on the front end, directly in the View itself.

#### 1. First, go to the View Configuration page for your desired View.

Stay on the _Multiple Entries Context_ tab and scroll down to the _Entries Fields_ section. Click _Add Field._

![add-field](../.gitbook/assets/add-field.png)

Then, scroll down in the modal window about halfway. We want the _Approve Entries_ Field. Click it to add it to your View.

![approve-approval](../.gitbook/assets/approve-entries-field.png)

You can also edit the Field's settings by clicking on the blue gear icon.

![blue-gear](../.gitbook/assets/blue-gear.png)

#### 2. Then, update the View and preview it on your site.

The _Approve / Reject_ column is now visible.

![front-end-view](../.gitbook/assets/front-end-view.png)

To approve or reject an Entry, simply click on it:

![approve-in-view](../.gitbook/assets/approve-in-view.png)

And that's it! To read more about Front End Entry Approval, [check out this Knowledge Base article.](https://docs.gravityview.co/article/390-entry-approval)

## Other Tips and Tricks

#### The {approval\_status} Merge Tag

The {approval\_status} Merge Tag allows you display the approval status of Entries. [Check out this documentation for using it.](https://docs.gravityview.co/article/389-approvalstatus-merge-tag)

#### Modifying the CSS of Front-End Approval

Want to modify the CSS of the View you use for Front-End Approval? [Try this guide.](https://docs.gravityview.co/article/388-modifying-the-css-of-front-end-approval)

#### Hiding the Approve/Reject Column

Didn't find this lesson useful? Not a problem, you can also just [remove the Approve/Reject column entirely.](https://docs.gravityview.co/article/248-hiding-the-approvereject-entry-column)

