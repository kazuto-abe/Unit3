# Quiz20

### python code
```.py
class Swap():
    def __init__ (self, x:str):
        self.x = x

    def swap_characters(x):
        length = len(x)
        new_x = ""
        for i in range(0, length, 2):
            new_x = new_x + x[i+1] + x[i]

        print (new_x)
    
print(Swap.swap_characters(x = "01ABxy"))
```

### test result
