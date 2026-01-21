# Adding Experiment 1 Functionality 

**Table of Contents**
1. [Button Functionality](#button-functionality)
2. [Force a Selection](#force-a-selection)

---

## Button Functionality
Create a function called `confirmSelect` in the JS that will be called from the HTML with a ng-directive.
This function adds a class called `selected` to the selected button and removes the 
same from the other two buttons on the page.

> `$("#" + opt)` is a JQuery request for an element on the webpage. 
> In this case, the `"#"` looks for an element with an ID. 
> The ID which is provided through the concated variable `opt`.

```js
this.confirmSelect = function (selectedOpt) {
    // the 3 options created in the HTML
    let opts = ["opt1", "opt2", "opt3"]
    
    for (const opt of opts) {
        if (opt !== selectedOpt) {
            $("#" + opt).removeClass("selected")
        } else {
            $("#" + opt).addClass("selected")
        }
    }
}
```

Before changing the HTML, update the CSS file to add a background color 
to any UI element with the two classes `btn` and `selected`. This `selected` 
class is the one the `confirmSelect` function is adding and removing to the
3 option buttons. The `btn` is defined in the HTML.

> NOTE: chain classes like this to get very specific CSS selectors

```css
.btn.selected {
    background-color: lightblue;
}
```

Add the `ng-click` directive to each button definition, providing it with the
previously defined function and an argument that corresponds to the button. 
In this example, `opt2` is passed in as the argument because this is the second button.

> be careful with single and double quotes when passing arguments

```html
<button id="opt2" ... ng-click="RC.confirmSelect('opt2')">
    {{question.opt2}}
</button>
```

<details>
<summary>
Refresh the instance and check that the buttons change colors when selected.
</summary>
    <image src="../images/exp1-blue-selection.png"></image>
</details>

---

## Force a Selection

Clicking on the "Next" button will trigger `nextQuestion` no matter what. 
In order to force a selection, a check for answer must occur before moving on to the
next question. 

Since a `selected` class is added to any of the defined buttons when they are clicked,
it is possible to check for the existance of a button with this class inside 
a try-catch block. If an error is thrown, then alert the participant that they must
answer the question and make the button do nothing.

```js
this.nextQuestion = function(blockNumber=1) {
    try {
        document.querySelector("button.selected").innerText
    } catch {
        alert("Please answer the question before continuing");
        return;
    }
    
    // ...
}
```

---

**Continue to [Saving Experiment 1 Responses](06-saving-exp1-responses.md)**
