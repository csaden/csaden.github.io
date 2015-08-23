---
layout: post
title:  Jekyll Blog and Navigation Styling
date:   2015-08-20 10:17:00
categories: javascript
comments: true
---

This post technically isn't about JavaScript. Instead, this post centers on HTML, Liquid markup, and debugging. I've been playing with my blog's navigation and the navigation's styling over this week, and I faced a few problems that I wanted to solve.

For one, the order of my navigation bar was not quite right. The 'About' section link in the navigation sat in the middle of the other categories, and I wanted the 'About' section to come last in the navigation. Another problem that I faced was that my navigation bar didn't do a good job of telling users which section of the blog they were reading. I wanted to have a highlight on the navigation that gave users an idea of where they were located in the site. Many sites make use of colored tabs or breadcrumbs so that users can quickly determine where they are within a site. Breadcrumbs are especially helpful in complex hierarchical sites like Amazon.com or Walmart.com. Here some examples of those.

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

To solve the two problems, I reworked the header.html file which is one of the `_includes` in my Jekyll blog. Jekyll creates pages by combining smaller HTML files in one of the predefined `_layouts`. You can also build your own layouts. Here's what my current file structure looks like.

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

The html from all the `include` statements is pulled into any web page that is created with this default layout. Notice how the html files are listed between curled braces. This syntax is for Liquid templates. [Liquid](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers) is a type of markup language that allows for tag markup and output markup. Output markup is used to render text on the web page, while tag markup, which cannot resolve to text, is used for logic. While writing this blog post, Liquid replaced the `head.html` (and all the other `includes`) with the actual html files so I needed to surround the liquid output markup with `{{ "{% raw " }}%}` and `{{ "{% endraw " }}%}` so you can read the actual file as it is rather than the rendered one.

To change my blog's navigation, I needed to make some changes in the `header.html`, which comes pre-written with Jekyll. Here's that original code in the `header.html` file.

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

The variable `site.pages` is available for Jekyll blogs, and it's how you can create different pages or sections of the blog. I rewrote this file to include the navigation links in the order that I wanted. Problem one solved!

I also added a `page.url` variable inside of a Liquid tag so that I could set an `active` class on each link when a user navigates to a particular page. Essentially when a user clicks on one of the links in the nav, the user is taken to a "page" or section of the blog. Each page has it's own url, such as `/javascript/` or `/datavis/`. This allows me to set an active class, which styles the link element that was just clicked.

{% highlight html linenos %}
<ul class="nav-list">
  <li {% raw %}{% if page.url == '/javascript/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/javascript/">Javascript</a></li>
  <li {% raw %}{% if page.url == '/datavis/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/datavis/">DataVis</a></li>
  <li {% raw %}{% if page.url == '/hackreactor/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/hackreactor/">HackReactor</a></li>
  <li {% raw %}{% if page.url == '/about/' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/about/">About</a></li>
</ul>
{% endhighlight %}

There was still one more problem. I could not get the nav bar to retain it's active styling when clicking on posts within each section of the blog.

The home page looked fine. No clicks yet, so no styling change.

<img src="../assets/javascript/nav1.png">

<br>
<hr>
<br>

The pages worked great. After clicking on the Data Vis tab, I saw this.

<img src="../assets/javascript/nav2.png">

<br>
<hr>
<br>

But when clicking on a post within Data Vis, I saw this...

<img src="../assets/javascript/nav3.png">

<br>
<hr>
<br>

I thought about the problem and then realized that I was trying to match the `page.url` rather than one part of the url that corresponds to the page (or section of the blog) for <em>any</em> web page on my site. I needed to take the entire url, split it on the forward slash, get the page.url (datavis, javascript, etc.), and then check to see if it matched one of the links. Here's that code.

{% highlight html linenos %}
  {% raw %}
  {% assign url_parts = page.url | split: '/' %}
  {% endraw %}
  <ul class="nav-list">
    <li {% raw %}{% if url_parts[1] == 'javascript' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/javascript/">Javascript</a></li>
    <li {% raw %}{% if url_parts[1] == 'datavis' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/datavis/">DataVis</a></li>
    <li {% raw %}{% if url_parts[1] == 'hackreactor' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/hackreactor/">HackReactor</a></li>
    <li {% raw %}{% if url_parts[1] == 'about' %}{% endraw %}class="active" {% raw %}{% endif %}{% endraw %}><a class='page-link' href="/about/">About</a></li>
  </ul>
{% endhighlight %}

Notice the first liquid tag. It creates a variable called url_parts by splitting the current page's url (everything after the base url at the forward slash). Liquid has some helpful manipulation and filter functions and one of this is `split`. Another function that does filtering is `first`. The `first` filter does what you might have guessed. It grabs the first element in an array. The first filter, however, would not work in this scenario, because it returns an empty string. The urls are of the form `/page/postTitle` so the split function creates an empty string because of the first forward slash.

Problem two solved!

<img src="../assets/javascript/nav4.png">

<br>
<hr>
<br>

That's all for now. If you're looking for more useful tips on navigation and usability, check out Usability Geek's [quick tips for tab usability](http://usabilitygeek.com/14-guidelines-for-web-site-tabs-usability/).
