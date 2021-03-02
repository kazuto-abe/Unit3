# Quiz 18

Given a number as a String N. Multiply all of the digits of N, and repeat the same with the product obtained till the product consists of only one digit. Output the number of steps taken to do so.

Example: N = 39 <br>
        Step 1: 3 * 9 = 27 <br>
        Step 2: 2 * 7 = 14 <br>
        Step 3: 1 * 4 = 4 <br>
        
Since it took us 3 steps to reach a number with only 1 digit, the output is 3. 

### python code
```.py
class Step():
    def __init__(self, n):
        self.n:str = n
        
    def find_steps(n):
        step = 0
        length = len(n)
        
        while length > 1:
            product = 1
            for i in range(length):
                product *= int(n[i])
            
            n = str(product)
            step += 1
            
        return step
        
    
print(Step.find_steps(n = "39"))
```
### test result 

