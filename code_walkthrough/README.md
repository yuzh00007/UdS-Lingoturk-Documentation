# Code Walkthrough Introduction

This section is divided into two parts. 
The first part is a very quick introduction to web design concepts
as well as a general overview of the code that Lingoturk uses to run
experiments. 
The second part puts that information to practice through
a follow along tutorial that will build a working experiment from scratch.

# 1. Code Overview
1. [The Very Basics of Web Design](./overview/01-Basic-Overview.md)
2. [Quick Code Rundown](./overview/02-Code-Rundown.md)
3. [Experiment Slide Structure](./overview/03-slide-structure.md)


# 2. Experiment Tutorial
We will start with an empty experiment type and work it into an example
experiment, by following along, you'll get experience working with Lingoturk
and have a working experiment at the end. 

If this is your first time working
with web design, it'll be a good hands on experience.
Each section, we'll add one thing to the experiment until, by the end, 
we will have a working project that is able to submit responses to your
local Lingoturk server's database.

### Planned Experiment
This tutorial will build a experiment type from scratch. The experiment will
consist of two tasks, one followed by another. The tasks were chosen to be simple
but help give an idea of how development on Lingoturk works. The tasks are:
1. Picture Naming (image, multiple choice, text input)
2. Sentence Oddity (image & sliders)

### Angular vs JavaScript
There are two main ways to control both 1) what/how elements are displayed on the screen
and 2) the logic powering the elements or their behavior. Using base Javascript requires
heavily editing the JS file and its functions, whereas using Angular can cut
down on a lot of the work by incorporating existing code snippets using NG-directives
into the HTML itself. 

There is no right or wrong way to program an experiment and sometimes one way
makes more sense than the other. And in fact, normally, developers mix the two
constantly, selecting whichever is more suited for the job at hand.

However, in this tutorial, the two planned tasks will be split across these two
code design philosophies. The Picture Naming task will focus on using NG-directives 
for controlling its logic, and the Sentence Oddity task will focus on using base 
Javascript.

### Prerequisites
You will need:
- the local copy of the Lingoturk repository, cloned from
  https://github.com/FlorianPusse/Lingoturk.
- fully set up pgadmin and Lingoturk backend
- an IDE of some sort (IntelliJ offers education licenses for free)
- basic understanding of Lingoturk (see: [Lingoturk Introduction](../lingoturk_introduction/README.md))

Create an experiment type called "TutorialExperiment" that has five
fields. We will use this for the code walkthrough.
- id (String)
- imagePath (String)
- opt1 (String)
- opt2 (String)
- opt3 (String)

Then create an experiment instance with [this CSV file](). 

### Table of Contents
1. [Adding Slides](./steps/01-adding-slides.md)
2. [Adding Instructions](./steps/02-adding-instructions.md)
3. [Preprocessing the Data](steps/03-data-preprocessing.md)
4. Experiment 1 (mainly Angular Directives)
   - [Creating UI Elements](steps/04-adding-exp1-ui-elements.md)
   - [Adding Functionality](steps/05-adding-exp1-functionality.md)
   - Saving Responses
5. Experiment 2 (mainly base JavaScript)
   - [Creating UI Elements](steps/07-adding-exp2-ui-elements.md)
   - [Adding Functionality](steps/08-adding-exp2-functionality.md)
   - Saving Responses


