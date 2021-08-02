---
layout: post
title:  "
Whatsapp Chat Analysis And Exploration Using Python
"
date:   2021-02-23 16:01:15 +0300
categories: jekyll update
---
# Image 
Whatsapp is a widely used social media messaging application with over 2 billion users worldwide.Whatsapp users one can join groups or chat to a single person.Users can send text messages, video calls, send voice notes, share documents, contacts and other kinds of media. Whatsapp is a cross platform and does not have complicated features making it ideal for both Android users and iOS users who wish to communicate with people on different operating systems.
With whatsapp groups a lot of messages are shared by people hence hence the need for analysis. one might just be curious to do analysis on chats with someone.

In this post, I will be taking you through how to do analysis on WhatsApp data. I encourage you to follow along with WhatsApp chat data you are curious about. I will not be sharing the chat messages I am using in this post because the messages exchanged are personal data.

## Export Whatsapp Chats
WhatsApp chat messages are downloaded as a text file with a .txt extension. The steps for downloading might be different according to your operating system(os).Here is how you can download depending on your os.

### Android
To download chats from a group or individual chat follow the following steps

### Open the individual or group chat
Tap more options > More> Export chat.
There will be an option for you to export with media or without media. Choose without media
The chats will be sent to your email. Download the file to the project folder.
### IOS
Open the individual or group chat
Tap on the group profile/ group info> scroll down and tap Export chat
There will be an option for you to export with media or without media. Choose without media
Share to email. Download the file to the project folder.

## Reading WhatsApp Data And Creating A Dataframe.
We open and read the text file using builtin functions i.e open and read then turn the data into a pandas dataframe for easier manipulation.

``` python 
def read_file(file_path):
    '''
    Reads Whatsapp text file into a list of strings
    param:file path.
    Return: list of strings
    ''' 
    

    x = open(file,'r', encoding = 'utf-8')
    y = x.read() 
    content = y.splitlines() 
    return content
``` 
## Create A Pandas  Dataframe
Before we turn the data into a pandas dataframe let us look at the different formats of the lines of the chat depending on the operating system and time format on the device.

Iphone 24 hour format
[6/7/20, 12:37:37] Napro: Hi

Iphone am-pm format
[8/20/19, 1:33:05 PM] Napro: Hi

Android 24 hour format
20/08/2019, 17:59 – Napro: Hi

Android am-pm format

As you can see WhatsApp chat data have different formats so we shall be writing different functions for creating a dataframe. Our dataframe should have the date, time, sender and message columns to start with. To do this we shall use a regular expression. I know regular expressions are a nightmare for many and I am no exception so we shall be using the re package to match the patterns without overthinking and writing a lot of code.

In this post, the functions are for data in a 24-hour format for both android and ios. Be sure to use the function that suits your data format to avoid errors. I will add code for a 12-hour format but if you do it before me then feel free to share your code. if you have any suggestions/improvements open a pull request here and work it will be appreciated.

Android

data format

``` 
``` 
08/11/2019, 10:24 - Napro: Hi 
This function can also be used for data in the format 08/11/2019, 10:24 AM - Napro: Hi . if your os is not android or the data isnt in these formats then skip to try the next section.
```

```python 
def dataframe_android(data):
    #Remove empty lines
    clean_chat = [line for line in data if len(line) > 1]

    #Merge messages that belong together
    messages = [] # message array
    pos = 0 #counter for position of message in the array 

    for line in clean_chat:
        if re.findall("\A\d+[/]", line): # check if message starts wirh number then slash e.g 24/
            messages.append(line) # add to message array
            pos += 1
        else:
            con_message = messages[pos-1] + ". " + line # if it doesnt begin with date then its a continuation of previous message. add it to the string
            messages.append(con_message)
            messages.pop(pos-1) # remove non concaticated message
    #get time        
    time = [messages[i].split(',')[1].split('-')[0] for i in range(len(messages))]
    time = [s.strip(' ') for s in time] 
    #get date
    date = [messages[i].split(',')[0] for i in range(len(messages))]
    #get senders
    name = [messages[i].split('-')[1].split(':')[0] for i in range(len(messages))]
    #get messages
    content = []
    for i in range(len(messages)):
      try:
        content.append(messages[i].split(':')[2])
      except IndexError:
        content.append('Missing Text')
    len(content)
    df = pd.DataFrame(list(zip(date, time, name, content)), columns = ['Date', 'Time', 'Author', 'Message'])
    return df 
```
iOS

Data format

if you are using android skip this step as the function is a modification of the above function and go to the next section. first, let us read a helper function to help us get the data and time

```python 
#get time and date for iOS
def date_time(a_string):
    result = re.findall("\[(.*?)\]", a_string)
    x = result[0].split(", ")
    (date, time) =x[0],x[1]
    return (date, time)
    ```
It is a good practice to use helper functions if the code is long to try and make it readable and easy to debug.

```python 
def dataframe_ios(data):
    #Remove empty lines
    clean_data = [line for line in data if len(line) > 1]

    #combine messages that are continuation
    messages = [] # message array
    pos = 0 #counter for position of message in the array 

    for line in clean_data:
        if re.findall("\[(.*?)\]", line): # check if message starts with a list e.g [10]
            messages.append(line) # add to message array
            pos += 1
        else:
            print(pos)
            print(messages)
            con_message = messages[pos-1]+ ". " + line # if it doesnt begin with date then its a continuation of previous message. add it to the string
            messages.append(con_message)
            messages.pop(pos-1) # remove non concaticated message
    

    #getting date and time
    dates =[]
    times =[]
    for i in range(len(messages)):
        date, time = date_time(messages[i]) # call date_time helper function
        dates.append(date)
        times.append(time)

    #get author
    names = []
    for i in range(len(messages)):
      try:
        names.append(messages[i].split(' ')[2])
      except IndexError:
        names.append('Missing Name')
    names
    
    #split by third column
    #get message
    content = []
    for i in range(len(messages)):
      try:
        content.append(messages[i].split(':')[3])
      except IndexError:
        content.append('Missing Text')
    content

    df = pd.DataFrame(list(zip(dates, times, names, content)), columns = ['Date', 'Time', 'Author', 'Message'])
    return df 
    ```
Let us take a peek at one of our data. To keep the parties involved private I will be renaming the authors. You don’t have to do the renaming of authors unless if you are sharing with others or if someone decides they want to be anonymous.

renaming
```python 
#get dataframe
file ='data/chat.txt'
ios_data = read_file(file)
ind_df = dataframe_ios(ios_data)
#remove notifications for true authors
ind_df = ind_df[grp_df["Message"]!='Missing Text']
#rename authors
ind_df.Author.unique()
authors = ind_df.Author.unique()
ind_df.Author = ind_df.Author.apply(lambda author: 'Author ' + str(np.where(authors == author)[0][0] + 1))
#check dataframe
ind_df.head()
``` 
# Image 

## Feature Engineering
This step is called feature engineering in data analysis and machine learning which is just a fancy word for creating more columns/features. The columns we are going to create are important in our analysis. The truth is working with just the first 4 features is not that interesting and we can’t get a lot of insights from them.The features we are going to create are word count, day, month, year, letter count, emoji, url/website count etc.

### Datetime
The date time format is an easy way to get date and time values for example the day, year, month, minutes etc. Date time features will help us get/map events, discover seasonal trends, know the peak hours etc.After creating DateTime we extract the date ,hour,day, month and year.

```python 
ind_df['DateTime'] = pd.to_datetime(ind_df['Date'] + ' ' + ind_df['Time'])
#hour message was sent
ind_df['Hour'] = ind_df['Time'].apply(lambda x : x.split(':')[0]) 
ind_df['weekday'] = ind_df['DateTime'].apply(lambda x: x.day_name()) 
ind_df['year'] = ind_df['DateTime'].apply(lambda x: x.year) 
ind_df['month'] = ind_df['DateTime'].apply(lambda x: x.month) 
``` 
### Get Message Length
We are going to evaluate the message length using two metrics, the message word count and message character/letter count.

``` python 
#getting message length
ind_df['Letter_Count'] =ind_df['Message'].apply(lambda s : len(s))
ind_df['Word_Count'] = ind_df['Message'].apply(lambda s : len(s.split(' ')))
``` 
## Url Count
Oftentimes people share useful links in whatsApp groups especially if it is a business group or class group . We shall mark the links in messages and assign a number to messages with links . This task requires us to use regular expressions. This link code is for simple https url but if you have other kinds of url like localhost then this Link should be useful.
```python 
URLPATTERN = r'(https?://\S+)'
ind_df['urlcount'] = ind_df.Message.apply(lambda x: re.findall(URLPATTERN, x)).str.len()
```
Emoji

Emojis are part of our communication and help us communicate our feelings well and sometimes save us from writing longer text. Let us create a column for them.
``` python 
def message_emoji_list(text):

    emoji_list = []
    data = re.findall(r'[^\w\s,]', text)
    for word in data:
        if any(char in emoji.UNICODE_EMOJI for char in word):
            emoji_list.append(word)

    return emoji_list
#create emoji column
ind_df["emoji"] = ind_df["Message"].apply(message_emoji_list)
``` 
Data Analysis And Visualization
The packages I am using in this section are emoji, matplotlib, pandas , numpy, wordcloud. Matplotlib, pandas , numpy are my go to packages and I suggest you learn them if you want to do more analysis and data exploration in future.Link to the post
This section is the main and fun step we have been preparing for. The moment is now and let us find out the unknown.

Media Sent, Deleted Media And Links
Check for number of links shared, messages deleted, media shared using sentences that replaced them.
``` python
links =ind_df[ind_df["urlcount"]>0]
print(len(links))
deleted_message =ind_df[(ind_df['Message'] == "you deleted this message")| (ind_df['Message']=="this message was deleted.")]
print(len(deleted_message))
media_message =ind_df[(ind_df["Message"] == "<media omitted>")| (ind_df["Message"]=="image ommitted")| (ind_df["Message"] =="video ommitted")]
print(len(media_message))
```
## Rank User By Number Of Messages Sent
Most active people send more messages. I did it with media files deleted but you can do it without that for more accuracy since some people chat more using memes.
You can also group by who sends most messages by letter or word count. I have used data from group chat here since for individual chats its only two people and not so much variations

grouping
```python 
grp_df.groupby('Author')['Message'].count().sort_values(ascending=False)
```
# Image 

Let us visualize the pattern of message per author
```python 
df1 =grp_df
df1['DAY_OF_WEEK'] = pd.Categorical(df1['weekday'], categories=
    ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday', 'Sunday'],
    ordered=True)
pd.crosstab(df1.Author,df1.DAY_OF_WEEK).plot(kind='bar')

plt.xlabel('Names')
plt.ylabel('Chart')
``` 
# Image 
## Most Frequent Emojis In The Chat
Find out the most frequently used emojis, this helps us discover the mood of the individual or group chats.
```python 
# Count all the emojis in the chat.
emoji_counter = Counter()
emojis_list = map(lambda x: ''.join(x.split()), emoji.UNICODE_EMOJI.keys())
r = re.compile('|'.join(re.escape(p) for p in emojis_list))
for index, row in ind_df.iterrows():
  emojis_found = r.findall(row['Message'])
  for emoji_f in emojis_found:
    emoji_counter[emoji_f] +=1

for item in emoji_counter.most_common(6):
  print(f'{item[0]} - {item[1]}')
  ``` 

## Peak Hours And Days
When is the chat most active.This helps determine what is the right time to send a chat because there is a high probability of your chat being seen and engaged.Plot by messages each day of the week, what is the best day to send a message.

```python 
#mesage per hour
grp_df.groupby(['Hour']).size().sort_index().plot(x="Hour", kind='bar')
#messages shared in group by  week day 
df1.groupby(['DAY_OF_WEEK'], sort=True)['Author'].count().plot(kind='bar')
``` 
Hour messages

# Image 

day of the week

# Image 

## Wordcloud
Let us create a word cloud of most commonly used words by members. To prevent common words from dominating the charts we consider then stop words for them to be skipped. There is no need to add common English words like the, and because they are already considered. If you are multilingual and chat in a local language or use local language connecting words then you can add them to stop words. you can also add just any words that you feel should be skipped.

```python 
stop_words = ["chat","blabla","eeh","haha"] + list(STOPWORDS)
words=''.join(ind_df.Message.astype(str)).lower() 
  
# making the word cloud 
wordcloud = WordCloud(stopwords = stop_words, 
                      max_words =50,
                      min_font_size = 10, 
                      background_color = 'white',  
                      width = 800, 
                      height = 800, 
                ).generate(words)
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud, interpolation = "bilinear") 
plt.axis("off") 
plt.tight_layout(pad = 0) 
plt.savefig("chatcloud.png")
plt.show()
```
# image 

We can see some of the top 50 used words. I mage or media omitted show that some files were not downloaded. by the side of Image omitted we can say a lot of images(Memes) were shared in this chat.

You can also do a word cloud for each author in a chat.
```python 
# word cloud per member
authors = ind_df.Author.unique()
for author in range(len(authors)):
  temp_df = ind_df[ind_df['Author'] == l[i]]
  text = " ".join(chat for chat in temp_df.Message)
  stopwords = ["thing","ooh","s"] + list(STOPWORDS)
  #Generate a word cloud image
  print('Author name',authors[i])
  wordcloud = WordCloud(stopwords=stopwords, background_color="white").generate(text)
   
  plt.figure( figsize=(10,5))
  plt.imshow(wordcloud, interpolation='bilinear')
  plt.axis("off")
  #save for each author
  name = "{}cloud.png".format(author)
  plt.savefig(name)
  plt.show()
  ```

## Conclusion
I was fascinated by the way my analysis turned out and I hope it goes well for you too.You can scale this to other groups and individual messages, add more analysis that isn’t covered in this post. I think for some groups you will have to get permission from the administrators if you are not one. Analysis is good but due to ethical reasons people need to consent and know their data is being is good intentions

I hope you enjoyed the blog. Follow me on Instagram or Twitter to be updated whenever a new post is uploaded.






