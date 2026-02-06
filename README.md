v = "alpha 00.1"

print(f"{v}\n")

debug_mode = True

def calculator():
    print("calculator")
    try:
        num1 = float(input("enter number: "))
        op = input("enter operator (+, -, *, /): ").strip()
        num2 = float(input("enter another number"))
        
        if op == '+': result = num1 + num2
        elif op == '-': result = num1 - num2
        elif op == '*': result = num1 * num2
        elif op == '/': result = num1 / num2
        else: result = "invalid operator you idiot"
        
        print("answer:", result)
    except ValueError:
        print("error: invalid number idiot")
    except ZeroDivisionError:
        print("error: cannot divide by zero lol")   
if __name__ == "__main__":
     while True:
         calculator()