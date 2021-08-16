---
layout: post
title:  "
Introduction To Machine Learning

"
date:   2020-09-16 16:01:15 +0300

---
![Hero Image](/img/posts/ml/hero.png)

We hear about machine learning every day in the news, articles and on social media. I work as a data scientist at AirQo, a company that collects air quality data and uses machine learning to improve forecasting and accuracy of the data. I often get asked what machine learning is about so I decided to compile this summary of machine learning.

Machine learning is an application of Artificial Intelligence (AI) that gives systems the capability to automatically learn from data. The system is not explicitly programmed, but instead, it is exposed to data through training in order to learn patterns and generalize on new data. With the fourth industrial revolution, we see machine learning applications around us like self-driving cars, intelligent drones, recommendations on websites, image recognition, language translation, search engines healthcare solutions as well as everyday uses such as filling gaps in data or predicting customer buying behaviour. The increase in the applications of machine learning is due to the increasing availability of vast amounts of data and powerful computing tools. 

## Types Of Machine Learning
 
### Supervised Learning
This is the type of machine learning where the algorithm is given labelled data to learn from. During the training process, the algorithm tries to learn the relationship between features from the data and their corresponding labels so that when new information is introduced it is able to accurately perform predictions or classification. Two common methods for supervised learning are classification for categorical data e.g if the expected output is bottle or box, and regression for continuous numerical values e.g trying to predict prices of online courses according to ratings.

![Supervised Learning](/img/posts/ml/supervesed learning .png)

### Unsupervised Learning
Unsupervised learning uses unlabelled data, with the goal of finding the underlying structure of the data and assigning the data to the best groups (clusters) rather than predefined groups. It’s not ideal to use it on a single type of data. Unsupervised learning is mostly used when we want to find the distribution pattern in data, for example, most online companies use algorithms to group consumers into different classes using customer data, such as previous purchases, location, basic demographic data, etc.

![Supervised Learning](/img/posts/ml/unsupervised learning .png)

### Semi-Supervised Learning
This method takes on both unsupervised and supervised machine learning concepts. It is mostly used when we have less labelled data than unlabelled data. Consider the bottle/box example in the supervised learning section, if we had over 10,000 images it would be tedious for us to label all of them. With semi-supervised learning we label a portion of the images, train the model on the 2000 labelled images, use the trained model to predict pseudo labels of the remaining unlabelled data, then merge the labelled and pseudo labelled images into one dataset for model retraining.
 
### Reinforcement Learning
Reinforcement learning is inspired by animal behaviour in the sense that a reward helps the model to learn the best actions. e.g people tend to avoid things that lead to punishment and do things where they will be rewarded. The same concept is used in machine learning where the system has an agent that interacts with the environment through actions to earn rewards. It is mostly used in robotics, navigation (autonomous vehicles) and games (for example, Chess). The model developer sets incentives to guide the model to the outcome they want to achieve.
![Supervised Learning](/img/posts/ml/reinforcement learning .png)

## Issues With Machine Learning
Machine learning algorithms might be biased due to training with small datasets or a lack of diverse data. This can cause harm when the model is deployed in the real world, for instance, when Amazon’sAmazon’s hiring and recruitment algorithm discriminated against women for roles because the data used in training was primarily from male candidates.

Another machine learning issue is privacy. It’s not easy to anonymize data since even removed information can often be inferred. For example, gender or ethnicity may be removed but could be inferred by name or occupation. This is known as the inference control problem. Problems of privacy can lead to security issues, and certain groups of people can be discriminated against. For example, a business might market prices differently, with people assumed to be in the rich group being charged with high prices or low-income people not being shown certain products.

Computational intensity. Most algorithms require a lot of computation power since they use a lot of data during training. 

Thanks for reading, if you have any feedback or questions feel free to reach out also don’t forget to follow me for more posts. Here are amazing sites and courses you should check out if you are keen on starting your machine learning journey