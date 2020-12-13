# CS510Final

Updates from midterm:
- Better documentation
- Better Readme
- Interpretation of results in ReadMe
- Export graphs as files and save them in the directory
- Try to better follow Wilson coding practices
- Added a ggplot 

- I wanted to do an R markdown for my project as it would make the results and interpretations very easy to see and format, but for some reason my rmarkdown would not install/update so after reseatching and doing every stack overflow and other webistes tried to troubleshoot I still couldnt get it to work so I just added my interpretation of the results here. 
- In terms of testing I didn't create any functions in the could so I'm unaware of how I could use the testthat function in my code.

How to run code:
Simplying running the code through from start to finish will upload, clean, and model all the data in the directory and saves the graphs to directory.
Below is an interpretation/walkthrough of all the code and will be broken up by section.

Interpration of Results:
1. Load and Clean Data
  - This section is pretty straightfoward, the code takes the four datasets (daily, weekly, monthly, quartely) and add colnames or deletes empty rows from the data and then changes the date date to a date type

2. Convert W/ TS
  - In this section the code transforms each of the variables in each data into time series using the ts function.
  - We do this because the data we're working with is time series meaning that the series of data points is indexed by time order.
  
3. Convert W/ XTS
  - Here the code is simply changing the data from ts to an xts object so we can then work with it and model it.
  
4. Left Join All Data & Manually Combine
  - Here we can combine all the types of data into one and also read in the clean dataset from the directory.
  - We do this becuase part of the assignment this project was initially for was to convert the daily, weekly, monthly, and quartely data all into one format that we can model with then once thats taken care of we can just read into the dataset that already clean.
  
5. Stationary of Data
  - Here the code is simply going through each column in the dataset and testing whether it is stationary or not and it does this for every column, the log of every column, and the difference of logs for each function.
  - Stationary of data means that mean, variance and autocorrelation structure does not change over time and are results here are that all variables, log of every variables, and the difference of logs of every variable is all stationary data
  
 6. APPEND Diff_Log of data into dataset, and run lm model
  - Here in this section the code will appen the difference of logs of variables into our dataset and then began running linear models through the lm function.
  - Our first regression model (reg1a) is simple regression model with all the difference of log variables to predict the difference of log of the Wilshire REIT Index. The adjust r-square here is 0.3228 which basically tells how good the model is and 0.3228 means its not great and we want as close to 1 as possible. Then from the plot saved we can see the resiudals which is how far off the preditions we make from the model are from the actual data
  - Then by using the regsubsets function, which is a very complicated step-forward process for coming up with the best model, we can have it find the best possible model from our data and we see from reg2 that the adjust r-square is 0.3221 which is worse than the previous model but it does have more significant variables from looking at the p-values
 
7. Working with monthly data
  - In this section we turn to only monthly data to see if we can get a better model from just using monthly data.
  - The code first transforms the data previously used to monthly by applying the function, apply.monthy. Then the code takes adf test again to test for stationary and we see that the monthly variables, log of monthly variables, and difference of log of monthly variables are all stationary.

8. Regression models of monthly data
  - The first model we run (reg_monthly_a) is predicting the difference of logs of the REIT index using the difference of log of all monthly variables and we get an adjusted r-squared of 0.5842 which is a lot better than the previous models
  - Then the code messes around trying to find a better model but reg_monthly_a is our best possible model and we can then see from the plot the resiuduals vs the actual data.
  
9. Breusch-Pagan Test and Box Coc transormation 
  - Now that we have are best model (reg_monthly_a) we now use Breusch-Pagan Test to make sure there is no heteroskedasticity in are model and we see that p value is to high so there is in fact heteroskedasticity present in our model. 
  - In order to fix this we use a box cox transformation on our y variable and then get our new model lmMod_bc with our tranformed Y. Now running the Breusch-Pagan Test again on this model we get a much lower p-value so heteroskedasticity is no longer present.
  
10. ggplot2
  - Lastly in the code there is a ggplot showinf the residuals of the model vs the acutal data.
