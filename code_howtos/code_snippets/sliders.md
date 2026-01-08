# Sliders

## HTML
<html>
    <head>
        <style>
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
        </style>
    </head>
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
</html>

## JS

```js
// to display value
const odditySlider = document.getElementById("odditySlider");
const oddityLabel = document.getElementById("sliderLabel");
odditySlider.oninput = function () {
    oddityLabel.innerHTML = this.value + "%"
};

// to get value


```

## CSS


## Forcing an Answer

The cirlce is not displayed by default.
Taken from [this SO post](https://stackoverflow.com/a/36545855).

