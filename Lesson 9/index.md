# Lesson 9: Embedding Views and Entries

Want to embed your View on WordPress page or post? What about a specific Entry? Not a problem! In this lesson, we'll learn how to embed Views and specific Entries. 

Let's get started!



## Embedding a View

You can embed a View on any WordPress page or post via a shortcode. Here's how:

#### 1. First, go to your View's configuration page.

On the right side, under *Publish*, you'll see an Embed Shortcode. Copy this shortcode.

![embed-shortcode](./images/embed-shortcode.png)



#### 2. Go to your WordPress page or post page.

Paste the code into your Page or Post editor.

![paste-shortcode](./images/paste-shortcode.png)

Voilà - that's it! Your View is now embedded. You can also just click *Add View* directly in the Post/Page editor:



![add-view](./images/add-view.png)



#### Customizing the Embedded View

The [gravityview] shortcode can accept a number of parameters. The most commonly-used ones are...

- `id` - The ID of the View you want to display *(required)*
- `page_size` - Number of entries to show at a time *(Defaults to View setting)*
- `sort_field` - What form field id should be used to sort? *(See note)*
- `sort_direction` - ASC / DESC
- `search_field` - Only display entries with this text in the value *(See note)*
- `search_value` - Only display entries with this text in the value

[Read the full list of parameters on this page.](https://docs.gravityview.co/article/73-using-the-shortcode) 



## Embedding Views in Sidebar or Footer Widgets

Want to embed a View in a sidebar or footer widget? Unfortunately, the [gravityview] shortcode won't work in a standard Custom HTML widget by default. Instead, you'll need to install an additional plugin called [Shortcode Widget](https://wordpress.org/plugins/shortcode-widget/).

![shortcode-widget](./images/shortcode-widget.png)

When you install this plugin, a *Shortcode Widget* option will be added to your *WordPress > Widgets* page. 



![shortcode-widget-wp](./images/shortcode-widget-wp.png)



Simply drag this widget to your WordPress sidebar or footer and paste the shortcode:



![sidebar-example-widget-shortcode](./images/sidebar-example-widget-shortcode.png)



Your View will now be displayed!



## Embedding a Specific Entry

What if you want to embed a specific Entry, rather than the entire View? Easy-peasy. 

- Embedded Entries can be edited like normal
- Embedded Entries will display with the same configuration as on your View's *Single Entry* tab.
- You can embed multiple Entries on the same post or page.

### 1. First, navigate to your View.

In the View, navigate to the specific Single Entry that you want to embed by clicking on the Single Entry link.

### 2. Then, copy the URL of the Single Entry page.

Notice that this Entry has a specific number (11). Each Entry has its own ID number.



![single-entry-url](./images/single-entry-url.png)

### 3. Go to your WordPress Page or Post.

First, make sure you're on the *Visual* tab:



![visual-tab](./images/visual-tab.png)



Then, place your cursor where you want to put the Entry. Paste the URL, wait a moment, and you should see an image automatically appear:



![paste-embed-entry](./images/paste-embed-entry.png)



To edit the options of the embedded Entry, however over the placeholder image and click the pencil icon:



![edit-options](./images/edit-options.png)

Finally, save (or update) your Post or Page. Click *View Post* and you'll see your Entry! It's that easy.

 

![embedded-entry](./images/embedded-entry.png)