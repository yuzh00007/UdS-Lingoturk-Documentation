# Sliders

## HTML

```html
<div class="slidecontainer">
    <!-- a label for displaying the slider value -->
    <span id="sliderLabel"></span>

    <!-- slider and labels in a table -->
    <table>
        <tr>
            <td class="labelText">LABEL A</td>
            <td style="padding-bottom: 5px">
                <label for="odditySlider"></label><input type="range" min="0" max="100" class="slider not-clicked" id="odditySlider">
            </td>
            <td class="labelText">LABEL B</td>
        </tr>
    </table>
</div>
```

looks like this without any css applied:
<div class="slidecontainer">
    <table>
        <tr>
            <td class="labelText">LABEL A</td>
            <td style="padding-bottom: 5px">
                <label for="odditySlider"></label><input type="range" min="0" max="100" class="slider not-clicked" id="odditySlider">
            </td>
            <td class="labelText">LABEL B</td>
        </tr>
    </table>
</div>

## JS

```js
// to display value
const odditySlider = document.getElementById("odditySlider");
const oddityLabel = document.getElementById("sliderLabel");
odditySlider.oninput = function () {
    oddityLabel.innerHTML = this.value + "%"
};

// to get value
question.answer = odditySlider.value;

```

## CSS

### Forcing an Answer
The slider has a starting value by default. You can force a response by hiding
the circle and only showing it when the user clicks on the slider for the first time.
Hence the reason there is a .clicked style and a .not-clicked style. 

-webkit-slider-thumb works on almost all browsers. -moz-range-thumb covers
the Firefox edge case.

Taken from [this SO post](https://stackoverflow.com/a/36545855).

```css
.sliderValue {
    padding-top: 5px;
    width: 60px;
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

.clicked::-webkit-slider-thumb {
   -webkit-appearance: none;
   appearance: none;
   width: 18px;
   height: 18px;
   border-radius: 50%;
   background: #327ba8;
   cursor: pointer;
   opacity: 100;
}

.not-clicked::-webkit-slider-thumb {
   opacity: 0;
}

.clicked::-moz-range-thumb {
   width: 18px;
   height: 18px;
   border-radius: 50%;
   background: #327ba8;
   cursor: pointer;
   opacity: 100;
}

.not-clicked::-moz-range-thumb {
   opacity: 0;
}
```



