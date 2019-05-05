# picassopaintedit
Neural style transfer on images using [DeepAI API](http://deepai.org) and [Tensorflow Example](https://medium.com/tensorflow/neural-style-transfer-creating-art-with-deep-learning-using-tf-keras-and-eager-execution-7d541ac31398)

This application supports Neural style transfer on images in two modes.
1. fasttransform - Using DeepAI API.
2. deeptransform - Using [Neural Style Transfer with tf.keras](https://colab.research.google.com/github/tensorflow/models/blob/master/research/nst_blogpost/4_Neural_Style_Transfer_with_Eager_Execution.ipynb)

**Major Dependency:**
* DeepAI API
> https://deepai.org/api-docs/#neural-style
* TensorFlow and Keras
* Celery
> http://www.celeryproject.org/
* AWS EC2 instance for running deeptransform and S3 for storing images.

**app.py**

* Flask application to support fasttransform and deeptransform endpoints.

_Input:_
* key - Neural style transform request key. 
* style_url - URL of the style image used neural style transformation.
* content_url - URL of the content image used neural style transformation.

_Output_
* key - Neural style transform request key. 
* tranformed_image_url - URL of the neural style transformed image.

**flask_celery.py**

* deeptransform is handled asynchronously using flask_celery.

**deeptransformimpl.py**

* Starting point for handling asynchronous task for flask_celery.

**neuralstyle.py**

* Implementation of deeptransform based on [Neural Style Transfer with tf.keras](https://colab.research.google.com/github/tensorflow/models/blob/master/research/nst_blogpost/4_Neural_Style_Transfer_with_Eager_Execution.ipynb).

**util.py**

* Implements util functions for storing neural style transformed images on AWS S3 and sending deeptransform notification.
