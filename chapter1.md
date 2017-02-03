  ---
  title       : Introduction to Experiments
  description : This exercise helps you get to know your data better
  attachments :
  video_link :


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:4745db858e
## Controlled Experiments
*** =video_link
//player.vimeo.com/video/198212077

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:ebe90c9c16
## MC 1
Laurel cracked the screen on her old phone, and her next phone choice will be based on which is more durable: the WePhone 10S or the Universe S10. She looks at a YouTube channel that buys one of each phone and tests how much force is needed to crush each phone with a hydraulic press. If every WePhone or Universe is identical from the factory, and if the phones are tested under exactly the same condition, is just one crushing test enough to determine durability?

*** =instructions
- Yes
- No
*** =sct
```{r}
msg1 = "Correct, only two observations are needed to determine whether there is a causal effect between the treatment (phone type) and outcome (durability if all experimental conditions between the phones are identical (i.e. If all other factors that could influence the outcome are controlled for). That's assuming you think a crush test is a valid one for determining real-world durability, of course!"
msg2 = "Try again"
test_mc(correct = 1, feedback_msgs = c(msg1,msg2))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:e157142b3a
## MC 2
Laurel's video showed that the WePhone 10S was stronger than the Universe S10. Laurel is now interested in what factors caused the WePhone 10S to be more durable than the Universe S10. Laurel examines the model specifications of each phone, and assumes that whichever specification is most different between the phones is the cause of their different durabilities.

*** =instructions
- Examine the provided phone specifications in dataframe`PhoneSpecifications` and identify the specification that has the `largest ratio` between the WePhone 10S and the Universe S10
- In the console window, a.) write out the `name` that specification, and b.) write out the `size` of this ratio (expressed as a quotient)
*** =pre_exercise_code
```{r}
PhoneSpecifications<-data.frame(WePhone10S=c(190,4000,5.5,64,800),UniverseS10=c(180,3500,5.2,64,550))
row.names(PhoneSpecifications)<-c("Weight (g)","Battery Capacity (mAh)","Diagonal Length (in)","Storage (Gb)","Luminance (cd/m2)")
PhoneSpecifications<-t(PhoneSpecifications)
```
*** =sample_code
```{r}
PhoneSpecifications #Dataframe

print(Solution1<-" "  ) #Write column name of specification with the largest ratio between the WePhone 10S and the Universe S10

print(Solution2<-     ) #Write quotient of phone specifications selected in Solution1

```
*** =solution
```{r}
#loop through specification ratios to find max ratio
Ratios<-vector(length=5)
for(i in 1:length(PhoneSpecifications[1,])){
Ratios[i]<-PhoneSpecifications[1,i]/PhoneSpecifications[2,i]
}
print(Solution1<-dimnames(PhoneSpecifications)[[2]][match(max(Ratios),Ratios)])

print(Solution2<-max(Ratios))

```
*** =sct
```{r}
#I use regular expressions to allow for multiple spellings of answers. 

ex() %>% check_output('"[L|l]uminance.*"',
missing_msg = "Solution1 is incorrect. Please write out your answer. Make sure it is in string format and printed in the console") 

ex() %>% check_output("1.45.*",
missing_msg = "Solution2 is incorrect. Make sure to divide the WePhone10S's specification by the UniverseS10's specification")

success_msg("Good work! Keep in mind, even though there is a correlation between the treatment (luminance) and outcome (durability), this correlation is spurious; in reality, a phone's luminance (brightness) does not have a causal effect on its durability.
")
```


--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:9e9326a35b
## Randomized Experiments
*** =video_link
//player.vimeo.com/video/198212082


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:243af9a90f
## MC 3
Laurel is wondering if it would be more realistic to test phone durability through a bending test rather than a crushing test. To find out, she convinces four of her friends try to join her at an electronics store to bend one of the two phones for a duration of 1 minute each. 

Two of her friends really want to try to bend the Universe S10, so Laurel assigns those two friends to bend the Universe S10, and her other two friends try bending the WePhone 10S. They find the Universe S10 bent about 2 degrees more than the WePhone 10, so she concludes the average treatment effect of the WePhone 10S on bendability is -2 degrees. Of the following, which is the most problematic design error in this experiment?


*** =instructions
- Noncompliance
- Ethics
- Random assignment
- Data visualization

*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Correct, Laurel's friends were not randomly assigned to each treatment. Instead, she assigned them based on their own preferences, which could lead to confounded results. For example, what if the Universe S10 testers hated Universe phones, so tried harder to damage them?."
msg4 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1c689745b7
## MC 4
If Laurel was interested in what proportion of the U.S. population could bend a WePhone 10S with their hands, which group would serve as a better sample?


*** =instructions
- Perfect strangers in Laurel's neighborhood
- Perfect strangers across the world
- Perfect strangers in Laurel's town
- Perfect strangers across the U.S.

*** =sct
```{r}
msg1 = "Try again"
msg2 = "This answer may be tempting, but Laurel wants a sample that is reflective of the U.S. population"
msg3 = "Try again"
msg4 = "Correct. A single neighborhood is unlikely to reflect the diversity of the whole country, and involving people across the world brings in a lot of complicating confounders. People in her town is closer to ideal, but really to get a true representation of the US population, you need to survey strangers across the US"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```







--- type:VideoExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:ef7f2e2846
## Bounds Analysis for Missing Data
*** =video_link
//player.vimeo.com/video/199858153

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:fa050e19b1
## MC 5
Which one of the following approaches is *not* an appropriate way to deal with treatment noncompliance?

*** =instructions
- Bounds Analysis
- Instrumental Variables
- Randomized Control Trial
- Intention to Treat Analysis
- Assume Random Compliance
*** =sct
```{r}
msg1 = "Try again"
msg2 = "Try again"
msg3 = "Correct! Randomized Control Trials are not a valid way to correct for noncompliance, because they themselves are suscpetible to treatment noncompliance."
msg4 = "Try again"
msg5 = "Try again"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4,msg5))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1557ba9536
## MC 6
CreditCo, a large credit card company, decides to run an experiment. It sends an offer in the mail to a random 50% group of its customers: those in the treatment group are invited to navigate to a webpage to opt in for a 10% higher credit limit. CreditCo wants to see how credit balances and late payments are impacted six months later as a result of the experiment. Suppose that, of the group that received the mail offer, 40% of people opted in. Do you think that noncompliance will be a problem for CreditCo's analysis? Why or why not?

*** =instructions
- No, because people in the treatment group likely decided to opt in based on a coin flip
- Yes, because the opt-in rate is low
- No, because an opt-in rate of 40% is actually quite high
- Yes, because the set of people opting in are probably people with worse spending habits.
*** =sct
```{r}
msg1 = "This is partially correct. A low compliance rate is one symptom of a noncompliance problem."
msg2 = "While this is a possibility, it is unlikely to actually be the case."
msg3 = "While high compliance rates indicate a lower noncompliance problem, the rate of 40% in this situation is likely to be problematic."
msg4 = "Correct! In this situation, researchers at CreditCo should be worried about the spending habits of those who opted in to the offer."
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```




--- type:NormalExercise lang:r xp:100 skills:1 key:a00d1ebc4c
## Working with non-compliance

Let's continue with the CreditCo dataset described in the previous exercise.

A simulated version of this dataset, `CreditCo`, is available in the workspace.

In this exercise, you will compute the average treatment effect of taking a credit line increase offer on late payments (default).

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
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/CreditCoNonCompliance.Rda'))
CreditCo <- CreditCo[,c("id","offered","opt_in","FICO","female","race_white","default_pre","default_post","balance_pre","balance_post")]
```

*** =sample_code
```{r}
# The dataset `CreditCo` is available in your workspace

# Compute the fraction of people who were offered a higher credit limit


# Of the people who were offered, what fraction opted in?


# Compute a naive average treatment effect of late payment (variable `default_post`), where treatment state is defined by having been offered and opted in to the program

```

*** =solution
```{r}
# The dataset `CreditCo` is available in your workspace

# Compute the fraction of people who were offered a higher credit limit
mean(CreditCo$offered)

# Of the people who were offered, what fraction opted in?
mean(CreditCo$opt_in[CreditCo$offered==1])

# Compute a naive average treatment effect of late payment (variable `default_post`), where treatment state is defined by having been offered and opted in to the program and control state is defined as not being offered
 mean(CreditCo$default_post[CreditCo$opt_in==1])-mean(CreditCo$default_post[CreditCo$offered==0])
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

```




--- type:NormalExercise lang:r xp:100 skills:1 key:a42175703d
## Computing bounds under non-compliance

Continuing with the dataset from the previous exercise, you will now compute the bounds of  average treatment effect of opting in to a credit line increase offer.

*** =instructions
- Compute bounds on the average treatment effect under non-compliant behavior, and compare with other methods of correcting for non-compliance.

*** =hint
- Remember to be aware of selecting the correct subsample


*** =pre_exercise_code
```{r}
set.seed(1)
load(url('http://s3.amazonaws.com/assets.datacamp.com/production/course_1566/datasets/CreditCoNonCompliance.Rda'))
CreditCo <- CreditCo[,c("id","offered","opt_in","FICO","female","race_white","default_pre","default_post","balance_pre","balance_post")]
```

*** =sample_code
```{r}
# The dataset `CreditCo` is available in your workspace

# Create a variable called pct_opt that measures the fraction of opt-in among those offered the increase


# Calculate the upper bound of the ATE by assuming that all non-opt-in customers have a late payment, and subtract the non-offered average from this value


# Calculate the lower bound of the ATE by assuming that all non-opt-in customers don't have a late payment, and subtract the non-offered average from this value

```

*** =solution
```{r}
# The dataset `CreditCo` is available in your workspace

# Create a variable called pct_opt that measures the fraction of opt-in among those offered the increase
pct_opt <- mean(CreditCo$opt_in[CreditCo$offered==1])

# Calculate the upper bound (call it `ubound`) of the ATE by assuming that all non-opt-in customers have a late payment, and subtract the non-offered average from this value
ubound <- pct_opt*mean(CreditCo$default_post[CreditCo$opt_in==1]) + (1-pct_opt)*1 - mean(CreditCo$default_post[CreditCo$offered==0])

# Calculate the lower bound (call it `lbound`) of the ATE by assuming that all non-opt-in customers don't have a late payment, and subtract the non-offered average from this value
lbound <- pct_opt*mean(CreditCo$default_post[CreditCo$opt_in==1]) + (1-pct_opt)*0 - mean(CreditCo$default_post[CreditCo$offered==0])

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

```



