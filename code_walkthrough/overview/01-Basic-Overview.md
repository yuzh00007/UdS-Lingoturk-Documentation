# The Very Basics of Web Design

There are three main files to be aware of, not just for LingoTurk, but for 
web development in general. 

1. HTML file: located under `app/views/ExperimentRendering/`
2. CSS file: located under `public/stylesheets/ExperimentRendering/`
3. JS file: located under `public/javascripts/ExperimentRendering/`

If this is your first time ever doing web development, I'll go over a very
quick overview of the three files and some basic web-dev knowledge.

If not, go ahead and skip over this section, or recommend information you think
new developers should know about web-dev!

## HTML 

**HTML** files define the webpage that you are seeing. If you open up any HTML
file, you will see many of the different "tags" such as `<div>` `<p>` 
and `<button>` that define a lot of the _elements_ you see on any web page. 
LingoTurk experiments run on a single web page - so only a single HTML 
file is required per experiment. And you won't need to worry
about redirecting participants to different extensions either. (You can 
this is the case because the URL never changes during an experiment!)

More technically, HTML defines what's called a DOM (domain object model) tree.
What you need to know is that the tags looks like a tree, with different 
elements having parents, siblings, and children nodes. For example, a \<div\>
may have four children \<div\>s inside it, plus maybe some \<p\> (paragraph) 
elements as well. 

Inside many tags you will often see `id="...""` and `class="..."`, these id and
class names are defined such that you can find them if you want to modify or 
use them in the code. Combine this with the DOM tree, and you have the ability
to select and modify groups of elements within the web page. For example, 
selecting the parents of a specific element and changing their color based on
a condition.

## CSS

**CSS** files are called the stylesheets because they define everything that a
graphic designer may have control over on a web page, from the color of a button
to the size of a textbox, i.e. the style in which every element will be 
displayed to the user. 

Everything that you do with CSS files can be specified
directly into the HTML files. You'll often see `<style>` tags or `style="...""` 
code snippets within other tags inside larger HTML files. So technically CSS
files are completely optional, if you leave it empty, it won't cause an issue.
However, since your web page likely has a uniform theme, where buttons and
progress bars tend to look similar if not identical in every occurance, it's
best practice to limit code repetition and bring the style definition for 
most HTML elements into this file. Only hardcode styles into the HTML file for
one offs and exceptions to the rule.

## JavaScript

**JS** files will manage the logic of your web page. Code you write in here
will manage all the elements that you have defined in the HTMl file. That
being said, it is entirely possible to have a completely empty JS file and
include a <script> tag in the HTML file. In the same vein, it is entirely 
possible to have a bare minimum HTML document and create everything from code.

For our purposes, it's likely that most of the logic for what material
and question to be displayed will be handled in the 
JS file, while the UI is defined and handled by the HTML - this is the pattern
most of the experiment types on LingoTurk will follow. 

However, in some cases, for example, playing audio on button prompt, will 
have to be handled by a code snippet. And this will be placed in the JS file.

## Angular

Angular is a framework for single page applications. It provides more powerful
tools beyond just what is available with the three files highlighted above. 
For example, in the HTML file, you will see `ng-if=` and `ng-init=` inside 
many DOM elements. These are said tools that Angular provides for writing
logic into the HTML file itself. 
