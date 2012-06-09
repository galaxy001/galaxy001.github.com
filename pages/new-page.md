---
layout: page
date: 'Sat 2012-06-09 18:26:11 +0800'
slug: 'New-Page'
title: "Test Page"
description: ""
---
{% include JB/setup %}

Just for test ...

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
