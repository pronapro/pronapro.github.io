---
layout: post
title:  "
Create Quiz Application in python
"
date:   2022-07-28 14:01:15 +0200

---

Create Quiz Application in python
===========================================================
<div style="text-align: justify;">

This post features supplementary code associated with a tutorial on my <a href="https://www.youtube.com/watch?v=dmEjKdT4YjI" target="_blank">YouTube</a> channel, demonstrating the creation of a quiz application in Python. The program engages users by posing questions and prompting them to select an option. In building the quiz application, we leverage Python data structures like lists and dictionaries to manage variables, employ logical operators, and incorporate conditional statements such as 'if' statements. Additionally, we utilize loops, including 'for' and 'while' loops, for handling choices. If you are new to Python, you can explore the basics through this <a href="http://pronapro.com/2020/12/12/Beginner-s-Guide-To-Python-Programming.html" target="_blank">blog</a> where I cover fundamental concepts of Python programming.
</div>


```python

def quiz():
    """
    Conducts a quiz with multiple-choice questions and evaluates the user's answers.

    Returns:
    int: The number of correct answers.
    """
    correct_answers = 0
    play_again = True
    round_number = 1
    answer_list = []
    while play_again:
        print("********************************")
        print("THIS IS THE {} ROUND".format(round_number))
        print("You have to get 2 or more questions right")

        questions  = ["What are we doing today?", "What programming languange will we be using?", "Is python interesting?"]
        options = {1:["A: Quiz","B: Mathematics exams ","C:I don't know"],
                    2:["A:Rust","B: Javascript","C: Python"],
                    3:["A:Yes","B:Maybe","C: No"]}
        correct_answers_list = ["A","C","A"]

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

        round_number +=1
        print("You got {} questions right".format(correct_answers))
        print("Your answers: {}".format(answer_list))
        print("Correct answers: {}".format(correct_answers_list))
        print("")

    return correct_answers
                

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
You got 1 of questions right
Here are your answers['a', 'a', 'c']
The correct answers are ['A', 'C', 'A']
```
