  ---
  title       : Experiments 7: Noncompliance
  description : These videos and exercises will discuss the specific issue of noncompliance in experiments
  attachments :
  video_link :


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

--- type:NormalExercise lang:r aspect_ratio:62.5 xp:50 skills:1 key:ac78544021
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
