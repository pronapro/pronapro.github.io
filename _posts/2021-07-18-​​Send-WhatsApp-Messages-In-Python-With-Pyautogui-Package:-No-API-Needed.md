---
layout: post
title:  "Send WhatsApp Messages In Python With Pyautogui Package: No API Needed"
date:   2021-07-18 16:01:15 +0300
categories: jekyll update
---
## Introduction 
In this post, we will be looking at how to send messages using python. I have used this technique to send over 100 messages to someone at once. All you need is WhatsApp open in your browser and the necessary packages. This blog is a supplement to my youtube video that you can find here.

Libraries 
Pyautogui- helps control mouse and keyboard actions  

Webbrowser – open WhatsApp web in the browser

Time – to give time allowance between activities, for example, add sleep time to allow loading of web browser before the message is sent.

You can also use a scheduler if you want to send messages after a certain time interval

Scheduler – to schedule when messages should be sent 

## Implementation 
We will be creating a WhatsApp spam bot that sends messages to the contact selected. 

### Import libraries

First, we import the libraries we will be using
```python
import pyautogui 
import time
import webbrowser as wb
```
After , we use web browser to open WhatsApp in the browser 
```python
wb.open("https://web.whatsapp.com/")
time.sleep(30)
```
We give it 30 seconds to load before sending the message. This is an important step to avoid messages being sent before the browser opens. The wait time can vary according to your internet connection. If your internet is fast, you can use less than 30 seconds and if it is slow, then one minute or so can be used.

The next step is to send the message as a character or words. 

### Send character

You can send messages using one character at a time to do that you use the press function, this types the character in the message text box.
```python
pyautogui.press(i)
pyautogui.press("enter")
```
After the message typing function, we pass in “enter” to the press function. This will send the message

You can modify this using loops to send many characters from a word.
```python 
import pyautogui 
import time
import webbrowser as wb
 
wb.open("https://web.whatsapp.com/")
time.sleep(30)
for i in range(20):
    for i in "Great !!!":
 
        pyautogui.press(i)
    pyautogui.press("enter")
```
Send word 

Sending one character at a time is okay when you have just one word,  if you want to send a sentence then more efficient methods are needed. we use typewrite method to send words and sentences.

import pyautogui 
import time
import webbrowser as wb

wb.open("https://web.whatsapp.com/")
time.sleep(30)
for i in range(20):
    pyautogui.typewrite('I am serious!')
    pyautogui.press("enter")
```python 
import pyautogui 
import time
import webbrowser as wb
 
wb.open("https://web.whatsapp.com/")
time.sleep(30)
for i in range(20):
    pyautogui.typewrite('I am serious!')
    pyautogui.press("enter")
```
When you run the program the WhatsApp will open on the web, look for the contact you want to send the message and click on it. The message will be typed and send the number of times you specified.


## Modifications 
We can do more modifications to this program for example getting the message and numbers to send it from user input. You can also schedule the time you want the message to be sent.

```python
def send_message():
 
    msg = input("Enter message to send: ")
    count = int(input("Enter number of times message is to be sent: "))
    wb.open("https://web.whatsapp.com/")
    time.sleep(30)
    for i in range(count):
        pyautogui.typewrite(msg)
        pyautogui.press("enter")
        #time.sleep(5)
 
send_message()
```
## Conclusion 
With just a few lines of code, you can send your friends WhatsApp messages using python. Make sure you don’t send people you don’t know because your number might be reported and blocked. Thanks for reading. You can also check out my youtube related video on this.