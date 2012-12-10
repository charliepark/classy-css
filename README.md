# Classy CSS

Classy CSS is a CSS styleguide and design principle.

It leverages the best enhancements of CSS preprocessors like Sass / LESS, the best architectural principles of OOCSS and SMACSS, and can drop in to any existing CSS framework you're currently using. It's efficient and elegant — for writing, reading, rendering, and refactoring.

It gives you the following benefits:

* Writing code is faster, with less cognitive overhead. You don't waste time worrying about selector specificity or the DOM. You know *exactly* where that CSS declaration should go.
* Editing code is easier, as you know exactly where to find any component. You don't have to search through multiple files, or run Cmd+f's within a large CSS file. Everything is where it should be.
* Page rendering time is faster. Classy CSS uses Steve Souders-style best practices to give you the most efficient loadtimes on your pages.
* Easier file management. You don't have to wrangle lots of files together at runtime, or think about whether something fits into a certain compartmentalizing file, or adjust which file your CSS should go in if you realize a CSS declartaion should be more global (or more specific). There's only one CSS file.
* Code cleanup is easier. You can prune out-of-date code without worrying that you're missing some obscurely nested "aside.popup h3.subarticle.subtitle" somewhere on the site.
* Writing CSS for large sites uses the same methodology as writing CSS for small sites. There are more moving parts, of course, but they're pretty straightforward parts.
* Creating a styleguide for your site is totally painless.

It's probably clarifying to talk about what it isn't.
* It is **not** a framework, like Bootstrap, or Foundation, or Blueprint, or similar. It doesn't come with any pre-existing classes or modules.
* It is **not** an architecture, like SMACSS, or like OOCSS, though it's similar. You can use it alongside either one of those if you like them, though it contradicts some of the principles in both.
* It is **not** a preprocessor, like Sass or LESS. Classy CSS leans very heavily on preprocessors, but isn't one itself. We use Sass, and have written all documentation assuming you're using Sass.


