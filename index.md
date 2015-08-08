---
layout: page
title: Galaxy's World
tagline: 银河雪尘
---
{% include JB/setup %}

## Welcome

This is Galaxy's blog.

Since the contents mean more than the cover, thus no time spent on this cover.

## Sub Sites

* [My Doctuments](/galaxy-doc/)

## Recent Posts
<ul class="posts">
  {% for post in site.posts limit:12 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a> <em>Posted on {{ post.date | date_to_long_string }}.</em></li>
  {% endfor %}
</ul>
<a href="archive.html"><span class="grey">...SEE ALL</span></a>

## Markdown 

* Markdown 语法 (简体中文版)

[本地镜像](/etc/Markdown-Syntax-CN/)  
`git subtree add --prefix=etc/Markdown-Syntax-CN https://gitcafe.com/riku/Markdown-Syntax-CN.git master`

[繁体中文版 Markdown 語法說明中文版](https://github.com/othree/markdown-syntax-zhtw/blob/master/syntax.md)

[英文原版](http://daringfireball.net/projects/markdown/syntax), 及其[源代码](http://daringfireball.net/projects/markdown/syntax.text)

* GitHub 官方Markdown指南 [Mastering Markdown](https://guides.github.com/features/mastering-markdown/#examples)

https://guides.github.com/features/mastering-markdown/#GitHub-flavored-markdown



## Old programming tips

Read [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

Complete usage and documentation available at: [Jekyll Bootstrap](http://jekyllbootstrap.com)

### Writing instructions

1. `rake post title="English title used for slug" tags="Tags, divided by, Comma"`
2. Edit prompted file and set `title` to proper *Chinese* ones for ***real display***.
3. `git add ./_posts/2013-05-03-that-post.md` or `rm` it to cancel.

### Tips

* `![](/assets/images/2015/1ofPlaned.jpg)`
* `<font color="navy">注:</font>`

### Update Author Attributes

In `_config.yml` remember to specify your own data:
    
    title : My Blog =)
    
    author :
      name : Name Lastname
      email : blah@email.test
      github : username
      twitter : username

The theme should reference these variables whenever needed.
    
### Sample Posts

This blog contains sample posts which help stage pages and blog data.
When you don't need the samples anymore just delete the `_posts/core-samples` folder.

    $ rm -rf _posts/core-samples

Here's a sample "posts list".

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

### To-Do

This theme is still unfinished. If you'd like to be added as a contributor, [please fork](http://github.com/plusjade/jekyll-bootstrap)!
We need to clean up the themes, make theme usage guides with theme-specific markup examples.
