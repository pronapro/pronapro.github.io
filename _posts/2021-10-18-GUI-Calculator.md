---
layout: post
title:  "
GUI Calculator App In Python Using tkinter
"
date:   2021-10-18 16:01:15 +0300

---

    
![png](/img/posts/GUI calculator/output_1_1.png)
    
The code below creates a calculator in python using tkinter. you can modify it to your preference. The main functionalities are button press, button clear and equals. These were put in the different functions for usability. 


```python
from tkinter import *

window = Tk() 
window.geometry("400x325")  
window.resizable(0, 0)  
window.title("GUI Calculator")
expression =""
input_text = StringVar()

```

The functions that carry out the basic calculator functionalities. to do the different arithmetic operations we use eval() function.we also use the global expression in the functions thats why we use the word global to prevent functions to create there own expressions or giving undefined error.


```python
## function when a button is clicked
def click_button(operation):
    global expression
    expression = expression+str(operation)
    input_text.set(expression)

#clear text field
def clear_button():
    global expression
    expression =""
    input_text.set("")

## getting answer
def equal_button():
    global expression
    answer = str(eval(expression))
    input_text.set(answer)
    expression = ""

```

We organize the different widgets in frames for easy grouping.
Text/expression field


```python
### field for the answer 
input_frame = Frame(window, width = 400, height = 50, bd = 0,bg = "#f7e2d7", highlightbackground = "black", highlightcolor = "black", highlightthickness = 1)
input_frame.pack(side = TOP)

input_field = Entry(input_frame, font = ('arial', 18, 'bold'), textvariable = input_text, width = 50, bg = "#fdcdcd", bd = 0, justify = RIGHT)
input_field.grid(row = 0, column = 0)
input_field.pack(ipady = 10)
```

We organze the buttons in a button frame and arrange them in a table like structure using grid. with grid we can give the button positons in terms of rows and colunms.



```python
### button frame 
button_frame = Frame(window, width = 400, height = 272.5, bg = "#f7e2d7")
button_frame.pack()

# first row

clear = Button(button_frame, text = "C", fg = "blue" , font = ( 'bold'),width = 10, height = 3, bd = 0,highlightbackground='orange', bg = "#fadede", cursor = "hand2", command = lambda: clear_button()).grid(row = 0, column = 0, padx = 1, pady = 1)
divide = Button(button_frame, text = "/", fg = "blue", width = 10, height = 3, bd = 0, highlightbackground='orange',bg = "blue", cursor = "hand2", command = lambda: click_button("/")).grid(row = 0, column = 3, padx = 1, pady = 1)
open_bracet = Button(button_frame, text = "(", fg = "blue", width = 10, height = 3, bd = 0, highlightbackground='orange',bg = "#fff", cursor = "hand2", command = lambda: click_button("(")).grid(row = 0, column = 1, padx = 1, pady = 1)
close_bracket = Button(button_frame, text = ")", fg = "blue", width = 10, height = 3, bd = 0,highlightbackground='orange', bg = "#eee", cursor = "hand2", command = lambda: click_button(")")).grid(row = 0, column = 2, padx = 1, pady = 1)
## second row
seven = Button(button_frame, text = "7", fg = "black", width = 10, height = 3, bd = 0, highlightbackground='#946b4d',bg = "#203c3b", cursor = "hand2", command = lambda: click_button(7)).grid(row = 1, column = 0, padx = 1, pady = 1)
eight = Button(button_frame, text = "8", fg = "black", width = 10, height = 3, bd = 0, highlightbackground='#946b4d',bg = "#fff", cursor = "hand2", command = lambda: click_button(8)).grid(row = 1, column = 1, padx = 1, pady = 1)
nine = Button(button_frame, text = "9", fg = "black", width = 10, height = 3, bd = 0, highlightbackground='#946b4d',bg = "#fff", cursor = "hand2", command = lambda: click_button(9)).grid(row = 1, column = 2, padx = 1, pady = 1)
multiply = Button(button_frame, text = "*", fg = "blue", width = 10, height = 3, bd = 0,highlightbackground='orange', bg = "#eee", cursor = "hand2", command = lambda: click_button("*")).grid(row = 1, column = 3, padx = 1, pady = 1)

## third row
four = Button(button_frame, text = "4", fg = "black", width = 10, height = 3, bd = 0,highlightbackground='#946b4d', bg = "#fff", cursor = "hand2", command = lambda: click_button(4)).grid(row = 2, column = 0, padx = 1, pady = 1)
five = Button(button_frame, text = "5", fg = "black", width = 10, height = 3, bd = 0, highlightbackground='#946b4d',bg = "#fff", cursor = "hand2", command = lambda: click_button(5)).grid(row = 2, column = 1, padx = 1, pady = 1)
six = Button(button_frame, text = "6", fg = "black", width = 10, height = 3, bd = 0, highlightbackground='#946b4d',bg = "#fff", cursor = "hand2", command = lambda: click_button(6)).grid(row = 2, column = 2, padx = 1, pady = 1)
minus = Button(button_frame, text = "-", fg = "blue", width = 10, height = 3, bd = 0, highlightbackground='orange',bg = "#eee", cursor = "hand2", command = lambda: click_button("-")).grid(row = 2, column = 3, padx = 1, pady = 1)

# fourth row 
one = Button(button_frame, text = "1", fg = "black", width = 10, height = 3, bd = 0,highlightbackground='#946b4d', bg = "#fff", cursor = "hand2", command = lambda: click_button(1)).grid(row = 3, column = 0, padx = 1, pady = 1)
two = Button(button_frame, text = "2", fg = "black", width = 10, height = 3, bd = 0,highlightbackground='#946b4d', bg = "#fff", cursor = "hand2", command = lambda: click_button(2)).grid(row = 3, column = 1, padx = 1, pady = 1)
three = Button(button_frame, text = "3", fg = "black", width = 10, height = 3,highlightbackground='#946b4d', bd = 0, bg = "#fff", cursor = "hand2", command = lambda: click_button(3)).grid(row = 3, column = 2, padx = 1, pady = 1)
plus = Button(button_frame, text = "+", fg = "blue", width = 10, height = 3, bd = 0, highlightbackground='orange',bg = "yellow", cursor = "hand2", command = lambda: click_button("+")).grid(row = 3, column = 3, padx = 1, pady = 1)

## fifth row
one_zero = Button(button_frame, text = "0", fg = "black", width = 10, height = 3, bd = 0,highlightbackground='#946b4d', bg = "#fff", cursor = "hand2", command = lambda: click_button(0)).grid(row = 4, column = 0, padx = 1, pady = 1)
two_zeros = Button(button_frame, text = "00", fg = "black", width = 10, height = 3, highlightbackground='#946b4d',bd = 0, bg = "#fff", cursor = "hand2", command = lambda: click_button("00")).grid(row = 4, column = 1, padx = 1, pady = 1)
point = Button(button_frame, text = ".", fg = "black", width = 10, height = 3, highlightbackground='#946b4d',bd = 0, bg = "#eee", cursor = "hand2", command = lambda: click_button(".")).grid(row = 4, column = 2, padx = 1, pady = 1)
equals = Button(button_frame, text = "=", fg = "blue", width = 10, height = 3, bd = 0,highlightbackground='orange', bg = "#00ffff", cursor = "hand2", command = lambda: equal_button()).grid(row = 4, column = 3, padx = 1, pady = 1)

```

main loop to run the app 


```python
window.mainloop()
```

