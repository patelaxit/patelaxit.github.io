---
layout: post
title: Setting up MathJax with Jekyll
date: 2015-08-24
summary: A tutorial on using MathJax with Jekyll and basic usage of MathJax.
---

### Why MathJax?
Since most of the posts in this blog will talk about electrical engineering concepts, it'd be wrong to introduce or discuss these topics without any kind of mathematical rigor. This means however, that the equations in the blog posts need to be easily readable and [MathJax](www.mathjax.org) is perfect for this. According to its homepage, MathJax is *a Javascript display engine for mathematics that works in all the browsers*.

### How to set it up?
It is really easy to set up MathJax with Jekyll. Note that I installed MathJax with the Pixyll theme pre-installed, but the installation process is the same regardless of the theme.

The first thing to do is to make sure that the Ruby library that parses the Markdown in our posts is updated in the `_config.yml` file. The Markdown processor should be updated to `kramdown`. This is what the line would look like in `_config.yml`:

{% highlight Ruby%}
# Build settings
markdown:     kramdown
{% endhighlight %}

Now that we have changed the Markdown parser, we need to include the HTML script tag that will include MathJax in all of our posts. We need to put the script tag in the layout file that gets used when rendering all of our posts. Conveniently this happens to be `post.html` in the `_layouts` folder of your jekyll site. Open up `_layouts/post.html` and include the following code in the beginning of the file:

{% highlight html %}
<script type="text/javascript" 
        src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
{% endhighlight %}

That is all you need to do! Now you should be able to render LaTeX-like equations in your blog posts on all browsers.

### Basic Usage
I'll be assuming that the reader has a little familiarity with LaTeX and its syntax. Although most of LaTeX syntax is valid for MathJax, there are some cases where they don't behave in the same manner.

There are two ways to display mathematical equations using MathJax: `inline` or `block`. As the name suggests, inline mode allows us to render the mathematical expressions inline with regular text like this: \\( x^2 + y^2 = 0 \\). To render our text inline, we need to use `\\( ... \\)` as delimeters in our markdown. Note that the default syntax for the delimeters according the MathJax docs is `\( ... \(`, but since Jekyll uses markdown, we have to escape `\` by using another `\`.

For example, in order to render the expression \\( i = \sqrt{-1} \\), your markdown would look as follows:

{% highlight tex %}
\\( i = \sqrt{-1} \\)
{% endhighlight %}

Note that `$ ... $` is also a valid delimeter for inline rending mode. It is however disabled by default due to the fact that `$` is used quite often even in non-mathematical contexts. You can enable it by following the instructions [here](http://docs.mathjax.org/en/latest/start.html).

The delimeters to render our equations in block mode are `$$ ... $$` and `\\[ \\]`. The double dollar signs are used much more frequently because they aren't that common besides in LaTeX code. An example of using this mode is presented below.

{% highlight latex %}
% This is a comment
% Equation of a circle

$$ \frac{x^2}{R} + \frac{y^2}{R} = 0 \\
x^2 + y^2 = R $$
{% endhighlight %}

$$
% This is a comment
% Equation of a circle

\frac{x^2}{R} + \frac{y^2}{R} = 0 \\
x^2 + y^2 = R
$$


Well that is all for today! I hope this blog post was helpful to those setting up their blogs to use MathJax.