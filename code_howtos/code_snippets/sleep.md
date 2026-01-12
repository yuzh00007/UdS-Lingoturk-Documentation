# sleep(ms) Equivalent

## JS
define this function in your JS file on its own, i.e. outside of everything else
```js
async function sleep(milliseconds){
    return new Promise(resolve => {
        setTimeout(resolve, milliseconds);
    });
}
```

any time you need to call it, make sure the function it is in is async
```js
this.myFunction = async function() {
    // sleeps for 3 seconds
    await sleep(3000);
}
```