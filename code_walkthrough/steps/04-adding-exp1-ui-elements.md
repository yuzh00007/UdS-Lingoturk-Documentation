# Creating Experiment 1 UI Elements

The tutorial experiment contains a picture naming task. 
The idea is to display an image, provide a 3FC, then
give the participant the option to type in an alternative name for the image.

<image src="../images/exp1-ui-elements-all.png"></image>

**Table of Contents**
1. [Focusing on Experiment 1 Content](#focusing-on-experiment-1-content)
2. [Creating UI Elements](#creating-ui-elements)
   - [Adding an Image](#adding-an-image)
   - [Adding the Choices](#adding-the-choices)
   - [Adding the Input Text Box](#adding-the-input-text-box)

---
## Focusing on Experiment 1 Content
<details>
<summary>Uncomment the question slide and comment out the instruction slide.
This section will focus on setting up the experiment elements.</summary>

> Remember: both `instructionsSlide` and `workerIdSlide` should stay to ensure
> Lingoturk functions (removing them will require additional code changes)

```js
self.allStates = [
    "instructionsSlide",
    "workerIdSlide",
    "statisticsSlide",
    // "experimentInstructionSlide",
    "questionSlide"
];
```
</details>

---

## Creating UI Elements

In the HTML, locate the `div` with `id="experiment_body_1"`. 
It comes predefined with a `{{question}}` interpolation (more info on interpolation
in [Angular documentation](https://v17.angular.io/guide/interpolation)) and a button
that calls `self.nextQuestion` on click. 
The new elements for this task will be added inside this element as siblings
of the button. 

Delete the question interpolation. The comments can be deleted or left, it does not matter. 

> Note that `questionSlide` is using `ng-repeat` to loop through `RC.questions`
> (which is `self.questions` in the JS file). The data is assigned to the variable 
> `question` as defined in the ng-directive. This can be changed as necessary (this will
> be done in a future step).
>
> This loop is an iteration through the
> lines of the provided CSV file (after any preprocessing steps) used when
> creating the instance. Therefore, every child element can access the information in the
> row of data through the variable `question`.

### Adding an Image
`ng-src` allows the definition of image source through directive related variables.
Make sure the folder name matches the name of the Experiment. Ensure the path exists
in the local environment during development.

> `dynamicAssets/` represents the local path `lingoturk/public/`

Add this image element to the HTML, using a Angular expression to dynamically 
provide the path of the image. 

```html
<img class="exp1Image" ng-src="/dynamicAssets/images/Experiments/TutorialExperiment/{{question.imagePath}}">
```

Add the folowing to the CSS file in order to ensure the images are not too large.
```css
.exp1Image {
    width: 20%;
}
```

> The tutorial is resizing images to demonstrate the ability to resize images with
> the CSS stylesheet. However, 
> it is usually advisable to resize the images with editing software 
> as a preprocessing step instead of with code.  


<details>
<summary>The experiment will display a random image from the CSV. 
Clicking on the Next button will continue to the next image
until all images are looped through. And a submission prompt is presented.
</summary>
    <image src="../images/exp1-image-only.png"></image>
</details>


### Adding the Choices
The multiple choice options will be presented horizontally. Note the use of 
double-brackets to dynamically display the multiple choices (as defined in the CSV).

All the buttons are created with an ID - these will be used later when adding
functionality to the buttons.

> NOTE: elements can have many different classes, which are used to group 
> similar uses and styles. but elements can only have a single ID, which must be
> unique from all other elements currently displayed on screen. 

Add this code snippet below the image:

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

The buttons belong to the `fcButtons` class,  
this CSS snippet should make the buttons a bit more pleasant to look at.
```css
.fcButtons {
    text-align: center;
    width:150px;
    margin-top:20px;
    color: #327ba8;
}
```

> A common issue with buttons during development is clicking a button, the webpage refreshes
> and displays an `Action Not Found For request 'POST /mturk/externalSubmit'` error.
> Most likely it's because the button is missing this in its definition: `type="button"`  

<details>
<summary>Refreshing the experiment instance now should display both the image and the multiple choice
options. These buttons do not have function yet, so clicking on them will do nothing.</summary>
    <image src="../images/exp1-image-and-mc.png"></image>
</details>

### Adding the Input Text Box
Code for a simple textbox. Add this below the multiple choices.

```html
<label>
    <input id="altNameInput" type="text" class="form-control" placeholder="Enter alternative name here">
</label>
```

> Note: the `placeholder` option is text that will be displayed inside the box when
> it is empty.

---

<details>
<summary>Even though they might not yet have function,
all the planned UI elements should be complete!
Feel free to add little flourishes here and there. Try changing the CSS and 
customizing colors, text size, and font. 
</summary>
    <image src="../images/exp1-ui-elements-all.png"></image>
</details>

> To easily put some vertical space between UI element, optional breaks `<br>` tags
> can be added. NOTE: these do not have end tags, i.e. `</br>` is not a thing.


Continue to [Adding Experiment 1 Functionality](05-adding-exp1-functionality.md)
