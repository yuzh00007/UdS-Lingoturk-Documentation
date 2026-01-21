# Creating Experiment 1 UI Elements

The first task will picture naming. Display an image, provide a 3FC, then
give the participant the option to type in an alternative name.

**Table of Contents**
1. [Focusing on Experiment 1 Content](#focusing-on-experiment-1-content)
2. [Creating UI Elements](#creating-ui-elements)

---
## Focusing on Experiment 1 Content
<details>
<summary>Uncomment Experiment 1 slide and comment out the instruction slides.
This section will focus on getting Experiment 1 up and running.</summary>

> Remember: both `instructionsSlide` and `workerIdSlide` should stay to ensure
> Lingoturk functions (removing them will require additional code changes)

```js
self.allStates = [
    "instructionsSlide",
    "workerIdSlide",
    "statisticsSlide",
    // "experiment1_instruction",
    "experiment1_content",
    // "experiment2_instruction",
    // "experiment2_content"
];
```
</details>

---

## Creating UI Elements

Define the image, multiple choice options, and a textbox inside the
`id="experiment_body_1"` div.
Keep the already defined `button`, but all other comments and code can be removed.

Note that `experiment1_content` is using `ng-repeat` to loop through `RC.questions_block1`
(which is `self.questions_block1` in the JS file). The data is assigned to the variable 
`question` as defined in the ng-directive. This can be changed as necessary (this will
be done in a future step).

This loop is an iteration through the
lines of the provided CSV file (after any preprocessing steps) used when
creating the instance. Therefore, every child element can access the information in the
row of data through the variable `question`.

### Adding an Image
`ng-src` allows the definition of image source through directive related variables.
Make sure the folder name matches the name of the Experiment. In a local environment,
ensure the path used here exists.

> `dynamicAssets/` represents the local path `lingoturk/public/`. 

```html
<img class="exp1Image" ng-src="/dynamicAssets/images/Experiments/TutorialExperimentExperiment/{{question.imagePath}}">
```

Add the folowing to the CSS file in order to ensure the images are not too big.
```css
.exp1Image {
    width: 20%;
}
```



<details>
<summary>With just this bit of code, the experiment will display a randomized image from the CSV. 
Clicking on the Next button will continue to the next image
until all images are looped through. And a submission prompt is presented.
</summary>
    <image src="../images/exp1-image-only.png"></image>
</details>


### Adding the Choices
The multiple choice options will be presented horizontally. Note the use of 
double-brackets to programatically add the options (as defined in the CSV).

All the buttons are created with an ID - these will be used later when adding
functionality to the buttons.

> NOTE: elements can have many different classes, which are used to group 
> similar uses and styles. but elements can only have a single ID, which must be
> unique from all other elements currently displayed on screen. 

```html
<div class="3fc">
    <button id="opt1" type="button" class="btn btn-default fcButtons">
        {{question.opt1}}
    </button>
    <button id="opt2" type="button" class="btn btn-default fcButtons">
        {{question.opt2}}
    </button>
    <button id="opt3" type="button" class="btn btn-default fcButtons">
        {{question.opt3}}
    </button>
</div>
```

Since the buttons are created with the `fcButtons` class,  
here is some CSS to make the buttons more pleasant to look at by adding style
properties to that class.
```css
.fcButtons {
    text-align: center;
    width:150px;
    margin-top:20px;
    color: #327ba8;
}
```

> A common issue with buttons during develop is clicking a button, the webpage refreshes
> and displays an `Action Not Found For request 'POST /mturk/externalSubmit'` error.
> The issue is the button missing this line in its definition: `type="button"`  

<details>
<summary>Refreshing the experiment instance now should display both the image and the multiple choice
options. These buttons do not have function yet, so clicking on them will do nothing.</summary>
    <image src="../images/exp1-image-and-mc.png"></image>
</details>

### Adding the Input Text Box
Code for a simple textbox:

```html
<label>
    <input id="altNameInput" type="text" class="form-control" placeholder="Enter alternative name here">
</label>
```

Note the `placeholder` option is the text that will be displayed inside the box when
it is empty.

To easily put some vertical space between each UI element, optional breaks `<br>` tags
can be added. NOTE: these do not have end tags, i.e. `</br>` is not a thing.

<details>
<summary>With this, all the planned UI elements should be complete!</summary>
    <image src="../images/exp1-ui-elements-all.png"></image>
</details>

---

Continue to [Adding Experiment 1 Functionality](05-adding-exp1-functionality.md)
