---
title       : Exercise Title
description : This exercise does something
attachments :
video_link : https://vimeo.com/179938122
[comment]: # (Course information. Note, due to markdown constraints, all comments below code they refer to) 


--- key:9772960bd4
type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1
[comment]: # (First exercise, set type to video)
## Introduction to Experiments
[comment]: # (Title) 
*** =video_link
//player.vimeo.com/video/179938122
[comment]: # (Link to video) 


--- key:25754115c7
type:MultipleChoiceExercise lang:r xp:100 skills:1
[comment]: # (Second exercise, set tupe to multiple choice) 
## Problem 1: Something
[comment]: # (Title) 
This is a question
[comment]: # (Problem text) 
*** =instructions
- Answer 1
- Answer 2
- Answer 3
- Answer 4
[comment]: # (Choices) 
*** =hint
- Here is a useful hint: Answer 3 is the right answer
[comment]: # (Hints) 

*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Well done"
msg4 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```
[comment]: # (Feedback dependent on answer. test_mc identifies which is correct )   


--- key:701b063e55
type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1
[comment]: # (Third exercise, set type to normal to code with R) 
## Problem 2: Something Different
[comment]: # (Title) 
This describes (in general terms) what you need to do.
[comment]: # (Problem text)
*** =instructions
- Do this something with `variable`
- Do  something else with `key term` 
[comment]: # (Specific Instructions)
*** =hint
- This is a useful hint
[comment]: # (Hint)
*** =pre_exercise_code
```{r}
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
```
[comment]: # (Data for exercise)
*** =sample_code
```{r}
# Useful initial code
```
[comment]: # (Initial code written in R workspace)
*** =solution
```{r}
# Solution and ideal way to solve problem. For example, imagine we want the user to add 2+2 and store result in "x"
x <- 2+2
```
[comment]: # (Ideal way to solve problem)
*** =sct
```{r}
test_object("x")
success_msg("Good work!")
```
[comment]: # (Check to determine if student was correct)
[comment]: # (The above tests if x contains the right value. If we don't care how they arrive at the solution (i.e. x<-4 would be an accurrate solution), then this is enough. More options and detail for syntax described at: https://github.com/datacamp/testwhat/wiki
