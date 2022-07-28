---
layout: post
title:  "
Create Quiz Application in python
"
date:   2022-07-28 14:01:15 +0200

---

Create Quiz Application in python
===========================================================
This post contains a follow-up code from the video on youtube, in the video, we look at home to create a quiz application in python. The program asks questions and prompts the user to pick an option. We are utilising python data structures like lists, dictionaries, operators less than, equal and greater than. We will also utilise if statements and loops(for loop and while loop). If you are not familiar with python check out the where beginner blogs [here](http://pronapro.com/2020/12/12/Beginner-s-Guide-To-Python-Programming.html).

```python
#list , dictionary
#if statements 
#for loop and while 
#operators
#input 
def quiz():
    correct = 0
    play_again = True
    round = 1
    answer_list =[]
    while play_again:
        print("********************************")
        print("THIS IS THE {} ROUND".format(round))
        print("You have to get 2 or more questions right")

        questions  = ["What are we doing today?", "What programming languange will we be using?", "Is python interesting?"]
        options = {1:["A: Quiz","B: Mathematics exams ","C:I don't know"],
                    2:["A:Rust","B: Javascript","C: Python"],
                    3:["A:Yes","B:Maybe","C: No"]}
        answers = ["A","C","A"]

        for i, key in enumerate(options):
            print(questions[i])
            for value in options[key]:
                print(value)
            user_answer = input("Input your answer: ")
            if user_answer.upper() == answers[i]:
                correct +=1
            answer_list.append(user_answer)
        if correct >=2:
            play_again = False
        round +=1
        print("you got {} of questions right".format(correct))
        print("Here are your answers{}".format(answer_list))
        print("The correct answers are {}".format(answers))
        print("")
    return correct
                

quiz()
```

Sample output 
```
********************************
THIS IS THE 1 ROUND
You have to get 2 or more questions
What are we doing today?
A: Quiz
B: Mathematics exams 
C:I don't know
Input your answer: a
What programming languange will we be using?
A:Rust
B: Javascript
C: Python
Input your answer: a
Is python interesting?
A:Yes
B:Maybe
C: No
Input your answer: c
you got 1 of questions right
Here are your answers['a', 'a', 'c']
The correct answers are ['A', 'C', 'A']
```
