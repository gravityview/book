# Lesson 1: Fields, Forms, and Entries



![img](https://gravityview.co/wp-content/uploads/2018/04/floaty-1-234x400.png)

**Welcome to the first lesson of GravityView Academy!** In this ongoing series, we’ll walk through our plugin and the ins-and-outs of using it. In this first lesson, we’ll start with the basics – *Forms, Fields, and Entries.* While some of these topics may seem simple, they are critical to understand (trust us!)

Let’s get started!

## Forms

Everything starts with the Form. Even if you’re a new Gravity Forms or GravityView user, you’re probably very familiar with forms. These days, most websites have forms, which they use for a variety of purposes, like contact forms, business directories, RSVP lists, and more.



![Example Form](./gitbook/images/example-form.png)



## The Structure of a Form

Now, in order to grasp how Gravity Forms and GravityView work together, it helps to break down a form and understand its structure.

Put in the simplest terms possible, *a form allows users to submit information to the website.* A typical form has three basic components:

- **The place where users write their information.** These are called *Fields* and include things like *Name,* *Email* or *Your Message.* Normally, Fields are text-boxes or other HTML elements, but they can also include a place to upload files, a date selector, or other specific things.
- **The submit button.** When the user clicks submit, the information is put into a single “package” and then sent somewhere (usually to a database on the website).
- **The submitted information,** which is viewable on the back end of the website. This “package” is called an *Entry.*

**Make sense?** Let’s go through an example to be sure!

## Creating a Form in Gravity Forms

Let’s imagine that you’re throwing a potluck party at your apartment on the International Space Station. Since traveling into outer space isn’t cheap (and the dining room is tiny!) you want your guests to fill out a form beforehand. To do this, we want to create a form in Gravity Forms. 



![New Form](./gitbook/images/new-form.png)



After you install the Gravity Forms plugin, navigate to the *New Form* page on your WordPress sidebar. Then, we’ll need to give our form a name. Let’s call it *Who’s Coming to the Party?* and click *Create Form* to create the form.

Now we’re on the *Form Edit* page. Here, we can customize our Form and pick which Fields we want to add. In Gravity Forms, there are a few different types of Fields. 



![Types of Fields](./gitbook/images/types-of-fields.png)



We won’t cover all of the differences in this lesson, but in brief:

- **Standard Fields** are for basic HTML elements, like text boxes, drop-down menus, and radio buttons.
- **Advanced Fields** are pre-optimized for specific purposes and include *Name, Date, Time, Email,* and so on.
- **Post Fields** allow users to submit WordPress post drafts. They can submit the Post Title, Excerpt, Post Image, and related information.
- **Pricing Fields** enable you to sell products using your form. You can configure products and allow customers to purchase items using your form.
- **GravityView Fields** are for specific GravityView features, like Approving or Rejecting Entries or allowing users to opt-in to displaying their submission on the website.

## Creating Our Party Form

For our example, we want to gather four pieces of information from our party guests: 

- Name
- Email
- The food they are bringing to the party
- A fun fact about themselves

### Drag-and-Drop

Now we simply need to drag a Field into the Form for each of the four items.

- We can use the *Name Field* for names, which is on the *Advanced Fields* tab.



![Name Field](./gitbook/images/name.png)



- For email, let's use the *Email Field*, which is also on the *Advanced Fields* tab.



![Email Field](./gitbook/images/email.png)



- For *What food or drinks are you bringing?* we can use a *Paragraph Text Field,* which is under *Standard Fields.*

  

![What food or drinks are you bringing?](./gitbook/images/food-bringing.png)



- Finally, for *What is a fun fact about yourself?* we can use a *Single Line Text Field.*



![Fun fact about yourself](./gitbook/images/fun-fact.png)



Double-check that everything looks right, then click *Update!*



### Putting the Form on a Page

Now that we’ve created our form, we need to put in on a page. To do this, simply create a new WordPress page. Then, on the Editor page, click *Add Form.*



![Add Form](./gitbook/images/add-form-to-page.png)



Select your form, customize the options, and click *Add Form.* You’ll then see a shortcode for your form. Finally, publish the page.

### Form Submission and Viewing Entries

Let’s see what the form looks like. If we navigate to the page, we’ll see our form. It looks good! Let’s fill out the fields and press submit.

![Submit Form](./gitbook/images/submit-form.png)





![Entry](./gitbook/images/entry-01.png)



## What is an Entry?

Now, let's talk a little bit about Entries. As we mentioned before, an Entry is simply the data from one form submission, packaged together into one "unit". Entries are attached to a specific Form. It's important to understand the concept of an Entry, as they are fundamental to the way Gravity Forms and GravityView work.

To view your Entries, navigate to the *Forms > Entries* page and select your Form from the menu at the top of the page. You should see your submitted Entry listed. 

If you hover over the Entry itself and click *View,* you can view the Entry details on a full page. This is useful if your Form has more than a few Fields (or if each Field has a lot of information).



![Full Entry](./gitbook/images/full-entry.png)



**And that’s it!** Hopefully you now understand how Forms, Fields and Entries work! In the next lesson, we’ll learn how these concepts connect to Views, which allow you to display your Entries on the front end of your website.

*Class dismissed!*

