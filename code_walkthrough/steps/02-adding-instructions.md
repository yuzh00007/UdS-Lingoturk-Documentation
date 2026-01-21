# Adding Instructions

**Table of Contents**
1. [Experiment 1 Instructions](#experiment-1-instructions)
2. [Experiment 2 Instructions](#experiment-2-instructions)
3. [Testing the HTML](#testing-the-html)
4. [Common Errors](#common-errors)

Now that we have the slides structure completed and set up, 
let's add some content to them. 

Starting with the easiest part, which is displaying text in the form of instructions.

## Experiment 1 Instructions
In this section, the only thing required are instructions and potentially some images
to help the participants understand what they will be doing in the first part of the
experiment.

Since this is very heavily text based, all of this information can be hardcoded 
into the HTML. Use `div`s to hold the text information and create a button
to call `RC.next()` to advance to the next slide.

Things to note:
- add these classes `class="panel panel-primary"` to the instruction `divs` in order to 
to make panels show up. otherwise, only text will appear. 
- optionally, the `panel-heading` class creates a header above the instructions. use this to label the slides.
- remove the logic `&& RC.questionIndex == $index` from the ng-if directive, not necessary here. 
- remove `ng-repeat="question in RC.questions"` - instructions is just a single page.

Here is what the `experiment1_content` div should look like: 

```html
<div id="experiment1_instruction" class="panel panel-primary" ng-if="RC.state == 'experiment1_instruction'" style="width:90%; margin:auto">
    <div class="panel-heading" style="font-weight: bolder ;">Part 1 Instructions</div>
    <div class="panel-body">
        <p style="font-size: 20px">
            In this experiment, you will be presented with a picture and three choices.
            Please choose the choice that best defines the image.

            <br>
            <br>

            You will also be presented with a textbox. If you think there is a better description
            than the three choices presented, please provide an alternative.
        </p>
        <button ng-click="RC.next()" type="button" class="btn btn-default" style="float:right ; margin-top:20px">Next</button>
    </div>
</div>
```


## Experiment 2 Instructions
Follow the same procedure as the previous instruction slide, 
making sure to update the ng directive logic as well as the ID name. 

```html
<div id="experiment2_instruction" class="panel panel-primary" ng-if="RC.state == 'experiment2_instruction'" style="width:90%; margin:auto">
    <div class="panel-heading" style="font-weight: bolder ;">Part 2 Instructions</div>
    <div class="panel-body">
        <p style="font-size: 20px">
            In the following section, you will be presented with a sentence.
            Please rate the oddity of the sentence on the provided slider.
        </p>
        <button ng-click="RC.next()" type="button" class="btn btn-default" style="float:right ; margin-top:20px">Next</button>
    </div>
</div>
```


## Testing the HTML

With the changes made to the two instruction pages, let's create an instance of the
current experiment to check that the slide structure is working.

But first, go to the JavaScript file and comment out the two experiment content pages,
so we are left with the following `self.allStates`. This way, only the two 
instruction slides will be shown. 

```js
self.allStates = [
    "instructionsSlide",
    "workerIdSlide",
    "statisticsSlide",
    "experiment1_instruction",
    // "experiment1_content",
    "experiment2_instruction",
    // "experiment2_content"
];
```

## Common Errors

- Make sure that all the tags in the HTML file line up. 
If all the elements are on screen at once, 
it is likely caused by a mismatched `<div>` tag.

- Make sure that IDs in each `div` is correctly named
and that the ng-init logic is correct.

---

Continue to [Data Preprocessing](03-data-preprocessing.md)  
