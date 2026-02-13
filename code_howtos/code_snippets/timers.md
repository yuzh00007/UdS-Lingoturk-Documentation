# Timers and Countdown

## HTML

Most important part of this is that `{{countdown}}` interpolation.

`ng-init` will immediately run a function containing the logic for the countdown.

```html
<div ng-init="RC.startCountdown()">
    <span>COUNTDOWN: {{countdown}}</span>
</div>
```

## JS

Define a function to hold all the countdown logic.

The idea of a countdown is simple: 
- get the current time
- do some math to get when the timer expires
- update the display once a set amount of time as passed 

Create an inner function to update the `$scope.countdown` with the remaining
time left on the timer. This value is what the `{{countdown}}` interpolation will display.

Use Angular's `$timeout` to call this update function every 1000ms. 

> Note: as written in this code snippet, the `$timeout` call will
> continue to happen every 1000ms, even after the deadline has been reached.

```js
this.startCountdown = function () {
    // define amount of time for countdown
    $scope.countdown = 8;
    // calculate deadline
    const deadline = new Date().getTime() + $scope.countdown * 1000; 

    function updateCountdown() {
        // get current time 
        const now = new Date().getTime();
        // calculate remaining time, assign to countdown
        $scope.countdown = Math.max(0, Math.ceil((deadline - now) / 1000));
        
        // every 1000ms, call updateCountdown
        $timeout(updateCountdown, 1000);
    }

    // initial call
    updateCountdown();
}
```
