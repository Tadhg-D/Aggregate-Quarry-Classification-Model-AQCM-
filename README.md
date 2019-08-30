# Aggregate-Quarry-Classification-Model-AQCM-
User guide for the Aggregate quarry classification model (AQCM)

# Software needed to run AQCM
The AQCM is a notebook file which contains both computer code and text elements. To run and edit the code a Notebook application
needs to be intsalled. [Ananconda Distribution]( https://www.anaconda.com/distribution/) is the recommended notebook software. This includes
Python, Jupyter Notebook, and other commonly used packages for scientific computing and data science. *Jupyter Notebook App* can be run on desktop
requiring no internet access or it can be installed on a remote server which can be accessed through the internet.

## Models used in the AQCM

1. A linear, [Logistic Regression model](https://en.wikipedia.org/wiki/Logistic_regression)
2. A non-linear, "tree" [Random Forest model](https://en.wikipedia.org/wiki/Random_forest)

The linear model is the default model for the AQCM. Both models are contained within the **artifcats** folder, they are called ``model_linear.pkl``
and ``model_tree.pkl``. 

# Training the AQCM
The model first needs to be trained. To train the model, set ``mode`` equal to ``train``. The model will then expect a CSV file to be inputted. 
To input the CSV file set ``filename``to equal the file destination, this is the **full** folder and filename (e.g. *r"C:\Users\Documents\file1"*). The file destination link is found by
holding the **Shift key** and **right-clicking** on the desired file. 

***For Windows users please ensure that the ***r*** is placed before the pathway link to the file***.

Next decide which model you want to train/predeict with.  For **Logistic Regresion** set ``model_type`` equal to *linear*, for the **Random Forest** model 
set it to *tree*.

The next step is to input the column names from the CSV file into the ``feats = [] ``. If the elements/column names 
needed for classification are "Fe, S, Co and Pb", please ensure that the ``feats = [] `` equals to ``feats = ["Fe", "S", "Co", "Pb"] ``. 

***DO NOT INCLUDE "SOURCE" WITHIN THE ``feats = [] ``***

Finally, ensure that ``target = []`` equals to "Source" or whatever term you would like to classify your data by. For instance, f you are classifying "Rock type"
or "Rock formation", ensure that ``target = [] `` equals to these terms (e.g. ``target = ["Rock type"] `` and that they are included as the first column
of the CSV file.

To run the model just go to *Cell* in the menu bar, and select *Run all*.

If successful, an average 10-fold cross validation score will then appear.
If unsuccessful, an ``AssertionError`` will appear detailing the problem which has caused the model to fail.

The model will only need to be trained once if using the same dataset and same varibales. However, if new variables are added or a new dataset is introduced
the model will have to be retrained.

###### Formatting of CSV file
Any CSV used for classification in the AQCM must formatted like the ``AQCM_training_data.csv`` file. It should have a column called *Source*,
and the model will try to learn to predict this using the other columns supplied. Please ensure that all the columns supplied in the CSV, apart from *Source*,
are contained with the ``feats = []``. The easiest way to ensure this is done is by simply *copying and pasting* the column headings into the ``feats = [] ``.

# Testing the AQCM

To test the model set ``mode`` to equal ``predict``. Next enter the training dataset CSV into ``filename =``, this CSV file should be formatted 
much like the ``AQCM_training_data.csv``, however, "Source" column should not be contained as this is what the model will try to predict.

Next, re run the model using *Cell* and *Run all*.

If successful, a message saying *Prediction complete, model predictions saved to...* will appear. This will prompt a new CSV file, entitled *output*
to be saved within the model folder. 

## CSV Output file