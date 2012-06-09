---
layout: page
date: 'Sat 2012-06-09 17:54:04 +0800'
slug: 'HelpLiquid'
title: "HelpLiquid"
description: ""
---
{% include JB/setup %}

<ul>
    <li><a href="#liquid_extensions">Jekyll Liquid Extensions</a></li>
    <li><a href="#liquid_for_designers">Liquid for Designers</a></li>
    <li><a href="/pages/Help.html#syntax_cheatsheet">On Markdown</a></li>
</ul>

Liquid Extensions
=================

https://github.com/mojombo/jekyll/wiki/Liquid-Extensions

Jekyll uses [Liquid] [L] to process templates. Along with the [standard liquid tags and filters] [s], Jekyll adds a few of its own:

  [L]: http://www.liquidmarkup.org/
  [s]: http://wiki.github.com/shopify/liquid/liquid-for-designers

## Filters

### Date to XML Schema
Convert a Time into XML Schema format.
{% raw %}
	{{ site.time | date_to_xmlschema }} => 2008-11-17T13:07:54-08:00
{% endraw %}

### Date to String
Convert a date in short format, e.g. “27 Jan 2011”.
{% raw %}
	{{ site.time | date_to_string }} => 17 Nov 2008
{% endraw %}

### Date to Long String
Format a date in long format e.g. “27 January 2011”.
{% raw %}
	{{ site.time | date_to_long_string }} => 17 November 2008
{% endraw %}

### XML Escape
Escape some text for use in XML.
{% raw %}
	{{ page.content | xml_escape }}
{% endraw %}

### CGI Escape
CGI escape a string for use in a URL. Replaces any special characters with appropriate %XX replacements.
{% raw %}
	{{ "foo,bar;baz?" | cgi_escape }} => foo%2Cbar%3Bbaz%3F
{% endraw %}

### Number of Words
Count the number of words in some text.
{% raw %}
	{{ page.content | number_of_words }} => 1337
{% endraw %}

### Array to Sentence
Convert an array into a sentence.
{% raw %}
	{{ page.tags | array_to_sentence_string }} => foo, bar, and baz
{% endraw %}

### Textilize
Convert a Textile-formatted string into HTML, formatted via RedCloth
{% raw %}
	{{ page.excerpt | textilize }}
{% endraw %}

### Markdownify
Convert a Markdown-formatted string into HTML.
{% raw %}
	{{ page.excerpt | markdownify }}
{% endraw %}


## Tags

### Include

If you have small page fragments that you wish to include in multiple places
on your site, you can use the include tag.
{% raw %}
	{% include sig.textile %}
{% endraw %}
Jekyll expects all include files to be placed in an `_includes` directory at the root of your source dir. So this will embed the contents of `/path/to/proto/site/_includes/sig.textile` into the calling file.

### Code Highlighting

Jekyll has built in support for syntax highlighting of over [100 languages] [100] via [Pygments] [P]. In order to take advantage of this you’ll need to have Pygments installed, and the pygmentize binary must be in your path. When you run Jekyll, make sure you run it with [Pygments support] [Ps]

  [100]: http://pygments.org/languages/
  [P]: http://pygments.org/
  [Ps]: https://github.com/mojombo/jekyll/wiki/Configuration

To denote a code block that should be highlighted:
{% raw %}
	{% highlight ruby %}
	def foo
	  puts 'foo'
	end
	{% endhighlight %}
{% endraw %}

The argument to `highlight` is the language identifier. To find the appropriate identifier to use for your favorite language, look for the “short name” on the [Lexers](http://pygments.org/docs/lexers/) page.

### Line number

There is a second argument to `highlight` called `linenos` that is optional. Including the `linenos` argument will force the highlighted code to include line numbers. For instance, the following code block would include line numbers next to each line:
{% raw %}
	{% highlight ruby linenos %}
	def foo
	  puts 'foo'
	end
	{% endhighlight %}
{% endraw %}

In order for the highlighting to show up, you’ll need to include a highlighting stylesheet. For an example stylesheet you can look at [syntax.css](http://github.com/mojombo/tpw/tree/master/css/syntax.css). These are the same styles as used by GitHub and you are free to use them for your own site. If you use `linenos`, you might want to include an additional CSS class definition for lineno in syntax.css to distinguish the line numbers from the highlighted code.

### Post Url

If you would like to include a link to a post on your site, you can use the `post_url` tag.
{% raw %}
	{% post_url 2010-07-21-name-of-post %}
{% endraw %}

There is no need to include the extension.

To create a link, do:
{% raw %}
	[Name of Link]({% post_url 2010-07-21-name-of-post %})
{% endraw %}

* * *

Liquid for Designers
====================

https://github.com/shopify/liquid/wiki/liquid-for-designers

There are two types of markup in Liquid: Output and Tag.

* Output markup (which may resolve to text) is surrounded by

{% highlight ruby %}
{% raw %}
{{ matched pairs of curly brackets (ie, braces) }}
{% endraw %}
{% endhighlight %}

* Tag markup (which cannot resolve to text) is surrounded by

{% highlight ruby %}
{% raw %}
{% matched pairs of curly brackets and percent signs %}
{% endraw %}
{% endhighlight %}

## Output

Here is a simple example of Output:

{% highlight ruby %}
{% raw %}
Hello {{name}}
Hello {{user.name}}
Hello {{ 'tobi' }}
{% endraw %}
{% endhighlight %}

### Advanced output: Filters

Output markup takes filters.  Filters are simple methods.  The first parameter
is always the output of the left side of the filter.  The return value of the
filter will be the new left value when the next filter is run.  When there are
no more filters, the template will receive the resulting string.

{% highlight ruby %}
{% raw %}
Hello {{ 'tobi' | upcase }}
Hello tobi has {{ 'tobi' | size }} letters!
Hello {{ '*tobi*' | textilize | upcase }}
Hello {{ 'now' | date: "%Y %h" }}
{% endraw %}
{% endhighlight %}

### Standard Filters

* `date` - reformat a date [syntax reference](http://liquid.rubyforge.org/classes/Liquid/StandardFilters.html#M000012)
* `capitalize` - capitalize words in the input sentence
* `downcase` - convert an input string to lowercase
* `upcase` - convert an input string to uppercase
* `first` - get the first element of the passed in array
* `last` - get the last element of the passed in array
* `join` - join elements of the array with certain character between them
* `sort` - sort elements of the array
* `map` - map/collect an array on a given property
* `size` - return the size of an array or string
* `escape` - escape a string
* `escape_once` - returns an escaped version of html without affecting existing escaped entities
* `strip_html` - strip html from string
* `strip_newlines` - strip all newlines (\n) from string
* `newline_to_br` - replace each newline (\n) with html break
* `replace` - replace each occurrence *e.g.* `{{ 'foofoo' | replace:'foo','bar' }} #=> 'barbar'`
* `replace_first` - replace the first occurrence *e.g.* `{{ 'barbar' | replace_first:'bar','foo' }} #=> 'foobar'`
* `remove` - remove each occurrence *e.g.* `{{ 'foobarfoobar' | remove:'foo' }} #=> 'barbar'`
* `remove_first` - remove the first occurrence *e.g.* `{{ 'barbar' | remove_first:'bar' }} #=> 'bar'`
* `truncate` - truncate a string down to x characters
* `truncatewords` - truncate a string down to x words
* `prepend` - prepend a string *e.g.* `{{ 'bar' | prepend:'foo' }} #=> 'foobar'`
* `append` - append a string *e.g.* `{{ 'foo' | append:'bar' }} #=> 'foobar'`
* `minus` - subtraction *e.g.*  `{{ 4 | minus:2 }} #=> 2`
* `plus` - addition *e.g.*  `{{ '1' | plus:'1' }} #=> '11'`, `{{ 1 | plus:1 }} #=> 2`
* `times` - multiplication  *e.g* `{{ 5 | times:4 }} #=> 20`
* `divided_by` - division *e.g.* `{{ 10 | divided_by:2 }} #=> 5`
* `split` - split a string on a matching pattern *e.g.* `{{ "a~b" | split:~ }} #=> ['a','b']`
* `modulo` - remainder, *e.g.* `{{ 3 | modulo:2 }} #=> 1`

## Tags

Tags are used for the logic in your template. New tags are very easy to code,
so I hope to get many contributions to the standard tag library after releasing
this code.

Here is a list of currently supported tags:

* **assign** - Assigns some value to a variable
* **capture** - Block tag that captures text into a variable
* **case** - Block tag, its the standard case...when block
* **comment** - Block tag, comments out the text in the block
* **cycle** - Cycle is usually used within a loop to alternate between values, like colors or DOM classes.
* **for** - For loop
* **if** - Standard if/else block
* **include** - Includes another template; useful for partials
* **raw** - temporarily disable tag processing to avoid syntax conflicts.
* **unless** - Mirror of if statement

### Comments

Comment is the simplest tag.  It just swallows content.

{% highlight ruby %}
{% raw %}
We made 1 million dollars {% comment %} in losses {% endcomment %} this year
{% endraw %}
{% endhighlight %}

### Raw

Raw temporarily disables tag processing.
This is useful for generating content (eg, Mustache, Handlebars) which uses conflicting syntax.

<div class="highlight"><code class="ruby"><span class="nb">
&#123;&#37; raw %}<br>
&nbsp;&nbsp;In Handlebars, &#123;&#123; this }} will be HTML-escaped, but &#123;&#123;&#123; that }}} will not.<br>
&#123;&#37; endraw %}
</span></code>
</div>
<br>

### If / Else

`if / else` should be well-known from any other programming language.
Liquid allows you to write simple expressions in the `if` or `unless` (and
optionally, `elsif` and `else`) clause:

{% highlight ruby %}
{% raw %}
{% if user %}
  Hello {{ user.name }}
{% endif %}

{% if user.name == 'tobi' %}
  Hello tobi
{% elsif user.name == 'bob' %}
  Hello bob
{% endif %}

{% if user.name == 'tobi' or user.name == 'bob' %}
  Hello tobi or bob
{% endif %}

{% if user.name == 'bob' and user.age > 45 %}
  Hello old bob
{% endif %}

{% if user.name != 'tobi' %}
  Hello non-tobi
{% endif %}

# Same as above
{% unless user.name == 'tobi' %}
  Hello non-tobi
{% endunless %}

# Check if the user has a credit card
{% if user.creditcard != null %}
   poor sob
{% endif %}

# Same as above
{% if user.creditcard %}
   poor sob
{% endif %}

# Check for an empty array
{% if user.payments == empty %}
   you never paid !
{% endif %}

{% if user.age > 18 %}
   Login here
{% else %}
   Sorry, you are too young
{% endif %}

# array = 1,2,3
{% if array contains 2 %}
   array includes 2
{% endif %}

# string = 'hello world'
{% if string contains 'hello' %}
   string includes 'hello'
{% endif %}
{% endraw %}
{% endhighlight %}

### Case Statement

If you need more conditions, you can use the `case` statement:

{% highlight ruby %}
{% raw %}
{% case condition %}
{% when 1 %}
hit 1
{% when 2 or 3 %}
hit 2 or 3
{% else %}
... else ...
{% endcase %}
{% endraw %}
{% endhighlight %}

*Example:*

{% highlight ruby %}
{% raw %}
{% case template %}

{% when 'label' %}
     // {{ label.title }}
{% when 'product' %}
     // {{ product.vendor | link_to_vendor }} / {{ product.title }}
{% else %}
     // {{page_title}}
{% endcase %}
{% endraw %}
{% endhighlight %}

### Cycle

Often you have to alternate between different colors or similar tasks.  Liquid
has built-in support for such operations, using the `cycle` tag.

{% highlight ruby %}
{% raw %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}
{% cycle 'one', 'two', 'three' %}

will result in

one
two
three
one
{% endraw %}
{% endhighlight %}

If no name is supplied for the cycle group, then it's assumed that multiple
calls with the same parameters are one group.

If you want to have total control over cycle groups, you can optionally specify
the name of the group.  This can even be a variable.

{% highlight ruby %}
{% raw %}
{% cycle 'group 1': 'one', 'two', 'three' %}
{% cycle 'group 1': 'one', 'two', 'three' %}
{% cycle 'group 2': 'one', 'two', 'three' %}
{% cycle 'group 2': 'one', 'two', 'three' %}

will result in

one
two
one
two
{% endraw %}
{% endhighlight %}

### For loops

Liquid allows `for` loops over collections:

{% highlight ruby %}
{% raw %}
{% for item in array %}
  {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

During every `for` loop, the following helper variables are available for extra
styling needs:

{% highlight ruby %}
{% raw %}
forloop.length      # => length of the entire for loop
forloop.index       # => index of the current iteration
forloop.index0      # => index of the current iteration (zero based)
forloop.rindex      # => how many items are still left?
forloop.rindex0     # => how many items are still left? (zero based)
forloop.first       # => is this the first iteration?
forloop.last        # => is this the last iteration?
{% endraw %}
{% endhighlight %}

There are several attributes you can use to influence which items you receive in
your loop

`limit:int` lets you restrict how many items you get.
`offset:int` lets you start the collection with the nth item.

{% highlight ruby %}
{% raw %}
# array = [1,2,3,4,5,6]
{% for item in array limit:2 offset:2 %}
  {{ item }}
{% endfor %}
# results in 3,4
{% endraw %}
{% endhighlight %}

Reversing the loop

{% highlight ruby %}
{% raw %}
{% for item in collection reversed %} {{item}} {% endfor %}
{% endraw %}
{% endhighlight %}

Instead of looping over an existing collection, you can define a range of
numbers to loop through.  The range can be defined by both literal and variable
numbers:

{% highlight ruby %}
{% raw %}
# if item.quantity is 4...
{% for i in (1..item.quantity) %}
  {{ i }}
{% endfor %}
# results in 1,2,3,4
{% endraw %}
{% endhighlight %}

### Variable Assignment

You can store data in your own variables, to be used in output or other tags as
desired.  The simplest way to create a variable is with the `assign` tag, which
has a pretty straightforward syntax:

{% highlight ruby %}
{% raw %}
{% assign name = 'freestyle' %}

{% for t in collections.tags %}{% if t == name %}
  <p>Freestyle!</p>
{% endif %}{% endfor %}
{% endraw %}
{% endhighlight %}

Another way of doing this would be to assign `true / false` values to the
variable:

{% highlight ruby %}
{% raw %}
{% assign freestyle = false %}

{% for t in collections.tags %}{% if t == 'freestyle' %}
  {% assign freestyle = true %}
{% endif %}{% endfor %}

{% if freestyle %}
  <p>Freestyle!</p>
{% endif %}
{% endraw %}
{% endhighlight %}

If you want to combine a number of strings into a single string and save it to
a variable, you can do that with the `capture` tag. This tag is a block which
"captures" whatever is rendered inside it, then assigns the captured value to
the given variable instead of rendering it to the screen.

{% highlight ruby %}
{% raw %}
  {% capture attribute_name %}{{ item.title | handleize }}-{{ i }}-color{% endcapture %}

  <label for="{{ attribute_name }}">Color:</label>
  <select name="attributes[{{ attribute_name }}]" id="{{ attribute_name }}">
    <option value="red">Red</option>
    <option value="green">Green</option>
    <option value="blue">Blue</option>
  </select>
{% endraw %}
{% endhighlight %}
