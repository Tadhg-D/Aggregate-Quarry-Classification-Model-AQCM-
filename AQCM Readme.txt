
Pyrite Source Model
This notebook contains the code for modelling pyrite sources.

The code is contained in this notebook, below, and it provides for training and saving a model, given some input chemical data along with sources, or predicting sources, just given the chemical data.

The code implements 2 types of model:

a linear, Logistic Regression model
a non-linear, "tree" Random Forest model
When you train a model it will output to the screen the score of the model, the percentage of predictions it gets right. The Logistic Regression model scores ~88% (there's a random element to the scores, you won't get the same thing every time), the Random Forest is better, scoring ~96%. The Logistic Regression model has the benefit of being easier to interpret, as explained below.

The linear model is the default. In both cases I've trained a model already, and they are in the artifacts folder, they are called model_linear.pkl and model_tree.pkl. If an artifacts folder doesn't exist the code will make one.

When you train a model this also creates a feature importances file in the artifacts folder. Again, I've already trained one model of each so these files are in the folder.

Feature Importances
These files contain the information on how the model uses the input to predict the Source.

feature_importances_linear.csv: This file has a row for each Source, and a column for each of the features it uses to make the predictions. You can easily interpret these values, for a given row the value for a given chemical tells you how this chemical changes the prediction.

For example, for Source A and Fe we have the value, -2.643681213392997. This means that increasing the amount of Fe decreases the likelihood that a given sample comes from Source A. For Source A and S we have, 3.953436861312359. This means that increasing the amount of S increases the probability that a sample comes from Source A, and it has a larger effect than Fe (since the absolute value is greater).

feature_importances_tree.csv: This file has a row and a value for each chemical. These values are less easy to interpret, all we can say is that the larger the absolute value, the more important that chemical is in making the prediction, i.e. the stronger the relationship between this chemical and Source.

Inputs and Outputs
To train a model the code expects input in a csv file (formatted like the one in the train folder). It should have a column called Source, and it will try to learn to predict this using the other columns. It requires the other columns to be called:

Fe, S, Co, Cu, Zn, As, Se, Mo, Ag, Sb, Pb, Stoichiometry

To make a prediction it expects all of the columns above, except Source, in a file formatted like the training file. It will output a file called output.csv, which is exactly the same as the input file but with an added column called Prediction.

How to use
To train a model (which I've already done on the data you've provided, you won't need to redo this unless you're using new data), set mode (in the cell below) equal to 'train'. For predicting, set it to 'predict'.

Next decide what kind of model (as described above) you want to train/predict with. For Logistic Regresion set model_type equal to 'linear', for the Random Forest model set it to 'tree'.

Finally add the location of the data that you want to train/predict with, set filename to this path. By path I mean the full fodler and filename of the data you want to use, something like: 'C:\Windows\User\Desktop\train.csv'. (I've set it to 'train/train.csv', this works on my machine but will not work on yours. 'train\train.csv' might, but the best bet is to go to the file and click on it, I think that shows the full path).
