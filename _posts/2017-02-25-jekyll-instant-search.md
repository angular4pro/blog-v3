---
title: Jekyll Instant Search in 3 simple steps!
desc: Adding an instant search to jekyll website can be easily achieved with this method. Instant Jekyll search also gives a feel that the website is live and is using a database even though it isn't. Also, we are not using JQuery here!
author: sharathdt
tags: Jekyll Plugins
image: jekyll-search-instant.png
img-src: "http://www.freepik.com/free-vector/businessman-with-spyglass_761446.htm"
img-src-name: Designed by Freepik
layout: post
permalink: /instant-jekyll-search/
---

Finding specific content can be hard if a website doesn't have a search option. I had no search option before because I had very few articles and pages. Eventually, when the number of posts grew, it became hard for me to search even a small paragraph in some article that I know I have written.

* Do not remove this line (it will not be displayed) 
{:toc}


Currently, I'm using google custom search engine which does a pretty good job but it doesn't fetch posts while I'm typing like how the actual google.com does. 
~~I might change this in the future but for now I'm keeping it.~~ 
I changed it in the new layout.

If you're looking for Custom Search Engine by Google then please visit: [The easiest search option for Jekyll](https://blog.webjeda.com/jekyll-search/){: target="_blank"}

## Why a Jekyll blog needs search option?
If your Jekyll site has just 4 to 5 pages, then you will not need a search option. All those pages can be listed, linked in a menu bar or shown on the footer.

A Jekyll blog with lots of articles needs a search bar. There are plenty of options available to implement search in Jekyll. 

 **1 .Lunr**
 
 **2 .Google Custom Search Engine**
 
 **3 .Simple Jekyll Search**

Lunr is instant but heavy. Google Custom Search Engine is light but not instant(yet). Simple Jekyll Search is light as well as instant.
{: .y}

Let's implement it in a Jekyll site. Simple Jekyll Search is developed by [christian-fei](https://github.com/christian-fei){: target="_blank"}. So far it is the easiest instant search available for Jekyll. Credit also goes to [Alex Pearce](https://github.com/alexpearce) who posted [his idea](https://alexpearce.me/2012/04/simple-jekyll-searching/){: target="_blank"}{: rel="nofollow"} on how it can be achieved.


Here is a simple demo where Jekyll Simple Search finds keywords in 5 recent posts.

<!-- Html Elements for Search -->
<div id="search-container">
<input type="text" id="search-input" placeholder="How, Jekyll, Liquid...">
<ul id="results-container"></ul>
</div>




## How to implement Jekyll Instant Search?

Since Jekyll has no server side execution, we have to rely on storing all the required content in a single file and search our keyword from that file.

We will be creating a JSON file in which we will store page title, page link, category, tags, description(if needed) etc., JSON(JavaScript Object Notation) is a human readable way to store data in key-value pairs(it can take other forms as well).

For example:

{% highlight js %}
[
    {
     "Name": "Webjeda"
    }
]
{% endhighlight %}


### Step 1 - Create a JSON file

Create a file in the root of your Jekyll blog and name it ``search.json``. Now, copy the below code in it and save.


{% highlight liquid %}{% raw %}

---
---
[
  {% for post in site.posts %}
    {
    
      "title"    : "{{ post.title | escape }}",
      "url"      : "{{ site.baseurl }}{{ post.url }}",
      "category" : "{{ post.category }}",
      "tags"     : "{{ post.tags | join: ', ' }}",
      "date"     : "{{ post.date }}"
      
    } {% unless forloop.last %},{% endunless %}
  {% endfor %}
]

{% endraw %}{% endhighlight %}

What it does is that it converts your Jekyll data from all the posts and puts it as key value pair which can then be easily read by a search script.

If you are trying it out on a local machine then you can verify ``search.json`` inside ``_site`` folder to see whether all the values are generated or not.

The output would look somewhat like this,

<pre><code>
        [
  
            {
              "title"    : "Materialized",
              "url"      : "/materialized/",
              "category" : "cards",
              "image"    : "materialized.png",
              "dev"      : "lpsandaruwan"
            } 
            ,

            {
              "title"    : "Time-machine",
              "url"      : "/time-machine/",
              "category" : "onepage",
              "image"    : "time-machine.png",
              "dev"      : "pages-themes"
            } 
        ]
</code></pre>

This is a sample from a website of mine where I have implemented the search option.

Visit: [Jekyll Themes](https://jekyll-themes.com){: target="_blank"}

{% include adsense-inside-post.html %}

The above code can be changed (be careful not to mess it up) according to your needs. Remove whatever field is not required for your Jekyll search. Add if you want to include some other front matter or the content of posts say **description**, **content** or multiple categories as shown below.



{% highlight liquid %}{% raw %}

---
---
[
  {% for post in site.posts %}
    {
    
      "title"    : "{{ post.title | strip_html | escape }}",
      "url"      : "{{ site.baseurl }}{{ post.url }}",
      "category" : "{{post.categories | join: ', '}}",
      "tags"     : "{{ post.tags | join: ', ' }}",
      "date"     : "{{ post.date }}",
      "discription" : "{{post.description | strip_html | strip_newlines | escape }}"
      
    } {% unless forloop.last %},{% endunless %}
  {% endfor %}
]

{% endraw %}{% endhighlight %}

The ``escape`` filter is important because, if you have a double inverted comma inside the value say ``post.description`` then the whole JSON breaks and becomes unusable. I also recommend not to use whole content to create JSON because it might result in creating a huge file.

You can also add ``post.content`` to this. But I recommend not to. Adding content will result in a huge JSON file and also inaccurate search result.


Make sure that the last value has no comma at the end.
{: .r}

From what I have seen, the value you place at the top will be given priority. In the above example, title will be given the highest priority and excerpt gets the lowest. Change this as per your requirements.

### Step 2 - Save the search script
Save the search script available [here](https://raw.githubusercontent.com/christian-fei/Simple-Jekyll-Search/master/dest/simple-jekyll-search.min.js){: target="_blank"} and save it as ``search-script.js`` (or any name that you prefer).

It is better to create a folder named ``js`` in the root and keep this file inside it just to avoid any confusions.
{: .g}

### Step 3 - Create a Jekyll search page

Create a page with the name ``search.md`` or ``search.html`` and add the following in it.

{% highlight html %}{% raw %}

<!-- Html Elements for Search -->
<div id="search-container">
<input type="text" id="search-input" placeholder="search...">
<ul id="results-container"></ul>
</div>

<!-- Script pointing to search-script.js -->
<script src="/path/to/search-script.js" type="text/javascript"></script>

<!-- Configuration -->
<script>
SimpleJekyllSearch({
  searchInput: document.getElementById('search-input'),
  resultsContainer: document.getElementById('results-container'),
  json: '/search.json'
})
</script>

{% endraw %}{% endhighlight %}

This step isn't necessary. You can add the below code to your default layout or homepage. Why I avoid adding search on all pages is because, the search option is not used by all users all the time. There is no reason to call the search script(which is quite big) on all the pages. This may affect your page load time.

{% include adsense-inside-post-2.html %}

Give extra attention to the path for the script file and the JSON file. If any one of them is wrong then you will not get any output.

This page should be accessible at ``/search/`` or ``/search.html``.


I don't recommend using this on default layout (which is used on every page) because it may result in slower page load. Use a separate search page instead.

Now your search is ready! Try to type something in the input field and see if it fetches any result.

If the search doesn't work then use inspection >> console option on chrome browser to see what the error was. Many times the JSON created will be invalid because of some special character. Also, the order in which the search script can also cause issues.

### Customizations

The default Jekyll search result will be in this format,

{% highlight html %}{% raw %}
<li><a href="{url}">{title}</a></li>
{% endraw %}{% endhighlight %}

You can change this in the configuration script by adding this line,

{% highlight html %}{% raw %}
searchResultTemplate: '<div><a href="{url}"><h1>{title}</h1></a><span>{date}</span></div>',
{% endraw %}{% endhighlight %}

Here ``{url}``, ``{title}``, ``{date}`` are the respective data found in JSON file.

You can also show a message when no result is found by adding this line to the configuration script.

{% highlight html %}{% raw %}
noResultsText ("No result found!") 
{% endraw %}{% endhighlight %}

Remember that all these values are comma seaprated.
{: .g}

There are many other configurations that can be tweaked. Please visit this [repository](https://github.com/christian-fei/Simple-Jekyll-Search){: target="_blank"} to know more.


## Conclusion
There are many things that may go wrong while implementing Jekyll Simple Search and may result in getting no output. Trust me I have been there. Don't give up, follow every step without miss. Use Google Chrome Inspect tool >> console to see what went wrong. 

Instant search will definitely help your viewers to find what they're looking for, easier and faster. This factor will indirectly help to decrease your website bounce rate.

Let me know whether you were able to successfully implement Jekyll Instant Search. Ask any questions or doubts in the comment section.


<style>
input[type=text] {

    outline: none;
    padding: 15px 25px;
    margin: 5px 1px 3px 0px;
    border: none;
    width: 100%;
    border-radius: 1px;
    box-shadow: 0 1px 0px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);

}
    
input[type=text]:hover {
    outline: none;
    border: none;
    margin: 5px 1px 3px 0px;
    padding: 15px 25px;
    -webkit-transition: all 0.30s ease-in-out;
    -moz-transition: all 0.30s ease-in-out;
    -ms-transition: all 0.30s ease-in-out;
    -o-transition: all 0.30s ease-in-out;
     box-shadow: 0 2px 2px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);
}
    
input[type=text]:focus {
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);
    margin: 5px 1px 3px 0px;
    padding: 15px 25px;
    border: none;
    outline: none;
        -webkit-transition: all 0.30s ease-in-out;
    -moz-transition: all 0.30s ease-in-out;
    -ms-transition: all 0.30s ease-in-out;
    -o-transition: all 0.30s ease-in-out;
}

@media screen and (max-width: 600px) {
    input[type=text]{
            width: 100%;
            box-sizing: border-box;
    } 
    }
</style>
<!-- Script pointing to jekyll-search.js -->
<script src="/demo/search-script.min.js" type="text/javascript"></script>
<script>
SimpleJekyllSearch({
  searchInput: document.getElementById('search-input'),
  resultsContainer: document.getElementById('results-container'),
  json: '/demo/search.json',
})
</script>