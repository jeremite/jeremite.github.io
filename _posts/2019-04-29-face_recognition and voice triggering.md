---
layout: post
title:  "Face Detection and Recognition Model"
date:   2019-04-29
excerpt: "A live-streaming face detection and recognition model; and a Voice triggering model"
project: true
tag:
- CNN
- Transfer learning
- Face recognition
- triple loss function
- cosine similarity
comments: true
---

CLICK HERE:
[Notebook Version](https://github.com/jeremite/Roll_Call_AI/blob/master/AI_rollCall1005.ipynb)



## Overview
In this project, I transfer-learnt the pre-trained *faceRecoModel* to transform every input image into a *vector with 128 dimensions.*, then the *cosine similarity* was used to pair the image with the pre-saved images in the database in order to recognize the image. The input image would be a *face* detected and cropped from a living stream operated by *CV2* module from *opencv* package.
I even tried a *word-trigeer* function: the model will recognize the voice of the word 'activate', then open the camera for the following face recognition.


## Build Face Database 
The Database features the dictionary format, with the *name* of the face as the *key* and the image-transformed 128-d *vector* as the *value*. <br>
There are at least two ways to save *faces* into the database: I could both collect people's photos or use the camera; Then the faces in the photos or the living-stream will be detected and sent into *faceRecoModel* to be turned into vectors and saved into the Database.
### face detection
    # using detectMultiScale function in cv2.CascadeClassifier() to detect faces
    cascade = cv2.CascadeClassifier(cascade_path)                
    faceRects = cascade.detectMultiScale(frame_gray, scaleFactor = 1.2, minNeighbors = 3, minSize = (32, 32))        
    if len(faceRects) > 0:                 
        for faceRect in faceRects: 
            x, y, w, h = faceRect
### transform face images into vectors
    def img_to_encoding(image_path, model):
        img1 = cv2.imread(image_path, 1)
        img = img1[...,::-1]
        img = np.around(np.transpose(img, (2,0,1))/255.0, decimals=12)
        x_train = np.array([img])
        embedding = model.predict_on_batch(x_train)
        return embedding
    embeddings = image_to_encoding(image, FRmodel) 

When the camera of the computer is used to collect faces, the procedure is as shown below: <br>
    1. A *prompt* is displayed to ask users to input their name.
    ![prompt](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/f1.png?raw=true) <br>
    2. Then the camera is activated, and the face will be detected.<br>
    3. If user push the 'S' button, a screenshot will be saved and the faces detected will be transformed into vectors and saved into database. 'Q' button is hit to quit.
    ![saving face](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/f2.png?raw=true) <br>
    
    
## Face Recognition
When you want to recognize a face, just run the program and the camera is open again. Fot this time, your face will be detected and sent into the *faceRecoModel* with the 128-d vector as output. Then through this *cosine similarity* to find the most similar vector in the database and the *name* of that vector will be displayed.
    ![detection and recognition](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/f3.png?raw=true) <br>

## How does the FaceRecoModel look like? Why Transfer learning?
The model is known as [*faceNet*](https://arxiv.org/pdf/1503.03832.pdf), which is a deep CNN neural network featuring a *triplet loss function* that ensures the image is closer to all other images (positive) of the same person than it is to any image (negative) of any other person. The distance is Euclidean distance. The function is as follows:
 ![triplet loss](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/f4.png?raw=true) <br>
Since the model is so complex, and the time consumed to train the model would be days to months; Therefore I loaded the pre-trained weights and used the images I had to train a few more epochs until the model converged.

## Word-triggering
TBC


