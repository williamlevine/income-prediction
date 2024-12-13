# Income Prediction Neural Network

### William Levine - Adolphus Momoh - Dylan Phimister - Michael Rhee

## Overview


## Instructions

To run the model, first clone the repository to your local machine, or download all necessary files individually.

Next, in your browser, navigate to Google Drive. Ensure you are ready to use Google Colaboratory. To check if you have Colaboratory prepared on your Google Drive account, click the `+ New` button at the top left of the screen, and then `More` at the bottom of the dropdown menu. If Google Colaboratory does not appear, you will need to connect it to your account by clicking the `+ Connect more apps` button. You will be directed to Google Workspace Marketplace, from which you can install Google Colaboratory. After setting it up, return to the Drive homepage.

Using the leftmost sidebar, navigate to `My Drive`. Create a new folder titled `income_prediction`. **The code uses specific, hard-coded file paths to retrieve the data, so it is crucial that this folder name appears exactly as it does here, and that it is stored in `My Drive`.** If you care to change the path in which you store the materials for this model, make sure to update the file paths in the code accordingly.

From the `Notebooks` folder in the repository, drag the files titled `first_model.ipynb`, `tuned_model.ipynb`, and `tuned_model_2.ipynb` to the `income_prediction` folder in your Google Drive.

From the `Resources` folder in the repository, drag the file titled `cleaned_df.csv` to the `income_prediction` folder in your Google Drive.

Once the `.ipynb` files and the `.csv` files are loaded into your `income_prediction` folder, right click on `first_model.ipynb`. Hover over `Open with`, and then click on `Google Colaboratory`. 

You should now be able to run the model by clicking `Runtime` on the top menu bar, and then `Run all`.

You may be prompted to allow Google Colaboratory to mount to your Google Drive account. Allow this to happen by following the on-screen prompts.

The code will run. At the bottom of the screen, you will see the model’s accuracy and loss percentages.

The same procedure can be followed for the tuned models by opening the `tuned_model.ipynb` and `tuned_model_2.ipynb` with Google Colaboratory.

## Process

### Data Cleaning and ETL
The initial dataset was in a file called `adult.data`. This file, along with the `adult.names` file, can be found in the `Resources` section of the repository. To clean the data, we brought the `adult.data` file into Python, and turned it into a pandas DataFrame. This dataset had 14 columns: 13 of these columns were feature columns, and one was the target column of income. We did some cursory investigation of the DataFrame to make sure that its data types were correct, that it didn’t have any null values, and that the target column was properly binary. Unnecessary columns were dropped, the target column was formatted to have values of 0 or 1, and the DataFrame was exported as a csv titled `cleaned_df.csv`. The notebook for this data cleaning is titled `data_cleaning.ipynb`, and can be found in the `Notebooks` folder in the repository. The `.csv` file which it outputs can be found in the `Resources` folder in the repository.

As part of the ETL pipeline for this model, the cleaned `.csv` was, in a new notebook, loaded into a Spark DataFrame. This Spark DataFrame was then converted to a pandas DataFrame for easier manipulation. We could then convert categorical columns, such as ‘workclass’, ‘marital-status’, and ‘native-country’, to numerical columns using the `get_dummies` method. We split the data into a target and a feature array, and then used `train_test_split` to split the data into training and testing sets. We normalized the data with `StandardScaler`, and then fit and scaled the data.

### First Model
For the first model, we opted for two hidden layers, both activated with `relu` functions and with 80 and 30 units, respectively. The output layer used a `sigmoid` activation function. After fitting this model with 100 epochs, we received our first accuracy and loss percentages of **83.76%** and **54.26%**, respectively. The code for this model, as well as for the data cleaning and ETL process, can be found in the file titled `first_model.ipynb`, located in the `Notebooks` folder.

![first_model](https://github.com/user-attachments/assets/ecf54922-c83a-4303-9f57-d3e0118a157d)

### First Tuning
Before altering the data which was fed into the model, we tried a few different tuning techniques to raise accuracy and lower loss. These techniques included:
-	Adding Dropout to hidden layers, helping to prevent overfitting the model
-	Reducing number of epochs from 100 to 50
-	Adding BatchNormalization
-	Adjusting dropout rate from 0.2 to 0.3
-	Adding another hidden layer and increasing number of units to 128, 64, and 32

These techniques led to a small increase in accuracy, with a final percentage of **85.71%**, but significantly decreased loss, with a percentage of **31.42%**.

![tuned_model](https://github.com/user-attachments/assets/d8937edc-6008-4a25-acf9-8663c50518db)

### Further Data Cleaning

We decided to bin the 'native-country' column to try and help increase our accuracy score and decrease our loss. We binned this into two groups, "United States" and "Not United States". This was then turned into its own column called 'native-country-binned' and would be binary where 1 is "United States" and 0 is "Not United States". This is done to better help the model's accuracy.

### Further Tuning
We tried a few more tuning techniques to raise accuracy and lower loss after the binning. These techniques included:
- Added an additional hidden layer
- Adjusted the dropout rate from 0.3 to 0.5
- Added binning to 'native-country' column to help improve the model's accuracy


## Sources
Original data set: https://archive.ics.uci.edu/dataset/2/adult
