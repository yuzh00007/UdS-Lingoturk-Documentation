# Experiment Slide Structure

Experiments in Lingoturk are run in a single web page (i.e. refreshing the page will
immediately restart the experiment). So what if we have multiple tasks and need to show
the participants a lot of different UI setups? We can use Angular directives to hide
and show HTML elements. And to facilitate the directives, we will introduce "slides" or
"states". 

I will use the word "slide" here to describe each unique screen that is
shown to participants.

In this section, we will add some new slides to the newly created experiment type. 

## Managing State Overview

There are two variables to be aware of here: `self.showMessage` and `self.state`.
By setting these two variables to different values, you control what is shown
by the Angular directives.

> of course, you can introduce new variables and make updates to the HTML to
> utilize your new variable. `self.showMessage` and `self.state` will always 
> be available in the starter code.
 
If you check the HTML file, you will see three Angular directives that are controlled
by `self.showMessage`. 
```html
<div ng-if="RC.showMessage == 'none'" ...></div>
<div ng-if="RC.showMessage == 'nextSubList'" ...></div>
<div ng-if="RC.showMessage == 'goodBye'" ...></div>
```

Under the case where showMessage is none, four slides are controlled by the
`self.state` variable. 
```html
<div ng-if="RC.state == 'instructionsSlide'" ...></div>
<div ng-if="RC.state == 'workerIdSlide'" ...></div>
<div ng-if="RC.state == 'statisticsSlide'" ...></div>
<div id="experiment_content" ng-if="RC.state == 'questionSlide' ..."></div>
```

### self.allStates

In the `$(document).ready()` main function, you will find a list variable called
`self.allStates`. The function `self.next()` advances through this list. So any time
in your experiment, this function is called, we progress through the states, showing
different slides with every state change. Often, the `self.next()` function is tied
to a button on the UI that advances to the next slide.

## Adding Slides

A general set up you can have is a button on every slide, which will call `self.next()`
to move to the next slide in your list. For this tutorial, let's create a two part
experiment with an instruction page in front of each. So, the experiment flow looks like
this: 

```text
experiment1instruction -> experiment1 -> experiment2instruction -> experiment2 
```

> I haven't written the three parter (instruction -> workerID -> statistics) 
> because they'll likely almost ALWAYS be necessary.  
> if you do need them removed, HTML updating will be required.

### updating self.allStates

The starter code will provide a div with id `experiment_content` that is dependent on 
a state called `questionSlide`. But since we are creating a two part experiment, let's 
rename this and add more slides to our `self.allStates` list. 

```javascript
self.allStates = [
    "instructionsSlide",
    "workerIdSlide",
    "statisticsSlide",
    "experiment1_instruction",
    "experiment1_content",
    "experiment2_instruction",
    "experiment2_content"
];
```

### updating the HTML

#### creating new divs 

Since we have added more slides and also renamed some slides, we'll need to make
changes to reflect that in the HTML file. 

First, let's rename the div that depends on `questionSlide` state name. You can ignore 
the other logic in the ng-if directive for the moment.

```html
<div id="experiment1_content" ng-if="RC.state == 'experiment1_content' && ...></div>
```

Next, we'll add one div for each of the other three slides we added to `self.allStates`. 
You can copy and paste the div we just renamed for the other three states, making
sure to give them different id names and ensuring the state logic is correct. We'll 
cover how to change the contents later.

```html
<div id="experiment1_instruction" ng-if="RC.state == 'experiment1_instruction' && ..."></div>
<div id="experiment1_content" ng-if="RC.state == 'experiment1_content' && ..."></div>
<div id="experiment2_instruction" ng-if="RC.state == 'experiment2_instruction' && ..."></div>
<div id="experiment2_content" ng-if="RC.state == 'experiment2_content' && ..."></div>
```
 
#### testing the HTML 

If you were to create an instance and use any data for the csv and leave the instructions
blank, you can click Next to get to the workerID page, where you can submit any value. 

You should then see a box with the words 
"Instructions here:" at the top. This is one of the four slides we had defined previously.
Since we haven't modified the contents just yet, all four slides will be the same.
If the csv file you used had a number of rows, each row will be used as a question,
displaying each row with every click. This is the `experiment1_instruction` slide
using the `ng-repeat` directive to loop through `self.questions`.

Once it stops refreshing, we've moved on to the second slide `experiment1_content`.
And after a couple more clicks, you'll be presented with the Submission screen - an
indication that everything worked. 
