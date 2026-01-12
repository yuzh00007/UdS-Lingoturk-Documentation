# Timing Trials

## JS
define a variable to hold a start time
```js
self.startTime = 0
```

easiest to probably handle this in the `nextQuestion()` function:
```js
this.nextQuestion = function(ans) {
    const endTime = performance.now()
    const timeTaken = endTime - self.startTime
    self.startTime = endTime
}
```

then save `timeTaken` in your answer