# Classy CSS

**This is *very* much still in development. Consider this alpha at best.**

Classy CSS is a CSS styleguide and design principle. It's best described as a common-sense specification for CSS.

It was inspired by a few other approaches to CSS. It leverages the best enhancements of CSS preprocessors like Sass / LESS, the best architectural principles of OOCSS and SMACSS, and can drop in to any existing CSS framework you're currently using. It's efficient and elegant — for writing, reading, rendering, and refactoring.

If you want to jump in, check out [How to write Classy CSS](#how).

### So, the benefits?

It gives you the following benefits:

* Writing code is faster, with less cognitive overhead. You don't waste time worrying about selector specificity or the DOM. You know *exactly* where that CSS declaration should go.
* Editing code is easier, as you know exactly where to find any component. You don't have to search through multiple files, or run Cmd+f's within a large CSS file. Everything is where it should be.
* Page rendering time is faster. Classy CSS uses Steve Souders-style best practices to give you the most efficient loadtimes on your pages.
* Easier file management. You don't have to wrangle lots of files together at runtime, or think about whether something fits into a certain compartmentalizing file, or adjust which file your CSS should go in if you realize a CSS declartaion should be more global (or more specific). There's only one CSS file.
* Code cleanup is easier. You can prune out-of-date code without worrying that you're missing some obscurely nested "aside.popup h3.subarticle.subtitle" somewhere on the site.
* Writing CSS for large sites uses the same methodology as writing CSS for small sites. There are more moving parts, of course, but they're pretty straightforward parts.
* Creating a styleguide for your site is totally painless.

### Hmm. Isn't it like _______________

It's probably clarifying to talk about what it isn't.

* It is **not** a framework, like Bootstrap, or Foundation, or Blueprint, or similar. It doesn't come with any pre-existing classes or modules.
* It is **not** an architecture, like SMACSS, or like OOCSS, though it's similar. You can use it alongside either one of those if you like them, though it contradicts some of the principles in both.
* It is **not** a preprocessor, like Sass or LESS. Classy CSS leans very heavily on preprocessors, but isn't one itself. We use Sass, and have written all documentation assuming you're using Sass.

If you already have a CSS flow that you like, there's a good chance that Classy won't work for you. But if you're like me — you've tried a lot of approaches, and none have worked yet — this could be a great fit.

Let's make CSS fun again.

### So who are you, to be writing this? ###

I'm Charlie Park. I've been writing CSS for about 12 years now. I've tried just about every approach out there, and have been refining my approach with every project.

The principles that Classy CSS emphasizes are extracted out of my own building of sites, and out of frustration that the existing tools haven't met my needs.

### What influenced you in making Classy CSS? ###

Primarily, my years writing CSS and not finding any of the methodologies to be sifficient. There are a few articles, conference talks, and blog posts that I've read over the years that have impacted it. The most recent ones are the easiest to find, so here are two:

* [OOCSS + Sass = The best way to CSS](http://ianstormtaylor.com/oocss-plus-sass-is-the-best-way-to-css/) (Ian Storm Taylor)
* [GitHub's CSS Performance](https://speakerdeck.com/jonrohan/githubs-css-performance) (Jon Rohan)


***

<a name="how"></a>
## How to Write Classy CSS

The main thing you'll see when you write Classy CSS is --- surprise --- there are lots of classes. A good shorthand: "Everything that deserves styling deserves a class. Nothing deserves more than one class."

### 1. Lots of Classes

The first thing you'll notice is that everything is a class. Hence the name.

Every styled item has one (and only one) class at runtime. More on dynamically-added classes in a bit.

### No Naked HTML Elements in Your CSS

Before we had CSS preprocessors, it made sense to worry a lot about the structure of your site and to reflect that structure in your CSS file. So you'd have declarations like `div#main_nav li a{}`. You then had to decide where that went in your CSS files. (Does it go in a section for links? For "things in lists"? For "navigation stuff"?) With Classy, you would give each of those links a class: `.link-main-nav` (or similar). You'd put it in the appropriate place in the CSS file (alphabetically), and you'd be done.

It's tempting to write a universal layout template for your `<h3>`s, or for `<p>`s, or whatever. A base class that everything else can build off of. Before CSS preprocessors like SASS, that wasn't a bad idea. But Classy shifts all of that trickle-down design (the *cascade*!) to the initial file. Again, if the element deserves to have a style, it deserves to have a class.

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

Similarly, you might find that you have content that flows into different containers, which should be styled differently depending on where it gets displayed. If your site uses this kind of content, y


### No IDs

There's no good reason to declare anything in CSS with an ID. If you're trying to scope declarations via a containing div, you should create a new class and extend the existing class.

### Limit Nesting As Much As Possible ###


### Give Your CSS Classes Descriptive Names

Instead of trying to decipher cryptic names when you're reading your code in a year or two, it's better to give your CSS classes descriptive names. So instead of `.postDate`, call it `.post-metadata-`

### Use A Single File for Your CSS

In *Getting Things Done*, David Allen recommends having a single filing structure, based alphabetically. He's worked with hundreds of thousands of clients, and sold millions of books. He probably has good things to say about filing structures.

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

### Babysitting elements ###





## JS ##

Some notes to flesh out:

* All JS keys off of HTML5 data attriibutes, not classes. (Example: `<input class='input-zip' data-save-on="blur" data-placeholder-text="ZIP Code" value="90210" />`)
* If you *must* use classes, JS classes use the `js-` prefix on the class.




