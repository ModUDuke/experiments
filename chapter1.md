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
## Multiple Choice: Controlled experiments
Laurel is in the market for a new phone after cracking the screen on her old one. Her next phone choice will be based on which is more durable: the WePhone 10S or the Universe S10. She looks at a YouTube channel video where the host buys one of each phone and tests how much force is needed to crush each phone with a hydraulic press. If every WePhone or Universe from the factory is truly identical and if the phones are tested under exactly the same condition, then is just one crushing test enough to determine durability?

*** =instructions
- Yes
- No
*** =sct
```{r}
msg1 = "Correct, only two observations are needed to determine whether there is a causal effect between the treatment (phone type) and outcome (durability) if all experimental conditions between the phones are identical (i.e. If all other factors that could influence the outcome are controlled for). That's assuming you think a crush test is a valid one for determining real-world durability, of course!"
msg2 = "You might think not, but consider this as the most theoretically ideal case, and try again"
test_mc(correct = 1, feedback_msgs = c(msg1,msg2))
```

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:e157142b3a
## Comparing Ratios
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
## Multiple Choice: Experimental design
Laurel is wondering if it would be more realistic to test phone durability through a bending test rather than a crushing test. To find out, she convinces four of her friends to join her at an electronics store and bend one of the two phones for a duration of 1 minute each. 

Two of her friends really want to try to bend the Universe S10, so Laurel assigns those two friends to bend the Universe S10, and her other two friends try bending the WePhone 10S. 

The Universe S10 was bent about 2 degrees more than the WePhone 10, so Laurel concludes that the average treatment effect of the WePhone 10S on bendability is -2 degrees. Of the following, which is the most problematic design error in this experiment?


*** =instructions
- Noncompliance
- Ethics
- Random assignment
- Not enough data

*** =sct
```{r}
msg1 = "Not in this case, as all her friends did what she asked. Try again"
msg2 = "There are probably ethical issues involved with knowingly breaking things in a store, but from a scientific perspective, there's a bigger experiment design issue than that. Try again"
msg3 = "Correct, Laurel's friends were not randomly assigned to each treatment. Instead, she assigned them based on their own preferences, which could lead to confounded results. For example, what if the Universe S10 testers hated Universe phones, so tried harder to damage them?"
msg4 = "Sample size is not related to experimental design. We'll talk later about how sample size matters in making inference about experimental results."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1c689745b7
## Multiple Choice: Sampling
If Laurel was interested in what proportion of the U.S. population could bend a WePhone 10S at least 1 degree with their hands, which group would serve as a better sample?


*** =instructions
- Perfect strangers in Laurel's neighborhood
- Perfect strangers across the world
- Perfect strangers in Laurel's town
- Perfect strangers across the U.S.

*** =sct
```{r}
msg1 = "One neighborhood is probably not as diverse as the whole country, so try another option"
msg2 = "This answer may be tempting, but Laurel wants a sample that is reflective of the U.S. population"
msg3 = "This is closer to the best case, but is unlikely to be as diverse as the whole U.S. Try again"
msg4 = "Correct. A single neighborhood is unlikely to reflect the diversity of the whole country, and involving people across the world brings in a lot of complicating confounders. People in her town is closer to ideal, but really to get a true representation of the US population, you need to survey strangers across the US"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```


--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:e97cd6d50d
## Practice identifying imbalance
Laurel has saved all of the wePhones that she has broken and she now wants to auction them off on eBay. However, Laurel is uncertain what base-acution price to set for her broken WePhones. 

To determine what price to set at the beginning of her WePhone auctions, Laurel conducts a new experiment: Laurel grabs a random sample of broken WePhones from her closet, and randomly assigns them to a treatment group (WePhones to be base priced at $10), and a control group (WePhones to be base priced at $5). However, before auctioning the WePhones, Laurel discovers that her sample is unbalanced. Using the data frame `WePhones`:

*** =instructions
- Look through each column in the dataframe, and determine which factor level (WePhone trait) is unbalanced between the treatment and control groups.

*** =hint
- You will need to `subset` the `WePhones` dataframe by treatment group. 
- It may help to create a new dataframe called `TreatmentGroup` that contains only WePhones in the treatment group, and a new data frame called `ControlGroup` that contains only WePhones in the control group.
- Keep in mind that all vectors in dataframe `WePhones` are of class "factor"
- Use the `t.test` function where on each trait of the treatment and control groups to determine which traits are unbalanced

*** =pre_exercise_code
```{r}
# Initialize dataframe
    set.seed(1)
    n <- 100
    WePhones <- as.data.frame(matrix(0, ncol=6,nrow=n))
    colnames(WePhones) <- c("Treatment","Color","Hard_Drive_Capacity","Model","Condition","Network")
# Simulate baseline data
    WePhones$Treatment<-rbinom(n,1,.5)
    WePhones$Color<-rbinom(n,1,runif(1,.2,.8))
    WePhones$Hard_Drive_Capacity<-rbinom(n,1,runif(1,.2,.8))
    WePhones$Model<-rbinom(n,1,runif(1,.2,.8))
    WePhones$Network<-rbinom(n,1,runif(1,.2,.8))
    WePhones$Condition<-rbinom(n,1,runif(1,.2,.8))
# Simulate unbalanced data
  # probability baseline
      p<-runif(1,.1,.7)
  # Randomly assign unbalanced variable
      WePhones[,sample(2:6,1)]<-ifelse(WePhones$Treatment==1,rbinom(n,1,p),rbinom(n,1,p+.2))
# Transform into factor variables
    WePhones$Color<-as.factor(ifelse(WePhones$Color==1,"Platinum","Black"))
    WePhones$Hard_Drive_Capacity<-as.factor(ifelse(WePhones$Hard_Drive_Capacity==1,"64gb","32gb"))
    WePhones$Model<-as.factor(ifelse(WePhones$Model==1,"8","7"))
    WePhones$Network<-as.factor(ifelse(WePhones$Network==1,"Mendizon","Trot"))
    WePhones$Condition<-as.factor(ifelse(WePhones$Condition==1,"Broken","In_Pieces"))
```
*** =sample_code
```{r}
WePhones #Dataframe

Solution1<-" " #Write column name of specification with the largest ratio between the WePhone 10S and the Universe S10

```
*** =solution
```{r}
  a<-vector()
for(i in 2:6){
  a[i-1]<-t.test(as.character(WePhones[,i][WePhones$Treatment==0])==(levels(WePhones[,i])[1]),as.character(WePhones[,i][WePhones$Treatment==1])==(levels(WePhones[,i])[1]))$p.value
}    
  Solution1<-names(WePhones)[match(a[a<.05],a)+1]
```
*** =sct
```{r}
test_object("Solution1")

success_msg("Good work!")
```



