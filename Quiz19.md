# Quiz 19
Reverse Mode: Given the input/outputs shown, create the program that produces the output. <br>
[HL] Using OOP in your solution. binary to decimal.

example: <br>
100!000!111 => 407
101!010!100 => 524

(numbers are splited by "!")


### python code
```.py
def convert(x:str):
    nums = {
        '000' : '0',
        '001' : '1',
        '010' : '2',
        '011' : '3',
        '100' : '4',
        '101' : '5',
        '110' : '6',
        '111' : '7'
    }

    x = x.split("!")
    for i in range (0, len(x) - 1):
        for i in range (0, len(nums) - 1):
            if x[i] == nums[i]:
                n = nums[i]
                return n
                
    
    
print(convert(x = "100!000!111"))
print(convert(x = "101!010!100"))
```

### test result
![Screen Shot 2021-03-02 at 22 36 50](https://user-images.githubusercontent.com/60457723/109656505-d6e4b600-7ba7-11eb-9743-f91fc2c6d8f9.png)
