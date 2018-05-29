# Lesson 2: Views

**Welcome to the second lesson of GravityView Academy!** Hopefully, you've gone through the first lesson. If not, we recommend doing so first! **At the very least, you'll need to have a Form created in order to complete this lesson.**

Last time, we talked about Forms, Fields, and Entries. In this lesson, we'll start using the GravityView plugin itself. After all, this is GravityView Academy! Specifically, we'll talk about Views.

Let's get started!


## What is a View?

The concept of a View can be a little hard to grasp at first. The easiest way to think about a View is to think about the concepts of **Front End** and **Back End.**



### Front End vs. Back End

If you aren't a tech-savy user, you might be unfamiliar with these terms. What's the difference? It's pretty simple:

- **The Front End is where users interact with your website.** On a WordPress website, the Front End is where Pages and Posts are displayed.

  

![front-end](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/front-end.png)



- **The Back End, alternatively, is where the website administrator(s) manages the site.** On a WordPress website, the Back End is also referred to as the "WordPress Admin page". By default, the URL for the Back End is *Example.com/wp-admin*.

  

![back-end](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/back-end.png)



## Gravity Forms and Entries

If you remember from last lesson, we said that an Entry is simply the data from one form submission, packaged together into one "unit". Entries are attached to a specific Form and are created when a user submits the form.

**Here's the important point to understand:** in Gravity Forms, the only way to see these Entries is on the Back End in the settings, on the *Forms > Entries* page. There is no way to display or modify these Entries on the Front End on your website.

That's where GravityView comes in. GravityView allows you to create *Views* - hence the company name ;) **A View is simply the display of Entries on the Front End of your website.**

Let's say that again - **a View is simply the display of Entries on the Front End of your website.** A View has many different pieces, but the the entire over-arching concept is called a *View.* (We'll talk about these different pieces in a separate lesson.)



## Creating Your First View

To help you really understand this concept of a View, let's walk through creating our own. Let's continue our example from Lesson 1:

> Let’s imagine that you’re throwing a potluck party at your apartment on the International Space Station. Since traveling into outer space isn’t cheap (and the dining room is tiny!) you want your guests to fill out a form beforehand.

Except now, we want to go a step further and display these Form Entries on a page on the Front End of our site, so that everyone can see it. To do this, we need to create a View.

First, go to the *View > New View* page on your WordPress sidebar.



![new-view](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/new-view.png)



We need to give our View a name. Let's call it *Who's Coming to the Party?*



![new-view-name](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/new-view-name.png)



### Connecting the View to a Form

Now we need to link this View to a Form. This Form is called our *Data Source.* Let's select the Form we created in Lesson 1 - *Who's Coming to the Party?*

**Note:** we created this Form in Lesson 1. If you haven't yet completed Lesson 1, you'll need to go back and do it now.



![data-source](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/data-source.png)



### Choosing a Layout

After we choose a Data Source, we need to choose a Layout. A Layout is simply *how* our Entries will be displayed on the page. There are two default layouts in GravityView:

- Table Layout
- Listing Layout

Let's talk about each of them individually.



![view-layout](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/view-layout.png)



#### Table Layout

The Table Layout will display your Entries in a table. This layout is something like a spreadsheet or Excel document - you can browse Entries, search, filter by Industry, and do other actions.



![table-layout](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/table-layout.png)



#### List Layout

But what if you want to display more information about each Entry (and have multiple Entries displayed on the same page?) In that case, you'll want to use the *List Layout.*

The List Layout will display your Entries as a series of Listings. This is particularly useful for directories or listings. 

![list-layout](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/list-layout.png)



#### Other Add-on Layouts

In addition to the Table Layout and Listing Layout, there are a few other Layouts available. [You'll need to purchase a *Galactic Plan* in order to use them.](https://gravityview.co/pricing/)



![premium-addons](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/premium-addons.png)



##### Maps Layout

Want to display your Entries on a Google Map? The Maps Layout has got you covered.

##### DataTables Layout

The DataTables Layout allows you to use [DataTables](https://datatables.net/), the best script for working for tabular data. Browse, filter, and sort entries with live updates.

##### DIY Layout

Are you a designer or developer? The DIY Layout lets you do-it-yourself.



## Configuring the View

For our example, let's just use the default Table Layout.  Click *Select* to choose it.

After you choose the Layout, you'll be presented with a bunch of options - don't be intimidated! This is the View Configuration page. It's where all the action happens in GravityView.

This page is divided into three tabs:

- Multiple Entries

- Single Entry

- Edit Entry

  

  ![contexts](/Users/gravityview/Dropbox/GravityView/Academy/Book/book-academy/Lesson 2/2-images/contexts.png)



We call these *Contexts*. You can think of them as different components, or sides, of a View. We'll cover each of them in more detail in future lessons.

---



Whew, that's enough for today! In the next few lessons, we'll explore the *Multiple Entries,* *Single Entry* and *Edit Entry* contexts in more detail.

*Class dismissed!*