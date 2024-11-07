# Using Neural Networks to Predict Political Party

This study was conducted in the ITC 535 Machine Learning cours at Missouri State University. Data set, framework, and teachings from Dr. Randall Sexton was utilized in this project.

## Data Set
[Political Party Data.xlsx](https://github.com/user-attachments/files/17655089/Political.Party.Data.xlsx)

## Results
[Political Party Results.xlsx](https://github.com/user-attachments/files/17655088/Political.Party.Results.xlsx)


## Analysis

### 1. Classification problem and experiment
The purpose of this study is to determine the effectiveness of using a NNSOA trained Neural Network to predict political parties. The data was collected from 500 participants who were asked a variety of questions.

The collected data generated a total of 12 inputs for this data set. Those input categories were the number of teeth, preference on guns, yearly income, age, if they smoke, if they do drugs, if they like to drink, work years at current job, weight (lbs.), height (in), gender, and their living situation. Some of the categories are classification categories where there can be multiple inputs. For preference of guns, smoke, drugs, and drink no was set to 0 and yes was set to 1. For gender, male was set to 0 and female was set to 1. For their living situation, it is divided into whether they own, rent, or live at home. Own was set as “A”, rent was set to “B”, and living at home was set to “C”. These 12 inputs are shown in Table 1.

Through the data collection process, we ended up with 500 different observations. Following the collection of the data, a ten-fold cross validation was led to ensure that all the data was getting a chance to be represented and wasn’t being cherry-picked to get the best possible solution. This helps to ensure accuracy and reliability within this study. 10 training and 10 relating test sets were used from the 500 observations. This was done after ensuring that the data was in a random order – which it was as presented in the original file – then taking the last 50 observations and saving them into a test file. The remaining 450 observations were saved into a training file. For the next set of files, the 50 observations from the test set were placed at the top of the training observations in the previous file. Then the last 50 observations from the new set were removed and placed into a second test file while the 450 observations were placed into a second training file. This was done for all 10 data sets as the number of observations was divisible by ten and each observation was represented once in the data.

#### Table 1
Input variables
![Table 1](https://github.com/user-attachments/assets/38c478cb-a502-4815-a7a1-429b36fc2882)

#### 1.1 Training with the NNSOA
When using the NNSOA, there are two user-defined parameters which are MAXHID and MAXGEN. For the 10 training sets the hidden node search was administered using 100 generations, or MAXHID = 100. Once the appropriate structure was found, an additional 1000 generations were performed, or MAXGEN = 1000.

### 2. Results
Following the training of the 10 training sets, the HitRate of each run was calculated. The Hitrate shows the number of times that the prediction was correct compared to the total number of predictions conducted for that training set. The NNSOA found good solutions for predicting political parties with this dataset. For 8 out of the 10 runs conducted, the NNSOA was able to correctly classify all test observations. As shown in Table 2, the average HitRate for all 10 runs was 99.60%. This means that 99.60% of the time, the NNSOA was able to accurately predict the political party. Additionally, each solution and their HitRate were similar to each other with a standard deviation of 0.008433. The low standard deviation shows that the data and training conducted is reliable.

#### Table 2
HitRate percentages for the 10 Neural Network runs
![Table 2](https://github.com/user-attachments/assets/84bd494c-c75d-4d51-a910-bdac5f0c419f)

One characteristic of the NNSOA is to only utilize the input weights that are the most important and have a significant contribution to predicting the output. Each run uses its own number of hidden nodes, which then relates to the number of input weights that were used. For example, run 1 had 8 hidden nodes (shown in Table 3) and utilized 104 input weights This was calculated by taking the number of inputs (12) and adding 1 to account for the bias, this number was then multiplied by 8 for the number of hidden nodes. However, of the 104 input weights only 46 of them were nonzero (Table 4), meaning that they were used and significant. 

Table 3 shows the number of hidden nodes that were used during the 10 runs to achieve the desired solution. Run 1 and Run 2 used the highest number of hidden nodes with 8 and 9 hidden nodes used respectively. Run 9 and Run 10 used the lowest number of hidden nodes, both using 4. The average of hidden nodes used across all 10 runs was 6.1.

Table 4 looks at the input weights that were not equal to zero. This means that these weights were used and did contribute a significant amount to the solution. Run 1 used the most nonzero input weights at 46, while run 8 used the least at 17. The average number of nonzero input weights for all 10 runs was 29.3 nonzero weights. 

#### Table 3
Optimal hidden nodes
![Table 3](https://github.com/user-attachments/assets/ddb9ab6f-3fa3-4da8-b2d8-8281b6124670)

#### Table 4
Nonzero input weights
![Table 4](https://github.com/user-attachments/assets/541b4958-d733-42dc-96fb-a81489458814)

One highlight of using the NNSOA is that it gets rid of weights that aren’t important to the output which helps to lower the chances of errors while predicting the solutions. This can be a reason why the average HitRate was so good at 99.60%. Additionally, when looking at the input weights it can be determined that they are multicollinear, meaning they are related to each other. It can be said that WEIGHT and HEIGHT are related, and inputs SMOKE, DRUGS, and DRINK are related to each other. Overall, 63.10% of the weights were unused across the 10 runs, showing that much of the input variables had some sort of impact on the solution.

Table 7 lists the frequency of the relevant variables (inputs) in the 10 runs. Each nonzero weight that the inputs have counts as one and is totaled across all 10 runs. Essentially, this table helps to show if the input had an impact, and if so, how big, when predicting political parties. If an input was used in all 10 runs, then it can be determined that it is an important factor on the output. If an input wasn’t used in any of the 10 runs, then it can be concluded that this input isn’t needed for prediction. For this data set, HEIGHT was the only variable that wasn’t relevant in every run, it was relevant in 8 runs. Otherwise, the remaining 11 variables were relevant in all 10 runs. 

#### Table 7
Frequency of the relevant variables for all 10 runs
![Table 7](https://github.com/user-attachments/assets/997fbb1b-4715-4f0a-bded-e0fef71383cf)

Utilizing a sensitivity analysis can allow more insight into the impact of the input on the prediction output. The sensitivity analysis was created using a test set to determine degree of change and the direction of the input on the output. To create the test set, two artificial observations were created for each of the 12 input variables. In those observations, was the minimum and maximum values for each input from the initial 500 observations, ending with 24 total artificial observations. The remaining 22 input values (24 total artificial observations minus the 2 artificial observations for 1 input) were set to the average across the initial 500 observations. This was done so that when the artificial observations were run through the networks, the only thing that changed was the value of the input that was being focused on. 

When the sensitivity analysis was run in the networks, we were able take the two estimates for each input from the neural network and see how much they changed. Additionally this was used as a guideline to recognize trends. We were also able to determine if this change was a positive or negative change. Graph 1 shows the changes in the estimates for all 12 inputs. This graph shows that INCOME, SMOKE, DRUGS, DRINK, WEIGHT, and HOME all had a positive change. TEETH, GUNS, AGE, YEARS, HEIGHT, and GENDER all had a negative change. The variables with a positive change means that the estimates will increase in value for those variables, while those with a negative change will decrease in value. 

Additionally in Graph 1, we can look at the impact of the input on the result. The inputs with a larger amount (closer to -.05 or .05) will have the most impact. For the positively correlated variables, INCOME, SMOKE, DRUGS, and HOME have the largest bars so they have the biggest impact among the positive variables. For the variables with a negative change, GENDER is the largest and therefore has the biggest impact in that sense. Amongst the entire graph and all the variables, INCOME is the largest factor and has the largest impact on the solution. HEIGHT is the smallest factor and has the lowest impact on the solution. This makes sense because as shown in Table 7, HEIGHT was the only input that wasn’t used in all 10 runs.

### 3. Conclusion

The NNSOA was able to predict political parties while eliminating weights that didn’t have an impact on the outcome well. Through the training and testing process, the neural network was able to go to a simpler structure to test these data sets. The simple structure allows for the neural network to create more generalized solutions; meaning that it will work for all observations that it will see. The improvement of generalization in the neural network is important to make sure that it doesn’t become brittle or begin to memorize the inputs. Instead, it is creating rules that allow it to determine which pattern is the best for the data set that is being presented. This is also helpful to determine which weights are not needed, which can help the efficiency of the network. In all, the NNSOA was able to predict political parties and was easy to use while maintaining the integrity of the data involved.

#### Graph 1
Sensitivity Analysis
![Graph 1](https://github.com/user-attachments/assets/a5300a25-1549-46c7-8390-bf56a1e0cb89)

Overall, though the testing and training conducted with the 12 inputs with 500 observations produced good results. Limitations can arise through future testing and research conducted and even if the number of parties in the output is expanded.
