# Disabling & Enabling a Button
Or any other element.

## Option 1: with JS

### HTML
```html
<button id="myBtn" ng-click="RC.next()" type="button" class="btn btn-default" disabled>
    Next
</button>
```

### JS
```js
const myBtn = document.getElementById("myBtn");

// switching between disabled and enabled
next_button.disabled = !next_button.disabled;
```

## Option 2: with Angular
### HTML
```html
<button id="myBtn" ng-disabled="question.answer === undefined || question.answer === '' || question.answer == {}" ng-click="RC.next()" type="button" class="btn btn-default">
    Next
</button>
```

When used in an experiment, forces `question.answer` to have non null value in order
for the button to be clickable.
