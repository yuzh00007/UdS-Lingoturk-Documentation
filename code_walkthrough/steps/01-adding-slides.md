# Adding Slides

This experiment will follow a basic general set up for advancing between parts of the
experiment: on every slide, put a button which will call `self.next()`
when clicked and advance to the next state. Since the experiment has two parts, the
slide structure will look like this (with an instruction slide appearing before
the actual experiment content):

```text
experiment1instruction -> experiment1 -> experiment2instruction -> experiment2 
```

> there are three other slides (instruction -> workerID -> statistics)
> that will almost always be necessary.  
> if you do need them removed, further updates may be required to prevent
> the code from breaking.

> the statistics slide is also controlled by a variable called `self.useStatistics`
> turn this on/off in the .js file.

**Table of Contents**
1. [updating self.allStates](#updating-selfallstates)
2. [updating the HTML](#updating-the-html)

---

## updating self.allStates
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

---

## updating the HTML

### creating new divs

Since we have added more slides and also renamed some slides, we'll need to make
changes to reflect that in the HTML file.

First, let's rename the div that depends on `questionSlide` state name. You can ignore
the other logic in the ng-if directive for the moment.

```html
<div id="experiment1_content" ng-if="RC.state == 'experiment1_content' && ...></div>
```

Next, we'll add one div for each of the other three slides we added to `self.allStates`.
You can copy and paste the div we just renamed for the other three states, making
sure to give them different id names and ensuring the state logic in ng-if is correct. We'll
cover how to change the contents later.

```html
<div id="experiment1_instruction" ng-if="RC.state == 'experiment1_instruction' && ..."></div>
<div id="experiment1_content" ng-if="RC.state == 'experiment1_content' && ..."></div>
<div id="experiment2_instruction" ng-if="RC.state == 'experiment2_instruction' && ..."></div>
<div id="experiment2_content" ng-if="RC.state == 'experiment2_content' && ..."></div>
```

At the moment, if you were to create an instance of this Experiment, there would be a lot of
pages that look the same. So before we test this for the first time, let's add some
text to distinguish each of the divs.

Inside each of the `<div></div>` tags, add an unique identifier as text anywhere outside
other tags. For example:
```html
<div id="experiment1_instruction" ng-if="RC.state == 'experiment1_instruction' && ...">
    hello Experiment1 Instructions slide!
    <div>...</div>
</div>
```

Creating an instance of the experiment right now would work, but it would just display
a page with a text box, cycling through the contents of the provided csv file. 
So before testing this HTML file, let's add some instructions so the changes are
more obvious and visually recognizable.

---

Continue to [Adding Instructions](02-adding-instructions.md)
