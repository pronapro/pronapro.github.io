---
layout: post
title:  "
Add Picture Logo Or Branding To Your Matplotlib Plots In Python 

"
date:   2021-08-17 16:01:15 +0300

---
Data analysis or scientists deal with a lot of data and to make it understandable people often create a visualization that is shared. Sometimes you might want to add your brand feel for instance if you are sharing with external sources or social media and want to add ownership. in this post I will be sharing how to add your picture or brand logo to your plots, the different ways you can position and resize your logo.

**imports** 

we import images from matplotlib and this will help open and write our image.



```python
import matplotlib.image as image
import matplotlib.pyplot as plt
from matplotlib.offsetbox import OffsetImage, AnnotationBbox
import pandas as pd
```

## Input data

In this post, we are going to use line plots but the knowledge can be transferred to other kinds of plots. we shall be plotting two functions f(x+1) and f(x**2) for x from 1 to 9.



```python
#markers
x = range(10)
y = [X+3 for X in x]
y2 =[X**2 for X in x]
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')
plt.title("Functions of X")
plt.xlabel("x =1-9")
plt.ylabel("function of x(f(x^2),f(x+3))")
watermark(ax,0,0)
plt.show()
```

    transData(0,0) = [138.43636364  91.76727273]



    
![png](/img/posts/addlogo/output_5_1.png)
    


### Working with image
Let us read the data and display the image we shall be working with.
The image is converted to a NumPy array.
**read the image**


```python
## read the image 
logo = plt.imread('afro.png')
print(logo)
```

    [[[0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      ...
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]]
    
     [[0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      ...
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]]
    
     [[0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      ...
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]]
    
     ...
    
     [[0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      ...
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]]
    
     [[0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      ...
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]]
    
     [[0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      ...
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]
      [0.8980392 0.8980392 0.8980392 1.       ]]]


**show image**

The imshow function  displays the Image.


```python
plt.imshow(logo)
```
   
![png](/img/posts/addlogo/output_9_1.png)
    


## Add our image to the plot
We shall be exploring two ways of adding images, the first is using figimage function then we will also look at how to do it using the AnnotationBbox function.
### Some housekeeping rules when adding an image
* Try to make the image at a low opacity so that it doesn’t cover the other content on the plot
* Make the image small so that it is not the centre of attention
* Keep it at the position with no data preferably at corners.

### Add image using figimage
Syntax: matplotlib.pyplot.figimage(*args, **kwargs)

fig.figimage(logo, 30, 20,alpha=.5 ,zorder=3)]

figimage has a lot of parameters but we are interested in the following:
* x: The image data
* xo, yo: The x/y image offset in pixels.
* alpha: It is used to give the blending value for the image 
* zorder: To make the image overlay 
You can read about the rest 




```python
fig, ax = plt.subplots()
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')
ax.grid()
fig.figimage(logo, 0, 20,alpha=.5 ,zorder=3)

plt.show()
```


    
![png](/img/posts/addlogo/output_11_0.png)
    


### Add Image using  AnnotationBbox
We can also add an image to our plot using AnnotationBbox. this gives more control than using the axes method annotate.

**important parameters**
zoom  and x0,y0 tuple
We can also add an image to our plot using AnnotationBbox. This gives more control than using the axes method annotate.



```python
#plot data
fig, ax = plt.subplots()
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')
#add image
imagebox = OffsetImage(logo, zoom=1.)
ab = AnnotationBbox(imagebox, (6, 40))
ax.add_artist(ab)
plt.grid()
plt.draw()
plt.show()
```


    
![png](/img/posts/addlogo/output_13_0.png)
    


## Scaling and Positioning 

## figimage
we are going to create two functions for reusability. the first fuction will scale the image to desired length and width and the second function will be used to add the scaled image. 


```python
#function to scale the image to desires length and with
def scale(im, nR, nC):
    """
    parameters
    im :image
    nR:row size
    nC:column size 
    Return: scaled image 
    """
    number_rows = len(im)     # source number of rows 
    number_columns = len(im[0])  # source number of columns 
    return [[ im[int(number_rows * r / nR)][int(number_columns * c / nC)]  
                 for c in range(nC)] for r in range(nR)]
```


```python
def watermark(ax,x0,y0):
    """
    adds image logo and positions it on the plot
    ax: figure object 
    x0: adds x 
    y0: adds y 
    """
    logo = plt.imread('afro.png')
    #scale Image
    logo =scale(logo, 100, 100)

    
    print('transData(0,0) = {}'.format(ax.transData.transform((0,0))))
    ax.figure.figimage(logo, x0,y0, alpha=.5, zorder=1,origin="upper")

```


```python
fig, ax = plt.subplots()
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')
ax.grid()
watermark(ax,30,30)
plt.show()
```

    transData(0,0) = [108.  72.]



    
![png](/img/posts/addlogo/output_18_1.png)
    


### AnnotationBbox

Scaling is much easier with OffsetImage, AnnotationBbox. We use zoom in OffsetImage() to scale the image to fit a given size and a (xo, yo)tuple in AnnotationBbox to position the image at certain coordinates on the x and y-axis.
in the figure below our zoom is 0.2 and the x0 is 2 positioning the midpoint of the figure on x-axes at 2, our yo is 70. You can experiment with the values until you are after.



```python
fig, ax = plt.subplots()
plt.plot(x, y, marker ="*", ms =15)
plt.plot(x, y2, marker ="o",mec = 'r')


imagebox = OffsetImage(logo, zoom=.2)

ab = AnnotationBbox(imagebox, (2, 70))

ax.add_artist(ab)

plt.grid()

plt.draw()
plt.savefig('add_picture_matplotlib_figure.png',bbox_inches='tight')
plt.show()
```


    
![png](/img/posts/addlogo/output_21_0.png)
    




Thank you for reading if you enjoyed this post check out my [youtube channel](https://www.youtube.com/channel/UC1p_MdyNCb_fEXVZIJ5weFA) for more content. subscribe to be notified whenever I post something new.
