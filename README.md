# OCR on Devanagiri Handwritten Characters

Just like the MNIST Dataset for English digits, a dataset for "Hindi" or "Devanagiri" characters also exists.
The aim of this mini-project is to create ML and DL models which can effectively identify the characters.

## Filing structure

There are three folders in this project.
1. The **data** folder contains all the data. It may be the original data oe even the data created during the modelling.
2. The **models** folder saves all the models which one may need to save during or after modelling. It may also save pre-built models which are useful for the application.
3. The **notebooks** folder contains almost all the coding. This folder will be used to load, explore and manipulate the data and then eeven create the models and save them in the respective folders.

### Data folder

1. **DevanagariHandwrittenCharacterDataset** - This is the actual dataset which we have in the beginning of the project. This dataset can be found at [this UCI link](https://archive.ics.uci.edu/ml/datasets/Devanagari+Handwritten+Character+Dataset).
2. **Train.csv, Test.csv** - These two csv files save the flattened arrays of the digit images. This file can directly become a Pandas dataframe and then used to create models.
3. **test.png** - This image is used to create a manual prediction to see if the model is able to predict correctly.

### Models folder

1. **Digit OCR model** - This is the first SVM model created during the project.
2. **Digit OCR best model** - This is the tuned SVM model.
3. **NN model** - This is the best Neural Network model created during the project.


### Notebooks folder

#### Hindi Digits Recognition and Hyperparameter Tuning for SVM Classifier

This notebook is just for digit recognition and only uses SVM classifier. It does not classify all characters because SVM models take a long time in training and prediction with an increase in the amount of data.

The notebook shows how images can be preprocessed to perform ML tasks and how Hyperparameter tuning is done using *GridSearch*.


#### Hindi OCR Deep Learning

This notebook is used to classify all the characters using Deep Learning models. We preprocess the data differently by skipping the flattening. The image can be flattened by the model directly.

We create a Simple Neural Network and a Convolutional Neural Network (CNN) to see how CNNs are more effective in learning from images. The notebook aims to create a faster, more effective model to classify all the characters present in the dataset.