# Bayesian-Average-Sampling
### Predicting Area of a building in a Zip Code, with the help of the data available; having Zip Code, State and Area available of various buildings. 
I was given a task to predict Area of various buildings of a state with the help of given the data present in hand. There were 50 States with Zip codes and Area of a particular building in each state. I was exploring various options to perform this particular task, such as using PyMC3 or PyStan and build a predictor; but when I explored and found this mamazing BAS(Bayesian Adaptive Sampling) Package, I decided to learn and use R for this Model.
## 1. Training the Model with the Data present
First, Lets call the Library by the following Command:
#### > library(BAS)
Then, build the model and train it using the data present in hand.
#### databas <- bas.lm(at_areabuilding ~ ., data = maindata,method = "MCMC", prior = "ZS-null",  modelprior = uniform())
I am giving my independent variable as the input because I have to calculate area with the help of all other data available and keeping in mind the different variables that can affect the output. 
I used MCMC(Markov Chain Monte Carlo) Method as it helps me to improve the Model's Search and efficiency.
Prior used in this model is Zellner-Siow Cauchy as it is a distribution which can be used for multivariate cases and I have assigned equal probablities to all the model as I would like to have a best outcome from my model to be considered.

### Below are the Marginal Inclusion probablities obtained for the Model:

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/1.PNG)

### Now, We can see the function Summary in order to check which model includes the variables in order to predict the Area:

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/2.PNG)

### If we have a look at the visual image of Log Posterior Odds and Model Rank, we can see that Model 1 includes all the necessary variables that are required in order to predict the area.

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/3.PNG)

From the Model image above, We can confirm that zip & state index has Marginal probablitiy of 0.99 and apperars in the Top 2 Models.

### Now, I plotted the graph in order to examine the Marginal Distribuitions of our important variables.

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/4.PNG)

We can see that our variables(Intercept, Zip and State Index) are not showing any non-zero Probablity. Ihave also checked that True Mean is contained within 95% Credible intervals.
#### attr("Probability"): 0.95

Now, I plot the graphs using a easy way which is provided by the BAS package. In the Graph below, I have plotted Residuals v/s fitted plot and we can see that there are some outliers; but a constant spread over the prediction.

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/6.PNG)

I did a plotting for Model probablities in the order that they are sampled and the probablity rises directly at 3.0 

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/7.PNG)

The next plot shows Model deimensions for each Model, and we can again see that the Highest log marginal reaches at 3.0 dimension.

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/8.PNG)

The next plot explains the important variables for data and prediction and marginal posterior probablities greater than 0.5.

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/9.PNG)

## 2. Predicting Area of a State

I have predicted the area of state New York, using the State index, Zip and the State Initials giving as an Input to the Model.
> NY <- data.frame(zip = 12180, loc_st_prov_cd = "NY" ,state_idx = 33)
> new1 <- predict(databas,NY, estimator="BMA", interval = "predict", se.fit=TRUE)
> data.frame('State' = 'New York', 'Estimated Area' = new1$Ybma, 'Real Area' = 15840)

The Area predicted by the Model:

![ScreenShot](https://raw.github.com/uttasarga9067/Bayesian-Average-Sampling/master/10.PNG)
