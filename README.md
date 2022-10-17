# Neural_Network_Charity_Analysis
## Table of Contents
- [Overview of the Analysis](#overview-of-the-analysis)
    - [Purpose](#purpose)
    - [About the Dataset](#about-the-dataset)
    - [Tools Used](#tools-used)
    - [Description](#description)
- [Results](#results)
    - [Preprocessing Data for a Neural Network Model](#Preprocessing-Data-for-a-Neural-Network-Model)
        - [Determining the Target and Features Variables](#Determining-the-Target-and-Features-Variables)
        - [Density Plots and Binning](#Density-Plots-and-Binning)
        - [Encoding Categorical Variables](#Encoding-Categorical-Variables)
        - [Splitting the Preprocessed Data](#Splitting-the-Preprocessed-Data)
        - [Standardizing the Numerical Variables](#Standardizing-the-Numerical-Variables)
    - [Compiling, Training, and Evaluating the Model](#Compiling,-Training,-and-Evaluating-the-Model)
    - [Optimizing the Model](#Optimizing-the-Model)
- [Summary](#summary)
- [Contact Information](#contact-information)

## Overview of the Analysis
### Purpose:
The purpose of this analysis is to determine which organizations are worth donating to and which ones are high-risk. 

### About the Dataset:
The Alphabet Soup Charity dataset contains data on more than 34,000 organizations that have received charitable donations from it over the years. The dataset can be found in the following CSV file:
 - [charity_data.csv](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/charity_data.csv)

The dataset has metadata on each organization in the following columns:
 - EIN and NAME - Identification
 - APPLICATION_TYPE - Alphabet Soup application type
 - AFFILIATION - Affiliated sector of industry
 - CLASSIFICATION - Government organization classification
 - USE_CASE - Use case for funding
 - ORGANIZATION - Organization type
 - STATUS - Active status
 - IMCOME_AMT - Income Classification
 - SPECIAL_CONSIDERATIONS - Special considerations for the application
 - ASK_AMT - Funding amount asked for
 - IS_SUCCESSFUL - Whether the money was utilized effectively or not

### Tools Used:
 - Python (TensorFlow, Pandas, and Scikit-Learn libraries)

### Description:
The purpose of this project (code to be found in the file [AlphabetSoupCharity.ipynb](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity.ipynb) is to design a neural network (a deep learning model) to create a binary classification model that can predict if an organization that receives donations will be succesful in utilizing the donations in an impactful way or not. 

The data is preprocessed: the target and features variables are determined, density plots are created to successfully bin the unique values, the categorical variables are encoded, and the data is split followed by standardizing the numerical variables. Next, the deep learning model is designed by assigning the number of hidden layers to be used, the number of neurons in each hidden layer, and the activation functions to be used by the hidden and outer layers. The results are saved in an output file [AlphabetSoupCharity.h5](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity.h5).

## Results
### Preprocessing Data for a Neural Network Model
#### Determining the Target and Features Variables
The data in [charity_data.csv](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/charity_data.csv) is read into a Pandas DataFrame. The variables 'EIN' and 'NAME' are removed from the input data for they are neither target nor features variables, and do not add anything useful for our purposes.

The target variable is 'IS_SUCCESSFUL' which tells us if the charitable donation was successfully utilized by the receiving organization or not. The features variables are: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL_CONSIDERATIONS', and 'ASK_AMT'.

#### Density Plots and Binning
The unique values for each column are determined. If the unique values exceed 10 in number, a density plot is created to determine the distribution of the column values. The density plot is then used to determine a cutoff point, which allows the 'rare' values to be binned into the 'Other' column.

INSERT PICS

#### Encoding Categorical Variables
A list for categorical variables is generated. The categorical variables are then one-hot encoded, and placed into a new DataFrame. This DataFrame and the orginal DataFrame are then merged, and the originals dropped.

![DataFrame for Preprocessed Data](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/Images/preprocessed_data.png)

#### Splitting the Preprocessed Data
The preprocessed data is then split into arrays for features and target. It is also split into training and testing sets. 

#### Standardizing the Numerical Variables
Scikit-Learn's StandardScaler class is used to standardize the numerical values. 

### Compiling, Training, and Evaluating the Model
This model (code can be found in the [AlphabetSoupCharity.ipynb](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity.ipynb) file) starts off with two hidden layers containing 80 and 30 neurons respectively. This is because the data contains 42 features variables after preprocessing and the 'neuron rule of thumb' says that the neurons selected for the hidden layer must be two or three times larger than the number of features variables (42 * 2 = 84; rounding it off gives us 80). The following layer should have a lower number, hence 30. The activation function ReLU was used for the hidden layers, and sigmoid for the output layer since the outer layer is a binary classified layer. The loss function used is 'binary_crossentropy' and the optimizer used is 'adam'.

ADD CODE?

The model is then trained (or 'fit') using the training set. A callback is created which saves the model's weights every 5 epochs. The model is evaluated by using the test data to determine its accuracy and loss. The results are saved and exported to an HDF5 file [AlphabetSoupCharity.h5](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity.h5).

### Optimizing the Model
The model has an accuracy level of 73.3%. Four attempts to optimize the model were made with the following specification changes:
 - Attempt 0 [[code](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization-Attempt_0.ipynb)] [[output](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization_0.h5)]: Added neurons to the 2 hidden layers (80 increased to 120; 30 increased to 70).
 - Attempt 1 [[code](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization-Attempt_1.ipynb)] [[output](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization_1.h5)]: Added neurons to the 2 hidden layers (80 increased to 100; 30 increased to 50) and changed activation function on output layer to tanh.
 - Attempt 2 [[code](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization-Attempt_2.ipynb)] [[output](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization_2.h5)]: (Experiment) Reduced neurons in the 2 hidden layers (80 decreased to 30; 30 to 20).
 - Attempt 3 [[code](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization-Attempt_3.ipynb)] [[output](https://github.com/SohaT7/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization_3.h5)]: Added neurons to the 2 hidden layers (80 increased to 100; 30 increased to 50) and added a third layer with 10 neurons only.
    
Unfortunately, none of these four attempts yielded higher accuracy levels for the model. The accuracy scores for these four attempts are as follows:
 - Attempt 0: 71.07%
 - Attempt 1: 71.07%
 - Attempt 2: 71.02%
 - Attempt 3: 70.97%

## Summary
The deep learning model designed herein has an acuuracy level of 73.3%. It comprises of two hidden layers, with 80 and 30 neurons respectively. The hidden layers use ReLU as the activation function, and the outer layer uses the sigmoid as the activation function. Four attempts were made to optimize the model by trying out different variations on numbers of neurons added, adding a third hidden layer, and changing the activation function used by the outer layer. All four of these yielded an accuracy level lower than 73.3%. Since the model here tries to predict a binary classification, we can try setting up a supervised learning model instead, such as the Random Forest Classifier. Not only is that highly interpretable but might also yield higher accuracy levels. 

## Contact Information
Email: st.sohatariq@gmail.com
