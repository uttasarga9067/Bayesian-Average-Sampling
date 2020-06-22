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
