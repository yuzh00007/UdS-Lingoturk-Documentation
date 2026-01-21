# Data Preprocessing

**Table of Contents**
1. [Creating New Arrays](#creating-new-arrays)
2. [Updating Slides](#updating-slides)

---

## Creating New Arrays

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

Next, here is logic to separate out the data into the two different blocks.
For this CSV file, the second task has an empty "opt3" column, which can be
used to filter the questions.

This logic will depend on the CSV file that was provided to the experiment
and will look different from experiment to experiment. It is normal to provide
a CSV file that contains a column that identifies which experiment the row belongs to.

```js
self.questions.shift(); // drop header
if(self.shuffleQuestions){
    shuffleArray(self.part.questions);
}
self.questions.forEach(element => {
    if (!element["opt3"]) {
        self.questions_block2.push(element)
    } else {
        self.questions_block1.push(element)
    }
})
```

> NOTE: the load function has 3 different branches - this represents all the
> different ways data could be loaded (across different platforms). Make sure that any
> data loading changes are applied to all the branches.

---

## Updating Slides

Since `self.questions` is no longer in use, since it contains both sets of questions,
all the previous created Slides need updates in their ng-directive logic. 

Ensure that the `ng-if` and `ng-repeat` logic now references the newly created 
questions Arrays instead.

```html
<div id="experiment1_content" ng-if="RC.state == 'experiment1_content' && RC.block1QuestionIndex == $index" ng-repeat="question in RC.questions_block1" style="width:90%; margin:auto">
<div id="experiment2_content" ng-if="RC.state == 'experiment2_content' && RC.block2QuestionIndex == $index" ng-repeat="question in RC.questions_block2" style="width:90%; margin:auto">
```

---

Continue to [Creating Experiment 1 UI Elements](04-adding-exp1-ui-elements.md)
