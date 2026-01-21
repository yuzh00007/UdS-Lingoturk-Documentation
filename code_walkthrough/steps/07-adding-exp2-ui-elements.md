# Creating Experiment 2 UI Elements

In the second task, participants are shown an image and a sentence. 
They are asked to judge the sentence on how odd it sounds. 
Participants will provide their answers with via a slider.

> NOTE: Experiment 2 will differ from Experiment 1 in many ways because
> this task will focus on using vanilla Javascript to show how JS can be
> used as well.

**Table of Contents**
1. [Focusing on Experiment 2 Content](#focusing-on-experiment-2-content)
2. [Creating UI Elements](#creating-ui-elements)
    - [Adding an Image](#adding-an-image)
    - [Adding Text](#adding-text)
    - [Adding a Slider](#adding-a-slider)

---

## Focusing on Experiment 2 Content

<details>
<summary>
When working on Experiment 1, other slides were commented on. Make sure to
check the content slide for Experiment 2 is active before moving on. 
</summary>

```js
self.allStates = [
    "instructionsSlide",
    "workerIdSlide",
    "statisticsSlide",
    // "experiment1_instruction",
    // "experiment1_content",
    // "experiment2_instruction",
    "experiment2_content"
];
```
</details>

---

## Creating UI Elements

Unless it was changed while setting up the slide order, 
many of the divs inside the `experiment2_content`, still have IDs labeling
them as belonging to Experiment 1. Update these IDs from 1 to 2 for sanity's sake.

Next, similar to the first experiment, remove all the code under the `experiment_body_2` div
except for the button.

### Adding an Image

Image `src` will be populated with code, so it is not provided in its definition.

```html
<img id="experiment2image" class="exp2img" style="width:20%" >
```

### Adding Text

Add some divs and paragraphs to hold text in the HTML. 
We can hardcode a question into the `<p id="scaleQuestion">` tag in the current 
example task. However, imagine the question phrasing was a variable in the study,
then it makes sense to have a function to dynamically update the
question instead of hardcoding it.

```html
<div align="center">
    <p id="scaleSentence"></p>
</div>

<br>

<div align="center">
    <p id="scaleQuestion"></p>
</div>
```

### Adding a Slider

Add the slider. The table can be used, like in this instance, to arrange objects
and text neatly. 

```html
<div id="oddityDiv" align="center">
    <div class="slidecontainer">
        <span id="sliderLabel"></span> 
        <table>
            <tr>
                <td class="labelText">Not Odd</td>
                <td style="padding-bottom: 5px">
                    <label for="odditySlider"></label><input type="range" min="0" max="100" class="slider not-clicked" id="odditySlider">
                </td>
                <td class="labelText">Very Odd</td>
            </tr>
        </table>
    </div>
</div>
```

Add some styling. 

```css
.labelText {
  font-size: small;
  padding-top: 7px;
 }

table, th, td {
  border: none;
  padding: 5px;
  vertical-align: bottom;
  text-align: center;
}

.slider {
    -webkit-appearance: none;
    width: 100%;
    height: 15px;
    border-radius: 5px;
    background: #d3d3d3;
    outline: none;
    opacity: 0.7;
    -webkit-transition: .2s;
    transition: opacity .2s;
}
```

<details>
<summary>
Unfortunately, since most of the UI is still missing functionality,
only the slider shows up. Even so, by using the Inspector, you can make sure
that in fact all the divs are working properly.
</summary>
<img src="../images/exp2-ui-elements.png">
</details>


--- 

**Continue to [Adding Experiment 2 Functionality](08-adding-exp2-functionality.md)**
