# Disabling & Enabling a Button
Or any other element.

## HTML
```html
<button id="myBtn" ng-click="RC.next()" type="button" class="btn btn-default" disabled>
    Next
</button>
```

## JS
```js
const myBtn = document.getElementById("myBtn");

// switching between disabled and enabled
next_button.disabled = !next_button.disabled;
```