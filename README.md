# OCR on Devanagiri Handwritten Characters

Just like the MNIST Dataset for English digits, a dataset for "Hindi" or "Devanagiri" characters also exists.
The aim of this mini-project is to create ML and DL models which can effectively identify the characters.

## Filing structure

There are five folders and an app.py file in this project.
1. The **data** folder contains all the data. It may be the original data oe even the data created during the modelling.
2. The **models** folder saves all the models which one may need to save during or after modelling. It may also save pre-built models which are useful for the application.
3. The **notebooks** folder contains almost all the coding. This folder will be used to load, explore and manipulate the data and then eeven create the models and save them in the respective folders.
4. The **templates** folder is used to store our html pages. A template is an HTML file which can receive Python objects and is linked to the Flask application.
5. The **static** folder stores Style sheets, scripts, images and other elements that will never be generated dynamically. We will place our Javascript and CSS files in it.
6. The **app.py** file is the main code that will run our Flask application. It will contain the different routes for our application, respond to HTTP requests and decide what to display in the templates. In our case, it will also call our CNN classifier, operate pre-processing steps for our input data and make predictions.

The frontend of our project requires Two static files : draw.js and styles_draw.css , Two template files : draw.html and results.html. , Our main file : app.py , Our model_cnn.plk saved earlier. We use the data from the data folder, store our tensorflow.keras code files in our notebooks folder, use these .ipynb files to generate our model and store them in the models folder. Finally the frontend utilises **NN_model.h5** saved model to generate predictions.

## Generating our CNN model

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

Now that our model is ready, we would like to embbed it into a Flask Web-App.

## Flask-Cnn-Recognition-App
Flask Hindi Character Recognition Application based on CNN model

### Static folder

#### styles_draw.css
This css file includes the basic css required for the html page 

#### draw.js
This Javascript code allows us to design and interact with our drawing area.
drawCanvas() aims to initialize the canvas’ main functions (mouseUp, mouseDown, …) that will allow interactions with the user’s mouse.
addClick() saves the cursor’s position when the user clicks on the canvas.
redraw() clears the canvas and redraws everything each time the function is called.

### templates

#### draw.html
This html page is made to acquire the user input : a drawing that will be classified by our trained model. To do so, we wil design the drawing area using javascript and HTML5.

We import our css and js files located in the static folder using {{url_for('static',filename='styles_draws.css’)}}and {{url_for('static',filename='draw.js’)}}. This is the Jinja syntax to import files.

We set our drawing area with the <canvas> tag.

We call the drawCanvas() javascript function contained in draw.js.

We initialize our form so we can use the POST method to send data to our flask instance/app.py.
action = “{{url_for('predict')}” is again Jinja syntax. It specifies the path that will be used in app.py when submitting the form.

We add an extra hidden field to our form which will be used to transfer the image.<input type = “hidden“ id =’url' name = ‘url' value = “”>

#### results.html
We use results.html to display the prediction computed in app.py. We will again need to use the Jinja syntax to display the prediction.

### app.py
1) Initializing the app and specifying the template folder. We can do that using this line of code :
app = flask.Flask(__name__, template_folder =’templates’)
2) Define the routes (only two for our app) :
@app.route(‘/’) : Is our default path — It will return the default draw.html template.
@app.route(‘/predict’) : Is called when clicking on the ‘predict’ button. Returns the results.html template after processing the user input.
3) The predict function will be triggered by a POST action from the form (remember when we set this path in result.html thanks to Jinja syntax ! ). It will then proceed as follows :
Access the drawing input with request.form['url'] , where ‘url’ is the name of the hidden input field in the form which contains the encoded image.
Decode the image and set it into an array.
Resize and reshape the image to get a 32 * 32 input for our model. We care about keeping its ratio.
Perform the prediction using our CNN classifier.
As model.predict() returns a probablity for each class in a single array, we must find the array’s highest probability and get the corresponding class using the pre-defined dictionary.
Finally return the results.html template and pass the previously made prediction as parameter :
return render_template('results.html', prediction= final_pred)

This project is made by Hitesh Goyal, Nirmal Prabhu and Akhil Shaji.

It aims to deploy a Deep Learning Model using Flask.