---
layout: post
title:  Adding tags for Navigation
date:   2022-07-29 01:10:00 -0400
tags: navigation jekyll
---

Let's add some navigation.
I've found two ways to add navigation to your side.

One way to do this is to simply add additional pages, then add a navigation menu and hardcode everything. While this probably works I just hate hard-coded stuff and don't think anyone should waste time and effort with keeping code alive if there is not a really good reason to do so.

Lucky for us Jekyll offers another way to do navigation with its "built-in plugin" called jekyll-archives.
Unlucky for us GitHub pages does not support jekyll-archives..

But [this guy here](http://codinfox.github.io/dev/2015/03/06/use-tags-and-categories-in-your-jekyll-based-github-pages/) (Big time Kudos!) found a pretty cool solution which I used as a base and customized a little bit..(due to my complete lack of html skills it took me a couple of days but if I can do it, you can too!)

Actually, I had to invest quite some work because I didn't just want a list with all posts, but **I wanted my list to actually filter** when I click a tag!

> **Important note:** Jekyll is **static** and gets executed when the page is loaded. To get the interaction we need to add some **Javascript** and filter out the posts we don't want to see upon a click.

## Solution

Most of the changes will be in your home.html

Go to your folder _layouts and open your home.html.
This is what we will change first - if you want you can copy it for your references so you can always go back (without going through your version control).

# Step 1: create a list of tags

First you add these two parts to extract all the tags, sort them and remove duplicated ones.

**[insert picture]**



{% highlight ruby %}

%- assign rawtags = "" -%
%- for post in site.posts -%
	%- assign ttags = post.tags | join:'|' | append:'|' -%
	%- assign rawtags = rawtags | append:ttags -%
%- endfor -%
%- assign rawtags = rawtags | split:'|' | sort -%

%- assign tags = "" -%
%- for tag in rawtags -%
	%- if tag != "" -%
		%- if tags == "" -%
			%- assign tags = tag | split:'|' -%
		%- endif -%
		%- unless tags contains tag -%
			%- assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' -%
		%- endunless -%
	%- endif -%
%- endfor -%

{% endhighlight %}

# Step 2: add the tags to the site

Then we will add the list of tags (lin 80)

**[insert picture]**

# Step 3: create the base function

Then we will some javascript with a function - first we just want to see what we actually clicked. so add line 115 and also add this:

```
<h1 class="page-heading">Posts<span id="tagID"></span></h1>
```

test it and see how it changes based on what you click. your url changes too, this is just for cosmetic reasons though.

**[insert picture]**

# Step 4: add the logic to the function

now you can add the rest of the function:

**[insert picture]**

> remember: the whole page is rendered already so we actually just need to hide some unwanted elements

# Step 5: add a class to your CSS 

to make it work you have to go to your sass folder and add a class named **hidden** to it.

basically the function now adds this class to all elements that have the specific class post-elements

add a new segment at the top for *Custom* (or just add it to whatever area you like)

```
/**
 * Custom
 */
```


# Step 6: add the new class to your elements

now we add this class to the post-elements *(I don't think you need joinedtags)*

```

<li class="post-elements joinedtags joinedcats">

```

now it should work

# Step 7: add the tags to each post in the landing page

Last thing is to add the tags to each post in the landing page

we leave the assing stuff and just check if a post has a tag, then put in a new span element, sort, join and prepend a #

{% highlight ruby %}
      
      %- comment -%
          %- if post.tags -%
          <span class="post-meta">| post.tags |sort | join:" #" | prepend: "#"</span>
          %- endif -%
      %- endcomment -%

{% endhighlight %}

# Step 7: add a removal tag #all

ich habe noch ein tag am anfang das mir alles wieder auf null setzt.


# Step 8: add the tags to each post site

if you click a post I want to have the tags of this post there as well..

the process is similar to the steps 1-7

go to *_layouts*/post.html

basically we just want to add the following code into the post-meta part

also, we will change the bullet point to a | because I think it looks cooler!
to do so just change line 14 and replace the bullet with a |
also make sure to add a space after before the last </span>
{{ page.author }} </span></span>




we will use the following code (we add the if clause in case there is no tags)

```
      %- if page.tags -%
      <span class="post-meta"> page.tags | sort | join:" #" | prepend:"| #"</span>
      %- endif -%
```

## References

[Here](https://stackoverflow.com/questions/4825295/onclick-to-get-the-id-of-the-clicked-button) I learned how to get the ID from a clicked tag so you can filter down the posts.

The display property stuff comes form [here](https://bobbyhadz.com/blog/javascript-hide-element-by-class#:~:text=To%20hide%20an%20element%20by%20a%20class%3A%20Use,to%20get%20the%20element%20you%20want%20to%20hide.)


# More References for Jekyll archives

[This guy](https://aneejian.com/automated-jekyll-archives-github-pages/) shows a way to deploy the archives plugin on GitHub pages. This could actually work but I think it is way to much effort and a lot harder to implement than my solution.



You can check out how to work with Jekyll archives in general [here](https://github.com/jekyll/jekyll-archives) and [here](https://learn.cloudcannon.com/jekyll/jekyll-archives/) if you want to deploy it to your own webserver.


