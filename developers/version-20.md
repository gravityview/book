# Introduction

This document highlights the current state of the future versions of GravityView. Notes, ideas, guidelines, explanations, documentation.

# Philosophy

It has become apparent that global state plagues GravityView to the extent that it is no longer funny anymore. For example, HTML templates relying on and querying global state data from singleton-based APIs. So much has gone into keeping global state accessible and up to date during the lifetime of a request that disassembling all the dependencies is a nightmare we're currently fighting :godmode:

The new API relies on passing controllable state from one component to the next as function call arguments. This allows for better unit testing, dependency injection and state decoupling; a better experience for all involved in the development ecosystem of our project. 

Unfortunately, WordPress does force us to sometimes depend on global state. Globals like `$wp_query`, `$post` and the whole notion of actions and filters leave us with no other choice but to play the global game :feelsgood:

The only instances of shared global state currently reside in the following globals:

- `$wp_query` - used by `wp_query_get` calls to parse the current URL.
- `$post` - Determines the current post inside tag filters (e.g. `the_content` callbacks).
- `$wp_actions` - Some various mocks and hacks that we do.
- `gravityview()->request` - the current request used by some components where request cannot be passed via arguments (e.g. shortcode callbacks, etc.)
- The legacy globals, still used by some of the code around (see `\GV\Mocks\Legacy_Context` class) that tries to encapsulate this into one bundle.

# Notes on...

## PHP Version

The future has a minimum version requirement of PHP 5.3, although it would love to someday be able to function on PHP7 (maybe in 2025?). The plugin will not activate on PHP 5.2 and lower any more.

## Querying Entries

Gravity Forms 2.3 is planning on releasing a new `GF_Query` class, which, however, is not powerful enough for what GravityView wants to do. The new APIs will eventually include our own query generator which will allow for very advanced joins (including joins and unions among different forms, think merging two or more form sources into one list vertically, horizontally :wand:).

The legacy codebase interfaces with Gravity Forms' good 'ol `search_criteria`. We have wrapped it into our own object-based entry query builder (think ORM for Gravity Forms) which provides a nice interface to query and filter and sort entries (eventually join and union entries, too).

 [`\GV\Entry_Collection`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-collection-entry.php) class. An instance of the class can be queries by applying filters, sorts, limits, offsets and paging. While the `limit()`, `offset()` and `page` methods of an `Entry_Collection` instance accept integer arguments, `filter()` and `sort()` accept special [`\GV\Entry_Filter`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-collection-entry-filter.php) and [`\GV\Entry_Sort`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-collection-entry-sort.php) instances, which provide a unified API for filtering and sorting entries, while hiding all data source querying implementations behind it.

Right now, there's only one very simple `\GV\Entry_Filter` implementation for Gravity Forms - the [`\GV\GF_Entry_Filter`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-collection-entry-filter-gravityforms.php). It understands the standard `$search_criteria['field_filters']` array and passes it as is during querying. This means that the power of querying is limited to what Gravity Forms can do for now.

See [`\GFAPI::get_entries`](https://www.gravityhelp.com/documentation/article/api-functions/#get_entries) for search criteria details and information. The sort, limit, paging and offset parameters are ignored, though.

Here's a simple example:

```php
$form = \GV\GF_Form::by_id( 1 );
$entries = $form->entries->filter(
    \GV\GF_Entry_Filter::from_search_criteria(
        /** Gravity Forms search_criteria go here */
    )
);
```

Keep in mind, that entries have not been fetched yet due to lazy-loading callback mechanisms inside the [`\GV\GF_Form`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-form-gravityforms.php#L63) data source, which knows how to fetch its entries.

Filtering a second time will merge the search criteria, since Gravity Forms doesn't support advance querying and boolean operations (maybe when `GF_Query` hits in 2.3? :crossed_fingers:)

```php
$field = new \GV\Field();
$field->ID = 'date_created';
$entries = $entries->sort( \GV\Entry_Sort( $field, \GV\Entry_Sort::ASC, \GV\Entry_Sort::ALPHA ) );
```

Sort. Notice how every operation returns a copy of the backing `\GV\Entry_Collection` and is non-destructive to the previous instance.

```php
$entries = $entries->limit( 5 )->page( 1 );
```

Page size and page number. Still no queries to the data source (and database, in the case of Gravity Forms).

```php
printf( "The total number of entries in the database: %d\n", $entries->total() );
printf( "The total number of entries available/fetched: %d\n", $entries->count() );
```

Once `count()` has been called, the entries are actually fetched. Calling `fetch()` fetches entries in a collection as well (i.e. calls all registered fetching callbacks).

An array of [`\GV\Entry`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-entry.php) objects is returned when calling the `all()` method.

This is a highly simplified filter and sorting API, designed up to the limits of the current Gravity Forms querying mechanisms - simple searching with no advanced boolean logic, single-column sorting. A more advanced version of the API should support an ORM-like interface:

```php
new Entry_Filter(
    Field::by_id( 3 )->eq( 99 )->and(
        Field::by_id( 4 )->neq( null )->or( Field::by_id( 4 )->lte( 0 ) )
    )->and(
        Field::by_id( 5 )->like( "%search%" )->and( Field::by_id( 6 )->between( $t, $f ) )
    )
);
```

The multiple form sources interface would provide additional queries objects like `\GV\Entry_Join` and `\GV\Entry_Union`. Eventually moving all query objects to their own namespace.

### And state?

Let's discuss how state would impact querying a set of entries. In short: it doesn't, and it shouldn't.

Entry collections are completely decoupled from the global state, so are queries. Calling `\GV\GF_Form::get_entries` does not affect any global state or the data source itself, merely returning a brand new collection instance that can further be filtered, sorted, paged and finally retrieved.

Any augmentations to a collection have to be done as closely to a context that is to be affected as possible. Filters and actions will be in place in rendering and output procedures along with a rendering context (which would contain a `\GV\Request` right there and then). Catch-all filtering should be provided, alas without any exposed context, and used with utmost care by developers, pushing towards better programming practices.

## Sources and Fields

The new API revolves around hiding all sources of data behind [`\GV\Source`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-source.php) subclasses. We already are at a point where we have two source subclasses: [`\GV\Internal_Source`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-source-internal.php) and [`\GV\GF_Form`](https://github.com/gravityview/GravityView/future-render/future/future/includes/class-gv-form-gravityforms.php). Every entry in a View can contain a combination of data from our internal (custom content, edit link, etc.) and Gravity Forms (form fields, etc.) sources.

These sources know how to fetch a [`\GV\Field`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-field.php) instance by a combination of parameters. The parameters are usually limited to the field ID, but may require additional data, like form ID for Gravity Form fields. Thus, we always query a particular source (even via aliases like `\GV\Field::get( $source, $args )`) for a field we are interested in. The respective source has other various methods that can be used in source-related contexts. Meanwhile, the `\GV\Field` class provides a unified API across all field types and related sources.

### Cool beans. Now show me some code :)

Absolutely. Say we want to fetch a value for the name field on a GravityView application form. Here's how we'd go about doing this.

```php
$form_id = /** ID of Gravity Form */;
$field_id = /** ID of name field */;

$source = \GV\GF_Form::by_id( $form_id );
$field = \GV\GF_Form::get_field( $source, $field_id );
/** or, just an alias */
$field = \GV\Field::get( '\GV\GF_Form', array( $source, $field_id ) );
```

Having retrieved our field, we can now ask it for a value, the `get_value` method accepts any of the following in order: a `\GV\View`, a `\GV\Source`, a `\GV\Entry` and a `\GV\Request`. Right now, all our implementations require just the `\GV\Entry` to be set, ignoring everything else, although, if possible, everything should be supplied so that filters can access the context in its entirety.

```php
$entry = \GV\GF_Entry::by_id( $entry_id );
echo esc_html( $field->get_value( null /** View */, $source, $entry, null /** Request */ ) );
```

### What about state?

Note how field retrieval from sources is stateless, nothing is changed, nothing is kept around, the required stuff is created there and then, dispensable and only relevant for the shortest required amount of time. Value retrieval from fields is, in a similar way, stateless, and always requires an ad hoc context.

Want to filter the value of a field? There a `gravityview/field/value` filter that provides the state (the field class, context and value) for developers to hook into. If we require more state to be shared we can push related information, like the current `\GV\View` this field is requested in, the current `\GV\Request` even.

The sane `\GV\Request` default falls back onto `gravityview()->request` when needed, which in turn falls back to `\GV\Frontent_Request`.

## Rendering

A `\GV\View` is rendered by a [`\GV\View_Renderer`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-renderer-view.php). The renderer needs the `\GV\View` instance to be rendered and a `\GV\Request` instance for context, from which it gathers which pieces to render (single view, edit, etc.).

```php
$renderer = new \GV\View_Renderer();
$renderer->render( $view, new \GV\Frontend_Request() );
```

### Wow, is that it?

Yes, but the `render()` call hides a lot of quite complex magic inside. Here's what happens inside:

1. An `\GV\Entry_Collection` is retrieved depending on the passed request, View settings, etc.
1. A [`\GV\View_Template`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-template-view.php) is instantiated with the View, entries and the request context. There are many `\GV\View_Template` subclasses for the different View templates GravityView provides (table, listing, etc.), and a `\GV\Legacy_Template` that is a fallback for older plugins, theme templates, etc.
1. `$template->render()` is finally called, which puts in motion another chain-reaction.

Every `\GV\View_Template` provides a set of required methods that the templates can use via the `$gravityview` object. The object exposes the following data:

- `$gravityview->template` - the `\GV\View_Template` instance that's rendering the template. Which exposes:
  - all [`Gamajo_Template_Loader`](https://github.com/GaryJones/Gamajo-Template-Loader/blob/develop/class-gamajo-template-loader.php) functionality (like `get_template_part`, etc.)
  - other "template tags" which are implementation-specific, like `the_columns()` for table Views, `the_entry()`, etc.
- `$gravityview->view` - the View being rendered
- `$gravityview->entries` - the filtered entries
- `$gravityview->request` - the current request
- `$gravityview->fields` - the View fields

This is where another renderer comes into light: the [`\GV\Field_Renderer`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-renderer-field.php).

### Wait, fields need a renderer? Hmm...

Absolutely. Different contexts call for different rendering strategies and processes. For example, in a table we might want to output "$2,949.10", while outputting the same value as "2949.10" in an REST API request. So renderers gonna render, while haters gonna hate :punch:

`\GV\Field_Renderer`'s `render` method requires a `\GV\Field`, a `\GV\View`, a `\GV\Source`, a `\GV\Entry` and a `\GV\Request`. The renderer will process this context and require the necessary templates. While field templates are not necessary, the renderer will attempt to find a template to render the raw returned value from `\GV\Field::get_value` or render it as is.

The default field fallback template is `field.php`, overridden by `field-html.php` for HTML output. A myriad of granular overrides are also available, the more important of which is the `field-$type.php` template.

Field templates, just like View templates have a `$gravityview` variable defined (a `\GV\Template_Context` instance) which comes with the following data:

- `$gravityview->template` - the `\GV\Field_Template` instance that's rendering the field. Similar to the View template instance, it exposes defined helpers and Gamajo methods.
- `$gravityview->field` - the `\GV\Field` being rendered.
- `$gravityview->value` - the raw value for this field.
- `$gravityview->display_value` - the display value for this field (localized dates, numbers, currencies, etc.)

As well as some context:

- `$gravityview->field` the `\GV\Field` context if applicatble.
- `$gravityview->view` - the `\GV\View` context if applicable.
- `$gravityview->source` - the `\GV\Source` (form) context if applicable.
- `$gravityview->entry` - the `\GV\Entry` context if applicable.
- `$gravityview->request` - the `\GV\Request` instance if applicable.

### Single entry rendering

Yes. Single entry View and edit output is also performed by a renderer: the [`\GV\Entry_Renderer`](https://github.com/gravityview/GravityView/blob/future-render/future/includes/class-gv-renderer-entry.php).

In fashion similar to the other renderers it requires a `\GV\Entry` instance, a `\GV\View` instance and a `\GV\Request` instance (default: `gravityview()->request`). The templates should make use of the `$gravityview` variable, which is exactly like the one passed to View templates.

### Speaking of templates...

All templates are kept in "/templates/". User overrides are searched for in "gravityview/{entries,views,fields}" of the child and then parent themes. Legacy templates (DataTables comes to mind) and theme overrides work thanks to the `\GV\Legacy_Template` which sets up legacy state and restores it immediately afterwards.

New templates should use the `$gravityview` variable inside them. If you're using `global`, `::getInstance`, `$GLOBALS` in the future, then you're doing it wrong. Admins will receive a message regarding the presence of legacy and deprecated template files.

Complex logic should be kept inside a subclass of the Template class, and overridden using the `gravityview/template/{view,entry}/class` filters.

### A word on edit entries

The edit entries process has not been touched by future yet. The `\GV\Edit_Entry_Renderer` is responsible for setting up legacy state, and invoking the necessary reaction from the edit-entry extension. The edit-entry (as well as the delete-entry and approve-entry) extension will eventually be moved into the core codebase.

### Output

GravityView can generate output in the following cases:

- Accessing a View directly by URL - outputs a View or an Entry depending on the URL
- Accessing a View or View details via the `[gravityview]` shortcode (in content or `do_shortcode`, or even `\GV\Shortcodes\gravityview::callback` for the tinkerers out there) - outputs a View or an Entry depending on the URL, or View details they are requested.
- Accessing an entry via oEmbed (link to Entry in content, could be content on an external site, too!) - outputs an Entry
- Accessing a field via the `[gvfield]` shortcode - outputs a field from a specified View, Entry.

That said, anyone is welcome to use the renderers directly as needed in their PHP code. Bear in mind, though:

### Security

There are no permissions checks in play inside the renderers, so it's up to the calling context to perform the necessary checks. GravityView does these inside build-in output handlers (`the_content`, shortcodes, oEmbed). Failing to do so will expose data that should not be visible.

That said, deleting and editing have their own permissions checks, so they won't work. Fields that should not be displayed won't be displayed since they are filtered by visibility in the renderers themselves.

## Ugh, this is pretty complicated...

It is, yes. Managing state through argument passing is pretty ugly and complicated. There are, however, several utility wrappers that help with simple development use-cases, where parameters are automatically guessed and initialized as defaults. This is the core of the GravityView API wrapper.

Meet `gravityview()`. Do not call before the `init` hook has been fired.

### The current request

`gravityview()->request` stores the current detected request. `\GV\Frontend_Request`, `\GV\Admin_Request`, `\GV\Mock_Request`, `\GV\AJAX_Request`, `\GV\REST_Request`, etc. The value is writable and is considered a global until we introduce a better way (using dependency injection, probably) to control what request exists at any given point in time.

### Views

`gravityview()->views->get()` retrives a view by context, ID, posts, etc. Feed it anything, it will try to find out what you meant and return a `\GV\View`.

## Extensions

Extensions should inherit from the `\GV\Extension` class instead of `GravityView_Extension`. The `gravityview_tooltips` filter has been renamed to `gravityview/metaboxes/tooltips` to conform with our newer filter/action nameing standards.

## Settings

`GravityView_Settings` is deprecated in favor of the `gravityview()->settings` instance.

##  Widgets

`GravityView_Widget` is now, you guessed it - `\GV\Widget`. Back-compatibility is achieved via inheritance (`GravityView_Widget` inherits from `\GV\Widget`).

New `\GV\Widget_Collection` along with object-based configurations mean that widget constructors are now called as many times as needed and not just once. Thus, it is imporant to prevent widgets from hooking into actions and filters multiple times (resulting in duplicate output of widgets) by checking for `$this->is_registered()` before any `add_action`, `add_filter` calls, especially in constructors.

### More to come soon, as needed...