## Two Sets of Questions
When there are multiple sets of questions, 

Since only one CSV file was provided when creating this experiment instance,
this single CSV file actually contains two studies worth of material. This is obviously
not ideal... That's where this step comes in. Since this tutorial experiment
has two tasks, it's best to separate the questions into two separate Arrays.

First, define new variables to hold the questions and new indices to iterate through
them. This can be done at the top of the screen with all the other variables.


```js
self.questions_block1 = []
self.questions_block2 = []
self.block1QuestionIndex = 0;
self.block2QuestionIndex = 0;
```

This logic will depend on the CSV file that was provided to the experiment
and will look different from experiment to experiment. It is normal to provide
a CSV file that contains a column that identifies which experiment the row belongs to.


If the variable `self.questions` is no longer in use, i.e. it has been renamed,
all the Slides that use that list need updates to their ng-directive logic.

For example, if two sets of questions are created and named `block1Questions` 
and `block2Questions`, it would make sense for the code to go from this:
```html
<div id="1" ng-if="... RC.questionIndex == $index" ng-repeat="question in RC.questions">
```

to this:
```html
<div id="1" ng-if="... RC.block1QuestionIndex == $index" ng-repeat="question in RC.questions_block1">
<div id="2" ng-if="... RC.block2QuestionIndex == $index" ng-repeat="question in RC.questions_block2">
```
