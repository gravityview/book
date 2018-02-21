# The `[gvfield]` Shortcode

The `[gvfield]` shortcode provides an easy way to plop any field from any entry based on some View settings. This feature is exclusive to GravityView 2.0 alpha.

## Use Cases

- Outputting a link to edit or view a user profile? Check.
- Showing the approval status of the latest entry submitted? Check.
- Showing the latest registered user name? Check.
- Showing the latest donation message, amount and name? Check.
- A thousand and one other uses? Check.

## Usage

This is a WordPress shortcode. It can be used in post content by adding `[gvfield]` (+ parameters) and in PHP code by calling [`do_shortcode`](https://developer.wordpress.org/reference/functions/do_shortcode/). The parameters:


|parameter|values|description|
|-|-|-|
|`view_id`|$id|The numeric View ID the entry should be displayed from. Required.|
|`entry_id` required|$id, "last", "first"|A numeric ID or slug referencing the entry. Or the last, first entry from the View. The View's sorting and filtering settings will be applied to the entries. Required.|
|`field_id`|$id[,$id..]|The field ID that should be ouput. Required. If this is a merge of several form feeds multiple fields can be provided separated by a comma; the `entry` parameter would have to be in `last` or `first` mode. Required.|
|$key|$value|Field setting overrides, like title, etc. These will be pulled in from the View if field was added to the the View, otherwise defaults will be used.|

## Examples

Outputting the latest donation message from View ID 4, field ID 49:

```
Latest donation message: [gvfield view_id=4 entry_id="last" field_id=49]
```

Outputting the latest registered member username and date registered, merged from two form feeds:

```
Latest registered user: [gvfield view_id=8 entry_id="last" field_id="1,5"]
Date registered: [gvfield view_id=8 entry_id="last" field_id="date_created"]
```

Outputting the edit link for the current user where the View is filtered to display entries only for the current user:

```
[gvfield view_id=1 entry_id="first" field_id=5 custom_label="My Profile"]
```

## Security

The standard security rules to outputting fields apply. In short, a field will not be shown if the current user cannot see such fields in the context of the view and the entry. Unapproved entries? A no show to non-admins. Deleted? Nope. View is password protected, a draft, private? Nuh-uh.

If you need to output a field from a View that shouldn't be accessible by frontend users, set it as "Embed-only".

## Advanced Usage: Filters

The `[gvfield]` shortcode calls upon several filters that allow developers to modify the output as needed.

### gravityview/shortcodes/gvfield/output

Filter the final output value of the field about to be output. Useful to override empty entries; for example, for non-logged in users, this can be used to output the registration link instead of a blank profile link.

```php
add_filter( 'gravityview/shortcodes/gvfield/output', function( $output, $view, $entry, $field ) {
    if ( $view && $view->ID == MY_SECRET_VIEW ) {
        if ( ! is_user_logged_in() ) {
            return "<a href="#">Login</a>";
        }
    }
    return $output;
}, 10, 4 );
```

### gravityview/shortcodes/gvfield/atts

Filter the initial shortcode attributes. Useful to tack on defaults or dynamically change IDs, etc.

```php
add_filter( 'gravityview/shortcodes/gvfield/atts', function( $atts ) {
    if ( $atts['view_id'] == MY_SECRET_VIEW && $user = wp_get_current_user() ) {
        $atts['entry_id'] = $user->secret_entry_id;
        $atts['custom_label'] = $user->secret_label;
    }
    return $atts;
} );
```