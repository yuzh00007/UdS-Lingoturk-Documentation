# Experiment Slide Structure

Experiments in Lingoturk are run in a single web page (i.e. refreshing the page will
immediately restart the experiment). So what if we have multiple tasks and need to show
the participants a lot of different UI setups? We can use Angular directives to hide
and show HTML elements. And to facilitate the directives, we will introduce "slides" or
"states". 

## Managing State Overview

There are two variables to be aware of here: `self.showMessage` and `self.state`.
By setting these two variables to different values, you control what is shown
by the Angular directives.

> of course, you can introduce new variables and make updates to the HTML to
> utilize your new variable. `self.showMessage` and `self.state` will always 
> be available in the starter code.
 
If you check the HTML file, you will see three Angular directives that are controlled
by `self.showMessage`. 
```html
<div ng-if="RC.showMessage == 'none'" ...></div>
<div ng-if="RC.showMessage == 'nextSubList'" ...></div>
<div ng-if="RC.showMessage == 'goodBye'" ...></div>
```

Under the case where showMessage is none, four slides are controlled by the
`self.state` variable. 
```html
<div ng-if="RC.state == 'instructionsSlide'" ...></div>
<div ng-if="RC.state == 'workerIdSlide'" ...></div>
<div ng-if="RC.state == 'statisticsSlide'" ...></div>
<div id="experiment_content" ng-if="RC.state == 'questionSlide' ..."></div>
```

### self.allStates

In the `$(document).ready()` main function, you will find a list variable called
`self.allStates`. The function `self.next()` advances through this list. So any time
in your experiment, this function is called, we progress through the states, showing
different slides with every state change. Often, the `self.next()` function is tied
to a button on the UI that advances to the next slide.
