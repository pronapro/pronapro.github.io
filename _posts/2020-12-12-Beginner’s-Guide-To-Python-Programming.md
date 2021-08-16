---
layout: post
title:  "
Beginner’s Guide To Python Programming

"
date:   2020-12-12 16:01:15 +0300

---
![Hero](/img/posts/python beginner/hero.png)
# Introduction
I assume you are here because you want to learn Python. Maybe you were told it is the easiest programming language, or you are diving into data science or you have an issue you want to solve. Whatever your reason is for checking out my blog, I will try my best to make this post provide an overview of the basics of Python programming and address any questions you may have.

## What Is Python And Why Do We Use It? 
Python is a popular programming language with many use cases and is one of the easiest programming languages to learn. It was created by Guido van Rossum and released in 1991.

Before we dive into the technical details, these are the reasons why I am using Python and why you might need to use it too.

Python can be used in several tasks, including desktop applications, gaming, mobile applications, database applications, network programming, data science and machine learning.
Python uses a language-like structure making it easier to read and learn code, and requiring fewer lines of code.
There are many libraries that can be used with Python. A library is simply a collection of resources and pre-written code that we can use when we write our programs.
Python is cross-platform: code written for one platform can be used on another platform.
 

I have sectioned the code into levels. I suggest you follow the structure I used on the blog, but if you are familiar with the concepts then feel free to jump to the section that you need.

### Prerequisites
You should have Python installed. This post will be referencing Python 3. Most computers come with Python already installed, but if you don’t have it installed you can take a look at this post.

 

## Basics
Python Syntax
Python syntax defines a set of rules to follow when writing Python programs.

Python uses a new line to complete a command.

Python uses indentation to define the scope. We shall see this later for functions and conditional statements.

Comments help to tell us what the code does, and are ignored by the interpreter.

Identifiers are names that identify variables, functions, modules, and classes
User Input
Input is a built-in function we use to get user input. User input can be something like a name, age, or numbers that we want to add or multiply. Input can be from a keyboard, mouse click or any other input device. The input function tells the program to stop and wait for the user data and resumes after the user presses the enter key, returning user data as a string data type.

input([prompt])

The prompt is optional. You can just use input() or add a prompt that is a string to guide the user on what to enter. The user input can also be assigned to a variable.

Let’s take a look at an example. You can read the input from the user interface or command line. For our example, we shall use the command line.
```python 
 >>> input()
Friends

'Friends'

>>> input("Enter your name ")
Enter your name, Emma
'Emma'

>>> number_1 = input("Enter your first number: ")
Enter your first number: 20
>>> number_1
'20'
``` 
### Print Statement
We use the print() function to display our information. It takes in an argument and prints it on the next line. The print function outputs data to the screen. You can print the value directly or assign it to a variable first.
```python 
>>> print("Hello World")
Hello World

>>> message = "Hello World"
>>> print(message)
Hello World
```
### Comments
We use # to make comments within the code. Comments are important because they make code readable, and we can use them to explain what the code does.

Creating a comment is easy. All it requires is # before the comment for it to not be executed as code. This is what a single line comment looks like.
```python 
>>> print("Hello World")
Hello World

>>> message = "Hello World"
>>> print(message)
Hello World
``` 

Python doesn’t have a generic way of writing multiline comments like other programming languages. The advised way of writing multiline comments is writing single-line comments consecutively.

We can also create multi-line comments using triple quotes at the beginning and end of a comment.
```python 
""" hello world is the first program most people run when
       learning a new programming language
"""
print("hello world")
``` 

You should be careful while using triple code comments because if you don’t indent the first ” ” ”  correctly you will get a syntax error.
You should also be careful about where you place multiline comments in functions, classes and modules. Writing it right after a function declaration makes it a Python documentation string (docstring).
We access the docstring using .__doc__ or help functions.
```python
def hello_world():
""" 
To demonstrate how to use docstring
we shall just print hello world
"""
	message ="Hello world"
	return message
	
print(hello_world())
print("Using __doc__:") 
print(hello_world.__doc__) 
print("Using help:") 
help(hello_world)
```
The single-line comments serve as internal documentation for developers of a function. Docstring serves as external documentation for developers using the function. For example, if someone wants to use your function in an imported module and they are not sure what it does, they can use the help function to access the description of the function.

### Use Case
To make understanding the Python programming language easier, we are going to create an example use case. In our example, a group of friends decide to throw a party for another friend, and they must do all the work from planning to auditing after the party.

The friends are Emma, Mark, John, Jack, Audrey, Sofia, Sally, Mary, Ali, and Chris. The information we have about them is age, height, likes, residence, and occupation.

We also have information about possible venue locations, e.g beach, hotel, bar, movie theatre.

The friends have tasks to perform, such as deciding on a venue, assigning tasks to others, creating games, making a party checklist to ensure everything is on time, tracking deadlines, sending invitations and making the party fun.

To help make party work less hectic, at the end of the blog we are going to create a tool that automates some tasks, helps with calculations and makes it easy for the friends to have a successful party.

# Variables And Operators

## What Is A Variable?
Variables are names for data we want to store and manipulate in our programs. When you declare a variable, the computer allocates memory to store it, and you can access and modify the data at any time by calling the variable name. Every time you declare a new variable you must give it an initial value.

for example, to keep the average of the friend’s age we store it in a variable. 
```python 
average_age = 19.
``` 

Unlike other programming languages, in Python, if the initial value of variables is the same we can assign them simultaneously in just one line. This is called a chained assignment. There is no limit on how many variables you can assign. For example, if multiple friends have the same age we can assign them the age in one statement.
```python
Mark = Sofia = Ali = Jack = 20
``` 

Sequence unpacking helps unpack iterables into variables using the assignment sign. The variables are separated by commas. The number of variables and elements of the sequence must be the same.
```python 

Age, residence, name =22, ” Central”, “Chris”
```

We can also switch the contents of different variables using sequence unpacking.
```python 
residence, name  = name,residence
``` 

We can use _ character to skip values we don’t want to unpack. If we don’t want to get the age and height we use _ in their position.
```python
Name, _, title, _ =(“Emma”, 20, 6ft, ”Dr.”)
``` 


We use * if we don’t know the number of sequence elements or if we are interested in specifying only one element, for example, the first or last.

## Naming A Variable
Variables names can contain alphabet (A-Z), numbers, lowercase and underscore. However, the variable names can not start with numbers. Friend_1 and _friend are okay, but 1_friend is not allowed. Variables are also case sensitive. Jack is not the same as jack.

Python has some reserved words that can not be used as variables. These words include but not limited to while, print, if.

The Python style guide provides a naming convention for variables. The common naming conventions used are camelCase or snake case. For example ageScore and age_score. I prefer using snake case and its the one we shall be using throughout but you can use whatever you want. You just have to be consistent.

## The Assignment Sign
In Python and other programming languages, = has a different meaning from the = in mathematics. In mathematics, it shows equality, while in programming it is an assignment sign. It means to copy the value on the right side of the sign into a variable on the left.
```python 
>>> height = 18
>>> age = 20 
>>> height =age 
>>> print(height)
20
```
When we run code to print the height, we get 20. This is because the age value of 20 was assigned to the score on the last line. height=age and age = height are different statements.

Arithmetic Operators
Arithmetic operators help perform basic mathematical operations like addition, multiplication, subtraction, exponential, modulus and floor division on variables in Python. Like any mathematicians, for this example, we are using the variables x and y.

addition 
```python 
x+y
``` 
subtraction 
```python 
x-y
```
multiplication  
```python 
x*y
``` 
*  is used to multiply if the variables are numbers.

X is concatenated with itself y times if x is a string and y is an integer or y is concatenated with itself x times if y is a string and x is an integer

Exponent. x to power y =225
```python 
x**y
```
division 7.5
```python 
x/y
``` 
modulus gives remainder when x is divided by y =1
```python 
x%y
```
floor division. rounds number to the nearest whole number =7
```python 
x//y
```
## Augmented assignment

The augmented assignment is the combination of an operator and an assignment sign in a single statement. For instance, +=,*=, -=, <<= and any other operators. It updates and replaces the value of the variable.

Suppose we want to increment x by 2. The traditional way to do it is x =x+2, but with the augmented assignment, this can be written as x +=2

## Comparison operators

Comparison operators are used for comparing two variables, for example, comparing the height of friends. Comparison operator expressions always evaluate to a boolean value that can be either true or false.

| operator     | sign |Example |explanation|
| ----------- | ----------- |----------- |----------- |
|  Equal    | ==     |Equal Mary ==Sofia|Mary is equal to or same as Sofia. notice the equal operators as two equal signs|
| Not Equal  | !=      |Mary!=Ali|Mary is not equal to Ali|
|Greater than| >   |height>age|let’s say Ali’s height is greater/ more than his age|
|less than|< | height<salary|height is less than his salary|

## Logical operators

Logical Operators Are Used For Combining Conditional Statements.


|x 		|y 	|X and y	| X or y	|Not x	|
|----|----|----|----|-----|
|True|True|True|True|False|
|True|False|False|True|False|
|False|True|False|True|True|
|False|False|False|False|True|


***And***
Returns true if both statements are true.
```python
age < 25 and name == “Emma”
```

If the name we are given is Emma and the age is 25 then the statement is true otherwise false

***OR***

Equal Mary

Returns True if one of the statements is true
```python
height < 10 or age > 20
```
If both the height or age is true, or one of the two is true, then that statement will evaluate to true, otherwise, it will evaluate to false.

***Not***

Not reverses the result, returning False if the result is true. 
```python
not(height < 10 or age > 20)
```
## In: Membership Operator
We use In operator to check if a value is present in a sequence if it’s present then it is a member. We can use the keywords in or not in. The statement returns a True or false value Maybe you wrote a list of things to shop, you want to know if you wrote something down, we can use in the string to get it faster
```python 
>>> Msg= "Emma did a great job working on the guest list, I can't believe she did all that work alone" 
>>> x = "guest list" in Msg 
>>> print(x) True
``` 

## Identity Operator(Is And Is Not)
Identity operators check if two values are the same, that is to say, if they have the same memory location. There are two types is and is not. the identity operators are evaluated to true or false.
```python 
>>> firstname ="Emma" 
>>> nickname ="Emma" 
>>> surname ="Bill"
>>> _is = firstname is nickname 
>>> print(_is) True
``` 

## Data Types
Python has basic data types, such as integer, float, string and advanced types like list, tuple and dictionary.

### Integers
Integers are whole numbers without decimal points, for example, -2,-1,0,1,2,3,4. We don’t need to write the data type when declaring an integer in Python. 
```python 
age = 20
``` 
### Float
Floats are numbers with decimal points for example 45.6, 3.14. For example, height:
```python 
Height = 6.15
``` 
Float numbers can also have e followed by a positive or negative number
```python 
>>> 2e3 
2000.0 
>>> 2e-3
0.002
``` 
### String
Strings are sequences of characters. We use quotations to declare strings in Python, and you can either use single or double quotations.
```python 
Name ='Audrey'

comment ="I proud to be part of the team"
``` 

If you want to include a quotation within a string we use quotations different from the ones we used on the string. If the string is using single quotation then the inside string should use double quotation and vice versa.
```python 
>>> "she said "I will be back tomorrow" then left." 
  File "", line 1
    "she said "I will be back tomorrow" then left." 
               ^
SyntaxError: invalid syntax
>>> "she said 'I will be back tomorrow' then left." 
"she said 'I will be back tomorrow' then left."
``` 
Python has built-in string functions, for example upper(). We get a string length using len() function. print(len(“Mark”)). changing case upper() or lower(). These functions come in handy when you are using inputs from the user, python is case sensitive and users may forget the case they used while registering
```python 
>>> name = "sofia" 
>>> print(name.upper()) 
SOFIA
``` 
The split() method used to split a string into substrings where it finds the instance of a separator:
```python 
>>> a = "Mark, Mee"
>>> print(a.split(","))
['Mark', ' Mee']
``` 
### String Concatenation
Concatenation means combining or merging things together. In Python, we use add + operator symbol to concatenate or combine two or more strings.
```python 
>>> message ="Welcome"
>>> name = "Emma"
>>> special_message = message +" "+ name
>>> print(special_message)
Welcome Emma
``` 
### Format string

One of the ways to format a string is to use % operator. Using % we can format variables, and if there are more variables we use a tuple which is basically closed brackets. This is the old way of doing string formatting.
```python 
>>> Name ="Carlo"
>>> distance =10
>>> "%s walked %d kilometres." %(Name, distance)
'Carlo walked 10 kilometres.'
``` 
#### String formatting with format() method

Format method takes passed arguments and places them where the place holders are. The placeholders can be empty or have indexes of arguments. the arguments can be any data type. We use curly brackets {} as placeholders.
```python 
>>> Name ="Carlo"
>>> distance =10
>>> "{} walked {}kilometres.".format(Name, distance)
'Carlo walked 10 kilometres.'
``` 
We can also rearrange the order of display without changing the order of arguments but instead use their indexes.
```python 
>>> '{1} kilometres were walked by {0} '.format(Name,distance)
'10 kilometres were walked by Carlo '
```

## Typecasting
This is converting from one data type to another for instance from float to int, int to float, int to string and more.

we have python inbuilt functions that is str(),float(), int() .

suppose
```python 

x =4.567788 

y =6 

We can also

course ="python"
``` 

## int()

Int function converts any data type to an integer, for float values anything after a decimal point is truncated, actual text cant be converted, you can’t convert complex type to integer
```python 
>>> print(int(x))
4
>>> print(int(y))
6
>>> print(int(course))
Traceback (most recent call last):
File "", line 1, in
ValueError: invalid literal for int() with base 10: 'python'
``` 

## Str()
converts data types to strings
```python 
>>> print(str(x))
4.567788
>>> print(str(y))
6
>>> print(str(course))
python
``` 

### Float()
Float converts data types to float. Like in, you can’t convert complex type to float and to convert string type to float type, the string literal must contain the value in base-10
```python 
>>> print(float(x))
4.567788
>>> print(float(y))
6.0
>>> print(float(z))
7.0
>>> print(float(position))
Traceback (most recent call last):
File "", line 1, in
``` 

# Advanced Data Types
Advanced data types are sometimes called collectives. They are used for data collection and they include sets, lists, dictionaries, tuples.

## Lists
Lists are used to store collections of related data, for example, names, age, residence etc. We use square brackets of the data collection and separate data with a comma. List items can be changed. You can also have the same item multiple times in a list.
List declaration
List Name = [value]

Example names, locations and age lists can be written as
```python 
#list of names
Names =["Emma", "Mark", "John", "Jack","Audrey", "Sofia", "Sally", "Mary","Ali","Chris"]
#list of possible party location 
location = ["Beach", "hotel", "bar", "movie theatre"]
#list of ages
ages = [20,20,19,20,22,20,21]
#list of roles/activities to do
roles =["entertainment", "Decor", "signage", "invitation","food", "RSVP follow up","cleanup" ]
``` 
Empty lists can also be initialized
Add values
name_list =[ ]

To add values to the empty list we use append() function
We can also add elements at a particular position using insert() which takes two values, the position and the item
```python 
welcome_list =["Mark", "Ali", "Sofia"]
#to add John to the list we use append() function
welcome_list.append("John")
#add using insert()
welcome_list.insert(0, 'Jack')
``` 

To access an item in a list we use indexes. An index is the position of an item in the list and it starts with 0 to denote the first position.

ages =[20,21,19,20,22,20,22]
ages[0] gives us 20
ages[1] gives us 21

we can also access values starting from the last one at index -1, second last at index -2 and so on

ages[-1] =22
ages[-2] =20

you can assign a list to a variable
```python 
age =[]
another_age = ages
``` 
another_age is [20,21,19,20,22,20,22]

To assign part of a list we use a concept called slicing
list[a,b] a is the starting index, and b is the ending index. a is always included and b is excluded
if we want to access names in the list we can just get them using their indices
```python 
#list of names
Names =["Emma", "Mark", "John", "Jack","Audrey", "Sofia", "Sally", "Mary","Ali","Chris"]
#get names from Jack to Sally
Names[3:7]
``` 

We can also use a step to access values
list[a,b,c]
c is the step size. it basically picks elements at a step of c
```python 
step2_names =Names[0:3:2]
#we get
["Emma", "John"]
#we can also leave out the number of the end index to show that we are considering the whole list
All_list =Names[0::2]
['Emma', 'John', 'Audrey', 'Sally', 'Ali']
``` 

We can also modify an element in a list
list[index of element] = new value

our new Names list is now
```python 
Names[1] = "Ken"
print(Names)
['Emma', 'Ken', 'John', 'Jack', 'Audrey', 'Sofia', 'Sally', 'Mary', 'Ali', 'Chris']
``` 

Delete
To delete an item from a list, we use del.
```python 
ages =[20,20,19,20,22,20,21]
del ages[3] 
#new list
[20,20,19,22,20,21]
``` 
We can also remove an item by removing its value.
age.remove(21)

Length
We use the len() function to get the length of a list.
```python 
num_names = len(Names)
print("There are " + str(num_names) + " friends.")
``` 

### Sorting elements
If we want to sort elements in order, you can sort them either temporarily or permanently. If we want to get our names in order, we use sort().
```python 
#Sorting a list permanently
Names.sort()
#['Ali', 'Audrey', 'Chris', 'Emma', 'Jack', 'John', 'Ken', 'Mary', 'Sally', 'Sofia']

#sort in reverse order
Names.sort(reverse=True)
#['Sofia', 'Sally', 'Mary', 'Ken', 'John', 'Jack', 'Emma', 'Chris', 'Audrey', 'Ali']

#reversing order of list
Names.reverse()
#['Ali', 'Audrey', 'Chris', 'Emma', 'Jack', 'John', 'Ken', 'Mary', 'Sally', 'Sofia']
``` 
 

## Tuple
Tuples are like lists but their values can’t be modified throughout the program. We use round brackets for tuples and commas to separate values
tuple declaration
tuple name =(value1,value2)

We access tuple values using indexes just like lists

Even though we can’t change the elements in a tuple, we can overwrite the tuple.

```python 
>>> age_height = (20, 10)
>>> print(age_height)
(20, 10)
>>> age_height = (21, 9)
>>> print(age_height)
(21, 9)
``` 
## Sets
Sets don’t allow repetition of items, sets are declared using curly brackets.
```python 
>>> Names = {'Emma', 'Emma', 'Mark', 'John', 'Jack', 'Audrey', 'Audrey','Sofia', 'Sally', 'Mary', 'Ali','Chris'}
>>> Names
{'Sally', 'Jack', 'Sofia', 'John', 'Chris', 'Mark', 'Ali', 'Emma', 'Audrey', 'Mary'}
``` 
The duplicate names are removed in a set.

We cannot access items from a set using indexing
You can check if an item is in the set using membership operator  in
```python 
if "Emma" in Names:
    print("name exists") 
``` 

Add items
To add an item to a set we use add() and update() to add a list of items to a set.
```python 
#add item
Set_names = {'Emma', 'Mark', 'John', 'Jack'}
#adding Audrey to the set
Set_names.add("Audrey")
#adding many items to the set
set_names.update(['Sofia', 'Sally', 'Mary', 'Ali', 'Chris'])
``` 
Length
We use len() to get the length of a set

del to delete the set

we can use the remove function to delete an item from a set

To join two set we use union function

Other set methods are difference(), intersection(), issubset(), issuperset(), copy(), clear(), pop(), remove().

## Dictionary
Dictionary is used to store a collection of paired data, the data is in key-value pairs. A key must be unique in a dictionary. Dictionaries use curly brackets and key-value pairs are separated by a comma.
```python 
dictionary ={key:value}
``` 
Individual values are accessed using key

Let us make a dictionary to store a friend’s details, possible party location/venue details and one to hold the guest list.
```python 
Emma_details = {

  "Name": "Emma",

  "Age": 20,

  "occupation": "banker",

"residence": "downtown",

}

print(Emma_details)
``` 
The guest list has guests and their titles for invitation. We are going to use the unique names as keys, because people share titles.
```python 
guests ={

"Nevia": "Mr", 

"carr" : "Dr",

"John": "Professor", 

"Jack": "Mrs", 

"Andrew" : "Miss", 

"Sanny" : "Miss",

 "Levi" : "sir", 

"Markle" : "captain",

"Hill": "Lord"

}
``` 
Possible party venues and the amounts for each
```python 
locations ={‘Beach’:500,

"Hotel":1500,

"Bar":600,

"movie_theatre": 200}
``` 
We can declare an empty dictionary

new_dictionary ={ }

Access items
If we want to get the price of having the party at the beach we just write 
```python 
Location["beach"]
#Or 
location. get("beach")
``` 

we can also use get() function to access values
```python 
>>> guests.get("Emma")
"Mr"
``` 
If we want to print an invitation for Hill
```python 
>>> print("Hello, " +guests["Hill"] +" Hill, you are invited to seans birthday due to take place on 15th November ")
Hello, Lord Hill, you are invited to seans birthday due to take place on 15th November
``` 

To modify 
Suppose the friends asked for additional things that are not on the 500 dollar package to be added and the new price becomes 600. To update that value in the dictionary they write
```python 

Locations["beach"] = 600
``` 
We can also go through(loop) keys in a dictionary using for loops
```python 
for location in locations:
print(location)

Beach
Hotel
Bar
movie_theatre
``` 
We can return values of a dictionary using values() function
```python 
for amount  in locationss.values():
    print(amount)

500
1500
600
200
``` 
To get both key and values of elements in a dictionary we use items() function
```python 
for venue, amount in locations.items():
  	print(venue, amount)

Beach 500
Hotel 1500
Bar 600
movie_theatre 200
``` 
we use del just like with lists to remove an item from a dictionary
```python 
del locations["Hotel"]
``` 
#to delete the entire dictionary
```python 
del locations
```
use pop() to remove specified key
```python 
occupations.pop("Mary")
'business analyst'
``` 
Copy
to copy a dictionary to another we use copy
```python 
party_venues = location.copy()
``` 
### Nested dictionary

We can have a dictionary inside another. This is helpful when your key has a set of attributes for example with location, a beach has an amount, size it accommodates etc. 

We can add more information about the locations necessary to the party planning into the location dictionary. we are going to make each location dictionary having its own attributes and add it as a key to the location dictionary.
```python 
Location ={
"Beach":{"amount":500, "accommodation":100," entertainment": " music"},
"Hotel": {"amount":1500, "accommodation":300, "entertainment": "liveband"},
"Bar":{"amount":600, "accommodation":50, "entertainment": "karaoke"},
"Movie_theatre":{"amount":200, "accommodation":200: "entertainment": "latest movie"}
}
``` 
To check for the size of the dictionary we use len() function like with other iterables.

# Decision making

The programs we have written so far work but not in situations where we have alternatives. We often want the program to make choices based on particular conditions, to do this, we use if statements, for loops, and while statements.

## If /Conditional Statement
We have a base expression which evaluates to either be true or false and the decision is based on the returned value. The condition we are going to look at here is the if statement. If statements use comparison operators which are: equal (==), not equal to(!=), greater than, greater than or equal, less than, and less than or equal. if statements can also have an optional else/elif(else if) part that is executed when the boolean value of the condition above it is False.

If we have operations we don’t want to use

### Structure of if statement

if condition a is true:
    do action A
elif condition b is true:
    do action B
elif condition c is true:
    do action C
else:
    do action D

if-else statement

We can use this to assign each friend a task
```python 
if Name == "Emma":
	task  = "grocery shopping"
elif Name =="Ali":
	task ="get cake"
else:
	student ="Clean up"
``` 

We can also use logical operators if two conditions need to be met, recall AND operator returns true when both conditions are true while with OR operator at least one condition must be true, not is rarely used but one can use it when they want to reverse logic of the expression. We also use membership and identity operators.
For example, if the friends are having a hard time deciding which place to throw the party at, we can write down conditions that have to be met. For example, the friends might want a venue that costs less than 2000 and that can accommodate more than 100 guests.

```python 
if amount <2000 and accommodate >100:
	print("consider the place")
#if else statements can be nested inside other if else statement
if price <2000 and accommodate >100:
	if food == "Delicious":
		print("this is the place")
``` 

Let us use input function, operators and if conditions to create a simple calculating program that can be used to do math at the party.we used int() to convert the input string to an integer.
```python 
x= int(input("Enter first number: "))
y= int(input("Enter second number: "))
operator = input("Enter operation: ")
if operator == "+":
	print(x+y) 
elif operator == "-":
	print(x-y) 
elif operator == "*":
	print(x*y) 
elif operator == "/":
	print(x/y) 
elif operator == "%":
	print(x%y) 
elif operator == "^":
	print(x**y)
``` 
# Loops
We use loops when we want to execute blocks of code until the condition becomes invalid. We shall use loops to do repetitive tasks for example sending out invitation cards. It is tiresome to write an invitation for everyone, a simpler way is to use a loop that goes through names in a list and prints cards for each one.

### For loop
The for loop is used to iterate over a sequence, for example, tuples, lists, dictionaries, and strings. It can also be used with a given range instead of printing each word in a sequence.

Without a loop, we will have to write code to print each name in the list.
```python 
Names = ['Emma', 'Mark', 'John', 'Jack', 'Audrey', 'Sofia', 'Sally', 'Mary', 'Ali', 'Chris']
print("Emma")
print("Mark")
print("John")
print("Jack")
print("Audrey")
print("Sofia")
print("Sally")
print("Mary")
print("Ali")
print("Chris")
``` 
We use a loop to make code less messy and hectic.
```python 
Names = ['Emma', 'Mark', 'John', 'Jack', 'Audrey', 'Sofia', 'Sally', 'Mary', 'Ali', 'Chris']
for name in Names:
	print(name)
``` 
We can also use the range function to loop through a block of code for a specified number of times. The range function has 3 parameters, the start position, the end position and a step number. The start position is 0 by default and the increment number is 1.
```python 
for i in range(10):
print(i)
#Prints numbers from 0to 9
#with all parameters
for i in range(1,20,5):
print(i)
1
6
11
16
``` 
Now let us print our invitations

```python 
guests ={
"Emma" : "Mr", 
"Mark" : "Dr",
"John" : "Professor", 
"Jack" : "Mrs", 
"Audrey" : "Miss", 
"Sofia" : "Lady",
"Sally" : "sir", 
"Mary" : "captain",
"Ben": "Lord"
}

for key in guests:
  print("Hello, " +guests[key] +" "+ key+ " , you are invited to Sean's birthday due to take place on 15th November ")
``` 
Hello, Mr Emma, you are invited to Sean’s birthday due to take place on 15th November

Hello, Dr Mark, you are invited to Sean’s birthday due to take place on 15th November

Hello, Professor John, you are invited to Sean’s birthday due to take place on 15th November

Hello, Mrs Jack, you are invited to Sean’s birthday due to take place on 15th November

Hello, Miss Audrey, you are invited to Sean’s birthday due to take place on 15th November

Hello  Lady Sofia you are invited to Sean’s birthday due to take place on 15th November

Hello sir Sally you are invited to Sean’s birthday due to take place on 15th November

Hello, captain Mary, you are invited to Sean’s birthday due to take place on 15th November

Hello, Lord Ben, you are invited to Sean’s birthday due to take place on 15th November

We can also use the dictionary method items
```python 
for name, title in guests.items():
    print("Hello, " +title+" "+ name+ ", you are invited to Sean’s birthday due to take place on 15th November “)
```

This simplifies the work writing the template is the only task the person sending invitation has to do and the program will go through the list and print invitations for everyone

### While Loop
While loop is used to execute a set of statements as long as the given condition is true. The condition is tested before proceeding to the body.

With while conditions, we usually declare a variable that is used to keep count/track.
```python 
i =0
while i <10:
	print(i)
	i +=2
0
2
4
6
8
``` 
We can also it to remove all ages below 20 years
```python 
ages =[20,20,19,20,22,20,21]
print("ages before removing value")
print(ages)
while 20 in ages:
    ages.remove(20)
	print(ages)
[20, 20, 19, 20, 22, 20, 21]
[19, 22, 21]
``` 

## Break,Continue,Pass
### Break
Break statements are used when we want to exit the loop after a given condition has been met.
```python 
Names = ['Emma', 'Mark', 'John', 'Jack', 'Audrey', 'Sofia', 'Sally', 'Mary', 'Ali', 'Chris']
for name in Names:
	print(name)
	if name =="Audrey":
		break
Emma
Mark
John
Jack
Audrey
```
We want to print all names up to Audrey, and after reaching that point we want to stop printing.

Continue
With continue, we skip the statement after it and execute the other parts of code. In the following code example, the statement after the name John is encountered but is not printed.
```python 
Names = ['Emma', 'Mark', 'John', 'Jack', 'Audrey']
for name in Names:
	print(name)
	if name =="John":
		continue
	print("ok")
Emma
ok
Mark
ok
John
Jack
ok
Audrey
ok
``` 
We don’t want to print the ok when we find the name, John

Infinite Loop
An infinite loop executes its block of statement until the program is forced to quit.
For our use case, an infinite loop can be used for the person in charge of welcoming guests and signage. The person will continue doing that as long as the guests are coming but they can also be stopped to go attend other rules. since we don’t know the condition to evaluate we use while
```python 
while True:
	role = "attend to visitors"
``` 

# Functions
Function Definition
A function is a set of instructions under a block of code which executes only when it’s called by just writing their names. You might also pass data into your function with parameters that are separated by commas. We have already seen built-in functions like print(), upper() and now it’s time for us to create our own functions.

Once you define a function you can use it throughout the program by just calling it.
syntax
def functionName(parameter):
    statements
    return x

def is used to state the block of code is a function and return gives the desired results after execution. A function can have more than one return statement.

Variable scope
Variables declared inside a function are local variables and cannot be accessed outside of the function, while global variables can be accessed anywhere in the program. If a global variable shares the same name as a local variable, the local variable is accessed first.
```python 
Name ="Sally"  #global variable
def name_local():
	Name ="Emma" #local variable
	return Name # local variable returned
print(Name) #global variable
``` 
You can use the keyword global if you want to create a global variable inside a function.
```python 
age =10
def ages():
	global age 
	age = 20
	return age
ages()
print(age)
#prints 20
``` 

## Default function value
If a function is called without a parameter it passes the default parameter value.
```python 
def my_name(name= "Audrey"):
  return("I am  " + name)

print(my_name("Emma"))
print(my_name())
print(my_name("Jack"))
I am  Emma
I am  Audrey
I am  Jack
Arbitrary Arguments
``` 

## * Args
If you do not know the number of arguments you will be passing into your function, add a * before the parameter name in the function definition.
This way the function will receive a tuple of arguments, and can access the items accordingly:
```python 
def friends(*friend):
  return("Guess who didn't want to come? " + friend[2])
print(friends('Emma', 'Mark', 'John', 'Jack'))
Guess who didn't want to come? John.
``` 

## **kwargs
This way the function will receive a dictionary of arguments and can access the items accordingly
We use ** in front of the parameter name if we don’t know how many arguments are to be passed. The function will receive a dictionary.
```python 
def friends(**friend):
  return( friend['name'] + " is " +str(friend['age'] )+ " years old" )
print(friends(name ="John", age =21))
John is 21 years old
``` 
## Lambda Function
Lambda functions are anonymous functions meaning they have no names. A lambda function is written in one expression.
Syntax
lambda arguments: expression
example
```python 
x = lambda task : task + 2
print(x(5))
#lambda functions can also take on multiple arguments
x = lambda a, b,c : a * b * c
print(x(5, 6, 2))
``` 
# Classes/Objects
Python is an object-oriented programming language. objects have properties and methods classes are used to create objects. they are the constructors
## Reasons For Using Objects.
Polymorphism. you can use the same operation multiple times
Encapsulation which helps hide implementation details
Inheritance, specialized classes can use properties of the main class.

## Create A Class
We create classes using the keyword class
class AgeClass with a property age
```python 
class AgeClass:
  age = 20
``` 
Create An Object
```python 
age1 = AgeClass()
print(age1.age)
``` 

### The init function
We use the init() function to assign values to object properties or other operations that are necessary to do when the object is being created.
For example, we use init to assign name and age using init function.
```python 
class Friend:
  def __init__(self, name, age):
    self.name = name
    self.age = age
friend = Friend("Jack", 20)
print(friend.name)
print(friend.age)
``` 

## Object methods
Methods are functions that belong to the object. we can use object methods in a function that calls out peoples name and age. Methods will be things friends can do, such as delegate tasks or entertain guests.

```python 
class Friend:
  def __init__(self, name, age):
    self.name = name
    self.age = age
  def my_name(self):
    return("It is time for  " + self.name)
``` 

### Modify object property
Changing age of friend object.
friend.age = 22

Delete a property
We delete using del like in sequential data type.
del friend.name
Delete object
del friend

## Python Inheritance
Inheritance allows us to define a class that inherits all the methods and properties of another class.
Parent class or base class is the class being inherited.
Child class sometimes called derived class, is the class that inherits from another class.

### Parent class,
We define it the way we define classes. 

### Create child class
We use pass parent class as a parameter in the child class, it will inherit all parent properties
```python 
class Guest(Friend):
   Pass
``` 
A class can also inherit from multiple classes.

Suppose we have another class family. A guest can have both properties of family and friends classes
```python 
class Family:
	Pass
class Guest(Friend, Family):
	pass
Super Function
``` 

Python also has a super() function that will make the child class inherit all the methods and properties from its parent. you can also add properties and methods to the child class.
```python 
class Guest(Friend):
  def __init__(self, age, name):
    super().__init__(age, name)
    self.residence = "south"
``` 
## Miscellaneous
This section contains some important concepts we didn’t cover in the previous sections.

### Flag Variable
A flag variable is used to let one part of your program know when something happens in another part of the program. 
For example if someone comes to the reception we check to see if they are on the guestlist and if they are not we flag them as intruders.
```python 
num = input('Enter name: ')
Invited =True
for i in range(len(guests)): 
	if name not in guestlist: 
		invited = False 
	if flag==True: 
		print("you're welcome") 
	else:
		print('Sorry, you have to leave')
``` 
### Random Number
Random number modules are very useful if we want to get random values. It can be used in games but we can also use it to randomly assign tasks to friends.
```python 
from random import randint 
for i in range(20):
    rand_num = randint(1,5)
    print(rand_num)
```
The random module can also be used on lists using choice, sample, and shuffle functions

choice(list) picks a random item from the list.

sample(list, num) picks a group of num random items from list.

shuffle(list) shuffles the items of a list.

Final Program
This program contains all the concepts we have learned so far from variable declaration to classes. We are connecting the pieces we have been talking about.

## Conclusion
This blog is an introduction to Python written in a simple manner to help you understand the building block of the language. I have used a use case that I assume most of us relate to in order to help you understand the application of the different aspects better. Feel free to add your own code implementation. For any questions contact me at info@napro.dev. Thank you for reading, I hope to see you in the next blog pos

