# Neural_Network_Charity_Analysis
## Table of Contents
- [Overview of the Analysis](#overview-of-the-analysis)
    - [Purpose](#purpose)
    - [About the Dataset](#about-the-dataset)
    - [Tools Used](#tools-used)
    - [Description](#description)
- [Results](#results)
    - [Preprocessing Data for a Neural Network Model](#Preprocessing-Data-for-a-Neural-Network-Model)
    - [Compiling, Training, and Evaluating the Model](#Compiling,-Training,-and-Evaluating-the-Model)
    - [Optimizing the Model](#Optimizing-the-Model)
- [Summary](#summary)
- [Link to the Dashboard](#Link-to-the-Dashboard)
- [Contact Information](#contact-information)

## Overview of the Analysis
### Purpose:
The purpose of this analysis is to determine which organizations are worth donating to, and which ones are high-risk. 

### About the Dataset:
The Alphabet Soup Charity dataset contains data on more than 34,000 organizations that have received charitable donations from it over the years. The dataset can be found in the following CSV file:
 - [charity_data.csv]()

The dataset collects metadata on each organization in the following columns:
 - EIN and NAME - Identification
 - APPLICATION_TYPE - Alphabet Soup application type
 - AFFILIATION - Affiliated sector of industry
 - CLASSIFICATION - Government organziation classification
 - USE_CASE - Use case for funding
 - ORGANIZATION - Organization type
 - STATUS - Active status
 - IMCOME_AMT - Income Classification
 - SPECIAL_CONSIDERATIONS - Special considerations for the application
 - ASK_AMT - Funding amount asked for
 - IS_SUCCESSFUL - Whether the money was utilized effectively or not

### Tools Used:
 - Python (TensorFlow, Pandas, Scikit-Learn)

### Description:
The purpose of this project is to design a neural network (a deep learning model) to create a binary classification model that can predict if an organization that receives donations will be succesful in utilizing the donations in an impactful way, or not. The data is preprocessed through determining the target and features variables in our dataset, creating density plots to successfully bin the unique values, encoding the categorical variables, splitting the data, and followed by standardizing the numerical variables. 

Next, the deep learning model is designed by assigning the number of hidden layers to be used, the number of neurons in each, and the activation function sto be used by the hidden and outer layers.

## Results
### Preprocessing Data for a Neural Network Model
#### Determining the Target and Features Variables
The data in [charity_data.csv]() is read into a Pandas DataFrame. The variables 'EIN' and 'NAME' were removed from the input data for they are not target or features variables, and do not add anything useful for our purposes.

The target variable is 'IS_SUCCESSFUL' which tells us if the charitable donation was successfully utilized by the receiving entity or not. The features variables are: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL_CONSIDERATIONS', and 'ASK_AMT'.

#### Density Plots and Binning
The unique values for each column are determined. If the unique values exceed 10 in number, a density plot is created to determine the distribution of the column values. The density plot is then used to determine a cutoff point, which allows the 'rare' values to be binned into the 'Other' column.

#### Encoding Categorical Variables
A list for categorical variables is generated. The categorical variables are then one-hot encoded, and placed into a new DataFrame. 
This DataFrame and the orginal DataFrame are then merged, and the originals then dropped.

INSERT DF

#### Splitting the Preprocessed Data
The preprocessed data is then split into arrays for features and target. It is also split into training and testing sets. 

#### Standardizing the Numerical Variables
Scikit-Learn's StandardScaler class is used to standardize the numerical values. 

### Compiling, Training, and Evaluating the Model
This model starts off with two hidden layers containing 80 and 30 neurons respectively. This is because the data contains 42 features variables after preprocessing (as shown below in the dataframe; ignore the index and 'IS_SUCCESSFUL' columns in order to count accurate features variables' total number). 

![Features](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/Images/preprocessed_data.png)

The neuron rule of thumb says that the neurons selected for the hidden layer must be two or three times larger than the number of features variables (hence we rounded it off to 80). The following layer should have a lower number, hence 30. The activation function ReLU was used for the hidden layers, and sigmoid for the output layer since the outer layer is a binary classified layer. The loss function used is 'binary_crossentropy' and the optimizer used is 'adam'.

ADD CODE?

The model is then trained (or 'fit') on the training set. A callback is created which saves the model's weights every 5 epochs. The model is evaluated by using the test data to determine its accuracy and loss. The results are saved and exported to an HDF5 file.

### Optimizing the Model
The model has an accuracy level of 73.3%. Four attempts to optimize the model were made with the following specification changes:
 - Attempt 0: Added neurons to the 2 hidden layers (80 increased to 120; 30 increased to 70).
 - Attempt 1: Added neurons to the 2 hidden layers (80 increased to 100; 30 increased to 50) and changed activation function on output layer to tanh.
 - Attempt 2: (Experiment) Reduced neurons in the 2 hidden layers (80 decreased to 30; 30 to 20).
 - Attempt 3: Added neurons to the 2 hidden layers (80 increased to 100; 30 increased to 50) and added a third layer with 10 neurons only.
    
Unfortunately, none of these four attempts yielded higher accuracy levels for the model. The accuracy scores for these four attempts are as follows:
 - Attempt 0: 71.07%
 - Attempt 1: 71.07%
 - Attempt 2: 71.02%
 - Attempt 3: 70.97%

## Summary
The deep learning model designed herein has an acuuracy level of 73.3%. It comprises of two hidden layers, with 80 and 30 neurons respectively. The hidden layers use ReLU as the activation function, and the outer layer uses the sigmoid as the activation function. Four attempts were made to optimize the model by trying out different variations of numbers of neurons added, adding a third hidden layer, and changing the activation function used by the outer layer. All four of these yielded an accuracy level lower than 73.3%. Since the model here tries to predict a binary classification, we can try setting up a supervised learning model, such as the Random Forest Classifier instead. Not only is that highly interpretable but might also yield higher accuracy levels. 

## Contact Information
Email: st.sohatariq@gmail.com
