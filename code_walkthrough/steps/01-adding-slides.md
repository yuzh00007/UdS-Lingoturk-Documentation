# Adding Slides

This experiment will follow a basic general set up for moving between parts of the
experiment: on every slide, put a "Next" button. When clicked, the experiment will 
advance to the next slide. If the slide is an experiment slide (i.e. the actual task),
the button will display the next question until all the questions are shown.

The slide structure for the experiment will be an instruction slide appearing before
the actual experiment content:

```text
Slide for Instructions -> Slide with Experiment Content (repeated for each question)
```

> there are three other slides (instruction -> workerID -> statistics)
> that will almost always be necessary for all experiments.  
> if you do need them removed, further updates may be required to prevent
> the code from breaking.

> the statistics slide is also controlled by a variable called `self.useStatistics` -
> turn this on/off in the .js file.

**Table of Contents**
1. [General Process](#general-process)
2. [Updating self.allStates](#updating-selfallstates)
3. [Updating the HTML](#updating-the-html)

---

## General Process
Any time slides need to be added, follow this general process:
1. add name of state (could be anything) to `self.allStates` list
2. add new `<div>` next next to other state `<divs>`
3. add `ng-if` logic to the new `<div>`, ensuring name matches allStates

## updating self.allStates
The starter HTML code contains a div with id `experiment_content` that is displayed 
whenever `self.state` is set to `questionSlide`. That's the logic this portion of the 
HTML correponds to.

```html
<div id="experiment_content" ng-if="RC.state == 'questionSlide' ...>
```

To add any new slides into the 
experiment, the first step is always to update the states list. 

Order matters in this list since the base logic
will iterate through the states one by one (this is changeable but is beyond the
scope of this tutorial). 

Add the instruction state to the Experiment Type by adding 
to this list in the JS code:
```javascript
self.allStates = [
    "instructionsSlide",
    "workerIdSlide",
    "statisticsSlide",
    "experimentInstructionSlide",  // add this
    "questionSlide",  
];
```

> Note that there is already a slide called "instructionsSlide", this is the first
> page that is provided to the participants containing the main instructions. So,
> the experiment instruction slide needs to be called something else.

---

## updating the HTML

After updating the states list, the next step to make the slide appear is by adding
new code to the HTML file.

Here are the steps:
1. Create a `div` for the new intruction slide added to `self.allStates`.
2. Copy and paste the `questionSlide` div. 
3. Update the div
   - provide a different ID for the element
   - update the ng-if logic by updating the name of the state

The HTML should contain these two divs:

```html
<div id="experiment_instructions" ng-if="RC.state == 'experimentInstructionSlide' && ..."></div>
<div id="experiment_content" ng-if="RC.state == 'questionSlide' && ..."></div>
```

At the moment, an instance of this Experiment Type would contain many pages 
with the same content. So before testing it for the first time, update the instruction
page in order to make it visually differentiable.

Inside the instruction div, add a message below the main content comment. For example:
```html
<div id="experiment_instructions" ng-if="RC.state == 'experimentInstructionSlide' && ...">
    <!-- the main content of the experiment goes here -->
    hello world, this is the Experiment Instructions slide!
    <div>...</div>
</div>
```

Create an instance of the experiment to make sure these changes are working. 
The experiment should run through all the states as listed in `self.allStates`
(except for the statistics slide, which is only shown if manually turned on in the 
JS file). The "hello world" message should show up and with each click, the page 
will update and display each row of the CSV file. When iteration is completed, 
the content page (without the hello world message) will appear. 
One more click and a submission page will be displayed. 

This is a good start, but the Next button doesn't really do what it needs to do.
In the next section, changes to the Instruction slide should make this experiment
function more like what is expected.


---

Continue to [Adding Instructions](02-adding-instructions.md)
