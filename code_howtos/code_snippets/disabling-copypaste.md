# Disabling Copy Pasting into Textbox

## HTML
you can use these attributes to turn off a lot of things
```html
<input 
    oncopy="return false" 
    onpaste="return false" 
    oncut="return false" 
    ondrag="return false" 
    ondrop="return false"
>
```

## JS
add this snippet to remove ALL cut copy or pasting in your document
```js
$(document).ready(function () {
    .
    .
    
    $(document).on("cut copy paste", function (e) {
        e.preventDefault();
    });
    
    .
    .
}
```
you can use the same to remove cut copy and pasting from a specific element too
```js
document.getElementById("textboxA").on("cut copy paste", function (e) {
    e.preventDefault();
});
```


