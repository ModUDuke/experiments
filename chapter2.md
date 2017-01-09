---
[comment]: # (Course information) 
title       : Exercise Title
description : This exercise does something
attachments :
video_link : https://vimeo.com/179938122


--- 
[comment]: # (First exercise, set type to video)
type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1
[comment]: # (Title) 
## Introduction to Experiments
[comment]: # (Link to video) 
*** =video_link
//player.vimeo.com/video/179938122


--- 
[comment]: # (Second exercise, set tupe to multiple choice) 
type:MultipleChoiceExercise lang:r xp:100 skills:1
[comment]: # (Title) 
## Problem 1: Something
[comment]: # (Problem text) 
This is a question
[comment]: # (Choices) 
*** =instructions
- Answer 1
- Answer 2
- Answer 3
- Answer 4
[comment]: # (Hints) 
*** =hint
- Here is a useful hint: Answer 3 is the right answer
[comment]: # (Not clear whether this syntax is necessary)   
*** =pre_exercise_code
```{r}
#none
```
[comment]: # (Feedback dependent on answer. test_mc identifies which is correct )   
*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Well done"
msg4 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```


--- 
[comment]: # (Third exercise, set type to normal to code with R) 
type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1
[comment]: # (Title) 
## Problem 2: Something Different
[comment]: # (Problem text)
This describes (in general terms) what you need to do.
[comment]: # (Specific Instructions)
*** =instructions
- Do this something with `variable`
- Do  something else with `key term` 
[comment]: # (Hint)
*** =hint
- This is a useful hint
[comment]: # (Data for exercise)
*** =pre_exercise_code
```{r}
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
```
[comment]: # (Initial code written in R workspace)
*** =sample_code
```{r}
# Useful initial code
```
[comment]: # (Ideal way to solve problem)
*** =solution
```{r}
# Solution and ideal way to solve problem. For example, imagine we want the user to add 2+2 and store result in "x"
x <- 2+2
```
[comment]: # (Check to determine if student was correct)
*** =sct
```{r}
test_object("x")
success_msg("Good work!")
```
[comment]: # (The above tests if x contains the right value. If we don't care how they arrive at the solution (i.e. x<-4 would be an accurrate solution), then this is enough. More options and detail for syntax described at: https://github.com/datacamp/testwhat/wiki
