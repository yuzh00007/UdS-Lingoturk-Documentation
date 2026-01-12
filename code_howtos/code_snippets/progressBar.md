# Progress Bar

## HTML
```html
<div> Progress:
        <progress id="experimentProgressBar" class="audioProgressBar" value="0" max="1"></progress>
</div>
```
<div> Progress:
        <progress id="experimentProgressBar" value="0" max="1"></progress>
</div>

## JS
```js
// progress bar update
document.getElementById("experimentProgressBar").value = self.questionIndex / self.questions.length
```
