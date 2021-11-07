This post contains code for creating a simple commandline calculator app in python. This is a beginner friendly project and it covers basic concepts like variables, conditional statements, loops and functions. 
I have made a video going through it and it will be uploaded on my youtube channel so be sure to check it out. 


```python
print(""" Select arithmetic operation: 
            1.Addition
            2.Division
            3.Modulus
            4.Multiplication
            5.Subtraction
            
""")
#print answer function
def print_answer(one,two,operation, answer):
    print(one, operation, two, "=", answer )
def add(num1,num2):
    return num1+num2



while True:
    selection = int(input("select arithmetic operation: "))
    if selection in (1,2,3,4,5):
        first_number = int(input("Enter first number "))
        second_number = int(input("Enter second number "))
        if selection ==1:
            answer = add(first_number,second_number)
            print_answer(first_number,second_number,"+", answer)
        elif selection ==2:
            answer = first_number/second_number
            print_answer(first_number,second_number,"/", answer)   
        elif selection ==3:
            answer = first_number%second_number
            print_answer(first_number,second_number,"%", answer)   
        elif selection ==4:
            answer = first_number*second_number
            print_answer(first_number,second_number,"*", answer)   
        elif selection ==5:
            answer = first_number-second_number
            print_answer(first_number,second_number,"-", answer) 

        another_calculation = input("would you like to make another calculation? (1.Yes/2.No): ")
        if another_calculation == "2":
          break

    else:
        print("Make selection from list provided")

```

     Select arithmetic operation: 
                1.Addition
                2.Division
                3.Modulus
                4.Multiplication
                5.Subtraction
                
    
    select arithmetic operation: 1
    Enter first number 3
    Enter second number 5
    3 + 5 = 8
    would you like to make another calculation? (1.Yes/2.No): 1
    select arithmetic operation: 3
    Enter first number 5
    Enter second number 2
    5 % 2 = 1
    would you like to make another calculation? (1.Yes/2.No): 2



```python

```
