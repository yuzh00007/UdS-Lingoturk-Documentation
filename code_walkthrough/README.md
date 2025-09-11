# Code Walkthrough Introduction

This document will try to explain some portions of the code 
in a semi-interactive manner, including information I had to figure
out when I first used LingoTurk to create an experiment for a study.

We will start with an empty experiment type and work it into the PictureNaming
experiment, such that this document will cover the code required to do the 
basic changes you will want to make when creating experiments. 

Each section, we'll add one thing to the experiment until, by the end, 
we will have a working project that is able to submit responses to your
local Lingoturk server's database.

This will not be an incredibly in depth lesson in Javascript or front-end
development, as this was the first time I have used .js beyond programming 
assignments since beginning to work with code. So if there are odd and strange
coding practices that don't quite align with normal JS practices, that's on me.

# Prerequisites

You will need:
- the local copy of the Lingoturk repository, cloned from
https://github.com/FlorianPusse/Lingoturk.
- fully set up pgadmin and Lingoturk backend
- an IDE of some sort (IntelliJ offers education licenses for free)
- basic understanding of Lingoturk (see: other documentation pages)

Quickly create an experiment type called "TutorialExperiment" that has two
fields. We will use this for the code walkthrough.
- question (String)
- filepath (String)


# Table of Contents

1. [The Very Basics of Web Design](./01-Basic-Overview.md)
2. [Quick Code Rundown](./02-Code-Rundown.md)
3. Experiment Slide Structure
4. Iterating Through Questions
5. Adding a Textbox
6. Adding an Image
7. Adding a Key Handler on "Enter" Keypress
8. Displaying a Progress Tracker
9. Submitting the Answers
