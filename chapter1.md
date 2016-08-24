---
title       : Getting to Know Your Data
description : This exercise helps you get to know your data better
attachments :
  video_link : https://vimeo.com/179938122

--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:bfc8a2d235
## Design of the Oregon Healthcare Experiment

*** =video_link
//player.vimeo.com/video/179938122

--- type:NormalExercise lang:r xp:100 skills:1 key:1ecca31bfa
## Introduction to Analyzing Experimental Data

Let’s pretend that we’re on a research team that will look at the Oregon Health Insurance Experiment data for insights into improving people’s health results. The first thing any researcher does is to look at the structure of the data, and determining an appropriate method of analysis. 

A simulated version of the Oregon Health Insurance Experiment data, `OHIE`, is available in the workspace.

In this exercise, you will be manipulating the data by trying to divide it into a treatment group and control group.  That will allow us to use an experiment-style analysis to help us answer our research question.

*** =instructions
- Examine the structure of `OHIE`
- Subset the `OHIE` data frame into treatment and control groups
- The treatment variable is a column in `OHIE` called `treatment`
- Call the treatment group `treatmentgroup` and the control group `controlgroup`. 

*** =hint
- Use `str()` to examine the structure of the data

*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","age_19_34_inp","age_35_49_inp","age_50_64_inp")]
```

*** =sample_code
```{r}
# OHIE is available in your workspace

# Check out the structure of OHIE


# Create a new data frame called `treatmentgroup` that contains only treated individuals 


# Create a new data frame called `controlgroup` that contains only control individuals 

```

*** =solution
```{r}
# OHIE is available in your workspace

# Check out the structure of OHIE
str(OHIE)

# Create a new data frame called `treatmentgroup` that contains only treated individuals 
treatmentgroup <- OHIE[OHIE$treatment==1, ]

# Create a new data frame called `controlgroup` that contains only control individuals 
controlgroup <- OHIE[OHIE$treatment==0, ]
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("treatmentgroup")

test_object("controlgroup")

test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e054d70ffa
## Testing for Balancedness Across Experimental gGroups: Part I

Let’s take a look at the demographic makeup of our treatment and control groups to help us understand the kinds of people we have in our dataset, and how balanced the two groups look at first glance.  Hopefully,
we’ll have the same proportions of young people to old people, men and women, and other demographic traits in both the treatment and control groups. For now, a quick manual comparison of these values will give us a sense of what we’ll be dealing with as we move forward.

A simulated version of the Oregon Health Insurance Experiment data, `OHIE`, is available in the workspace. This has been divided into two separate dataframes: `treatmentgroup` and `controlgroup` denoting the treatment and control groups, respectively.

In this exercise, you will be comparing means of some demographic variables to see if the group of patients who did and did not receive health insurance have the same characteristics. If there is “balance” in these variables between the two groups then our analysis will be much easier.

*** =instructions
- Test whether the treatment and control groups have the same average values for the following characteristics: 
- gender (variable `gender_inp`)
- age in 19-34 (variable `age_19_34_inp`)
- age in 50-64 (variable `age_50_64_inp`)
- white (variable `race_white_inp`)
- black (variable `race_black_inp`)
- hispanic (variable `hispanic_inp`)

*** =hint
- Use `mean(x)-mean(y)` to compute the difference in the means of two vectors `x` and `y`
- For vectors that belong to different dataframes, use the $ to call the variable, e.g. `mean(df1$x)-mean(df2$x)` 

*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","age_19_34_inp","age_35_49_inp","age_50_64_inp","race_white_inp","race_black_inp","hispanic_inp")]
treatmentgroup <- OHIE[OHIE$treatment==1 & !is.na(OHIE$treatment),]
controlgroup <- OHIE[OHIE$treatment==0 & !is.na(OHIE$treatment),]
rm(OHIE)
```

*** =sample_code
```{r}
# treatmentgroup and controlgroup are both available in your workspace

# Compute the mean difference in the proportion female (gender_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion between ages of 19-34 (age_19_34_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion between ages of 50-64 (age_50_64_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion white (race_white_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion black (race_black_inp==1) in the treatment and control groups


# Compute the mean difference in the proportion hispanic (hispanic_inp==1) in the treatment and control groups


```

*** =solution
```{r}
# treatmentgroup and controlgroup are both available in your workspace

# Compute the mean difference in the proportion female (gender_inp==1) in the treatment and control groups
mean(treatmentgroup$gender_inp)-mean(controlgroup$gender_inp)

# Compute the mean difference in the proportion between ages of 19-34 (age_19_34_inp==1) in the treatment and control groups
mean(treatmentgroup$age_19_34_inp)-mean(controlgroup$age_19_34_inp)

# Compute the mean difference in the proportion between ages of 50-64 (age_50_64_inp==1) in the treatment and control groups
mean(treatmentgroup$age_50_64_inp)-mean(controlgroup$age_50_64_inp)

# Compute the mean difference in the proportion white (race_white_inp==1) in the treatment and control groups
mean(treatmentgroup$race_white_inp)-mean(controlgroup$race_white_inp)

# Compute the mean difference in the proportion black (race_black_inp==1) in the treatment and control groups
mean(treatmentgroup$race_black_inp)-mean(controlgroup$race_black_inp)

# Compute the mean difference in the proportion hispanic (hispanic_inp==1) in the treatment and control groups
mean(treatmentgroup$hispanic_inp)-mean(controlgroup$hispanic_inp)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

# test_function("mean", args = "object",
#              not_called_msg = "You didn't call `mean()`!",
#              incorrect_msg = "You didn't call `mean(object = ...)` with the correct argument, `object`.")

test_error()

success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:be77016734
## Testing for Balance Across Experimental Groups: Part II

We’ve now seen the basic descriptive information about the people in our data by comparing some average values about their ages, genders, and racial composition in both the treatment and control groups, and they look pretty balanced at first glance. Now we need to check whether these average values hold up as statistically balanced as well. 

A simulated version of the Oregon Health Insurance Experiment data, `OHIE`, is available in the workspace. This has been divided into two separate dataframes: `treatmentgroup` and `controlgroup` denoting the treatment and control groups, respectively.

In this exercise, you will be using a two-sided t-test to analyze if the difference in the means of demographic variables of patients who did and did not receive health insurance are statistically different. If it turns out that the groups are not balanced statistically, then our analysis will have to get more complicated, so let’s hope they pass this test!

*** =instructions
- The way to perfrom a t-test in `R` is with the  `t.test()` function
- Use a two-sided t-test to examine whether or not the treatment and control groups have significantly different average values for the following characteristics: 
- gender (variable `gender_inp`)
- age in 19-34 (variable `age_19_34_inp`)
- age in 50-64 (variable `age_50_64_inp`)
- white (variable `race_white_inp`)
- black (variable `race_black_inp`)
- hispanic (variable `hispanic_inp`)

*** =hint
- Use `t.test(controlgroup$var, treatmentgroup$var, mu=0)` to statistically test that the treatment and control groups are balanced

*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","age_19_34_inp","age_35_49_inp","age_50_64_inp","race_white_inp","race_black_inp","hispanic_inp")]
treatmentgroup <- OHIE[OHIE$treatment==1 & !is.na(OHIE$treatment),]
controlgroup <- OHIE[OHIE$treatment==0 & !is.na(OHIE$treatment),]
rm(OHIE)
```

*** =sample_code
```{r}
# treatmentgroup and controlgroup are both available in your workspace

# Test equality in means of female (gender_inp==1) in the treatment and control groups


# Test equality in means of proportion aged 19-34 (age_19_34_inp==1) in the treatment and control groups


# Test equality in means of proportion aged 50-64 (age_50_64_inp==1) in the treatment and control groups


# Test equality in means of proportion white (race_white_inp==1) in the treatment and control groups


# Test equality in means of proportion black (race_black_inp==1) in the treatment and control groups


# Test equality in means of proportion hispanic (hispanic_inp==1) in the treatment and control groups


```

*** =solution
```{r}
# treatmentgroup and controlgroup are both available in your workspace

# Test equality in means of female (gender_inp==1) in the treatment and control groups
t.test(controlgroup$gender_inp, treatmentgroup$gender_inp, mu=0)

# Test equality in means of proportion aged 19-34 (age_19_34_inp==1) in the treatment and control groups
t.test(controlgroup$age_19_34_inp, treatmentgroup$age_19_34_inp, mu=0)

# Test equality in means of proportion aged 50-64 (age_50_64_inp==1) in the treatment and control groups
t.test(controlgroup$age_50_64_inp, treatmentgroup$age_50_64_inp, mu=0)

# Test equality in means of proportion white (race_white_inp==1) in the treatment and control groups
t.test(controlgroup$race_white_inp, treatmentgroup$race_white_inp, mu=0)

# Test equality in means of proportion black (race_black_inp==1) in the treatment and control groups
t.test(controlgroup$race_black_inp, treatmentgroup$race_black_inp, mu=0)

# Test equality in means of proportion hispanic (hispanic_inp==1) in the treatment and control groups
t.test(controlgroup$hispanic_inp, treatmentgroup$hispanic_inp, mu=0)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

# test_function("mean", args = "object",
#              not_called_msg = "You didn't call `mean()`!",
#              incorrect_msg = "You didn't call `mean(object = ...)` with the correct argument, `object`.")

test_error()

success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:5349e868bb
## Estimating Average Treatment Effects (ATEs) Across Experimental Groups

We finally know that our treatment and control groups are balanced at a statistical level, and now we can look at the outcome variables we actually care about - like people’s blood pressure, diabetes diagnosis, or depression screen - and we can trust that the differences in means between the treatment and control groups will provide the Average Treatment Effect of having insurance on those outcomes.

A simulated version of the Oregon Health Insurance Experiment data, `OHIE`, is available in the workspace. This has been divided into two separate dataframes: `treatmentgroup` and `controlgroup` denoting the treatment and control groups, respectively.

In this exercise, you will be using a two-sided t-test to analyze if the difference in the means of health outcome variables of patients who did and did not receive health insurance are statistically different. The research team is eager to hear your results!

*** =instructions
- The way to perfrom a t-test in `R` is with the  `t.test()` function
- Use a two-sided t-test to examine whether or not the treatment and control groups have significantly different average values for the following health outcomes: 
- systolic blood pressure (variable `bp_sar_inp`)
- diastolic blood pressure (variable `bp_dar_inp`)
- diabetes (variable `dia_dx_post_lottery`)
- depression diagnosis (variable `dep_dx_post_lottery`)
- anti-depressant usage (variable `antidep_med_inpbinary`)

*** =hint
- Use `t.test(controlgroup$var, treatmentgroup$var, mu=0)` to statistically test that the treatment and control groups are balanced

*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","bp_sar_inp","bp_dar_inp","dia_dx_post_lottery","dep_dx_post_lottery","antidep_med_inpbinary")]
treatmentgroup <- OHIE[OHIE$treatment==1 & !is.na(OHIE$treatment),]
controlgroup <- OHIE[OHIE$treatment==0 & !is.na(OHIE$treatment),]
rm(OHIE)
```

*** =sample_code
```{r}
# treatmentgroup and controlgroup are both available in your workspace

# Test for presence of significant treatment effect for systolic blood pressure (variable `bp_sar_inp`)


# Test for presence of significant treatment effect for diastolic blood pressure (variable `bp_dar_inp`)


# Test for presence of significant treatment effect for diabetes (variable `dia_dx_post_lottery`)


# Test for presence of significant treatment effect for depression diagnosis (variable `dep_dx_post_lottery`)


# Test for presence of significant treatment effect for anti-depressant usage (variable `antidep_med_inpbinary`)


```

*** =solution
```{r}
# treatmentgroup and controlgroup are both available in your workspace

# Test for presence of significant treatment effect for systolic blood pressure (variable `bp_sar_inp`)
t.test(controlgroup$bp_sar_inp, treatmentgroup$bp_sar_inp, mu=0)

# Test for presence of significant treatment effect for diastolic blood pressure (variable `bp_dar_inp`)
t.test(controlgroup$bp_dar_inp, treatmentgroup$bp_dar_inp, mu=0)

# Test for presence of significant treatment effect for diabetes (variable `dia_dx_post_lottery`)
t.test(controlgroup$dia_dx_post_lottery, treatmentgroup$dia_dx_post_lottery, mu=0)

# Test for presence of significant treatment effect for depression diagnosis (variable `dep_dx_post_lottery`)
t.test(controlgroup$dep_dx_post_lottery, treatmentgroup$dep_dx_post_lottery, mu=0)

# Test for presence of significant treatment effect for anti-depressant usage (variable `antidep_med_inpbinary`)
t.test(controlgroup$antidep_med_inpbinary, treatmentgroup$antidep_med_inpbinary, mu=0)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

# test_function("mean", args = "object",
#              not_called_msg = "You didn't call `mean()`!",
#              incorrect_msg = "You didn't call `mean(object = ...)` with the correct argument, `object`.")

test_error()

success_msg("Good work!")
```
