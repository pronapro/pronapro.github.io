---
layout: post
title:  "
How To Make Word Cloud In Python

"
date:   2021-09-18 16:01:15 +0300

---
# Word cloud
Word cloud helps to know which words are common for example when analyzing what words are frequently used in a conversation or what words are used by a certain author. 
We use word cloud a lot in natural language processing, before we do word cloud it is important to remove stopwords which are common words like the, is, that, are, etc commonly used in English.
In this post, we shall be looking at how to do word clouds using python. A video explanation can be found [here](https://youtu.be/4j-axkt16_s)

## How it works 
In word clouds, the most frequent words take on the larger size. we can also use different colours to easily distinguish words.

## Ways to make word clouds 
we can:
Make word clouds of different shapes 
Make word cloud with different colours 
Make clouds with a limited number of words to avoid clutter


## Implementation

### Import Packages
These are the packages we shall need to make our word cloud. if you don't have them installed you should install them before proceeding. world cloud has the most common words used and they are the stopwords. we import them so we don’t have to manually remove them.


```python
import matplotlib.pyplot as plt 
from wordcloud import WordCloud,STOPWORDS 
import pandas as pd  

```

### Get data 
We use data in text format. since my data is in CSV I turned it into dataframe and I used contents on a dataframe and turn them into strings using the join function. I make the words to be in lowercase for consistency since one word can be written using different cases and python is case sensitive. you should also remove nulls at this step if you have them in your dataset.



```python
# reading the csv file as a DataFrame 
df = pd.read_csv("data.csv") 
# make a string
words=''.join(df.Content.astype(str)).lower() 
```

### Make word cloud 
To create a word cloud we use the WordCloud function which takes in a number of parameters but the ones we are using are:
* stopwords - contains the words we don't want to consider
* max_words - the maximum number of words you want to be in the word cloud 
* background_color - the colour of the word cloud background 
* width - the width of the word cloud 
* height - the height of the word cloud 
after passing in our parameters we then generate the word cloud using generate a function that takes in the text/words we are interested in.




```python
  
# defining the stop words 
stopwords = set(STOPWORDS)   
# making the word cloud 
wordcloud = WordCloud(stopwords = stopwords, 
                      max_words =20,
                      min_font_size = 10, 
                      background_color = 'white',  
                      width = 800, 
                      height = 800, 
                ).generate(words)
```

We use matplotlib's imshow to visualize the word cloud. we can and other functionalities like removing the axis, save the image, add title and so on.


```python
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud, interpolation = "bilinear") 
plt.axis("off") 
plt.tight_layout(pad = 0) 
#plt.savefig("wordcloud.png")
plt.show()
```


    
![png](/img/posts/wordcloud/output_9_0.png)
    


### Add words to leave out(Stopwords)
We can also update stopwords and remove the words we don't want to visualize. we use the update function and pass in a list of words we want to leave out. in the example below, I decided to leave out "quality", "pwd", "amp". 



```python
## list of stop words 
stopwords = set(STOPWORDS)
# Create stopword list:
stopwords.update(["quality", "pwd", "amp"])

# Generate a word cloud image
wordcloud = WordCloud(stopwords=stopwords,
                      max_words =20,
                      min_font_size = 10,  
                      width = 800, 
                      height = 800, 
                      background_color="white").generate(words)

# Display the generated image:
# the matplotlib way:
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")
plt.show()
```


    
![png](/img/posts/wordcloud/output_11_0.png)
    


### Add image mask
We can change the shape of the word cloud using images of different shapes. it is advised to use an image with white background to have the desired shape. here we are going to use two more libraries. pillow to read the image and NumPy to turn it into a NumPy array that can then be displayed/read by matplotlib.


```python
from PIL import Image
import numpy as np
from matplotlib.pyplot import imshow
```


```python
#display mask we are going to use 
im =Image.open('image.png')
imshow(np.asarray(im))
plt.axis("off")
```




    (-0.5, 1023.5, 767.5, -0.5)




    
![png](/img/posts/wordcloud/output_14_1.png)
    


create mask 

We create a mask from the image then mask into Wordcloud to make the word cloud have the shape of our image.


```python
mask = np.array(Image.open('image.png'))

# Generate a word cloud image
wordcloud = WordCloud(stopwords=stopwords,
                       mask=mask,
                      max_words =20,
                      min_font_size = 10,  
                      width = 800, 
                      height = 800, 
                      #width=mask.shape[1],
                      #height=mask.shape[0],
                      background_color="white").generate(words)

# Display the generated image:
# the matplotlib way:
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")
plt.show()
```


    
![png](/img/posts/wordcloud/output_16_0.png)
    


## Manipulate color

We can also manipulate the colour of the word cloud. In this section, we are looking at one way of doing it. we are going to make the word cloud take on the colour of our image. We do this using ImageColorGenerator and passing the generated color using color_func.


```python
im =Image.open('music.png')
imshow(np.asarray(im))
plt.axis("off")
```




    (-0.5, 1023.5, 767.5, -0.5)




    
![png](/img/posts/wordcloud/output_19_1.png)
    



```python
from wordcloud import ImageColorGenerator

mask = np.array(Image.open('music.png'))
mask_color = ImageColorGenerator(mask)
# Generate a word cloud image
wordcloud = WordCloud(stopwords=stopwords,
                       mask=mask,
                      max_words =20,
                      min_font_size = 10,  
                      width = 800, 
                      height = 800, 
                      color_func=mask_color,
                      background_color="white").generate(words)

# Display the generated image:
# the matplotlib way:
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")

plt.show()
```


    
![png](/img/posts/wordcloud/output_20_0.png)
    

