---
title       : Exercise Title
description : This exercise does something
attachments :
video_link : https://vimeo.com/179938122


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:bfc8a2d235
## Introduction to Experiments
*** =video_link
//player.vimeo.com/video/179938122


--- type:MultipleChoiceExercise lang:r xp:50 skills:1  key:1ecca31bfa
## Problem 1: Something key:1ecca31bfa
This is a question
*** =instructions
- Answer 1
- Answer 2
- Answer 3
- Answer 4
*** =hint
- Here is a useful hint: Answer 3 is the right answer
*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Well done"
msg4 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```


--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:fe659fa2fc
## Problem 2: Something Different
This describes (in general terms) what you need to do. For this example, what does 2+2 equal? key:fe659fa2fc
*** =instructions
- Do this something with `variable`
- Do  something else with `key term` 
*** =hint
- This is a useful hint
*** =pre_exercise_code
```{r}
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
```
*** =sample_code
```{r}
# Useful initial code
```
*** =solution
```{r}
# Solution and ideal way to solve problem. For example, imagine we want the user to add 2+2 and store result in "x"
x <- 2+2
```
*** =sct
```{r}
test_object("x")
success_msg("Good work!")
```