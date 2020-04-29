# MNIST-web-interface

A gorgeously ugly user interface for training and predicting with a model stored in a server

![](mnist-web.gif)

It can:
  1. Predict a drawn digit.
  2. Store multiple drawings of a digit and use them to enhance the server's neural network's model.
  
 
  
The website's DOM is updated without refreshing the page, the UI is responsive since the page was arranged with Bootstrap 4.

The server runs with flask and all the neural network code with the Tensorflow and Keras libraries for Python.

The base model was trained using the MNIST dataset.

The prediction works as follows:
  1. The user draws a digit on the canvas (made with HTML5 and JS)
  2. After clicking on "PREDECIR" the data is read by JS, converted into a string and a POST request is 
    sent to the server along with an identifier ("p" for prediction) to handle the request.
  3. The image data is prepared before entering the neural network:
      a) It's reshaped to 2D
      b) It's resized.
      c) it's normalized to only contain pixel values of 0's and 255's (black and white).
      d) The image's centroid is calculated and placed in the middle (the image is centered).
  5. The prepared image is fed to the model using keras which returns the digit with the biggest 
     prediction score.
  6. The prediction is rendered with the html and displayed.
  
 The training works as follows (omitting steps explained before):
  1. The user draws a digit and clicks on "Añadir".
  2. The image is sent to the server and prepared for the database (made 2D, resized, centered and 
      converted to black and white).
  3. The treated image is stored as /temp/[SESSION_ID]/[IMAGE_NUMBER]
  4. A thumbnail of the stored images are displayed above the drawing canvas.
  5. If the user clicks "Borrar último", the last drawing stored is deleted and its thumbnail disappears.
  5. When the user clicks on "Entrenar" javascript makes sure a ground-truth is given and makes a request.
  6. The server trains the model with the given ground-truth and the drawings stored.
  7. The stored drawings are erased.
