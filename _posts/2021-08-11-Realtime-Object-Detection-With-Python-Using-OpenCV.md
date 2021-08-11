---
layout: post
title:  "
Realtime Object Detection With Python Using OpenCV

"
date:   2021-08-11 16:01:15 +0300
categories: jekyll update
---
In this post, I will be looking at object detection using OpenCV and haar cascades. This post is mainly focused on object detection of objects from video and image capture. This is a continuation of the previous post where I covered the basics like how to read and write images using opencv.  We shall be using the face detection haar cascade but you can go ahead and use what you like or use many in combination. 
First we install open cv 
```python
pip install opencv-python
```

Download haar cascade and save it/them to our working directory 
[Haarcascade_frontalface_default.xml ](https://github.com/opencv/opencv/blob/master/data/haarcascades/haarcascade_frontalface_default.xml)

The cascades are trained on a large amount of negative and postive labelled images giving it the ability to do object detection. 

## Read camera object 

First we import opencv library
We initialize the webcam object that helps us capture the video.

We then create the cascade object that will help us do the object detection. 

We create an infinite loop that helps us loop through each frame in the video from camera.

We get the frame using the read method, this returns two parameters,flag if the frame was read and frame. We are only interested in the frame/image.

After capturing the image we convert it to the appropriate colour scale. Then do the face detections. After detecting the face we draw a rectangle around it.

The image is then displayed back to the camera using the write method.

```python 
import cv2

# Load the cascade
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')

# To capture video from webcam. 
cam = cv2.VideoCapture(0)


while True:
    # Read the frame
    _, img = cam.read()
    # Convert frame to grayscale
    gray_img= cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    #object dtection
    faces = face_cascade.detectMultiScale(gray_img,scaleFactor =1.05, minNeighbors =5)
    # Draw the rectangle around each face
    for (x, y, w, h) in faces:
        cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)
    # Display
    cv2.imshow('face detection', img)

    # Stop if space key is pressed
    
    key = cv2.waitKey(1)
    if key%256 == 32:
        break
# Release the VideoCapture object
cam.release()
cv2.destroyAllWindows()
```
## Detect objects from video 
The steps are similar to when doing object detection from webcame. The difference is we add the video file path in the videoCapture method. Here we read the video footage with the object we want to recognize. We then read the frames which are basically images one by one.  After we convert the colour then detect the object in the video and draw a rectangle around it.
```python 
import cv2

# Load the cascade
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
#file path
file_path = 'me.mp4'
# capture video 
vid_file= cv2.VideoCapture(file_path)


while True:
    # Read the frame
    _, img = vid_file.read()
    # Convert frame to grayscale
    gray_img= cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    #object dtection
    faces = face_cascade.detectMultiScale(gray_img,scaleFactor =1.05, minNeighbors =5)
    # Draw the rectangle around each face
    for (x, y, w, h) in faces:
        cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)
        #label detected face
        cv2.putText(img, 'face', (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0, 0, 255), 2)
    # Display
    cv2.imshow('face detection', img)

    # Stop if space key is pressed
    
    key = cv2.waitKey(1)
    if key%256 == 32:
        break
# Release the VideoCapture object
vid_file.release()
cv2.destroyAllWindows()
``` 
The steps followed are capture video frame, convert frame to grayscale, detecting object and drawing rectangle around the detected object.

Thanks for reading.


