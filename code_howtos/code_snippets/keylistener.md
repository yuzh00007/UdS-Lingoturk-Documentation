# Keyboard Listener

## Option 1: Basic
```js
document.addEventListener('keydown', async (e) => {
    if (e.key === 'a' || e.key === 'A') {
        console.log("a pressed")
    }
})
```
> NOTE: There is a very slight difference in using `keydown` vs `keyup`: an event handler 
> for `keyup` will have access to the new letter input. 

## Option 2: Adding & Removing Listener 
define the callbacks
```js
// on press, change color
const spaceKeyDownCallback = event => {
    if(event.code === "Space"){
        space_clicked_timestamp.push(full_experiment_audio.currentTime);
        $("#experiment1_content").css("background-color", "#edf5fd");
    }
}
// on release, reset to before key press
const spaceKeyUpCallback = event => {
    if(event.code === "Space"){
        $("#experiment1_content").css("background-color", "white");
    }
}
```

add the listeners
```js
document.addEventListener("keyup", spaceKeyUpCallback)
document.addEventListener("keydown", spaceKeyDownCallback)
```

removing listeners if necessary. you MUST have the callback setup. if the Event you're 
trying to remove is not registered, the remove function will not do anything.
```js
document.removeEventListener('keydown', spaceKeyDownCallback);
document.removeEventListener('keyup', spaceKeyUpCallback);
```