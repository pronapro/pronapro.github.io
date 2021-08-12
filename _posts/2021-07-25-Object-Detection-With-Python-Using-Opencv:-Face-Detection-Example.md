---
layout: post
title:  "Object Detection With Python Using OpenCV:-Face Detection Example"
date:   2021-07-25 16:01:15 +0300
categories: jekyll update
---
![face detected](/img/posts/face detection/hero.png)

I was watching the person of interest, it’s a fiction crime series where an ex-CIA agent and a billionaire software genius try to stop crimes before they happen. they have a program called The Machine which identifies perpetrators and victims of deadly crimes. It is some kind of surveillance system that has cameras all over new york city and this is where computer vision comes in to detect objects and faces.

I got an idea to make such a functionality(I won’t be spying on anyone) so that  I can later add to my other programmes like games plus it is fun.

Domain 

This project falls under computer vision which is the AI that deals with image recognition. The most common applications of computer vision are medical image analysis, autonomous vehicles, identification of handwritten digits etc.

In this post, we will focus on object detection using an image. we will use the OpenCV library and Haar Cascade classifiers to detect a face in an image. 
## Basics 
Before, we dive into object detection let us look at the basic operations we can perform using OpenCV.

Install OpenCV before using it.
pip install opencv-python

### Read An Image 
Opencv  converts the image into a NumPy array
To read an image we use imread function which takes in two parameters the image path and the image format that is to say coloured or grayscale. We use 0 for gray and 1 for RGB

```Python
import cv2
#read image 
img = cv2.imread('afro.png',1)
print(img)
img2 = cv2.imread('afro.png',0)
print(img2)

```
### Get image shape 
```python
print(img2.shape)
print(img.shape)
```
(292, 461)

(292, 461, 3)

For coloured images, there are three channels. Each representing the intensity of the colour pixels 

### Displaying Image
To display an image we use imshow() function which takes in the window name and image array as parameters. We use waitKey to indicate how long the window should stay open. 

If wait key is zero then the window will close when any key is pressed.

```python
cv2.imshow('afro',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
The waitkey also takes in the number of milliseconds we want to wait until the window closes. This waits 5000 milliseconds before closing. 
```python
cv2.imshow('afro',img)
cv2.waitKey(5000)
cv2.destroyAllWindows()
```
### Resize An Image 
You can resize it to any shape you want. This comes in handy when you have many images and you want them to have the same scale 

Resize takes in the image and tuple of the shape .here we are resizing it into half of each dimension.
```python
Python
resized =cv2.resize(img,(int(img.shape[1]/2),int(img.shape[0]/2)))
cv2.imshow('afro',resized)
cv2.waitKey(5000)
cv2.destroyAllWindows()
```
## Face Detection
Before we implement the face detector let us add the images and XML file we are going to use in the same folder as our script.

We will be using haarcascade_frontalface_default.xml which can be found here.

### Implementation
We use CascadeClassifier()function to create cascade object, use the detectMultiScale() function  to recognize the face.after face detection we can check for numbers of faces detected. 
found = len(faces)
```python
import cv2
#classifier 
face_cascade =cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
#read image
img = cv2.imread('download.jpeg')
 
#make it gray 
gray_img = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
 
faces =face_cascade.detectMultiScale(gray_img,scaleFactor =1.05, minNeighbors =5)
print(type(faces))
print(faces)
found = len(faces)
print(found)
```
This prints the x,y,w,h coordinates of the faces and the number of faces using len function since it is an array of arrays.

[[176 59 31 31]

[ 79 16 46 46]]

2

### Add Rectangular Box
If we want to display or check which object(in our case face ) was detected then we can draw a rectangle around it.
```python
for (x,y,w,h) in faces:
    img = cv2.rectangle(img,(x,y),(x+w,y+h),(255,0,0),thickness=3)
```
### Save And Display Image  
This is the last step where we carry out operations like displaying, resizing and saving the image. 
```python
#resized_img=cv2.resize(test_img,(500,500))
cv2.imwrite('twosavedImage.jpg', img)
cv2.imshow("face",img)
cv2.waitKey(0)
cv2.destroyAllWindow
```
## Use cases 

You can use this in your application where you want people to use images to signup/register. if no face is detected then info person to use an image with a face.  

Control access to certain files

Track attendance/access to files 

## Conclusion 
You can easily read an image detection without going through the hustle of training a machine learning model using OpenCV. Here we used face detection haar cascade but you can use any haar cascade according to your object of interest. This post looked at object detection using an image. In later posts, we will look at object detection in videos and real-time object detection from the camera.