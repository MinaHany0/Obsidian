# 04
- meta data: this is data that the browser uses for searching or the search engine uses to show the site to other browsers or crawlers
- notice that the <span style="color:rgb(255, 192, 0)">meta data doesn't appear on the website</span>, that's why we put the <span style="color:rgb(255, 192, 0)">style</span> and the <span style="color:rgb(255, 192, 0)">script tags</span> in the meta data, because they are <span style="color:rgb(255, 192, 0)">used</span> by the <span style="color:rgb(255, 192, 0)">browser</span> but not directly into the file
# 05
notice you can add any meta tag you want is add its name and content
`<meta name="your_custom_name" content="your_custom_content">`
# 06
`<!doctype html`
this is used to tell the browser that we are using html5 
also it is used to tell the browser to render the page using standard mode which supports more feature than the quirks mode (which is the default mode for browser if not specified)

# 07
- notice that when using a heading, the browser has default <span style="color:rgb(255, 192, 0)">user agent stylesheet</span> which it uses by default to give you the bold big font used for heading (all without using CSS)
- <span style="color:rgb(255, 192, 0)">heading H1</span> is always used <span style="color:rgb(255, 192, 0)">only once</span> per HTML file and it is usually the <span style="color:rgb(255, 192, 0)">page title</span> 
# 10
element have attributes:
- <span style="color:rgb(255, 192, 0)">global attributes</span>
	- can be used on <span style="color:rgb(255, 192, 0)">all</span> elements in any file, like the class attribute or the hidden attribute or much more...
- <span style="color:rgb(255, 192, 0)">element attributes </span>
	- they are specific for elements like: <span style="color:rgb(255, 192, 0)">href</span> for a (anchor), <span style="color:rgb(255, 192, 0)">src</span> for img or video or much more....

# 11
elements can be formatted without CSS using special attributes
- b for bold: used for marking some bold text for design purpose
- string: used for making text bold for <span style="color:rgb(255, 192, 0)">importance</span> purpose which maybe used by <span style="color:rgb(255, 192, 0)">search engines searching for strong tags in pages</span> 
- i for italic
- em for emphasized also gives italic text
- mark for highlighting
- u for underline
- small for smaller text
- del for deleted text which is striked through text
- ins for inserted text which is used to tell a user that this text was newly added
- sub for subscript
- sup for superscript

# 12
`<a href="www.google.com">GOOGLE</a>`
- the anchor is an <span style="color:rgb(255, 192, 0)">inline</span> element
- uses the attribute <span style="color:rgb(255, 192, 0)">target="_blank"</span> 
- we can use title global attribute title="go to google" that appears when you hover over a link
- you can go to another element 
	- <span style="color:rgb(255, 192, 0)">"href=#idName"</span> which goes to the element with id = idName
	- or `<a href="mailto:mina@gmail.com">contactme </a>` which then goes to your mail directly

# 13
attaching an image 
using the img tag
- attributes are 
	- src which is the link to the photo
	- alt which is the alternate text appearing when the photo doesn't load for some reason
# 14
list are ordered and un ordered  <span style="color:rgb(255, 192, 0)">(ul and ol)</span> and both have list items <span style="color:rgb(255, 192, 0)">li</span>
- notice that list can be <span style="color:rgb(255, 192, 0)">nested</span> inside each other
- some attributes are there 
	- example for ordered list: <span style="color:rgb(255, 192, 0)">reversed</span> attribute, <span style="color:rgb(255, 192, 0)">start</span> attribute, <span style="color:rgb(255, 192, 0)">type</span> ="1", "a", "A" and so on
- finally the descriptor list `<dl> 
	- and it has a description term`<dt>HTML</dt>`
	- and it has a description itself `<dd>language of the web<dd>`
# 15
table is the best way to sort your data
and it is done in the following way

header-> use <span style="color:rgb(255, 192, 0)">thead</span>
footer -> use <span style="color:rgb(255, 192, 0)">tfoot</span>
body use -> use <span style="color:rgb(255, 192, 0)">tbody</span>
for making any row inside any of this -> use <span style="color:rgb(255, 192, 0)">tr</span>
for making data inside any row -> use <span style="color:rgb(255, 192, 0)">td</span> 

for making caption -> use caption
to merge two cells ->use colspan attribute

you can use border attribute but it is not recommended to style your table using html, all styling should be by CSS

# 16
- span tag is used to give some word an element property so it can be have its own CSS styling, because you cannot give styling to normal text.
- the br is the break tag and it gives a newline
- hr is the horizontal rule , which is a block element


# 17 the <span style="color:rgb(255, 192, 0)">DIV</span>
- the div is used as a <span style="color:rgb(255, 192, 0)">handler</span> or a <span style="color:rgb(255, 192, 0)">container</span>
- if you have multiple elements lets say books, and we want some formatting (say color) for romance books , another for horror and so on....
	- option 1: you style each one and keep copying the style 
	- option 2: out the similar books into a div (<span style="color:rgb(255, 192, 0)">and identify it using a class attribute</span>) and then <span style="color:rgb(255, 192, 0)">style</span> the <span style="color:rgb(255, 192, 0)">div container</span> only one time which will be applied to all its contents
- we can say the div is the thread we use to <span style="color:rgb(255, 192, 0)">control</span> the stage easily at multiple places at the same time

# 18 Entities
if you need to print the < or the > you need to use the entity name of the symbol
- for < it is &ls;
- for > it is &gt;
notice how it is always ending in semicolon and many more symbols you can search for on the internet

# 19 Semantic tags
before when making anything we used to use lots of divs and lots of classes for the same elements over and over
- every page needed a class called (header, navigation bar, footer, article) and each element needed lots of tags
- so in HTML5 the made semantic tags which you can control directly, like the
	- header tag
	- nav tag
	- footer tag
	- section tag
	- article tag
	- aside tag
	- figure tag
- ![[El-Zero HTML-20241211214831740.webp]]
# 20 Layout without semantics
``<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Page</title>
</head>

<body>
    <div class="header">
        <h1>Title</h1>
        <ul>
            <li>about</li>
            <li>career</li>
            <li>contact us</li>
        </ul>
    </div>
    <hr>
    <div class="navigation">
        <ul>
            <li>link</li>
            <li>link</li>
            <li>link</li>
            <li>link</li>
            <li>link</li>
        </ul>
    </div>
    <hr>
    <div class="sidebar">
        this is the side bar article
    </div>

    <hr>
    <div class="article">
        paragraph and photo
    </div>

    <div class="footerr">
        thank you for coming to our website
    </div>

</body>

</html>``

this is the simple page done without any semantic tags, check how much div and classes there it and the visbility noise it is making


# 21 Layout with semantic
this is the same layout but using semantic tags

``<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Semantic Page</title>
</head>
<body>
    <header>
        this is my header
        <ul>
            <li>about</li>
            <li>career</li>
            <li>contact us</li>
        </ul>
    </header>
    <nav>
        <ul>
            <li>link</li>
            <li>link</li>
            <li>link</li>
            <li>link</li>
            <li>link    </li>
        </ul>
    </nav>
    <aside>
        side bar article
    </aside>
    <section>
        this is my main section 

        <figure>
            <img src=".blabla" alt="image normal">
            <figcaption>this is a template picture</figcaption>
        </figure>
    </section>

    <footer>
        this is my precious footer
    </footer>
</body>
</html>``



# 22 audio
audio can be done using audio tag
and you can use src attribute directly or use many <span style="color:rgb(255, 192, 0)">source tags</span> fot the browser to choose the most compatible format and then inside the <span style="color:rgb(255, 192, 0)">source</span> tag you can use the <span style="color:rgb(255, 192, 0)">src and type</span> attributes

- if the browser does not support the audio tags, you need to write a text to appear for this person to notify him![[El-Zero HTML-20241211223856455.webp]]
- audio control gives you the button for play/pause, volume up and down
- audio control autpplay will let the music start as soon as you go to the page and some browsers such as google chrome block this autoplay
# 23 Video
![[El-Zero HTML-20241220214509537.webp]]

# 24 Form  part 1
```
<form>
    <div>
        <label >username</label><input type="text">
    </div>
    <br> 
    <div>
        <label >password</label><input type="password">
    </div>
    <input type="submit">
</form>
```

- the password type makes the text get typed as stars or dots so it will be hidden
- don't forget the submit input type

# 25 form part 2
- using the placeholder attribute 
- using the required attribute 
![[El-Zero HTML-20241220223016885.webp]]

# 26 Form part 3
![[El-Zero HTML-20241224220459965.webp]] here we learn about the name and the method
- the name is the parameter which maps the data in the form to the tables of data used by the backend
- the method is the HTTP method used for sending the form data
	1. you can can use the GET method but all the form params will be as query parameters
	2. you can use the POST method where the form params will be put as form parameters in the HTTP request and will NOT be in the URL itself

# 27 Form part 4
```
<!doctype html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Book Store</title>
    <meta name="description" content="This Is Our Book Store" />
  </head>
  <body>
    <div>
      <h1>Book Store</h1>
      <p>This Is My Book Store, Welcome</p>
    </div>
    <form action="" method="POST">
      <div>
        <label>Username</label>
        <input type="text" required placeholder="Username" name="user">
      </div>
      <br>
      <div>
        <label>Subject</label>
        <input type="text" name="subject">
      </div>
      <br>
      <div>
        <label>Password</label>
        <input type="password" required placeholder="Write A Complex Password" name="pass">
      </div>
      <br>
      <div>
        <label>Email</label>
        <input type="email" required placeholder="Write A Valid Email" value="o@nn.sa" name="mail">
      </div>
      <input type="submit" value="Save">
    </form>
  </body>
</html>
```

remember that using the GET method puts the params in the query while using POST puts them in the form params but not visible in url

# 28 Form part 5