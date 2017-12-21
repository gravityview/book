The `[gvlogic]` shortcode
=========================

### Dynamically show or hide content

If you only want to show content if the value matches a certain condition, you can do that with `[gvlogic]`.

------------------------------------------------------------------------

If you are using GravityView for an [Issue Tracker](https://demo.gravityview.co/blog/view/issue-tracker/), you may want to display content to a user based on the ticket status.

	[gvlogic if="{Issue Status:13}" is="Closed"]
	  You are viewing a closed ticket.
		
	  {Assigned Staff:49} was working on your ticket. If you would like to get in touch with them, you can call them at {Assigned Staff Phone:54}.
	[/gvlogic]

You can also display alternate content if the value does not match:

	[gvlogic if="{Issue Status:13}" is="Closed"]
	  Your issue is closed.
	[else]
	  I see your issue is {Issue Status:13}. Please <a href="mailto:floaty@gravityview?subject=cool+demo">email us</a> with any questions.
	[/gvlogic]

For the example above, if the "Issue Status" field value is "Closed", users will see "Your issue is closed."

If the value is "Pending", users will see: "I see your issue is Pending. Please [email us](mailto:floaty@gravityview?subject=cool+demo) with any questions."

------------------------------------------------------------------------

Shortcode Parameters
--------------------

### Required Parameter: `if`

The `[gvlogic]` shortcode has one required parameter: `if` - it must be set so that the shortcode has something to compare against.

The `if` parameter accepts Gravity Forms Merge Tags, available in the Custom Content field.

### Comparison Parameters

*In the definitions below, the "left value" will be the value of the
`if` merge tag, and the "right value" is the value passed to the
parameter. See "Examples" below for more examples.*

- `is` or `equals` - The left and right values are the **same**
- `isnot` - The left and right values are **different**
- `contains` - The left value **contains** the right value, with or
without other text
- `not_contains` - The left value **does not contain** the right value
- `starts_with` - The left value **starts with** the right value
- `ends_with` - The left value **ends with** the right value

### Number comparison only

The following parameters are only able to compare numbers or prices.
Date comparison is currently not supported.

- `greater_than` - The left value is **numerically greater than** the
right value
- `greater_than_or_is` or `greater_than_or_equals` - The left value is
**numerically greater than or equal to** the right value
- `less_than` - The left value is **numerically less than** the right
value
- `less_than_or_is` or `less_than_or_equals` - The left value is
**numerically less than or equal to** the right value

### The `else` Parameter

You can define an `else` parameter to display if there is not a match,
like so:

	[gvlogic if="{Number:5}" is="28457" else="That didn't match."]
	  The field value was 28457.
	[/gvlogic]

You can also use Merge Tags in the `else` parameter.

	[gvlogic if="{Number:5}" is="28457" else="{Number:5} is a bad number."]
	  The field value was 28457.
	[/gvlogic]

In the example above, let's see what the output looks like with
different values for the "Number" field (Field ID \#5):

- `28457`: "The field value was 28457"
- `9`: "9 is a bad number."
- `100`: "100 is a bad number."

### The `[else]` shortcode

Instead of using the `else` parameter, you can add `[else]` inside the shortcode. This allows you to display different content if the conditions are not met.

	[gvlogic if="{Number:5}" is="28457"]
	  The field value was 28457.
	[else]
	  <h3>You can use HTML inside the shortcode if you want!</h3>
	[/gvlogic]
	
The `[else]` shortcode also supports logic! You can use multiple `[else]` blocks to check multiple conditions:

	[gvlogic if="{Address (City):14.3}" is="New York"]
	  You live in the Big Apple!
	[else if="{Address (State):14.4}" is="New York"]
	  You live upstate.
	[else if="{Address (Country):14.6" is="United States"]
	  You live in the U.S. of A.
	[else]
	  You live on Earth, but not in the USA.
	[/gvlogic]

In the example above, if the address submitted was outside the United States, the displayed content would be "You live on Earth, but not in the USA."

`[else if]` supports all of the same paramters as `[gvlogic]`, including the different comparisons.

------------------------------------------------------------------------

Examples
========

Use HTML and shortcodes inside the `[gvlogic]` shortcode
--------------------------------------------------------

*The only limitation is that you can't use the `[gvlogic]` shortcode inside itself.*

	[gvlogic if="{Number:5}" is="28457"]
	  <h1>28457 is my favorite number!</h1>
	[else]
	  <h3>You can use HTML inside the shortcode if you want!</h3>
	  <p>{Number:5} is not my favorite number. You lose.</p>
	[/gvlogic]

Text Comparison Examples
------------------------

#### Parameter: `is`

You can use `[else]` inside the shortcode to display different content if the conditions are not met.

	[gvlogic if="{Address (City):14.3}" is="New York"]
	  You live in the Big Apple!
	[else]
	  You live outside NYC.
	[/gvlogic]

#### Parameter: `is` (using the `else` parameter)

You can also use the `else` shortcode parameter instead of the `[else]` block to achieve the same goals. The `else` parameter cannot span multiple lines, so it is more limited.

	[gvlogic if="{Address (City):14.3}" is="New York" else="You live outside NYC."]
	  You live in the Big Apple!
	[/gvlogic]

#### Parameter: `isnot`

	[gvlogic if="{Address (City):14.3}" isnot="New York"]
	  You live outside NYC.
	[/gvlogic]

#### Parameter: `contains`

Let's say there's a paragraph text field where users submit their favorite quote. You have a special affinity for the [All the world's a stage monolog](https://en.wikipedia.org/wiki/All_the_world's_a_stage), and you want to share that love.

	[gvlogic if="{Paragraph Text:2}" contains="All the world's a stage"]
	  Whoa, you're quoting Shakespeare's the "All the world's a stage" monolog! It's as I like it!
	[else]
	  Why aren't you quoting "All the world's a stage"? Booo!
	[/gvlogic]

#### Parameter: `not_contains`

We can flip the `contains` example around, as well. This checks if the value does *not* contain the match.

	[gvlogic if="{Paragraph Text:2}" not_contains="All the world's a stage"]
	  Why aren't you quoting "All the world's a stage"? Booo!
	[else]
	  Whoa, you're quoting Shakespeare's the "All the world's a stage" monolog! It's as I like it!
	[/gvlogic]

#### Parameter: `starts_with`

Here we check whether the State value starts with "New ".

	[gvlogic if="{Address (State / Province):14.4}" starts_with="New "]
	  You may live in New York, New Jersey, New Hampshire, New Mexico.
	[else]
	  You live in an old state!
	[/gvlogic]

#### Parameter: `ends_with`

Now we check whether someone's email ends with `.rocks`, a [very silly top-level domain](http://domains.rocks).

	[gvlogic if="{Email:16}" ends_with=".rocks"]
	  Wooohooo! You are hard core! Your email is rad.
	[/gvlogic]

### Matching blank values

You can determine whether a field is empty by checking against an empty value, like so:

	[gvlogic if="{Text Field:38}" is=""]
	  This text field is empty
	[/gvlogic]

Similarly, you can check if a field is *not* empty:

	[gvlogic if="{Text Field:38}" isnot=""]
	  This text field is not empty
	[/gvlogic]

------------------------------------------------------------------------

Number Comparison Examples
--------------------------

In the examples below, `{Number:5}` is the Merge Tag generated by Gravity Forms. `:5` is the field ID, not the field value. It's a placeholder that will be replaced by each entry's value.

#### Parameter: `is`

	[gvlogic if="{Number:5}" is="12"]
	  The number is twelve.
	[else]
	  The number is not twelve.
	[/gvlogic]

#### Parameter: `is` (using the `else` parameter)

	[gvlogic if="{Number:5}" is="12" else="The number is not twelve."]
	  The number is twelve.
	[/gvlogic]

#### Parameter: `isnot`

	[gvlogic if="{Number:5}" isnot="12"]
	  The number is not twelve.
	[else]
	  The number is twelve.
	[/gvlogic]

#### Parameter: `greater_than`

	[gvlogic if="{Number:5}" greater_than="12"]
	  The number is greater than twelve.
	[else]
	  The number is less than or equal to twelve.
	[/gvlogic]

#### Parameter: `greater_than_or_is`

	[gvlogic if="{Number:5}" greater_than_or_is="12"]
	  The number is greater than or equal to twelve.
	[else]
	  The number is less than twelve.
	[/gvlogic]

#### Parameter: `less_than`

	[gvlogic if="{Number:5}" less_than="12"]
	  The number is less than twelve.
	[else]
	  The number is greater than or equal to twelve.
	[/gvlogic]

#### Parameter: `less_than_or_is`

	[gvlogic if="{Number:5}" less_than_or_is="12"]
	  The number is less than or equal to twelve.
	[else]
	  The number is greater than twelve.
	[/gvlogic]

------------------------------------------------------------------------

View Context Examples <a href="#" id="context"></a>
----------------------------------

Display content based on the current View mode ("context"), which correspond to the View Configuration tabs when editing an entry: Multiple Entries, Single Entry, and Edit Entry.

### Available `context` values:

- `multiple` - Multiple entries are visible
- `single` - Viewing a single entry
- `edit` - Editing a single entry
- `singular` - Is either `single` or `edit` context

#### Parameter: `is`

	[gvlogic if="context" is="multiple"]
	  Click the name of the person you want to learn more about!
	[/gvlogic]

#### Parameter: `is` (using the `else` parameter)

	[gvlogic if="context" is="single" else="You are viewing multiple entries."]
	  You are viewing a single entry.
	[/gvlogic]

#### Parameter: `isnot`

	[gvlogic if="context" isnot="singular"]
	  You are viewing multiple entries.
	[else]
	  You are viewing or editing a single entry.
	[/gvlogic]