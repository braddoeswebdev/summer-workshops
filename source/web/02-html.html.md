---
series: 'web'
number: 2
title: "HTML Basics"
icon: 'code'
desc: "Learn the basic structure of HTML"
---
# HTML Basics

Hypertext Markup Language (HTML) is the code that you use to structure your web content, and give it meaning and purpose. For example, your content could contain a set of paragraphs, or a list of bullet points. Or it could even have images or data tables.

## So what is HTML, really?

HTML is not really a programming language; it is a markup language, used to give the content you want to put on your websites structure and meaning. It consists of a series of elements, which you wrap around different parts of your content to give it specific jobs, or roles. For example, take the following line of content:

~~~~ html
My cat is very grumpy
~~~~

If we wanted to officially specify that this is a paragraph, we could wrap it in a paragraph (<p>) element:

~~~~ html
<p>My cat is very grumpy</p>
~~~~

## Anatomy of an HTML element

Let's explore this paragraph element a bit further.

![Illustration of HTML tag components](/img/grumpy-cat-small.png)

The main parts of our element are:

- The opening tag: This consists of the name of the element (in this case, p), wrapped in opening and closing angle brackets. This states where the element begins, or starts to take effect — in this case where the start of the paragraph is.
- The closing tag: This is the same as the opening tag, except that it includes a forward slash before the element name. This states where the element ends — in this case where the end of the paragraph is.
- The content: This is the content of the element, which in this case is just text.
- The element: The opening tag, plus the closing tag, plus the content, equals the element.

Elements can also have attributes, which look like this:

![Illustration of HTML tag attributes](/img/grumpy-cat-attribute-small.png)

Attributes contain extra information about the element, which you don't want to appear in the actual content. In this case, the class attribute allows you to give the element an identifying name that can be later used to target the element with style information and other things.

An attribute should always have:

- A space between it and the element name (or the previous attribute, if the element already has one or more attributes.)
- The attribute name, followed by an equals sign
- Opening and closing quote marks wrapped around the attribute value

## Nesting elements

You can put elements inside other elements too — this is called nesting. If we wanted to state that our cat is VERY grumpy, we could wrap the word "very" in a `<strong>` element, which means that the word is to be strongly emphasized:

~~~~ html
<p>My cat is <strong>very</strong> grumpy.</p>
~~~~

You do however need to make sure that your elements are properly nested: in the example above we opened the `<p>` element first, then the `strong`, therefore we have to close the `strong` element first, then the `p`. This is wrong:

~~~~ html
<p>My cat is <strong>very grumpy.</p></strong>
~~~~

The elements have to open and close neatly so they are clearly inside or outside one another. If they overlap like this, then your web browser will try to make a best guess at what you were trying to say, but you may well get unexpected results. So don't do it!

## Empty elements

Some elements have no content, and are called empty elements. Take the `<img>` element we already have in our HTML:

~~~~ html
<img src="img/firefox-icon.png" alt="My test image">
~~~~

This contains two attributes, but there is no closing `</img>` tag, and no inner content. This is because an image element doesn't wrap content to have an effect on it. Its purpose is to embed an image in the HTML page, in the place it appears.

## Anatomy of an HTML document

That wraps up the basics of individual HTML elements, but they aren't very useful on their own. Now we'll look at how individual elements are combined to form an entire HTML page. Let's revisit the code we put into our `index.html` example (which we first met in the Dealing with files article):

~~~~ html
<!DOCTYPE html>
<html>
  <head>
    <title>My test page</title>
  </head>
  <body>
    <img src="img/firefox-icon.png" alt="My test image">
  </body>
</html>
~~~~

Here we have:

- `<!DOCTYPE html>` — the doctype. In the mists of time, when HTML was young (about 1991/2), doctypes were meant to act as links to a set of rules that the HTML page had to follow to be considered good HTML, which could mean automatic error checking and other such useful things. However, these days no-one really cares about them, and they are really just a historical artifact that needs to be included for everything to work right. For now, that's all you need to know.
- `<html></html>` — the `<html>` element. This element wraps all the content on the entire page, and is sometimes known as the root element.
- `<head></head>` — the `<head>` element. This element acts as a container for all the stuff you want to include on the HTML page that isn't the content you are showing to your page's viewers. This includes things like keywords and a page description that you want to appear in search results, CSS to style our content, characterset declarations, and more.
- `<title></title>` — this sets the title of your page, which is the title that appears in the browser tab the page is loaded in, and is used to describe the page when you bookmark/favourite it.
- `<body></body>` — the `<body>` element. This contains all the content that you want to show to web users when they visit your page, whether that's text, images, videos, games, playable audio tracks, or whatever else.


## Images

Let's turn our attention to our image element again:

~~~~ html
<img src="img/firefox-icon.png" alt="My test image">
~~~~

As we said before, it embeds an image into our page in the position it appears. It does this via the `src` (source) attribute, which contains the path to our image file.

But we have also included an `alt` (alternative) attribute — this contains some text that should describe the image, which can be accessed by users that cannot see the image, perhaps because:

- They are blind or partially sighted. Users with significant visual impairments often use tools called Screen Readers to read out the alt text to them.
- Something has gone wrong in the code that means the image can't be displayed. For example, try deliberately changing the path inside your `src` attribute to make it incorrect. If you save and reload the page, you should see the alt text instead of your image.

The key phrase about alt text included above is "text that should describe the image". The alt text you write should give the reader enough to have a good idea of what the image shows, from reading it. So our current text of "My test image" is no good at all. A much better text for our Firefox logo would be "The Firefox logo: a flaming fox surrounding the Earth."

Try coming up with some better alt text for your image now.

## Marking up text

This section will cover some of the basic HTML elements you'll use for marking up text.

### Headings

Heading elements allow you to specify that certain parts of your content are headings, or subheadings of your content. In the same way that a book has a main title, and then can have titles for each individual chapter, and subtitles within those too, an HTML document can too. HTML contains six heading levels, `<h1>`-`<h6>` although you'll probably only use 3–4 at the most:

~~~~ html
<h1>My main title</h1>
<h2>My top level heading</h2>
<h3>My subheading</h3>
<h4>My sub-subheading</h4>
~~~~

Have a go now, at adding a suitable title to your HTML page, just above your `<img>` element.

### Paragraphs

As explained above, `<p>` elements are for containing paragraphs of text; you'll use these a lot when marking up regular text content:

~~~~ html
<p>This is a single paragraph</p>
~~~~

Add your sample text (you should still have it from the first section) into one or a few paragraphs, placed directly below your `<img>` element.

### Lists

A lot of the Web's content is lists, so HTML has special elements for these. Marking up lists always consist of at least two elements. The most common list types are ordered and unordered lists:

- Unordered lists are for lists where the order of the items doesn't matter, like a shopping list. These are wrapped in a `<ul>` element.
- Ordered lists are for lists where the order of the items does matter, like a recipe. These are wrapped in an `<ol>` element.

Each item inside the lists is put inside an `<li>` (list item) element.

So for example, if we wanted to turn the part of the following paragraph fragment into a list:

~~~~ html
<p>At Mozilla, we’re a global community of technologists, thinkers, and builders working together ... </p>
~~~~

We could do this:

~~~~ html
<p>At Mozilla, we’re a global community of</p>

<ul>
  <li>technologists</li>
  <li>thinkers</li>
  <li>builders</li>
</ul>

<p>working together ... </p>
~~~~

Try adding an ordered or unordered list into your example page.

## Links

Links are very important — they are what makes the Web A WEB. To implement a link, we need to use a simple link — `<a>` — the a being short for "anchor" (it's a long story...). To make some text inside your paragraph into a link, follow along with these steps:

* Choose some text. We chose the text "Mozilla Manifesto".
* Wrap the text in an `<a>` element, like so:

~~~~ html
<a>Mozilla Manifesto</a>
~~~~

* Give the <a> element an `href` attribute, like so:

~~~~ html
<a href="">Mozilla Manifesto</a>
~~~~

* Fill in the value of this attribute with the web address that you want the link to link to:

~~~~ html
<a href="https://www.mozilla.org/en-US/about/manifesto/">Mozilla Manifesto</a>
~~~~

You might get unexpected results if you omit the https:// or http:// part, called the protocol, at the beginning of the web address. So after making a link, click it to make sure it is going where you wanted it to.

`href` might appear like a rather obscure choice for an attribute name at first. If you are having trouble remembering it, remember that it stands for hypertext reference.

Add a link to your page now, if you haven't already done so.

## Conclusion

If you have followed all the instructions so far, you should end up with a page that looks like this:

![Product so far](/img/finished-test-page-small.png)

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Show us your page with a heading, image, paragraphs of text, and a list.

</div>
