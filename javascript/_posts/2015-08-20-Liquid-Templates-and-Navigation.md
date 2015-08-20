---
layout: post
title:  Jekyll Blog and Navigation Highlight
date:   2015-08-20 10:17:00
categories: javascript
comments: true
---

I recently started playing with the navigation and styling of the navigation for this blog. I faced a few problems that I wanted to solve. For one, the order of my navigation bar was not quite right. The 'About' section link in the navigation sat in the middle of the other categories, and I wanted the 'About' section to come last in the navigation. Another problem that I faced was that my navigation bar didn't do a good job of telling users which section of the blog they were reading. Many sites make use of colored tabs or breadcrumbs so that users can quickly determine where they are within a site. Here are some examples of those.

<div style="margin: 0 auto; text-align: center">
<h4><strong>Tabs</strong></h4>
  <img src="http://usabilitygeek.com/wp-content/uploads/2011/11/14-Guidelines-For-Website-Tabs-Usability-Active-Inactive-Tabs.jpg">
</div>

<br>
<br>
<div style="margin: 0 auto; text-align: center">
<h4><strong>Breadcrumbs</strong></h4>
  <img src="http://www.smashingmagazine.com/images/breadcrumbs-design-showcase/location_based_breadcrumb_example_sitepoint.jpg">
</div>

<br>
<br>

To solve the two problems, I reworked the header.html file which is one of the `_includes` in my Jekyll blog. Jekyll creates pages by combining smaller HTML files in one of its `_layouts`. Here's what the file structure looks like.

<div style="margin: 0 auto; text-align: center">
  <img src="../assets/javascript/blogFiles.png">
</div>
<br>
<br>

And here's the original code for the `default.html` layout on my blog.

{% highlight html linenos %}
<html>
{% raw %}
  {% include head.html %}
{% endraw %}
  <body>
  {% raw %}
    {% include header.html %}
  {% endraw %}
    <div class="page-content">
      <div class="wrapper">
        {{ content }}
      </div>
    </div>
  {% raw %}
    {% include comments.html %}

    {% include footer.html %}

    {% include analytics.html %}
  {% endraw %}
  </body>
</html>
{% endhighlight %}

The html from all the `include` files is pulled into any page that is created with this default layout. In particular, notice how html files are listed between curled braces. This syntax is for Liquid Templates. [Liquid](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers) is a type of markup language that allows for tag markup and output markup. Output markup is used to render text on the webpage, while tag markup, which cannot resolve to text, is used for logic. While writing this blog post, Liquid replaced the `head.html` (and all the other `includes`) with the actual html files so I needed to surround the liquid output markup with `{{ "{% raw " }}%}` and `{{ "{% endraw " }}%}` so you can read the actual file as is rather than the rendered one.

To change the navigation, I needed to make some changes in the `header.html`, which comes pre-written with Jekyll. Here's the code in the `header.html` file.

{% highlight html linenos %}
<div class="trigger">
  {% raw %}
  {% for page in site.pages %}

    {% if page.title %}

      <a class="page-link" href="{{ page.url | prepend:site.baseurl }}">{{ page.title }}</a>

    {% endif %}

  {% endfor %}
  {% endraw %}
</div>
{% endhighlight %}
<br>

The variable `site.pages` is available for Jekyll blogs, and it's how you can create different pages or sections of the blog. I rewrote this file to include the navigation links that I wanted in the order of that I wanted. I also added a `page.url` variable inside of a Liquid tag so that I could set an `active` class on each link when a user navigated to a particular page.

{% highlight html linenos %}
<ul class="nav-list">
  <li {% raw %}{% if page.url == '/javascript/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/javascript/">Javascript</a></li>
  <li {% raw %}{% if page.url == '/datavis/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/datavis/">DataVis</a></li>
  <li {% raw %}{% if page.url == '/hackreactor/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/hackreactor/">HackReactor</a></li>
  <li {% raw %}{% if page.url == '/about/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/about/">About</a></li>
</ul>
{% endhighlight %}

If you're looking for more useful tips on navigation and usability, check out Usability Geek's [quick tips for tab usability](http://usabilitygeek.com/14-guidelines-for-web-site-tabs-usability/).
