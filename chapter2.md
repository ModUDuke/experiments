  ---
  title       : Average Treatment Effects
  description : This exercise helps you get to know the basics of statistical inference
  attachments :
  video_link :


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:42e831dde4
## What is the Point of Statistical Inference?
*** =video_link
//player.vimeo.com/video/198212067

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:6ae426b824
## Multiple Choice: Statistical inference
Under which scenario might an experimenter *not* need to use statistical inference to justify his causal claims?

*** =instructions
- When his causal claim is logically sound.
- When his sample is large.
- When his experiment is well-designed.
- When he can have his entire population of interest participate in the experiment.
*** =sct
```{r}
msg1 = "Even if it makes sense, an argument without data isn't science, so it's not enough to avoid using statistical inference. Try again"
msg2 = "Even with a large sample, you still need to use statistical measures to verify the experiment's validity, so try again"
msg3 = "Even with a well-designed experiment, you still will have just a sample of the possible data to look at, so that's not quite right. Try again"
msg4 = "Correct! The purpose of statistical inference in randomized experiments is to help researchers make valid propositions about a population given a sample. This is unnecessary if the entire population of interest participates in the experiment."
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:d2fc3d44de
## Multiple Choice: Sample size
A professor was interested in whether myopia in children could be caused by environmental factors. He found a completely random sample of 10 children, and had 5 of them sleep with nightlights and 5 of them sleep without nightlights for the first 10 years of their lives. 

All of the children who had slept with nightlights developed myopia, whereas only 2 of the children who did not sleep with nightlights developed myopia. From this study, the professor determined that the average treatment effect of using a nightlight on myopia was 5/5 - 2/5 = 3/5, or 60%. Why might the professor want to get a larger sample before publishing these results?

*** =instructions
- To please his reviewers.
- To control for non-compliance.
- To make sure that the observed average treatment effect did not occur by chance.
- To control for confounding variables.

*** =sct
```{r}
msg1 = "While this might feel like the most immediate reason, what other reason do you think his reviewers mentioned? Try again"
msg2 = "Noncompliance isn't mentioned as an issue in this case, so it's not the key issue we're looking for. Try again"
msg3 = "Correct! Even when we draw from a completely random sample, there is always the chance that our sample is not representative of the whole population. The larger the sample size that we draw from, the less likely that our findings were to have occurred by chance."
msg4 = "Confounders are always an issue, particularly when looking at real world data, but that's not quite the best reason to get a larger sample in this case. Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

## Randomized Controlled Trial
*** =video_link
//player.vimeo.com/video/198212064

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:7eab53249a
## Multiple Choice: Experiments vs. RCTs
How are the results from randomized control trials interpreted differently than randomized experiments?

*** =instructions
- They are not interpreted differently from randomized experiments.
- They have real-world implications.
- They do not need to be tested for statistical significance.
- They should be estimated with conditional average treatment effects.

*** =sct
```{r}
msg1 = "Correct! A randomized control trial is a type of randomized experiment."
msg2 = "RCTs are not the only things with real-world implications, so try again"
msg3 = "RCTs must be analyzed using statistical methods as much as any experiment, so try again"
msg4 = "You can use all kinds of tools with RCTs, not just CATEs, so look again for a better answer"
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

## The Design of the Oregon Health Experiment.
*** =video_link
//player.vimeo.com/video/198212086

## Reading Average Treatment Effect & Confidence Intervals in a Table: Depression in the Oregon Health Experiment
*** =video_link
//player.vimeo.com/video/198212094


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:533b160157
## Multiple Choice: Significance
What is the difference between a statistically significant effect and a clinically (or "substantively") significant effect?

*** =instructions
- Statistically significant effects are bigger than clinically significant effects
- Statistically significant effects don't necessarily matter, whereas clinically significant effects do matter
- Statistically significant effects have smaller confidence intervals than clinically significant effects
- Statistically significant effects always matter, whereas clinically significant effects sometimes don't matter
*** =sct
```{r}
msg1 = "This might be true in some individual cases, but it's not true in general, so try again"
msg2 = "Correct! Statistical significance indicates whether an effect is real, but it does not necessarily indicate whether it is meaningful. With enough data, a study might find a statistically significant effect of season on people's preference to buy tissue paper, but the effect might not be important (for example, if people were 0.2% more likely to buy tissue paper in the spring over the fall)."
msg3 = "This might be true in some individual cases, but it's not true in general, so try again"
msg4 = "This is not how you should interpret treatment effects, so look again!"
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:0fa656dc08
## Practice Reading Tables (Part I)
Now let's practice reading tables from the Oregon Health Experiment. As described in the previous video, the Oregon Health Experiment studies the effect of getting Medicaid coverage on respondent's health, so let's look at some mental health results in the data.

The dataframe "OregonHealthResults" indicates results from the Oregon Health Experiment (in percentages) pertaining to depression, and to get a good sense of how this was affected in the experiment, you decide to review some results and then calculate some new numbers for yourself. 

One of the most interesting results of any experiment is the Average Treatment Effect relative to the mean value of a parameter. Therefore, With this dataframe, you decide to first look at two basic items: The average positive screen value in the control group, and the Average Treatment Effect of Medicaid on positive screen values. These calculations will give you a deeper sense of the impact of health insurance on basic mental health.


*** =instructions
- What is the mean value of positive screening in the control group?
- What is the average treatment effect of medicaid coverage on positive screening? 
- Given the mean value of positive screening in the control group and the average treatment effect of medicaid coverage on positive screening, estimate the mean value of positive screening in the treatment group.

*** =pre_exercise_code
```{r}
OregonHealth<-data.frame(c("Blood pressure - Systolic (mm Hg)","Blood pressure - Diastolic (mm Hg)","Blood pressure - Elevated (%)","Hypertension - Diagnosis after lottery (%)","Hypertension - Current use of medication for hypertension (%)","Cholesterol - Total level (mg/dl)","Cholesterol - High total level (%)","Cholesterol - HDL level (mg/dl)","Cholesterol - Low HDL level (%)","Hypercholesterolemia - Diagnosis after lottery (%)","Hypercholesterolemia - Current use of medication for high cholesterol level (%)","Glycated hemoglobin - Level (%)","Glycated hemoglobin - Level ???6.5% (%)","Diabetes - Diagnosis after lottery (%)","Diabetes - Current use of medication for diabetes (%)","Depression - Positive screening result (%)","Depression - Diagnosis after lottery (%)","Depression - Current use of medication for depression (%)","Framingham risk score - Overall","Framingham risk score - High-risk diagnosis","Framingham risk score - Age 50-65 yr"),
              c(119.3,76,16.3,5.6,13.9,204.1,14.1,47.6,28,6.1,8.5,5.3,5.1,1.1,6.4,30,4.8,16.8,8.2,11.6,13.9),
              c(-0.52,-0.81,-1.33,1.76,0.66,2.2,-2.43,0.83,-2.82,2.39,3.8,0.01,-0.93,3.83,5.43,-9.15,3.81,5.49,-0.21,1.63,-0.37),
              c(-2.97,-2.65,-7.16,-1.89,-4.48,-3.44,-7.75,-1.31,-10.28,-1.52,-0.75,-0.09,-4.44,1.93,1.39,-16.7,0.15,-0.46,-1.56,-1.11,-2.64),
              c(1.93,1.04,4.49,5.4,5.8,7.84,2.89,2.98,4.64,6.29,8.35,0.11,2.59,5.73,9.48,-1.6,7.46,11.45,1.15,4.37,1.9),
              c(0.68,0.39,0.65,0.34,0.8,0.45,0.37,0.45,0.46,0.23,0.1,0.82,0.61,0.001,0.008,0.02,0.04,0.07,0.76,0.24,0.75))
names(OregonHealth)<-c("Variable","Mean Value in Control Group","Change with Medicaid Coverage","95% Confidence Interval (lower bound)","95% Confidence Interval (Upper Bound)","P Value")
OregonHealthResults<-OregonHealth[16:18,]
OregonHealthResults$Variable<-c("Positive_Screening","Diagnosis_After_Lottery","Current_Use_Of_Medication")
rm(OregonHealth)
```
*** =sample_code
```{r}
str(OregonHealthResults) # Dataframe

print(Solution1<- ) # Write mean value of positive screening in the control group

print(Solution2<- ) # Write average treatment effect of medicaid coverage on positive screening

print(Solution3<- ) # Write mean value of positive screening in the treatment group

```

*** =solution
```{r}
print(Solution1<-OregonHealthResults[OregonHealthResults$Variable=="Positive_Screening",]$`Mean Value in Control Group`)
print(Solution2<-OregonHealthResults[OregonHealthResults$Variable=="Positive_Screening",]$`Change with Medicaid Coverage`)
print(Solution3<-Solution1+Solution2)

```

*** =sct
```{r}
test_object("Solution1")
test_object("Solution2")
test_object("Solution3")
success_msg("Good work!")
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:5fa7d35f25
## Practice Reading Tables (Part II)
Now that we know how an Average Treatment Effect is related to mean values in the treatment and control groups, we should examine the reliability of these results. Therefore, you decide to examine the 95% confidence interval lower bound, and statistical significance for one of the table's Average Treatment Effects.

*** =instructions
- What is the the 95% confidence interval lower bound for the treatment effect of medicaid coverage on current use of medication?
- Which average treatment effect of medicaid coverage on depression was not statistically significant? You can write this out as a line of text.

*** =pre_exercise_code
```{r}
OregonHealth<-data.frame(c("Blood pressure - Systolic (mm Hg)","Blood pressure - Diastolic (mm Hg)","Blood pressure - Elevated (%)","Hypertension - Diagnosis after lottery (%)","Hypertension - Current use of medication for hypertension (%)","Cholesterol - Total level (mg/dl)","Cholesterol - High total level (%)","Cholesterol - HDL level (mg/dl)","Cholesterol - Low HDL level (%)","Hypercholesterolemia - Diagnosis after lottery (%)","Hypercholesterolemia - Current use of medication for high cholesterol level (%)","Glycated hemoglobin - Level (%)","Glycated hemoglobin - Level ???6.5% (%)","Diabetes - Diagnosis after lottery (%)","Diabetes - Current use of medication for diabetes (%)","Depression - Positive screening result (%)","Depression - Diagnosis after lottery (%)","Depression - Current use of medication for depression (%)","Framingham risk score - Overall","Framingham risk score - High-risk diagnosis","Framingham risk score - Age 50-65 yr"),
              c(119.3,76,16.3,5.6,13.9,204.1,14.1,47.6,28,6.1,8.5,5.3,5.1,1.1,6.4,30,4.8,16.8,8.2,11.6,13.9),
              c(-0.52,-0.81,-1.33,1.76,0.66,2.2,-2.43,0.83,-2.82,2.39,3.8,0.01,-0.93,3.83,5.43,-9.15,3.81,5.49,-0.21,1.63,-0.37),
              c(-2.97,-2.65,-7.16,-1.89,-4.48,-3.44,-7.75,-1.31,-10.28,-1.52,-0.75,-0.09,-4.44,1.93,1.39,-16.7,0.15,-0.46,-1.56,-1.11,-2.64),
              c(1.93,1.04,4.49,5.4,5.8,7.84,2.89,2.98,4.64,6.29,8.35,0.11,2.59,5.73,9.48,-1.6,7.46,11.45,1.15,4.37,1.9),
              c(0.68,0.39,0.65,0.34,0.8,0.45,0.37,0.45,0.46,0.23,0.1,0.82,0.61,0.001,0.008,0.02,0.04,0.07,0.76,0.24,0.75))
names(OregonHealth)<-c("Variable","Mean Value in Control Group","Change with Medicaid Coverage","95% Confidence Interval (lower bound)","95% Confidence Interval (Upper Bound)","P Value")
OregonHealthResults<-OregonHealth[16:18,]
OregonHealthResults$Variable<-c("Positive_Screening","Diagnosis_After_Lottery","Current_Use_Of_Medication")
rm(OregonHealth)
```
*** =sample_code
```{r}
str(OregonHealthResults) # Dataframe

print(Solution1<- ) # Write the 95% confidence interval lower bound for the treatment effect of medicaid coverage on current use Of medication

print(Solution2<-"") # Write name of variable whose average treatment effect was not statistically significant

```

*** =solution
```{r}
print(Solution1<-OregonHealthResults[OregonHealthResults$Variable=="Current_Use_Of_Medication",]$`95% Confidence Interval (lower bound)`)
print(Solution2<-OregonHealthResults[OregonHealthResults$`P Value`>.05,]$Variable)

```

*** =sct
```{r}
test_object("Solution1")
ex() %>% check_output('"[C|c]urrent.*"',
missing_msg = "Solution2 is incorrect. Please write out your answer. Make sure it is in string format and printed in the console") 
success_msg("Good work!")
```


## Reading Average Treatment Effect & Confidence Intervals in a Table: Cholesterol in the Oregon Health Experiment
*** =video_link
//player.vimeo.com/video/198212098


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:5765daa781
## Multiple Choice: Interpreting effect sizes
The head of marketing at Bizer, Inc. is trying to decide whether to include a new cholesterol medicine's average treatment effect in the company's advertisements for that medicine. He knows that on average, the medicine reduces cholesterol in respondents by about 1mg/dL and knows that the effect is statistically different from zero. However, he's not sure whether that number is large or small; that is, whether the medicine's average treatment effect is worth advertising. 

If cholesterol is highly variable in the population (about 70% of the population has cholesterol between 160mg/dL and 240mg/dL), does an average treatment effect of 1mg/dL seem relatively small or relatively large? In other words, when an average treatment effect is substantially smaller than the standard error of the mean for a parameter, how would we tyipcally interpret the size of that average treatment effect?


*** =instructions
- The average treatment effect is large
- The average treatment effect is small
*** =sct
```{r}
msg1 = "Although a 1mg/dL reduction in cholesterol is statistically significant and might be substantial for some members of the population, it is not a very large reduction relative to the amount of variance in cholesterol in the population. Try again."
msg2 = "Correct! When an average treatment effect is small relative to the standard error of a sample mean, it suggests that the average treatment effect is small, relative to the amount of variance typically found in that parameter. This thought process is especially helpful when deciding if an estimated effect is clinically significant (even if it is statistically significant)."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:82150d848b
## Practice working with the Oregon Health Experiment
Let's say you're wondering how much mens' and womens' health differed in the experiment, and what the data says about Medicaid's effects on those differences, so you decide to look at some of the basic health numbers in the data. A simulated version of the Oregon Health Insurance Experiment data, `OHIE`, is available in the workspace. With this dataframe, you make some quick calculations to learn about any differences that might be linked to gender by looking at:

*** =instructions
- Test if there is a statistically significant difference in gender between the treament and control groups (i.e. whether gender is balanced between the treatment and control group). 
- Determine if the treatment and control groups have significantly different average values for the following health outcomes: systolic blood pressure (variable `bp_sar_inp`), and diastolic blood pressure (variable `bp_dar_inp`).

*** =hint
- For the first question, you will need to `subset` the `OHIE` data frame by treatment. 
- It may help to create a new dataframe called `TreatmentGroup` that contains only WePhones in the treatment group, and a new data frame called `ControlGroup` that contains only WePhones in the control group.
- For each of the following questions, use the `t.test` function where (mu=0) to statistically test whether the treatment and control group are different from each other.


*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/OHIEexperimental.Rda'))
OHIE <- OHIE[!is.na(OHIE$treatment),c("id","treatment","gender_inp","bp_sar_inp","bp_dar_inp")]

```

*** =sample_code
```{r}
str(OHIE) #Dataframe

print(Solution1a<- ) # Use a t.test to determine whether gender is balanced between the treatment and control groups 

print(Solution1b<-"" ) # Based on your t.test, is gender balanced? Answer with "Yes" or "No" 

print(Solution2a<- ) # Use a t.test to determine if the treatment had a statistically significant effect on systolic blood pressure 

print(Solution2b<-"" ) # Based on your t.test, does the treatment have a statistically significant effect on systolic blood pressure? Answer with "Yes" or "No" 

print(Solution3a<- ) # Use a t.test to determine if the treatment had a statistically significant effect on diastolic blood pressure 

print(Solution3b<-"" ) # Based on your t.test, does the treatment have a statistically significant effect on diastolic blood pressure? Answer with "Yes" or "No" 

```

*** =solution
```{r}
TreatmentGroup <- OHIE[OHIE$treatment==1, ]
ControlGroup <- OHIE[OHIE$treatment==0, ]
print(Solution1a<- t.test(TreatmentGroup$gender_inp,ControlGroup$gender_inp,mu=0))
print(Solution1b<-"Yes")
print(Solution2a<- t.test(TreatmentGroup$bp_sar_inp,ControlGroup$bp_sar_inp,mu=0))
print(Solution2b<-"No")
print(Solution3a<- t.test(TreatmentGroup$bp_dar_inp,ControlGroup$bp_dar_inp,mu=0))
print(Solution3b<-"Yes")

```

*** =sct
```{r}
test_object("Solution1a")
test_object("Solution1b")
test_object("Solution2a")
test_object("Solution2b")
test_object("Solution3a")
test_object("Solution3b")

success_msg("Good work!")
```



--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1
## Practice working with eGulf
To increase their commissions, the popular online auctioneer, eGulf, wants to help its sellers increase the final sales prices of their merchandise. For each auction on eGulf, sellers are allowed to post up to 10 pictures of an item that they are selling. Past studies suggest that customer's appraisals of merchandise (and subsequently, final bids of merchandise) improve when sellers include more pictures of their merchandise; therefore, eGulf considers raising the number of pictures that a seller can post on an auction's webpage. 

To test whether eGulf should allow sellers to post more than 10 pictures of their items, eGulf conducts an experiment: eGulf finds a random sample of dedicated used WePhone sellers that typically post 10 pictures of their used WePhones, and temporarily allows them to post up to 15 pictures for each auction of their WePhones. Using the results of this experiment, listed in dataset `eGulf`, test whether there is an added benefit to posting more than 10 pictures on WePhone auctions. Specifically:

*** =instructions
- Statistically test whether sellers who posted more than 10 pictures (`Seller_Opted_Into_Treatment`==1) on their WePhone auctions (`Final_Sales_Price`) sold their WePhones at higher prices than sellers who posted 10 or less pictures on their WePhone auctions (`Seller_Opted_Into_Treatment`==0)

*** =hint
- For the first question, you will need to `subset` the `eGulf` data frame by treatment. 
- It may help to create a new dataframe called `TreatmentGroup` that contains only WePhones in the treatment group, and a new data frame called `ControlGroup` that contains only WePhones in the control group.
- Use the `t.test` function where (mu=0) to statistically test whether the treatment and control group are different from each other.

*** =pre_exercise_code
```{r}
# Initialize dataframe
set.seed(1)
n <- 1000
eGulf <- as.data.frame(matrix(0, ncol=5,nrow=n))
colnames(eGulf) <- c("Seller_Offered_Treatment","Seller_Opted_Into_Treatment","Seller_Feedback_Count","Seller_Feedback_Score","Auction_Final_Sales_Price")
# Simulate baseline data
  # Make seller feedback count
    eGulf$Seller_Feedback_Count<-as.integer(abs(round(rnorm(n,200,100))))
  # Make feedback score loosely correlated with feedback count 
    eGulf$Seller_Feedback_Score<-round(.9+.1*eGulf$Seller_Feedback_Count/max(eGulf$Seller_Feedback_Count)-rbeta(100,1,10),2)
  # Make seller offered treatment loosely correlated with with feedback count 
    eGulf$Seller_Offered_Treatment<-rbinom(n,1,.5+eGulf$Seller_Feedback_Count/max(eGulf$Seller_Feedback_Count)/5)
  # Make seller opted_into_treatment correlated with seller_feedback_score
    eGulf$Seller_Opted_Into_Treatment<-ifelse(eGulf$Seller_Offered_Treatment==0,0,rbinom(n,1,eGulf$Seller_Feedback_Score^5)) #
  # Make final sales price also correlated with seller_feedback_score
    eGulf$Final_Sales_Price<-round(rlnorm(n, meanlog=log(400), sdlog = log(1.2))*eGulf$Seller_Feedback_Score)
```
*** =sample_code
```{r}
str(eGulf) #Dataframe
Solution1<- # Use a t.test to determine whether opting into treatment (i.e. posting more than 10 pictures) increased final sales prices
```
*** =solution
```{r}
Solution1<-t.test(eGulf$Final_Sales_Price[eGulf$Seller_Opted_Into_Treatment==1],eGulf$Final_Sales_Price[eGulf$Seller_Opted_Into_Treatment==0])
```
*** =sct
```{r}
test_object("Solution1")
success_msg("Good work! It looks like posting more photos was positively associated with final WePhone sales prices.")
```


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:ef7f2e2846
## Important Issues in Experiment Design These Modules Ignore
*** =video_link
//player.vimeo.com/video/198212060


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:5f5a6d0023
## Common Issues in Experiments
*** =video_link
//player.vimeo.com/video/199856354


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:e302f4bddd
## Multiple Choice: Drawing conclusions from experiments
The transportation network company, Unter Technologies, is interested in increasing their revenue. They hypothesize that they would generate substantially greater profits if they lowered their costs and profit margins per each ride. 

Unter conducts an experiment on how its sales are sensitive to price reductions by offering a 25% discount for all of its services for one day. To their pleasant surprise, Unter sees a huge spike in sales and profits during the promotional day. 

Seeing the results of his experiment, Unter's CEO decides that Unter should lower its prices permanently. Why might this conclusion be a bit hasty?

*** =instructions
- Unter did not survey its customers to determine if they were enticed by Unter's lower prices.
- Unter does not have enough data to test the statistical significance of its findings.
- The treatment in Unter's experiment might not have the same effect as the treatment in their policy proposal.
- Unter's experiment didn't address the strategic responses of its competitors.
*** =sct
```{r}
msg1 = "Doing additional research to learn The Why behind a behavioral change can be helpful, but there's an experiment design issue to address first. Try again"
msg2 = "This question doesn't say how much data Unter used, but there's another experiment design issue to consider, so try again"
msg3 = "Correct! Unter's experiment specifically tests the effect on profits of a temporary price reduction in its services, rather than the effect of a permanent price reduction. Profits increased during the promotional period, but there is no evidence that profits would remain higher over a longer period of time."
msg4 = "While Unter's profits are a function of its competitors' behavior, there is another experiment design issue that is more appropriate. Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:fa050e19b1
## Multiple Choice: Generalizing experimental results
Unter's CEO is still convinced that lowering the prices of their services might increase the company's profits. He is hesitant to lower Unter's prices for a longer period, since the company would risk losing a great deal of income if the price-drop did not substantially increase revenue. 

Therefore, to understand how a long-term price drop would affect Unter's profits, the CEO of Unter decides to drop the prices of their services in one city. Over the course of a year, Unter's profits in that city rose substantially. Unter's CEO is now convinced that he should drop Unter's prices nation-wide. Why might this conclusion still be too hasty?

*** =instructions
- Unter's experiment did not pay attention to how its changes affected its competitors.
- The context in Unter's experiment might not generalize to other contexts affected by Unter's policy proposal.
- Unter's experiment did not specify why people might be enticed by lower prices.
- Unter's experiment did not control for noncompliance.
*** =sct
```{r}
msg1 = "The company probably does exist in a complex market, but there's something else to worry about without that consideration. Try again"
msg2 = "Correct! Unter's experimental results may have been specific to the city that Unter conducted the experiment in. People from other cities may not be as sensitive to price-reductions as the city in Unter's experiment."
msg3 = "Doing some qualitative research to learn The Why behind a behavior change can be helpful, but there's an experiment design issue to address first. Try again"
msg4 = "The question assumes the CEO can successfully set prices in his own company, so if that's true, what other answer might still be a design issue we need to worry about?"
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:0f5e7a1e15
## Difficulties in Performing Randomized Experiments
*** =video_link
//player.vimeo.com/video/200052274


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:7c1f83a32b
## Multiple Choice: Ethics in experiments
Which of the following causal questions is possible to answer with a randomized experiment (without major ethical concerns)?

*** =instructions
- The effect of losing one's job on mental health.
- The effect of religion on financial well-being.
- The effect of social isolation on academic performance.
- The effect of financial incentives on athletic performance.
*** =sct
```{r}
msg1 = "This would definitely cause major ethical concerns because randomly assigning people to lose their job is not allowed.Try again"
msg2 = "This is a very personal topic to many people, and likely to involve big ethical concerns, so try again"
msg3 = "Randomly assigning people to social isolation is incredibly unethical, so look for a better answer!"
msg4 = "Correct! Each of the other experiments is not only difficult to create, but could cause substantial harm to an experiment's participants."
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:a5a7d9f747
## Noncompliance in Experiments
*** =video_link
//player.vimeo.com/video/198212091

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:c896674673
## Multiple Choice: Ways to deal with noncompliance
Which one of the following approaches is *not* an appropriate way to deal with treatment noncompliance?

*** =instructions
- Bounds Analysis
- Instrumental Variables
- Randomized Control Trial
- Intention to Treat Analysis
- Assume Random Compliance
*** =sct
```{r}
msg1 = "Bounds Analysis is definitely a common method used to deal with noncompliance, and we're looking for a way that is not appropriate, so try again"
msg2 = "Instrumental variables is definitely a common method used to deal with noncompliance, and we're looking for a way that is not appropriate, so try again"
msg3 = "Correct! Randomized Control Trials are not a valid way to correct for noncompliance, because they themselves are suscpetible to treatment noncompliance."
msg4 = "Intention to Treat Analysis is definitely a common way to deal with noncompliance, and we're looking for a way that is not appropriate, so try again"
msg5 = "Assuming Random Compliance is not always applicable, but it still is a common method used to deal with noncompliance, and we're looking for a way that is not appropriate, so try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4,msg5))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1
## Noncompliance in eGulf
Let's go back to our experiment with eGulf, the popular online auctioneer. In a previous exercise, we found that sellers on eGulf who posted more than 10 pictures of their WePhones during auctions had higher sales prices. However, we did not examine whether noncompliance could have confounded our results. Specifically, what if the sellers who chose to post more than 10 pictures of their WePhones were different from those who chose not to post more than 10 pictures? If the experiment's dependent variable is associated with a difference between compliers and noncompliers, its association with the treatment effect may be spurious. Therefore, we should test whether compliance was associated with any traits among the sellers, and whether such traits were associated with final sales prices. With the dataset `eGulf`:

*** =instructions
- Statistically test whether sellers who were offered treatment (`Seller_Offered_Treatment`) and opted into the treatment (`Seller_Opted_Into_Treatment`==1) had different prior average feedback scores (`Seller_Feedback_Score`) than sellers who were offered treatment but did not opt into treatment. 
- Test whether sellers' prior average feedback scores (`Seller_Feedback_Score`) were associated with their recent auction's final sales price (`Final_Sales_Price`) using R's correlation (`cor()`) function

*** =hint
- For the first question, you will need to `subset` the `eGulf` data frame by whether they were offered treatment `and` by whether they opted in. 
- It may help to create a new dataframe called `TreatmentGroup` that contains only WePhones in the who were offered and opted into treatment, and a new data frame called `ControlGroup` who were offered but did not opt into treatment.
- Use the `t.test` function where (mu=0) to statistically test whether the treatment and control group are different from each other.

*** =pre_exercise_code
```{r}
# Initialize dataframe
set.seed(1)
n <- 1000
eGulf <- as.data.frame(matrix(0, ncol=5,nrow=n))
colnames(eGulf) <- c("Seller_Offered_Treatment","Seller_Opted_Into_Treatment","Seller_Feedback_Count","Seller_Feedback_Score","Auction_Final_Sales_Price")
# Simulate baseline data
  # Make seller feedback count
    eGulf$Seller_Feedback_Count<-as.integer(abs(round(rnorm(n,200,100))))
  # Make feedback score loosely correlated with feedback count 
    eGulf$Seller_Feedback_Score<-round(.9+.1*eGulf$Seller_Feedback_Count/max(eGulf$Seller_Feedback_Count)-rbeta(100,1,10),2)
  # Make seller offered treatment loosely correlated with with feedback count 
    eGulf$Seller_Offered_Treatment<-rbinom(n,1,.5+eGulf$Seller_Feedback_Count/max(eGulf$Seller_Feedback_Count)/5)
  # Make seller opted_into_treatment correlated with seller_feedback_score
    eGulf$Seller_Opted_Into_Treatment<-ifelse(eGulf$Seller_Offered_Treatment==0,0,rbinom(n,1,eGulf$Seller_Feedback_Score^5)) #
  # Make final sales price also correlated with seller_feedback_score
    eGulf$Final_Sales_Price<-round(rlnorm(n, meanlog=log(400), sdlog = log(1.2))*eGulf$Seller_Feedback_Score)
```
*** =sample_code
```{r}
str(eGulf) #Dataframe

Solution1<- # Use a t.test to determine whether, among those offered treatment, those who opted into treatment had different seller feedback scores than those who chose not to opt into treatment.

Solution2<- # Determine whether seller's feedback scores are associated with final sales prices
```
*** =solution
```{r}
Solution1<-t.test(eGulf$Seller_Feedback_Score[eGulf$Seller_Opted_Into_Treatment==1&eGulf$Seller_Offered_Treatment==1],eGulf$Seller_Feedback_Score[eGulf$Seller_Opted_Into_Treatment==0 & eGulf$Seller_Offered_Treatment==1])
Solution2<-cor(eGulf$Seller_Feedback_Score,eGulf$Final_Sales_Price)
```
*** =sct
```{r}
test_object("Solution1")
test_object("Solution2")
success_msg("Good work! It looks like sellers who posted more photos tended to have higher prior average feedback scores than those who had not posted more photos. Additionally prior average feedback scores were strongly correlated with final WePhone sales prices. This suggests that the relationship between posting more photos and final sales prices might be spurious")
```


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:db0bf3e371
## Survey Noncompliance
*** =video_link
//player.vimeo.com/video/198212102


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1557ba9536
## Multiple Choice: Quantifying noncompliance concerns
CreditCo, a large credit card company, decides to run an experiment. It sends an offer in the mail to a random 50% group of its customers: those in the treatment group are invited to navigate to a webpage and opt in for a 10% higher credit limit. CreditCo wants to see how credit balances and late payments are impacted six months later as a result of the experiment. 

Suppose that, of the group that received the mail offer, 40% of people opted in. Do you think that noncompliance will be a problem for CreditCo's analysis? Why or why not?

*** =instructions
- No, because people in the treatment group likely used a coin flip to make their opt-in decision
- Yes, because the opt-in rate is low
- No, because an opt-in rate of 40% is actually quite high
- Yes, because the set of people opting in are probably people with worse spending habits.
*** =sct
```{r}
msg1 = "While this is a possibility, it is unlikely to actually be the case. Try again."
msg2 = "This is partially correct. A low compliance rate is one symptom of a noncompliance problem."
msg3 = "While high compliance rates indicate a lower noncompliance problem, the rate of 40% in this situation is likely to be problematic."
msg4 = "Correct! In this situation, researchers at CreditCo should be worried about the spending habits of those who opted in to the offer."
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```



--- type:NormalExercise lang:r xp:100 skills:1 key:a00d1ebc4c
## Working with non-compliance
Let's continue with the CreditCo dataset described in the previous exercise. The CFO has assigned you to figure out the average treatment effect of taking a credit line increase offer on late payments (defaults), and he wants to see something before lunch. You realize that you can give him a simple result: you just need to do some quick checks for balance in your samples and compute a "naive" average treatment effect to get the analysis started.

A simulated version of this dataset, `CreditCo`, is available in the workspace.  With that data:

*** =instructions
- See if treatment and control groups are of equal size
- Compute the fraction of people who opted in to the credit offer
- Compute a naive average treatment effect
- The treatment variable is a column in `CreditCo` called `offered`
- The opt-in variable is a column called `opt_in` 
- The late-payment variable is called `default_post`

*** =hint
- Remember to select the appropriate sample when computing the opt-in rate of the credit offer.


*** =pre_exercise_code
```{r}
  set.seed(1)
  n             <- 9e5
  frac_treated  <- .5
  frac_female   <- .5656
  frac_white    <- .688

# Initialize dataframe
  CreditCo <- as.data.frame(matrix(0, ncol=11,nrow=n))
  colnames(CreditCo) <- c("id","offered","opt_in","FICO","age","female","race_white","default_pre","default_post","balance_pre","balance_post")

# Simulate baseline data
  CreditCo$id         <- seq(1,n,1)
  CreditCo$offered    <- as.integer(runif(n)<frac_treated)
  CreditCo$opt_in     <- rep.int(0,n)
  CreditCo$FICO       <- rnorm(n, mean=736, sd=300)
  CreditCo$age        <- sample(18:55, n, replace=T)
  CreditCo$female     <- as.integer(runif(n)<frac_female)
  CreditCo$race_white <- as.integer(runif(n)<frac_white)

# make FICO score intelligible
  CreditCo$FICO[CreditCo$FICO>850] <- 850
  CreditCo$FICO[CreditCo$FICO<300] <- 300
  CreditCo$FICO                    <- round(CreditCo$FICO)

# simulate pre-experiment default rate
  draw <- runif(n)
  xb   <- -1.82-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-5.1*CreditCo$female-7*CreditCo$race_white
  p    <- exp(xb)/(1+exp(xb))
  CreditCo$default_pre <- as.integer(draw<p)

# simulate pre-experiment balance level
  draw <- rnorm(n, mean=0, sd=0.5)
  CreditCo$balance_pre <- 8.5-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-0.15*CreditCo$female-0.85*CreditCo$race_white + draw
  CreditCo$balance_pre <- exp(CreditCo$balance_pre)

# Simulate noncompliance and opt-in behavior
  draw <- runif(sum(CreditCo$offered))
  xb   <- 6.75-1.2*CreditCo$FICO/100+.07*(CreditCo$FICO^2)/10000-2.1*CreditCo$female-2*CreditCo$race_white
  p    <- exp(xb)/(1+exp(xb))
  CreditCo$opt_in[CreditCo$offered==1] <- as.integer(draw<p[CreditCo$offered==1])

# Simulate post outcomes
  draw <- runif(n)
  xb   <- -1.82-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-5.1*CreditCo$female-7*CreditCo$race_white+4*CreditCo$offered*CreditCo$opt_in
  p    <- exp(xb)/(1+exp(xb))
  CreditCo$default_post <- as.integer(draw<p)

# balance
  draw <- rnorm(n, mean=0, sd=0.5)
  CreditCo$balance_post <- 8.5-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-0.15*CreditCo$female-0.85*CreditCo$race_white + 1*CreditCo$offered*CreditCo$opt_in + draw
  CreditCo$balance_post <- exp(CreditCo$balance_post)

# Remove elements and variables from environment
  rm(draw,frac_female,frac_treated,frac_white,n,p,xb)
  CreditCo <- CreditCo[,c("id","offered","opt_in","FICO","female","race_white","default_pre","default_post","balance_pre","balance_post")]
```

*** =sample_code
```{r}
# The dataset `CreditCo` is available in your workspace

print(Solution1<- )# Compute the fraction of people who were offered a higher credit limit

print(Solution2<- )# Of the people who were offered, what fraction opted in?

print(Solution3<- )# Compute a naive average treatment effect of late payment (variable `default_post`), where treatment state is defined by having been offered and opted in to the program

```

*** =solution
```{r}
Solution1<-mean(CreditCo$offered)
Solution2<-mean(CreditCo$opt_in[CreditCo$offered==1])
Solution3<-mean(CreditCo$default_post[CreditCo$opt_in==1])-mean(CreditCo$default_post[CreditCo$offered==0])
```

*** =sct
```{r}
test_object("Solution1")
test_object("Solution2")
test_object("Solution3")
```

--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:25526ab294
## Bounds Analysis for Missing Data
*** =video_link
//player.vimeo.com/video/199858153


--- type:NormalExercise lang:r xp:100 skills:1 key:a42175703d
## Computing bounds under non-compliance
Your calculations on the CreditCo data showed that noncompliance was an issue in the experiment, so you decide to look at 2 methods for dealing with it.  One method will be a bounds analysis, and the other will be either 1) assuming random compliance, or 2) an Intention-to-Treat analysis. 

First, you compute the bounds of average treatment effect of opting into a credit line increase offer. Second, you calculate what the average treatment effect would be in one of the two other methods (or both, if you want to be complete!).

*** =instructions
- Compute bounds on the average treatment effect under non-compliant behavior
- Compare this with the result of another methods of correcting for non-compliance.

*** =hint
- Remember to be aware of selecting the correct subsample

*** =pre_exercise_code
```{r}
  set.seed(1)
  n             <- 9e5
  frac_treated  <- .5
  frac_female   <- .5656
  frac_white    <- .688

# Initialize dataframe
  CreditCo <- as.data.frame(matrix(0, ncol=11,nrow=n))
  colnames(CreditCo) <- c("id","offered","opt_in","FICO","age","female","race_white","default_pre","default_post","balance_pre","balance_post")

# Simulate baseline data
  CreditCo$id         <- seq(1,n,1)
  CreditCo$offered    <- as.integer(runif(n)<frac_treated)
  CreditCo$opt_in     <- rep.int(0,n)
  CreditCo$FICO       <- rnorm(n, mean=736, sd=300)
  CreditCo$age        <- sample(18:55, n, replace=T)
  CreditCo$female     <- as.integer(runif(n)<frac_female)
  CreditCo$race_white <- as.integer(runif(n)<frac_white)

# make FICO score intelligible
  CreditCo$FICO[CreditCo$FICO>850] <- 850
  CreditCo$FICO[CreditCo$FICO<300] <- 300
  CreditCo$FICO                    <- round(CreditCo$FICO)

# simulate pre-experiment default rate
  draw <- runif(n)
  xb   <- -1.82-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-5.1*CreditCo$female-7*CreditCo$race_white
  p    <- exp(xb)/(1+exp(xb))
  CreditCo$default_pre <- as.integer(draw<p)

# simulate pre-experiment balance level
  draw <- rnorm(n, mean=0, sd=0.5)
  CreditCo$balance_pre <- 8.5-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-0.15*CreditCo$female-0.85*CreditCo$race_white + draw
  CreditCo$balance_pre <- exp(CreditCo$balance_pre)

# Simulate noncompliance and opt-in behavior
  draw <- runif(sum(CreditCo$offered))
  xb   <- 6.75-1.2*CreditCo$FICO/100+.07*(CreditCo$FICO^2)/10000-2.1*CreditCo$female-2*CreditCo$race_white
  p    <- exp(xb)/(1+exp(xb))
  CreditCo$opt_in[CreditCo$offered==1] <- as.integer(draw<p[CreditCo$offered==1])

# Simulate post outcomes
  draw <- runif(n)
  xb   <- -1.82-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-5.1*CreditCo$female-7*CreditCo$race_white+4*CreditCo$offered*CreditCo$opt_in
  p    <- exp(xb)/(1+exp(xb))
  CreditCo$default_post <- as.integer(draw<p)

# balance
  draw <- rnorm(n, mean=0, sd=0.5)
  CreditCo$balance_post <- 8.5-0.2*CreditCo$FICO/100+.046*(CreditCo$FICO^2)/10000-0.15*CreditCo$female-0.85*CreditCo$race_white + 1*CreditCo$offered*CreditCo$opt_in + draw
  CreditCo$balance_post <- exp(CreditCo$balance_post)

# Remove elements and variables from environment
  rm(draw,frac_female,frac_treated,frac_white,n,p,xb)
  CreditCo <- CreditCo[,c("id","offered","opt_in","FICO","female","race_white","default_pre","default_post","balance_pre","balance_post")]
```

*** =sample_code
```{r}
# The dataset `CreditCo` is available in your workspace

print(Solution1<- )# Determine the fraction of opt-in among those offered the increase

print(Solution2<- )# Calculate the upper bound of the ATE by assuming that all non-opt-in customers have a late payment, and subtract the non-offered average from this value

print(Solution3<- )# Calculate the lower bound of the ATE by assuming that all non-opt-in customers don't have a late payment, and subtract the non-offered average from this value

```

*** =solution
```{r}
Solution1 <- mean(CreditCo$opt_in[CreditCo$offered==1])
Solution2 <- Solution1*mean(CreditCo$default_post[CreditCo$opt_in==1]) + (1-Solution1)*1 - mean(CreditCo$default_post[CreditCo$offered==0])
Solution3 <- Solution1*mean(CreditCo$default_post[CreditCo$opt_in==1]) + (1-Solution1)*0 - mean(CreditCo$default_post[CreditCo$offered==0])

```

*** =sct
```{r}
test_object("Solution1")
test_object("Solution2")
test_object("Solution3")
```


