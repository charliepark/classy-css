# Classy CSS

Good code is classy.

**This is *very* much still in development. Consider this alpha at best.**

## A good approach to CSS will be **efficient and elegant** &mdash; for **writing**, for **reading**, for **rendering**, and for **refactoring**.

## It should **leverage the best practices in the development community**, including **the good parts of OOCSS and SMACSS**, and **the power of preprocessors like LESS and Sass**.

## It should be **easily learnable and teachable**, and should be **easily applied** to any existing CSS file, so a web app could be converted over with little hassle.

## Classy CSS is all of these things.

### Classy CSS is a CSS styleguide and design principle for web applications. It's a common-sense specification for CSS.

We'll cover some more about Classy CSS, but If you want to jump in and learn the details, check out [How to write Classy CSS](#how).

### So, the benefits?

It gives you the following benefits:

* Writing code is faster, with less cognitive overhead. You don't waste time worrying about selector specificity or the DOM. You know *exactly* where that CSS declaration should go.
* Editing code is easier, as you know exactly where to find any component. You don't have to search through multiple files, or run Cmd+f's within a large CSS file. Everything is where it should be.
* Page rendering time is faster. Classy CSS uses Steve Souders-style best practices to give you the most efficient loadtimes on your pages.
* Easier file management. You don't have to wrangle lots of files together at runtime, or think about whether something fits into a certain compartmentalizing file, or adjust which file your CSS should go in if you realize a CSS declartaion should be more global (or more specific). There's only one main CSS file that you work in (and only two supporting files).
* Code cleanup is easier. You can prune out-of-date code without worrying that you're missing some obscurely nested "aside.popup h3.subarticle.subtitle" somewhere on the site.
* Writing CSS for large sites uses the same methodology as writing CSS for small sites. The learning curve is gentle, and plateaus quickly.
* Creating a styleguide for your site is totally painless.

### Hmm. Isn't it like _______________

It's probably clarifying to talk about what Classy CSS isn't.

* It is **not** a framework, like Bootstrap, or Foundation, or Blueprint, or similar. It doesn't come with any pre-existing classes or modules.
* It is **not** an architecture, like SMACSS, or like OOCSS, or like BEM, though it's similar. You can use it alongside any of those if you like them, though it contradicts some of their principles. If you don't use them, you can get the majority of their benefits by simply using Classy CSS and being done with it.
* It is **not** a preprocessor, like Sass or LESS. Classy CSS leans very heavily on preprocessors, but isn't one itself. We use Sass, and have written all documentation assuming you're using it, too. It should be easily portable to LESS.

If you already have a CSS flow that you like, there's a good chance that Classy won't work for you. But if you're like a lot of front-end developers — you've tried a lot of approaches, and none have worked yet — this could be a great fit for you.

### So who are you, to be writing this? ###

I'm Charlie Park. I've been writing CSS for about 12 years now. I've tried just about every approach out there, and have been refining my approach with every project.

The principles that Classy CSS emphasizes are extracted out of my own building of sites, and out of frustration that the existing tools haven't met my needs.

### What influenced you in making Classy CSS? ###

Primarily, my years writing CSS and not finding any of the methodologies to be sufficient. There are a few articles, conference talks, and blog posts that I've read over the years that have impacted it. The most recent ones are the easiest to find, so here are a few. You don't need to read these, but you'll probably like them.

* [OOCSS + Sass = The best way to CSS](http://ianstormtaylor.com/oocss-plus-sass-is-the-best-way-to-css/) (Ian Storm Taylor)
* [Your CSS Is A Mess](https://speakerdeck.com/snookca/your) (Jonathan Snook)
* [GitHub's CSS Performance](https://speakerdeck.com/jonrohan/githubs-css-performance) (Jon Rohan)
* [A Harder-Working Class](http://24ways.org/2012/a-harder-working-class/) (Nathan Ford)
* [BEM: The Block, Element, Modifier Approach To Decoupling HTML And CSS](http://www.vanseodesign.com/css/block-element-modifier/) (Steven Bradley)
* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/) (Nicolas Gallagher)
* [CSS Architecture](http://philipwalton.com/articles/css-architecture/) (Philip Walton)
* [The Future of OOCSS: A Proposal](http://philipwalton.com/articles/the-future-of-oocss-a-proposal/) (Phillip Walton)

But wait! surprise twist! Two posts from Phillip Walton that argue against some of the stuff that Classy CSS does! Worth reading!

* [Defending Presentational Class Names](http://tympanus.net/codrops/2013/01/22/defending-presentational-class-names/) (Phillip Walton)
* [CSS: Everything is global and how to deal with it](http://www.adobe.com/devnet/html5/articles/css-everything-is-global-and-how-to-deal-with-it.html) (Phillip Walton)


### A few TODOs

* revise notes about "only one class" … not on that team anymore. Balance.
* write about idea of "items" versus "collections"
  * item: a one-off object, like a specific link, or cell, given a class:
    * the class is assigned on the lowest-level element
    * `.td-highlighted{}`
    * `.popup-account{}`
  * collection: a number of objects together, which should all have similar properties
    * the class is assigned on the parent element
    * `.nav-links a{}`


***

<a name="how"></a>
## How to Write Classy CSS

### In a nutshell: ###

1. Only use classes. All HTML elements in your DOM get a single class.
2. Use the @extend functionality of Sass to keep your CSS code clean.
3. Organize all CSS in three files. Similar to SMACSS:
  * Classes (think: "classes"; where almost all of your details will be)
  * Layout (think: "ids"; used to set up a few one-time-per-page components, like headers and footers, and main content areas; you won't touch this much)
  * Base (think: "elements"; used for your reset and to set up defaults; after you set this up at the beginning, you'll barely touch it, ever)
4. Name classes by rough application, context, and function. This pulls from the *ideas* in OOCSS, but all the work is done in the stylesheet, rather than in the page's markup (with long strings of classes). So:
  * %button-default{…}
  * .button-cancel{(extend button-default)…}
  * .button-submit{(extend button-default)…}
  * %title-default{…}
  * .title-of-page{(extend title-default)…}
  * .title-of-section{(extend title-default)…}
5. DOM elements that are affected by JS can also have a .js-... class, but if possible, use data-attributes instead of classes. More on this soon.

The main thing you'll see when you write Classy CSS is — surprise — there are lots of classes. A good shorthand: "Everything that deserves styling deserves a class. Nothing deserves more than one class."

### 1. Lots of Classes

The first thing you'll notice is that everything is a class. Hence the name.

Every styled item has one (and only one) class at runtime. More on dynamically-added classes in a bit.

You might object: "Isn't adding lots of classes bad? Isn't that 'classitis'?"

Adding lots of classes isn't bad. As Steven Bradley notes, "At first glance it seems like adding classes to html increases coupling due to the added markup, but the opposite is actually true. Coupling is increased the more dependent we are on a specific html structure. Jonathan Snook referred to this as the *depth of applicability*. The greater this depth, the greater our html and css are coupled. … Unfortunately our best practices the last few years have been increasing coupling even as we thought we were decreasing it."

If you've ever hesitated to change the class of an HTML element, or hesitated to change the CSS that styled that class, because you were afraid of where else in your code you used the same class, you know the dangers of tight coupling.

### 2. No Naked HTML Elements in Your CSS

Before we had CSS preprocessors, it made sense to worry a lot about the structure of your site and to reflect that structure in your CSS file. So you'd have declarations like `div#main_nav li a{}`. You then had to decide where that went in your CSS files. (Does it go in a section for links? For "things in lists"? For "navigation stuff"?) With Classy, you would give each of those links a class: `.link-nav-main` (or similar). You'd put it in the appropriate place in the CSS file (alphabetically), and you'd be done.

It's tempting to write a universal layout template for your `<h3>`s, or for `<p>`s, or whatever. A base class that everything else can build off of. Before CSS preprocessors like SASS, that wasn't a bad idea. And with blogs and other simple layouts, that might be appropriate. But for rich web apps with lots of different types of `<h3>`s, and lots of `<p>`s, having raw HTML elements named in your CSS can be dangerous. 

Apart from a CSS reset (we like Eric Meyer's reset, but any reset will do). Apart from that, don't traffick in naked elements.

You ask: "But what about `p`aragraph tags? And `strong`s? And `em`s?" Okay. A caveat: There will be some atomic elements that you *will* include without classes. But that's why it's important to build your reset/base so that it conforms to the look and feel of the rest of the site. But if it's not an element that your CMS is going to dynamically generate, give the item a class and style it accordingly.

If you find that you absolutely *must* use non-classed elements, scoped inside parent elements, as long as the parent element has a class, it'll still work. So: `.byline a` would be okay, but it would be better to have a class: `.link-byline`.

Your classes should stand on their own.

Occasionally, you'll find that a certain "parent" class should affect the class of an item. For example, in a financial app, you might have a table showing spending categories and how much is available to spend. If a category is "overspent", you want to show both the name and amount for the category. If necessary, you can nest classes (so the `<tr>` might have a class of "overspent" or similar), and your CSS could look like this:

    .td-amount { color: black; }
    .tr-overspent .td-amount {color: red; }

Ideally, though, you'd set your app to spit out a more specific class:

    .td-amount { color: black; }
    .td-amount-overspent { color: red; }

Similarly, you might find that you have content that flows into different containers, which should be styled differently depending on where it gets displayed. If your site uses this kind of content, you should have enough control over the content generated that you can assign specfific classes. Decoupling your CSS is good.

### No IDs

Apart from a handul of layout CSS — which should go in your "layout.css" file — you shouldn't have any IDs in your CSS. Even these should be fairly minimal. Maybe a `nav#main-nav` or something.

### Give Your CSS Classes Descriptive Names

Instead of trying to decipher cryptic names when you're reading your code in a year or two, it's better to give your CSS classes descriptive names. So instead of `.postDate`, call it `.post-metadata-date` or something similar. One of the benefits of long, descriptive names is that it makes it trivial to do a find-all to see where your code needs to be updated / tweaked / adjusted. (See Pamela Fox's post, [A Tale of Two Bootstraps: Lessons Learned in Maintainable CSS](http://blog.pamelafox.org/2012/12/a-tale-of-two-bootstraps-lessons.html), for something related.)

### How to Name Your Clases ###

I've started using dashes in my CSS to separate words, mainly so I can know — at a glance — whether I'm dealing with Ruby (words_joined_by_underscores), JavaScript (whateverThisOneIsCalled), or CSS (words-separated-by-dashes). That's up to you, though.

Anyway, I recommend using a description of the type of element as the first word in the title. So, some examples:

    .button{}
    .button-cancel{}
    .button-submit{}
    .link{}
    .link-nav-main{}
    .link-nav-sub{}
    .td-amount{}
    .td-date{}
    .title{}
    .title-of-page{}
    .title-of-section{}

You'll notice that for the links and the titles, I've avoided using elements that have explicit HTML elements (like .h1 through .h6). The reason I've used "title" for those is that I don't want to be constrained by the name of the class, to get confused about where I can use them in my app.

For the .button and .td example, I *have* used HTML elements, as a table cell isn't really transferrable (so it'll always apply to a `<td>`), and even if an `<a>` is the element that gets the .button{} class, I'll still want it to look and feel like a button.

### Alphabetize the Classes in Your CSS File

Similar to David Allen's approach to organizing paper-based files, Classy CSS uses a single CSS file, with all classes listed alphabetically. Because you're naming them descriptively, they should fall into a natural order. For example:

    .td {}
    .td-amount {}
    .td-amount-overspent {}
    .td-category {}
    
    .title {}
    .title-of-page {}
    .title-of-popup-box{}
    .title-of-section {}


### No More Than Two Levels Deep ###

Because you have so many classes, and because you *only* have classes for defining style, you don't need to have complicated selector strings in your CSS. If you have a specific use-case where a certain style should be renedered differently in a different context (and you aren't able to change the elemnt's class), you shouldn't need more than two levels of classes *at most*.

An example: In PearBudget, we have table cells that show the amount of money remaining in a category. Think of it like a bank balance. So one category might be at $31.42, another might be at -$49.03. I want the negative values to be red.

I have three options:

1. I can have a JavaScript function run at loadtime, find the negative amounts, and assign a dynamic class (or style) to those specific cells.
2. I can evaluate the value of the cell when I'm dynamically building the page, and I can give the cell a specific class that recognizes the negative value (and that class would have a `color: red;`). While this could be a separate class added to the cell (so the HTML would look like `<td class='td-amount overspent'>`), a classier version would be to assign a single class: `td-amount-overspent`. That class (or chained set of classed) would then have the `color: red` in the CSS file.
3. I can assign a class to a parent element (like `<tr class='overspent'>`), and then have, in the CSS, a selector of `.overspent .td-amount`.

The specific use-case will determine which of these directions is best.

I'm still working through the pros and cons of these approaches. Will update when I have something more substantial. At the moment, I'm leaning towards using option 3, to have a class applied to the parent row, and to then have CSS that overrides the default style.



### Lean On Sass

Preprocessors like Less and SASS have opened up a whole world of possibility. Classy tries to make the most of that, especially with the `extend` command that SASS makes available.

In OOCSS, you'd have multiple classes that would apply to an object: `<button class='large primary rounded'>`. With a preprocessor, you can still have those classes, but you'd be able to combine them. So, in Classy CSS, you'd have code like this:

    .button{}
    
    .button-cancel{
      @extend .button-large;
      @extend .button-rounded;
      @extend .button-secondary;
    }

    .button-large{
      @extend .button;
      font-size: 2em;
      padding: 20px;
    }
    
    .button-primary{
      @extend .button;
      color: #fff;
      background: #678;
    }
    
    .button-rounded{
      @extend .button;
      border-radius: 10px;
    }
    
    .button-secondary{
      @extend .button;
      color: #444;
      background: #ccc;
    }
    
    .button-submit{
      @extend .button-large;
      @extend .button-primary;
      @extend .button-rounded;
    }

Then, in the actual HTML of the page to be rendered, we'd simply have:

    <button class="button-submit">comment</button>
    <button class="button-cancel">cancel</button>



Do we end up with more classes? Yes. Is that a problem? No. Why not?

Common critiques against having lots of classes (flesh out):

* CSS file size is embiggened
* 




## Downsides ##

There are, of course, downsides to this approach. Let's look at them.

(TODO: come up with some downsides.)

I'm not totally happy with certain "state" conditions, when I'm limited from using multiple classes in an element. For example, if I know that a class that affects the entire row of a table is going to be applied, and I want the cells within that row to be affected in some way (say, color), the mental gymnastics are a little tricky at the moment. I'm not saying they aren't worth it. I'm not saying they are. I think we'll need to consider the flexibility we need, so that a second class applied to an object doesn't create a cascade of new sub-classes required on the elements contained within that element. Perhaps the best way to think of Classy is as "OOCSS principles, in a SMACSS architecture, with some BEM conventions thrown in for clarity."

If you're developing a content-based site, like a magazine, or a blog, or something else where you have long strings of, say, `<p>` elements, you aren't going to want to give a class to each one. You'd want to set those up in the "Base" section of the file.




Some notes to flesh out:

* All JS keys off of HTML5 data attriibutes, not classes. (Example: `<input class='input-zip' data-save-on="blur" data-placeholder-text="ZIP Code" value="90210" />`)
* If you *must* use classes, JS classes use the `js-` prefix on the class.




