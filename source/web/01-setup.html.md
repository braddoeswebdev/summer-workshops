---
series: 'web'
number: 1
title: "Getting Set Up"
icon: 'laptop'
desc: "Set up your files & folders for your page"
---
# Getting Set Up

## An aside on casing and spacing

You'll notice that throughout this article, we ask you to name folders and files completely in lowercase with no spaces. This is because:

- Many computers, particularly web servers, are case-sensitive. So for example, if you put an image on your website at `test-site/MyImage.jpg`, and then you try to open the image as `test-site/myimage.jpg` somewhere else, it may not work.
- Browsers, web servers, and programming languages do not handle spaces consistently. For example, if you use spaces in your filename, some systems may treat the filename as two filenames. Some servers will replace the spaces in your filenames with "%20" (the character code for spaces in URIs), breaking all your links. It's better to separate words with dashes or underscores: `my-file.html` or `my_file.html`.

For these reasons, it is best to get into the habit of writing your folder and file names lowercase with no spaces, at least until you know what you're doing. That way you'll bump into fewer problems.

## What structure should your website have?

Next, let's look at what structure our test site should have. The most common things we'll have on any website project we create are an index HTML file and folders to contain images, style files, and script files. Let's create these on your L: drive now:

- `www`: This folder is set up to hold files that can be accessed by the web server.
- `img` folder: This folder will contain all the images that you use on your site. Create a folder called `img`, inside your `www` folder.
- `css` folder: This folder will contain the CSS code used to style your content (for example, setting text and background colors). Create a folder called `css` inside your `www` folder.

Note: On Windows computers, you might have trouble seeing the file names, because Windows has an annoying option called Hide extensions for known file types turned on by default. On Windows 8, it's easy to turn on - click the 'view' tab, and check the 'file name extensions' box.

## Let's write some HTML!

Let's dive in & start putting your web page together!  

- Copy the image you chose earlier into your `img` folder.
- Open Notepad++, if you haven't already and type the following code exactly as shown. Don't worry about what it all means for now — we'll look at the structures in more detail in the next lesson.  Don't just copy and paste - you won't learn anything that way.

~~~~ html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <img src="" alt="My test image">
  </body>
</html>
~~~~

- The line `<img src="" alt="My test image">` is the HTML code that inserts an image into the page. We need to tell the HTML where the image is. The image is inside the `img` directory, which is in the same directory as `index.html`. To walk down the file structure from `index.html` to our image, the file path we'd need is `img/your-image-filename`. For example, our image is called `firefox-icon.png`, so the file path is `img/firefox-icon.png`.
- Insert the file path into your HTML code between the double quote marks of the `src=""`` code.
- Save your HTML file, then load it in your web browser (double-click the file). You should see your new webpage displaying your image!


## Some general rules for file paths:

- To link to a file in the same directory as your HTML file, just use the filename, e.g. `my-image.jpg`.
- To reference a file in a subdirectory, write the directory name in front of the path, plus a forward slash, e.g. `subdirectory/my-image.jpg`.
- To link to a target file in the directory above your HTML file, write two dots. So for example, if `index.html` was inside a subfolder of `www` and `my-image.png` was inside `www`, you could reference `my-image.png` from `index.html` using `../my-image.png`.
- You can combine these as much as you like, for example `../subdirectory/another-subdirectory/my-image.png`.

For now, this is about all you need to know.

Note: The Windows file system tends to use backslashes, not forward slashes, e.g. C:\windows. This doesn't matter — even if you are developing your web site on Windows, you should still use forward slashes in your code.

<div class="panel panel-primary">
<div class="panel-heading">Before you continue, show this to one of the adult-y people</div>
  <div class="panel-body" markdown="1">

Show us that your folders & files are all set up correctly.

</div>
