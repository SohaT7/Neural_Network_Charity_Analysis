# Neural_Network_Charity_Analysis

## Overview of the Loan Prediction Analysis
The purpose of this analysis was to determine which charitable donations were being successfully utilized by the receiver. This analysis employs deep-learning neural networks in order to help achieve that goal.

## Results
### Data Preprocessing:

- What variable(s) are considered the target(s) for your model? The target variable is 'IS_SUCCESSFUL' which tells us if the charitable donation was successfully utilized by the receiving entity or not.

- What variable(s) are considered to be the features for your model? The features variables are: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL_CONSIDERATIONS', and 'ASK_AMT'.

- What variable(s) are neither targets nor features, and should be removed from the input data? The variables 'EIN' and 'NAME' were removed from the input data for they do not add any data useful to our purposes. If we are looking to further reduce the features variables, we can also drop 'SPECIAL_CONSIDERATIONS' as the special consideration (or lack thereof) of an application is not likely to affect or tell us at this point in time which entity will in the future successfully utilize the donation.

### Compiling, Training, and Evaluating the Model:

- How many neurons, layers, and activation functions did you select for your neural network model, and why? This model starts off with two hidden layers containing 80 and 30 neurons respectively. This is because the data contains 42 features variables after preprocessing (as shown below in the dataframe; ignore the index and 'IS_SUCCESSFUL' columns in order to count accurate features variables' total number). 
![Features](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/Images/preprocessed_data.png)
The neuron rule of thumb says that the neurons selected for the hidden layer must be two or three times larger than the number of features variables (hence we rounded it off to 80). The following layer should have a lower number, hence 30. The activation function ReLU was used for the hidden layers, and sigmoid for the output layer since the latter is a binary classified layer. The loss function used is binary_crossentropy and the optimizer used is adam.

- Were you able to achieve the target model performance? Unfortuantely, the target model performance could not be reached. The accuracy for the model was 73.3%, and the 4 optimization attempts resulted in 71.07%, 71.07%, 71.02%, and 70.97% accuracy levels, respectively. 

- What steps did you take to try and increase model performance?

We tried optimizing our model performance and made 4 attempts with the following specification changes:
    - Attempt 0: Added neurons to the 2 hidden layers (80 increased to 120; 30 increased to 70).
    - Attempt 1: Added neurons to the 2 hidden layers (80 increased to 100; 30 increased to 50) and changed activation function on output layer to tanh.
    - Attempt 2: (Experiment) Reduced neurons in the 2 hidden layers (80 decreased to 30; 30 to 20).
    - Attempt 3: Added neurons to the 2 hidden layers (80 increased to 100; 30 increased to 50) and added a third layer with 10 neurons only.

## Summary
To summarize, our deep learning model did not reach the ideal of an accuracy rate of 75%. The activation function tanh was used on the output layer during an optimization attempt, since tanh is known to be good when working with binary classifications with nonlinear data. However, that did not yield any better results. Since our model is trying to predict a binary classification, we can try using a supervised learning model instead: the Random Forest Classifier. It is not only high when it comes to interpretability but also might bring us higher accuracy rates.
